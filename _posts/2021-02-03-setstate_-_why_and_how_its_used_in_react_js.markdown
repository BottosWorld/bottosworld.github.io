---
layout: post
title:      "setState() - Why and How it's used in React.js"
date:       2021-02-03 04:01:13 -0500
permalink:  setstate_-_why_and_how_its_used_in_react_js
---


*Before we get into to setState(), we first need to get a basic understanding of what state, components, react, and javascript are..*

From the beginning we have **JavaScript**, a scripting language that is responsible for the creation of dynamic websites by updating content based on user events (such as clicks, scrolling, refreshing, even inputing information to login, and more!). JavaScript can also be behind animations, music and videos, and more things you see on a website. 

* *More information on JavaScript can be found [here!](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Firststeps/WhatisJavaScript)*

Next, there is **React.js**, a popular library used with JavaScript, created by Facebook. Simply put, React.js is a JavaScript file with pre-written functions that allow for easier development of the front-end of a dynamic website, in other words the User-Interface(UI), thus allowing an efficient way to build interactive websites quickly. React also introduces a new way to write code, JSX, which looks like HTML code but has the functionality of JavaScript. Thus, making it easier to for developers to write and understand. Lastly, Components, State, and setState all belong to the React.js library, so let's take a brief look at each below before diving into setState()

**Components:** Think of these as reusable pieces JavaScript code that return the visual aspects ("what you see") of a website. You will find State and setState() used in Components to update the website based on user events, such as clicks, scrolling, moving the mouse, and more. A simple example of a component is a navigation bar containing links to other areas of the website whereas a complex example could be an Account Component, which contains different Components for that Accounts' transactions, balance, images, even the previous example - navigation bar, and possibly many more.

**State:** This is where data that may change overtime by a user is stored, that data comes from either the user or the default setting of the Component. State lives inside of the Component and not all Components have State. An example of this would be a shopping cart feature on a website, which would be it's own Component and have a default "state" that is empty, but when a user adds an item to that shopping cart, the state is being changed to show that item, hence a new "state" of shopping cart. Think of this as the way the website interacts with the user, there needs to be a default setting before a user interacts with that Component on that website, and then a way to update that State based on what the user did, which leads us into setState()...

* *If you find the need for a deeper understanding, a great guide with these topics and many more on React.js can be found [here!](https://www.taniarascia.com/getting-started-with-react/)*

**setState():** We have finally arrived at setState(), the primary way to update the front-end of a website, it's UI. This takes into account that the website is in JavaScript, uses React.js, and has a Component with State. Triggered by user events, setState() re-renders that Component to display the new, updated State. A simple example of this is actually mentioned above in the shopping cart example given in State, setState() is responsible for that shopping cart updating from the default state to show the user the item they added to that cart. If setState() was not there, every time a user tries to add an item to that shopping cart, the State would remain in it's default status, empty. Now let's break this down with some code, explanations can be found followed by //...

```
import React, {Component} from 'react'
//importing Component from the React.js library

class ShoppingCart extends Component {
//your Component
  
  state = {
      itemName: '',
      price: ''
    }
  //your State, set to empty by default
	
  
  addToCart = (e) => {
    this.setState({ 
      itemName: 'Playstation 5',
      price: '$499.99'
    })
  }
  //the function used to update your default state by
	//taking in a user event and using setState()
  
  render(){
    return(
      <div>
        {this.state.itemName}: {this.state.price}
        <br></br>
        <button onClick={this.addToCart}>Add PS5 to Cart</button>
      </div>
    )
  }
	//render and return are used to display the state and button to update
	//state, this button calls upon the addToCart function which is where
	//setState() is found, you can see that the state is being 
	//changed here when the user clicks on that button
  
}

export default  ShoppingCart
```

As shown above, setState() is used inside of a function that is called upon when the user clicks the button. That 'click' is one of the many events that can trigger the addToCart function containing setState().
Without using setState(), the default State will always be dislpayed and there would not be a way for the user to update that state. At the end of day, setState() is required to update state and should be used for scenario's like shown above with the shopping cart. 
