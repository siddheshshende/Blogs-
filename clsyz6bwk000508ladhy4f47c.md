---
title: "Callback Functions and Event Listeners in JavaScript."
seoTitle: "Callback Functions and Event Listeners in JavaScript."
datePublished: Fri Feb 23 2024 18:18:03 GMT+0000 (Coordinated Universal Time)
cuid: clsyz6bwk000508ladhy4f47c
slug: callback-functions-and-event-listeners-in-javascript
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1708712208895/08235155-7215-46ad-9073-0126df62a9ec.png
tags: programming-blogs, javascript, web-development, hashnode, 2articles1week, wemakedevs

---

## Introduction

In the fast-paced world of web development, understanding the complexities of JavaScript is essential for creating cutting-edge and responsive applications. This blog post will look into the symbiotic relationship between two essential JavaScript concepts: <mark>callback functions and event listeners</mark>. As we delve deeper into these notions, we will discover the transformational powers they provide to developers, enabling a seamless merger of synchronous and asynchronous activities. Join us on this adventure as we explore the potential of callback functions and the efficiency of event listeners, opening up new possibilities in the world of web programming.

---

## Callback Functions: Exploring Asynchronous Possibilities

Functions are more than just lines of code in JavaScript; they are treated as first-class citizens. Consider this: taking a function A and handing it to another function B, where A becomes a callback function. This seemingly simple act allows function B to call function A, opening the door to a world of asynchronous possibilities within a synchronous environment.

```javascript
setTimeout(function () {
  console.log("Timer");
}, 1000);
```

The first argument is a callback function, while the second is a timer. Callbacks allow JavaScript, which is essentially synchronous and single-threaded, to ignore its nature and perform asynchronous activities.

```javascript
setTimeout(function () {
  console.log("timer");
}, 5000);

function x(y) {
  console.log("x");
  y();
}

x(function y() {
  console.log("y");
});
// o/p: x y timer
```

x and y are the first functions to appear on the call stack. After execution, they clear the stack. The anonymous function then appears in the stack 5 seconds later, due to setTimeout.  
  
Understanding the consequences is critical; any operation that blocks the call stack is referred to as blocking the main thread. For example, if x() takes 30 seconds, JavaScript must wait for it to complete because it only has one call stack and one main thread. Always use async for time-consuming operations like setTimeout.

## Understanding Callbacks: Another Example

Let's look at another example to further understand the callback concept:

```javascript
function printStr(str, cb) {
    setTimeout(() => {
        console.log(str);
        cb();
    }, Math.floor(Math.random() * 100) + 1)
}

function printAll() {
    printStr("A", () => {
        printStr("B", () => {
            printStr("C", () => {})
        })
    })
}

printAll(); 
// o/p: A B C // in order
```

## Using the Power of Event Listeners

**Implementing a Basic Event Listener.**

Moving beyond callbacks, let's look at Event Listeners. Consider building a button in HTML and assigning an event to it.

```xml
<!-- index.html -->
<button id="clickMe">Click Me!</button>
```

In your JavaScript file:

```javascript
// in index.js
document.getElementById("clickMe").addEventListener("click", function xyz(){
      console.log("Button clicked");
});
```

### Taking it Up a Peak: Increase Counter Button

To improve user involvement, let's build an increment counter button:

```javascript
let count = 0;
document.getElementById("clickMe").addEventListener("click", function xyz(){ 
    console.log("Button clicked", ++count);
});
```

### Using Closures for Data Abstraction,now.

Closures are a cleaner way to abstract data.

```javascript
function attachEventList() {
    let count = 0;
    document.getElementById("clickMe")
     .addEventListener("click", function xyz(){ 
     console.log("Button clicked", ++count);
    });
}
attachEventList();
```

## Event Listener Demo: Efficient Resource Management.

Event listeners, while effective, might be resource-intensive owing to closures. Even if the call stack is empty, the EventListener may not free the memory allocated to count. To optimize, event listeners should be removed when they are no longer required, avoiding excessive memory usage.

> Garbage Collection and removeEventListeners is performed.
> 
> onClick, onHover, onScroll etc all in a page can slow it down heavily.

---

## Conclusion: Understanding the System of Callbacks and Event Listeners

Finally, knowing the interaction of callback functions and event listeners not only unlocks JavaScript's full capabilities, but also assures efficient resource management. Mastering these concepts allows developers to create flawless and responsive online apps, which is a huge step forward in the pursuit of web development excellence.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1708711708071/71072137-59ee-42e8-9c98-6dc95716c3a4.jpeg align="center")

---