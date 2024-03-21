---
title: "Understanding SetTimeout() and Concurrency in JavaScript."
seoTitle: "Understanding SetTimeout() and Concurrency in JavaScript."
datePublished: Thu Mar 21 2024 20:15:27 GMT+0000 (Coordinated Universal Time)
cuid: clu1o9b0p000109jrge896qwi
slug: understanding-settimeout-and-concurrency-in-javascript
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1711052017247/94d2317f-ce2c-41c0-935a-67b38f2f731b.png
tags: programming-blogs, javascript, web-development, hashnode, 2articles1week, wemakedevs

---

## Introduction

JavaScript is a fundamental component in the large field of web development, enabling dynamic and interactive experiences on the internet. The setTimeout() method, which is valued for its capacity to run code asynchronously, is essential to its operation. But beyond the surface simplicity of it all is a hidden problem: <mark> trust issues</mark> with timing accuracy.

The complexities of JavaScript's asynchronous actions get increasingly complex, and developers must grasp the fundamental workings of setTimeout(). In this article, we attempt to solve the puzzles connected to its behaviour and clarify why this so-called dependable function doesn't always perform up to mark.

Come along as we explore the inner workings of <mark>JavaScript concurrency</mark>, examining the nuances of <mark>setTimeout()</mark> and revealing practical solutions to address its trust issues.

---

## The lack of clarity of SetTimeout():

The root of the difficulty is the confusion around the execution timing of the callback function passed to setTimeout(). Consider this code snippet:

```javascript
console.log('Start');
setTimeout(function cb() {
  console.log('Callback');
}, 5000);
console.log('End');
```

In this case, one may anticipate the callback code to execute exactly after 5 seconds. However, reality sometimes deviates from this notion.

### figuring out what's Happening in code:

1. Initialization: When setTimeout() is called, JavaScript starts a timer for the specified duration.
    
2. Continuation: Meanwhile, the main thread of execution continues without waiting for the timer to expire.
    
3. Execution Flow: Code execution proceeds, and some extra tasks are completed, such as printing "Start" and "End".
    
4. Callback Queuing: While the main thread is still active, the timer quietly counts down in the background.
    
5. Concurrency Model: JavaScript's execution model is single-threaded, which means it can only handle one task at a time.
    
6. Delayed execution:Despite the timeout, the callback function waits for its turn in the callback queue until the call stack is cleared.
    

## consequences :

1. Timing Discrepancy: Because setTimeout() is asynchronous, the callback may run with a delay longer than the provided duration.
    
2. Dependence on the Call Stack: Until the call stack is cleared, the callback stays in limbo(confusion), potentially leading to delays.
    
3. Concurrency Issues: The JavaScript event loop meticulously supervises task execution, but it cannot overcome the fundamental limits of a single-threaded system.
    

## The core of JavaScript's concurrency model

JavaScript prioritizes non-blocking activities to ensure responsiveness and efficiency. This requires extreme caution when using asynchronous operations such as setTimeout().

JavaScript was not designed for concurrency,as js is single threaded and synchronous.But, with the help of js Event Loop, it can perform server-side and client-side concurrency.

concurrency model tells us how exactly js handles multiple tasks happening at same time.

### Practical views:

* Avoid blocking: Use non-blocking paradigms to avoid stopping the main thread, resulting in smooth application performance.
    
* Optimise responsiveness: Use asynchronous actions wisely to establish a balance between functionality and user experience.
    

---

In the following example, we are blocking the main thread.Though, first rule of JavaScript is to not block the main thread (because JS is a single threaded language with only one callstack).

we are simulating blocking kind of environment (by suppose million lines of code) by using while loop to create it.

New Date() is a constructor function that returns a specified or current date and time.

getTime() is a method which is used to get timestamp in milliseconds of 'date' object.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1711049984970/38fa79c2-1390-48e2-b48f-36b11c75acc5.jpeg align="center")

### Using the Power of setTimeout():

While setTimeout() remains a useful tool in JavaScript programming, understanding it's oddities is critical for effective use. Understanding the complexities of timing disparities allows developers to use this function with precision and planning.

### Fine-Tuning Execution

**Strategic Delay**: Carefully setting timeouts allows you to prioritise vital tasks while deferring less urgent ones.

**Mitigating Risks:** Anticipate timing variances and create code to elegantly handle potential delays.

---

## What if timeout = 0sec?

When setTimeout()'s timeout option is set to 0 seconds, it may appear natural to anticipate the callback function to be executed immediately. However, JavaScript behaves differently as setTimeout() is registered, though it is zero.

```javascript
console.log('Start');
setTimeout(function cb() {
  console.log('Callback');
}, 0);
console.log('End');
// o/p: Start End callback
```

This use of setTimeout() with a timeout of 0 seconds can help to prioritise crucial tasks while delaying less important ones slightly. Developers can use this technique deliberately to optimise the execution flow of their JavaScript apps, improving overall performance and responsiveness.

## conclusion

While setTimeout() may have trust issues with timing precision, understanding how it works enables developers to traverse JavaScript's concurrent world effectively. Programmers can maximise the benefits of asynchronous programming by adopting an adaptable and anticipation attitude.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1711048920264/96fc56b2-3226-4b33-b745-568a69c9a18e.jpeg align="center")

---