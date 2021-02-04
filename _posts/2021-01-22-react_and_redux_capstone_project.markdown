---
layout: post
title:      "React & Redux Project Reflection: AMS Gem + 1 Reducer VS. combineReducer()"
date:       2021-01-22 13:47:10 -0500
permalink:  react_and_redux_capstone_project
---


A new beginning is in sight, the final module of the SE bootcamp has come to an end.
From learning what an IDE is and how to download my own local environment so I can do the labs to learning Ruby, SQL, Sinatra, Rails, JavaScript, React, Redux and building things like CLI's, API's, static user auth apps, and dynamic apps.. what a journey!

It's nice to take a moment to look back, reflect, and be amazed at what has just been done.

Ok, so let's get into it, the final project - a React and Redux app with a rails API backend. I felt much more confident setting up that API since it had to be done for the previous module. One thing I utilized in my back end this time that I haven't before was the Active Model Serializer (AMS) gem. I decided to try this out after having some difficulty with multiple reducers and redux's `combineReducers()` function, which I'll come back to.

Let me tell you, AMS made my life 1000% easier when it came to working with my redux flow. Now, there are two gems I considered here both covered in the learn.co curriculum, AMS and Fast JSON API, so why did I go with AMS? Well, I checked out the github for Fast JSON API and at the top of the readme it read.. "Fast JSON API — ⚠️ This project is no longer maintained!!!! ⚠️". I by no means know which is better, AMS is older and appears to be slower than the alternatives according to their readme.

I followed along with this nice [walkthrough for AMS that we have on learn](https://learn.co/lessons/using-active-model-serializer) and went ahead generating my serializers in my terminal the lovely way rails lets you, "rails g serializer Account" and "rails g serializer Transaction". Now I had a serializers folder inside my app folder holding the account and transaction serializer.

By simply adding the attributes I want passed along to my front end, and the **has_many relationship** (this is key), all my data passed through with just one reducer. Here's a look at those serializers..

```
class AccountSerializer < ActiveModel::Serializer
  attributes :id, :name, :balance, :acc_type
  has_many :transactions
end
```

Please note the `has_many :transactions` relationship, this is the reason I used a serializer and was able to simplify my redux flow using just one reducer, an accounts reducer, for my application.

```
class TransactionSerializer < ActiveModel::Serializer
  attributes :id, :t_name, :description, :t_type, :t_amount, :account_id
end
```

And here, your normal transaction serializer.

The attributes in both are going to the be the attributes rendered through my fetch request because of that has_many relationship..
```
export function fetchAccounts(){
    return(dispatch) =>{
        fetch('http://localhost:3000/accounts')
        .then(resp => resp.json())
        .then(accounts => {
            dispatch({type: 'FETCH_ACCOUNTS', payload: accounts})
        })
    }
}
```
Oh and guess what.. **only 1 fetch is needed to render both models** because of that `has_many :transactions` relationship in the account serializer!
I'm not sure if I can stress that enough, it was mindblowing to me!

So instead of having to manuever some code around to get `combineReducers()` built out and implemented, adding a transactions reducer, a fetch action to render all transactions, and build out a transactions component importing and invoking that action to change/update state using `mapStateToProps`, `componentDidMount`, and `{connect} from 'react-redux'`... we pulled a fast one on redux and used AMS to pass through transactions with accounts on the fetchAccounts action.

Although AMS was helpful this way for my project and allowed me to render all of my accounts and the transactions associated with each account with one action/reducer, combineReducer() is still extremely helpful and should be used most times when using multiple reducers, my case happened to be one of the exceptions.

Here is a peak at what my reducer looks like thanks to AMS with a bit more functionality than just fetching data..

```
export default function accountReducer(state = {accounts: []}, action) {

    switch(action.type){
        case "FETCH_ACCOUNTS":
            return {accounts: action.payload}
        case "ADD_ACCOUNT":
            return {...state, accounts: [...state.accounts, action.payload]}
        case "ADD_TRANSACTION":
            return {...state, accounts: state.accounts.map(account => {
                if (account.id === action.payload.id) {
                    return action.payload
                }
                else {
                    return account
                }
            })}
        case "DELETE_TRANSACTION":
            return {...state, accounts: state.accounts.map(account => {
                if (account.id === action.payload.id) {
                    return action.payload
                }
                else {
                    return account
                }
            })}
        default:
            return state
    }
}
```

If you noticed, the case for ADD_TRANSACTION and DELETE_TRANSACTION looked similar, right? That's because they are exactly the same, this works because of the serializer relationship, the actual account is being returned with the updated list of transactions belonging to it.



