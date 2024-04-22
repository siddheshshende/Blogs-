---
title: "Async/Await in Modern JavaScript Development."
seoTitle: "Async/Await in Modern JavaScript Development."
datePublished: Mon Apr 22 2024 16:37:01 GMT+0000 (Coordinated Universal Time)
cuid: clvb6jnq7000a09ky5do0dh30
slug: asyncawait-in-modern-javascript-development
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1713803491929/a13e9b04-41b6-4b3d-93d6-c11dbcc1f6b8.png
tags: programming-blogs, javascript, web-development, hashnode, 2articles1week, wemakedevs

---

## Introduction

Learning asynchronous programming is super important in the fast-paced world of JavaScript development today. Understanding the magic of <mark>async and await </mark> can make developers write code that's not just elegant but also super productive. Join us on a journey to explore these cool concepts and see how they've totally changed the game in JavaScript development today.

## Async: What Is It?

Fundamentally, async is a keyword that comes before a function and makes it an async function. This little change gives the function the ability to run asynchronously, which enables non-blocking JavaScript activities. It always return a promise.

```javascript
//  async function always returns a promise, 
//even if I return a simple string,boolean or number etc from below function, async keyword will wrap it under Promise and then return.
async function getData() {
  return "Namaste JavaScript";
}
const dataPromise = getData();
console.log(dataPromise); // Promise {<fulfilled>: 'Namaste JavaScript'}

//How to extract data from above promise?? One way is using promise .then
dataPromise.then(res => console.log(res)); // Namaste JavaScript

//One more instance of an async function returning a promise: 
const p = new Promise((resolve, reject) => {
  resolve('Promise resolved value!!');
})

async function getData() {
  return p;
}
// In above case, since we are already returning a promise async function would simply return that instead of wrapping with a new Promise.
const dataPromise = getData();
console.log(dataPromise); // Promise {<fulfilled>: 'Promise resolved value!!'}
dataPromise.then(res => console.log(res)); // Promise resolved value!!
```

## What's Await?

As an addition to async, await is a keyword that works inside async functions to make handling promises easier. Through the usage of await, developers can halt code execution until a promise is fulfilled, making asynchronous programming easier to understand and more linear.

### How we can use `await` along with async function?

`async` and `await` combo is used to handle promises. `await` is a keyword that can only be used inside a `async` function, otherwise it will throw syntax error.

```javascript
//old method:
const p = new Promise((resolve, reject) => {
  resolve('Promise resolved value!!');
})

function getData() {
  p.then(res => console.log(res));
}
getData(); // Promise resolved value!!

//Till now, we have been using Promise.then/.catch to handle promise.
//Now let's see, how async await can help us and how it is different
//New method:
// The rule is we have to use keyword await in front of promise.
const p = new Promise((resolve, reject) => {
  resolve('Promise resolved value!!');
})
async function handlePromise() {
  const val = await p;
  console.log(val);
}
handlePromise(); // Promise resolved value!!
```

### Why is async-await unique?

To better understand, let's compare the async-await method of promise resolution with an earlier one using an example.then/catch the trend. To accomplish this, we will modify the promise we made.

```javascript
const p = new Promise((resolve, reject) => {
  setTimeout(() => {
    resolve('Promise resolved value!!');
  }, 3000);
})

// Let's now compare with some modification:

//Promise.then/.catch way:
function getData() {
  // JS engine will not wait for promise to be resolved
  p.then(res => console.log(res));
  console.log('Hello There!');
}

getData(); // First `Hello There!` would be printed and then after 3 secs 'Promise resolved value!!' will be printed.
// Above happened as Javascript wait for none, so it will register this promise and take this callback function and register separately then js will move on and execute the following console and later once promise is resolved, following console will be printed.

//Problem: Normally one used to get confused that JS will wait for promise to be resolved before executing following lines.

//async-wait way:
async function handlePromise() {
  // JS Engine will waiting for promise to resolve.
  const val = await p;
  console.log('Hello There!');
  console.log(val);
}
handlePromise(); // This time `Hello There!` won't be printed immediately instead after 3 secs `Hello There!` will be printed followed by 'Promise resolved value!!'
//  So basically code was waiting at `await` line to get the promise resolve before moving on to next line.

// Above is the major difference between Promise.then/.catch vs async-await

// Let's brainstorm more around async-await
async function handlePromise() {
  console.log('Hi');
  const val = await p;
  console.log('Hello There!');
  console.log(val);

  const val2 = await p;
  console.log('Hello There! 2');
  console.log(val2);
}
handlePromise(); 
// In above code example, will our program wait for 2 time or will it execute parallely.
//`Hi` printed instantly -> now code will wait for 3 secs -> After 3 secs both promises will be resolved so ('Hello There!' 'Promise resolved value!!' 'Hello There! 2' 'Promise resolved value!!') 
//will get printed immediately.

// Let's create one promise and then resolve two different promise.
const p2 = new Promise((resolve, reject) => {
  setTimeout(() => {
    resolve('Promise resolved value by p2!!');
  }, 2000);
})

async function handlePromise() {
  console.log('Hi');
  const val = await p;
  console.log('Hello There!');
  console.log(val);

  const val2 = await p2;
  console.log('Hello There! 2');
  console.log(val2);
}
handlePromise(); 
//`Hi` printed instantly -> now code will wait for 3 secs -> After 3 secs both promises will be resolved so ('Hello There!' 'Promise resolved value!!' 'Hello There! 2' 'Promise resolved value by p2!!') 
//will get printed immediately. So even though `p2` was resolved after 2 secs it had to wait for `p` to get resolved


// Now let's reverse the order execution of promise and observe response.
async function handlePromise() {
  console.log('Hi');
  const val = await p2;
  console.log('Hello There!');
  console.log(val);

  const val2 = await p;
  console.log('Hello There! 2');
  console.log(val2);
}
handlePromise(); 
// `Hi` printed instantly -> now code will wait for 2 secs -> After 2 secs ('Hello There!' 'Promise resolved value by p2!!') 
//will get printed and in the subsequent second i.e. after 3 secs ('Hello There! 2' 'Promise resolved value!!') will get printed
```

