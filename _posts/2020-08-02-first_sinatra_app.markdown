---
layout: post
title:      "Sinatra App"
date:       2020-08-02 02:05:41 -0400
permalink:  first_sinatra_app
---


## You think all you need to worry about it code, huh?

### Don't let the program file structure scare ya, figure out the flow first!

I must say, the first impression of all the folders and files required to make this app appeared overwhelming.. There are many different folders/files you'll be creating, and with the help of corneal you'll get a nice start. This project required me to leverage all that I have learned since day 1 in ruby along with the newly acquired skills of sql, html, css, and activerecord to meet all the requirements. I love the fact that everything taught throughout the curriculum to this point had to be put to use, I definitely had to go back and review some of those older lessons. 

This project is where I truly felt like a software engineer, powering up shotgun and refreshing my page as I edit code to see my work in action was amazing. Nothing like instant gratification on the work you're doing. Even if I wasn't sure what my code would do, the Sinatra error messages and pry guided me in the right direction. I'm guessing that's some TDD ftw, now I see what that's all about.

Back to my brand new App, it's definitely not the prettiest.. and the thought process that goes into the development.. Good Lord! I found myself brainstorming for hours, coming up with the project idea was easy..deciding which one to do was hard. THEN, once you finally decide wha to work on.. putting together a proper flow and deciding which content should be where was another battle.

Finally, I came up with a topic and flow with what the user should experience throughout the app.
Back to the lab we go.. I open up my project and get to work creating each file needed in my models, controllers, and view. Now, I am ready to actually start writing some code!

And I thought to myself.. "Whew.. all that.. and I have yet to write a single line of code..."

Building out the model classes really showed me how powerful sinatra was, by adding has_many / belongs_to code and validations was all you really had to do there to build.. nice, clean, and simple. 

Controllers were a bit more work... to be honest, a LOT more. Majority of your code will go here, and figuring out how to organize your code is another feat in it's own. Every controller setup should have something like ApplicationController, UserController, SessionsController, and ___ Controller at the very least. These controllers will be responsible for nearly everything in your app, you'll need to achieve the following here:

* * Render Page Views
* * Signup / Login Enabling Sessions
* * CREATE, READ, UPDATE, and DELETE
* * Helper Methods (dry code is the best code)

Views, I think I had too many views.. and forms and code.. By far my least favorite of the MVC folders. I envisioned a beautiful app with all this incredible design meeting all functionality requirements while also look amazing.. Yeah, that didn't happen...

I ignored styling and focused on functionality, kept it straightforward with `<form action="/" method="POST>` etc. to post the model attributes, create a proper session id for the user, save each model class params in the approriate database, edit with `<input type='hidden name='_method' method="PATCH">`, delete with `method="DELETE"`, incorporate links to navigate, and some `<%= @current_user.name %>` or `<% array.each do |x| %> ... <% end %>`

All in all, this was quite an amazing project, one I truly enjoyed. Reflecting back on the CLI.. great first project to build confidence. This sinatra project.. even better and then some. Being forced to used multiple languages in just my second project and seeing it in action online.. oh my.. such an awesome feeling.
