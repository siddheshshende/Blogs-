---
title: "Learn Event Loop And Asynchronous JavaScript."
seoTitle: "Learn Event Loop And Asynchronous JavaScript."
datePublished: Sun Mar 10 2024 19:56:57 GMT+0000 (Coordinated Universal Time)
cuid: cltlxr5os000v09jy3lss8tk1
slug: learn-event-loop-and-asynchronous-javascript
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1710100415446/7b733112-0df8-4359-ad3c-f2386bd6e748.png
tags: programming-blogs, javascript, web-development, hashnode, 2articles1week, wemakedevs

---

In the dynamic world of web development, the ability to leverage the power of <mark>asynchronous JavaScript</mark> is essential. This piece of writing takes you on an educational trip, exposing the complexities of Asynchronous JavaScript and simplifying the frequently confusing idea of the <mark>Event Loop.</mark>

---

## The Basics: Call Stack and JavaScript Engine.

Time, tide, and JS(JavaScript) do not wait for anyone. The Call Stack, a key component of the JS Engine, runs any execution context that enters it. But what about the other superpowers the browser has?

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1710091035888/3156e7cc-5424-42eb-ab44-c24b3663433d.jpeg align="center")

## Web APIs: Bringing Call Stack to Superpowers

The browser provides a variety of superpowers, like local storage, timers, geolocation access, fetch and more. Web APIs can help bridge the gap between the call stack and these capabilities.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1710091055857/937caab5-62c6-44ec-8b81-8e924fa06be0.jpeg align="center")

## Understanding web APIs

Web APIs, which are not inbuilt in JavaScript, enable the call stack to exploit browser superpowers. Examples include setTimeout(), DOM APIs, get(), and localStorage. These functions are accessed via the global object "window".

```javascript
console.log("Start");
setTimeout(function cb() {
  console.log("Timer");
}, 5000);
console.log("End");
// Output: Start, End, Timer (after 5 seconds)
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1710097770941/1cf56813-a8c8-42f7-b656-0b8ceed68663.jpeg align="center")

## The Event Loop Is Introduced

How can we ensure that callbacks are executed on time now that we have Web APIs in place? Enter the Event Loop, a gatekeeper that monitors the Callback Queue for pending jobs and moves them to the call stack.

```javascript
// Accessing superpowers through the global object(window)
window.setTimeout(function cbT() {
  console.log("Callback Timeout");
}, 5000);

window.fetch("https://api.netflix.com").then(function cbF() {
  console.log("Callback Netflix");
});
```

## Demonstrating the Event Loop

Let us deconstruct a code excerpt to see the Event Loop in action. Every step, from creating the Global Execution Context to executing callbacks, is critical to understanding JavaScript's asynchronous behaviour.

```javascript
console.log("Start");
document.getElementById("btn").addEventListener("click", function cb() {
  console.log("Callback");
});
console.log("End");
```

## Callback Queue and Its Importance

Why does the callback queue exist? Consider this scenario: a user clicks a button many times. The Event Loop guarantees that all callbacks from those clicks are executed efficiently, avoiding potential delays.

## Microtask Queue: Priority System

Not all tasks are created equally. The Microtask Queue, which has a higher priority than the Callback Queue, handles callback functions from Promises and Mutation Observers quickly. Understanding this priority scheme is critical for efficient code execution.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1710098946139/92b20e07-3038-4473-a502-f9544936ef28.gif align="center")

## Fetch Behaviour and Microtask Priority

Analyse the behaviour of fetch together with the Microtask Queue. Asynchronous processes, such as waiting for data from external services, show the complex interaction between the Callback Queue and the Microtask Queue.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1710098702107/c40294f5-354c-4fee-816d-9bfa639e9e42.jpeg align="center")

```javascript
console.log("Start");
setTimeout(function cbT() {
  console.log("CB Timeout");
}, 5000);
fetch("https://api.netflix.com").then(function cbF() {
  console.log("CB Netflix");
}); // take 2 seconds to bring response
// millions lines of code
console.log("End");
```

### Observing Event Loop, Callback Queue, and Microtask Queue \[GiF\]:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1710099268017/44816111-46c7-4cb8-9b38-ede124fa078b.gif align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1710099319089/3c15894a-2e0a-49fb-ac92-f9611b3881e2.gif align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1710099353454/7da11796-4f6f-4fff-a70c-4c5332e192e1.gif align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1710099392882/fe3c9805-ddb8-41ca-94ef-01acda43d889.gif align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1710099427691/8eba54cf-1d39-4af1-a9a6-3f6dc5b2f63c.gif align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1710099445701/05f6cd55-dc24-4763-a1d0-5176bade0f6d.gif align="center")

A mesmerising GIF depicts the complicated dance of the Event Loop, Callback Queue, and Microtask Queue. Gain a better knowledge of how these components interact naturally.

---

## Conclusion: Knowing Asynchronous JavaScript.

It is critical for developers to understand the complications of Callback and Microtask Queues, as well as the Event Loop. This post attempted to clarify these ideas and lay a solid foundation for understanding JavaScript's asynchronous ecosystem.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1710099541289/39a4d2f1-1834-445d-9094-9f91f46619f0.jpeg align="center")

---