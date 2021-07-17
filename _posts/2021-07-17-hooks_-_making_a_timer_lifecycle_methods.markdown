---
layout: post
title:      "Hooks - Making a timer, lifecycle methods"
date:       2021-07-17 07:46:14 +0000
permalink:  hooks_-_making_a_timer_lifecycle_methods
---


Timers need access to lifecycle methods: constructor(), componentDidMount(), componentWillUnmount(), render()  

Last blog I thought you had to use a class Component to have access to Lifecycle methods and a local State. I was wrong… One has access to both using hooks in functional components. 

I seriously played with the useEffect Hook for a day, watched videos and read blogs. I can tell you for a fact that there are many bad ways to build a timer. In the end it turns out the documentation had the perfect answer all along that helped me understand what I needed to do. I invite you to copy and paste this in your code editor and open up your console when you import and render this `<HookTimer />`  component.

Play around with it and have fun. Read through the comments for a quick overview of hooks and how to properly mount and unmount a timer.

```
import React, { useEffect, useState } from "react"
//import the hooks
 
const HooksTimer = () => {
// 1. Constructor
   const [timer, setTimer] = useState(0)
   // timer is state variable
   // setTimer() is the function we use to setState of timer essentially
   // useState() is our initial state, can be a reference to a function
 
   useEffect(() => {
// 3. componentDidMount() - Yes, it's numbered correctly and needs to be in this order
// remember what happens when you return something in a function? It stops reading the rest of the code
       console.log('componentDidMount', timer) // timer will be 0
       increment() // see the DOM start at 1 // render happens twice before you see it
       const tickTock = setInterval(increment, 1000) // runs function increment every second
// Last. componentWillUnmount()
       return () => {
           console.log('componentWillUnmount')
           clearInterval(tickTock) // runs once during the unmounting
       }
   }, []) //4. componentDidUpdate
   // if no second argument / no array, useEffect will run everytime state updates
   // if empty array [] useEffect will only run once during mounting and unmounting
   // put the state if you'd like to trigger useEffect when a specific state updates, example [timer](this will make our code go crazy)
 
// 4. ran inside of useEffect
       const increment = () => {
           setTimer(t => t + 1) // this does not depend on 'timer'
       }
 
// 2, 5, & every second. Render
   return (
       <div>
           <p>{timer}{console.log('render')}</p>
       </div>
   )
}
 
export default HooksTimer
```
 
Comment out the `clearInterval(tickTock)` and watch what errors you get in the console when you unmount the component. 

Warning: Can't perform a React state update on an unmounted component. This is a no-op, but it indicates a memory leak in your application. To fix, cancel all subscriptions and asynchronous tasks in a useEffect cleanup function.

