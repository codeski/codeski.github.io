---
layout: post
title:      "Where’s That Video? OOJS"
date:       2021-04-30 17:06:29 -0400
permalink:  oojs_where_s_that_video
---


Ever wish you could organize videos by category and have them all embedded on one page? Well my application does just that. Simply fill out the form, add the embed code, create or choose an existing category, press “submit” and walla. No need to wait for a page refresh. The Object Oriented JavaScript is able to send and receive information to and from our backend Rails API server based on how the user interacts with the web application through JavaScript object event listeners. 

To make it easy to find your submit button using JS add an id to the HTML in your form 
example:  `<input id= “submit” type=”submit” value="submit"></input>`
Now in your index.js file assign a variable and add an event listener to that variable
`const submit = document.getElementById(“submit”)
submit.addEventListener(“click”, handleSubmit)`

Now you’ll have to write a handleSumbit function which will take an argument of the event from our event listener. 
`handleSubmit = (event) => event.preventDefault()` - this cancels the default event of a page refresh when a submit button is pressed. 

We communicate with our Rails API server through JS fetch()’s. The submission form sends a `POST` fetch request to our create route action in our Video and possibly Category controller(s) containing the form’s params.

Through these fetch requests and sometimes regardless the application creates, updates or removes our JS objects in the DOM(document object model full CRUD functionality). JS objects allow us to provide our user with a seamless and dynamic experience. 

The `fetch()` is a complicated subject to explain. The simplest `fetch()` request takes one argument, the URL path to the resource desired.
```
fetch(‘http://localhost3000/videos’)
.then(response => response.json())
.then(data => (do something with JSON data))
```
The `fetch()` is an asynchronous function that returns something called a promise object. The promise can be pending but will ultimately be resolved or rejected. To provide order to the asynchronous `fetch()` function we use a `.then()`. A `.then()` waits for the promise to be resolved or rejected and will return another promise object, so they can be chained. 

In our example, the `fetch()` promise object is a  HTTP response object. We `.then()` take that HTTP response object and turn that into a promise object that is a JSON object by using the `.json()` method. We `.then()` take the JSON object (data) and turn it into OO JavaScript using our JavaScript classes and constructors, which in my case ends up being video and category objects. 

While I didn’t, one could use a `.catch()` at the very end. A `.catch()`  deals with rejected promises objects only and could be used to display an error message. 

It’s cool to know that I’ve hardly scratched the surface of functionality that can be created with JS. It’s simply up to one's imagination for what they want to create. 

