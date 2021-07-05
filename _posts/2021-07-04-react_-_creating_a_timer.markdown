---
layout: post
title:      "React - creating a timer"
date:       2021-07-04 20:07:14 -0400
permalink:  react_-_creating_a_timer
---


This will be a basic guide, a crash course for the basic timer in React. 
Timer can only be used inside of class Components and require the use of component lifecycle methods: `componentDidMount()` &   `componentWillUnmount()`.

## Component lifecycle methods and phases 
### There are 3 phases to any component: Mounting, Updating, and Unmounting

### This guide will cover the lifecycle methods in making timers: 
*  `constructor()` - mounting - assigns props - happens automatically - does not need to be included in code
* `render()` - mounting and updating
* `componentDidMount()` - mounting - starting your timer
* `componentWillUnmount()` - unmounting - ending your timer

### Lifecycle methods are invoked, do not use arrow functions

I recommend copying and pasting this code into your editor: everything is in order and walks through the basics of a timer a component lifecycles it uses.  Just render the component in your App `<Timer />`

```
import React from 'react'
 
class Timer extends React.Component {
   // 1) - Mounting
   // constructor(props) {
   //     super(props) 
 
   //     //how to set local state through constructor
   //     this.state = {
   //         timer: 0
   //     }
   // }
 
   // ES6 syntax - constructors are automatic for props
   // 1) Mounting - timer needs a local state
   state = {
           timer: 0
   }
 
   // 2) Mounting and Updating
   render(){
       // most used
       // after constructor giving access to props and state
       return (
           <div>
               <p>{this.state.timer}</p>
           </div>
       )
   }
  
   // 3) Mounting
   componentDidMount(){
       // access to this. & .setState
       // good for using fetch
       // this.makeTimer() // if invoked before the user receives the UI
           // user would see a '1'
       this.interval =  setInterval(this.makeTimer, 1000)
       // UI starts at '0' 
       // will invoke .makeTimer() every second
   }
 
  
 
   // 4) Mounting and/or Updating
   // arrow function
   makeTimer = () => {
       this.setState(prevState => ({timer: prevState.timer += 1})) //adds 1
       // my console told me I should not mutate state directly
       // in the documentation anytime you use .setState()
           // access to .setState((prevState, prevProps) => ({})
   }
  
   // Last) Unmounting
   componentWillUnmount() {
       // last lifecycle method to be called
       clearInterval(this.interval)
       // no access to .setState()
       // common uses: invalidating timers,
           // canceling network requests,
           // cleaning up subscription created in componentDidMount()
   }
}
 
export default Timer
```

Remove the commented out part to invoke `this.makeTimer()` in `componentDidMount()` and watch how it changes the UI experience. Upon initial render you can see that `componentDidMout()` was called. Before you saw the `render()` a new state had been set.
