---
layout: post
title: 'How to create a step by step script'
date: "2019-04-17 13:59:00 +0200"
author: benoit
version: 1.0.0
categories: snippets
comments: true
post_description: Sometimes you need to slow things down to provide visual feedback to the user. Here's how to create a step by step script.
---

Some time ago, I was working on a app that generates json config files for online courses.
It was working great and the building process was fast. Too fast.  
It wasn't providing any **visual feedback** to the end user and no way of understanding what's going on. Here's a great 
[article](https://www.smashingmagazine.com/2017/01/how-functional-animation-helps-improve-user-experience/) on the subject.

So I looked for a way of slowing things down and provide a step by step animation when generating thoses files. 
I thought it will be a straightforward process using `setTimeout` but I was wrong.

My building script use different functions with parameters for each step and I couldn't 
simply add a `setTimeout` to each call **and** passing arguments.

Here's a basic script that illustrate the problem :

```js
// Each function take the results from previous steps, do some logic and pass it to the next one

function step1(foo) {
  // some logic and pass result to next step
  var bar = foo * 2
  step2(foo, bar)
}

function step2(foo, bar) {
  // some logic and pass result to next step
  var foobar = (foo + bar) * 2
  step3( foo, bar, foobar)
}

function step3(foo, bar, foobar) {
  console.log(foo + bar + foobar)
}

step1(2) // logs '18' immediately
```

So the solution is to rely on a callback and `...args` parameter to pass an undeterminated number of arguments to the 
the callback. That way you can create a function that takes the next step function as a callback and arguments to pass 
on after a certain delay. And at each step you can update your view to provide an animation feedback to the user.

```js
function nextStep(cb, ...args) {
	setTimeout(() => {
  	cb(...args)
  }, 1000)
}

function step1(foo){
  // some logic and pass result to next step
  var bar = foo * 2
	nextStep(step2, foo, bar)
}

function step2(foo, bar){
  // some logic and pass result to next step
  var foobar = (foo + bar) * 2
  nextStep(step3, foo, bar, foobar)
}

function step3(foo, bar, foobar){
  // some logic and pass result to next step
 console.log(foo + bar + foobar)
}

step1(2) // logs '18' after some time
```

See this working example :

<iframe width="100%" height="350" style="border: 1px solid #f0f0f0;" src="//jsfiddle.net/yskth1z3/1/embedded/result/" allowfullscreen="allowfullscreen" allowpaymentrequest frameborder="0"></iframe>
