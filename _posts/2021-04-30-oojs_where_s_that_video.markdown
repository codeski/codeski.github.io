---
layout: post
title:      "Where’s That Video? OOJS"
date:       2021-04-30 17:06:29 -0400
permalink:  oojs_where_s_that_video
---


Ever wish you could organize videos by category and have them all embedded on one page? Well my application does just that. Simply fill out the form, add the embed code, create or choose an existing category, press “submit” and walla. No need to wait for a page refresh. The Object Oriented JavaScript is able to send and receive information to and from our backend Rails API server based on how the user interacts with the web application through JavaScript object event listeners. 

To make it easy to find your submit button using JS add an id to the HTML in your form 
example:  `<input id= “submit” type=”submit”>Submit</input>`
Now in your index.js file assign a variable and add an event listener to that variable
`const submit = document.getElementById(“submit”)
submit.addEventListener(“click”, handleSubmit)`

Now you’ll have to write a handleSumbit function which will take an argument of the event from our event listener. 
`handleSubmit = (event) => event.preventDefault()` - this cancels the default event of a page refresh when a submit button is pressed. 

We communicate with our Rails server through JS fetch()’s. The submission form sends a `POST` fetch request to our create route action in our Video and possibly Category controller(s) containing the form’s params.

Through these fetch requests and sometimes regardless the application creates, updates or removes our JS objects in the DOM(document object model full CRUD functionality). JS objects allow us to provide our user with a seamless and dynamic experience. 

It’s cool to know that I’ve hardly scratched the surface of functionality that can be created with JS. It’s simply up to one's imagination for what they want to create. 