### Is the program genuinely waiting or is something else going on in the background?

Time, tide, and JS, as we all know, wait for no one. That is accurate. Although it looks like the JS engine is waiting over here, it is not. It hasn't taken up any space in the call stack; if it had, our page might have frozen. Thus, the JS engine is not idle. What is it doing in the background if it isn't waiting? Let's explore with the code sample below.

```javascript
const p1 = new Promise((resolve, reject) => {
  setTimeout(() => {
    resolve('Promise resolved value by p1!!');
  }, 5000);
})

const p2 = new Promise((resolve, reject) => {
  setTimeout(() => {
    resolve('Promise resolved value by p2!!');
  }, 10000);
})

async function handlePromise() {
  console.log('Hi');
  debugger;
  const val = await p;
  console.log('Hello There!');
  debugger;
  console.log(val);

  const val2 = await p2;
  console.log('Hello There! 2');
  debugger;
  console.log(val2);
}
handlePromise(); 
// When this function is executed, it will go line by line as JS is synchronous single threaded language. Lets observe what is happening under call-stack. Above you can see we have set the break-points.

// call stack flow -> handlePromise() is pushed -> It will log `Hi` to console -> Next it sees we have await where promise is suppose to be resolved -> So will it wait for promise to resolve and block call stack? 
//No -> thus handlePromise() execution get suspended and moved out of call stack -> So when JS sees await keyword it suspend the execution of function till promise is resolved -> So `p` will get resolved 
//after 5 secs so handlePromise() will be pushed to call-stack again after 5 secs. -> But this time it will start executing from where it had left. -> Now it will log 'Hello There!' and 'Promise resolved value!!' -> then it will check whether `p2` is resolved or not -> It will find since `p2` will take 10 secs to resolve 
//so the same above process will repeat -> execution will be suspended until promise is resolved.

//Thus JS is not waiting, call stack is not getting blocked.

// Moreover in above scenario what if p1 would be taking 10 secs and p2 5 secs -> even though p2 got resolved earlier but JS is synchronous single threaded language so it will first wait for p1 to be resolved and then will immediately execute all.
```

## Real-world Async/Await Example

Imagine a situation in which we asynchronously retrieve data from an external API. We can improve readability and maintainability by streamlining the process with async and await.

fetch() always give us promise and fetch() return a response (It is an response object).

```javascript
const fetch_url = "any api url";

async function fetchData() {
    const response = await fetch(fetch_url);
    const data = await response.json();
    console.log(data);
  };
fetchData();
```

## Error Handling

In async-await, we would use the try-catch block to handle errors instead of the .catch we used with regular Promise. So Basically, there are 2 methods to handle error in JavaScript : .catch method and try-catch method.

```javascript
const fetch_url = "any api url";

async function handlePromise() {
  try {
    const data = await fetch(fetch_url);
    const res = await data.json();
    console.log(res);
  } catch (err) {
    console.log(err);
  };
};
handlePromise();
// In above whenever any error will occur the execution will move to catch block. One could try above with bad url which will result in error.
// Other way of handling error:
handlePromise().catch(err => console.log(err)); // this will work as handlePromise will return error promise in case of failure.
```

## Promise versus Async/await :

**Which one should you use?**

* async/await is nothing more than syntactical sugar.
    
* In the background, async-await only promises things. Thus, both are the same
    
* async-await is just a new programming style.
    
* A few of Promise's shortcomings, such Promise Chaining, are fixed with async-await.
    
* Additionally, async-await improves readability.
    
* So in a manner, using async-await is always advised.
    

## Conclusion:

To sum up, any JavaScript developer who wants to fully utilise asynchronous programming must understand async and await. Developers can achieve new heights of efficiency and elegance in their code by grasping their complexities and making the most of their potential.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1713789199609/6cb33a6e-f68d-4e84-9259-f7b1878cc0ee.jpeg align="center")

---