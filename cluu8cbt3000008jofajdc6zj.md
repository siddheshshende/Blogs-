---
title: "The Role of Promises in Modern JavaScript Development."
seoTitle: "The Role of Promises in Modern JavaScript Development."
datePublished: Wed Apr 10 2024 19:55:13 GMT+0000 (Coordinated Universal Time)
cuid: cluu8cbt3000008jofajdc6zj
slug: the-role-of-promises-in-modern-javascript-development
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1712778790908/ce8771c6-96b2-496f-82e0-922ab22dcf7b.png
tags: programming-blogs, javascript, web-development, hashnode, 2articles1week, wemakedevs

---

## Introduction

Asynchronous operations are vital for creating responsive and effective applications when using JavaScript programming. Dealing with asynchronous code is necessary whether handling user interactions, I/O-bound processes, or retrieving data from an external API. But callback functions were previously a major part of controlling asynchronous operations, which resulted in complicated and difficult-to-maintain code structures.  
<mark>Promises</mark> were proposed as a simpler, more manageable solution to asynchronous operation management in order to overcome these issues. A standardised interface for expressing the eventual success or failure of an asynchronous activity is offered by promises. They make it easier to organise code and handle errors by enabling developers to attach callbacks to handle the outcomes of asynchronous actions.

---

## Before Promises: The Callback function

Let's first review how callbacks were previously used to manage asynchronous actions before delving into Promises. Take into consideration the following hypothetical situation at an online store:

```javascript
const cart = ['shoes', 'pants', 'kurta'];

// Callback approach
createOrder(cart, function () {
  proceedToPayment(orderId);
});
// here, we are passing the function to createOrder Api(or function).And,we are blindly trusting the Api.
```

The createOrder function in this callback method runs asynchronously and calls the supplied callback function when it's finished. This method creates layered and difficult-to-maintain code structures because it suffers from inversion of control, where the callback function's execution is dependent on the asynchronous operation.

## After introducing Promises:

Callback problems led to the development of Promises as a fix. Promises offer a more organised and controllable approach to working with asynchronous code by representing the eventual success or failure of an asynchronous operation. Let's use Promises to restructure the previous example:

```javascript
const cart = ['shoes', 'pants', 'kurta'];

const promiseRef = createOrder(cart);// this promiseRef has access to `then`

// {data: undefined}
// Initially it will be undefined so below code won't trigger
// After some time, when execution has finished and promiseRef has the data then automatically the below line will get triggered.
promiseRef.then(function () {
  proceedToPayment(orderId);
});
//here, we attached the function to createOrder Api and we can blindly trust promise.
```

The createOrder function in this rewritten code instantly returns a Promise object, which stands for the operation's future completion. Using the .then function, we attach a callback that will be triggered after the order creation is finished, which is the fulfilment of the promise.

## Advantages of Making Promises

Compared to the typical callback method, promises provide the following advantages:

1. Cleaner Code: Promises provide a more linear and legible code structure, which makes asynchronous code easier for developers to understand and maintain. This helps prevent callback hell.
    
2. Inversion of Control: Promises help to improve code organisation and maintainability by reading the code more synchronously while maintaining the control flow.
    
3. Error Handling: By using the catch method, promises incorporate built-in error handling techniques that enable centralised error management for asynchronous processes.
    
4. Promise Chaining: By enabling the sequential chaining of several asynchronous processes, promises help to minimise nesting and enhance the readability of code.
    

---

## What is Promise??

\-&gt; Promise object is a placeholder which will be filled latter with a value from asynchronous operation.

\-&gt; Promise is a container for future value.

\-&gt; **A Promise is an object representing the eventual completion or failure of an asynchronous operation.**

* Promise Objects are immutable (Upon the fulfilment of the promise, we will have data that we can pass on without fear of data tampering or mutating means promises, once resolved are immutable; thus building up immense trust).
    
* Promise can be resolved only once, either by `success` or `failure`.
    
* Promise has 2 main things:
    
    \-&gt;State of Promise(**<mark>PromiseState</mark>**): It tells us in what state promise is. There are three states in Promise which are
    

1. pending: initial state, neither fulfilled nor rejected.
    
2. fulfilled: meaning that the operation was completed successfully.
    
3. rejected: meaning that the operation failed.
    

> As soon as promise is fulfilled/rejected =&gt; It updates the empty object which is assigned undefined in pending state.

\-&gt;Result of Promise(**<mark>PromiseResult</mark>**): It will store the data whatever it returns.

## Use of Promises in the Real World

Promises are frequently used in conjunction with native browser APIs like fetch, which returns a Promise that represents the response to the HTTP request. They are not simply restricted to asynchronous operations.

As a reference, consider this example:

```javascript
//We will be calling public github api to fetch data i.e https://api.github.com/users/siddheshshende
const GitHubapi = "https://api.github.com/users/siddheshshende";
const user = fetch(GitHubapi);
// User will be considered as promise.
console.log(user); 
//o/p: Promise {<Pending>}
```

Fetch(): Fetch() is basically an API given by browsers to us to make external calls.

Now,we can attach callback to above response/promise by using `.then` only.

```javascript
//And so, this is how Promise is used by .then method.
//It guarantees that it could be resolved only once, either it could be `success` or `failure`
const GitHubapi = "https://api.github.com/users/siddheshshende";
const user = fetch(GitHubapi);

user.then(function (data) {
  console.log(data);
});
// Using .then(), we can control when we want to call/invoke the cb(callback) function.
```

Promises are used to *solve the problems* of callbacks like inversion of control and callback hell (Pyramid of doom).

1. .then solves one issue of callback i.e. Inversion of Control.
    
2. **Promise chaining** solves another issue of callback i.e callback hell.
    

```javascript
// Callback Hell Example
createOrder(cart, function (orderId) {
  proceedToPayment(orderId, function (paymentInf) {
    showOrderSummary(paymentInf, function (balance) {
      updateWalletBalance(balance);
    });
  });
});
// here,above code is expanding horizontally instead of vertically and this is called pyramid of doom.
//So, Promise fixes this issue too using `Promise Chaining`
// Example Below is of Promise Chaining.
createOrder(cart)
  .then(function (orderId) {
    proceedToPayment(orderId);
  })
  .then(function (paymentInf) {
    showOrderSummary(paymentInf);
  })
  .then(function (balance) {
    updateWalletBalance(balance);
  });

// ⚠️ Common PitFall/mistake many developers make is
// they forget to return promise in Promise Chaining
// The idea is promise/data returned from one .then become data for next .then
// So,
createOrder(cart)
  .then(function (orderId) {
    return proceedToPayment(orderId);
  })
  .then(function (paymentInf) {
    return showOrderSummary(paymentInf);
  })
  .then(function (balance) {
    return updateWalletBalance(balance);
  });
// when we don't return the promise in promise chain, then at that time, we can lose
// some data. Thus, it is recommended to return promise.
```

```javascript
// trying to explain the example and show different ways to write Promise.
// here, in the below line, createorder Api was returning us a promise.(promise is a variable in this case)
const promise = createOrder(cart);
// And then, we were attaching a callback function to createorder Api returned promise.
promise.then(function (orderId) {
  proceedToPayment(orderId);
});

//another way to write same code   
createOrder(cart).then(function (orderId) {
    proceedToPayment(orderId);
  });

//another way to write same code is by arrow function.
createOrder(cart)
  .then((orderId) => proceedToPayment(orderId));
```

## Conclusion

JavaScript asynchronous programming has been transformed with promises, which provide a more organised and controllable substitute for conventional callback-based methods. Promises improve code readability, maintainability, and error handling by offering a standardised interface for managing asynchronous processes. Since promises are the basis of many asynchronous patterns and frameworks in the JavaScript ecosystem, understanding them is crucial for current JavaScript developers. Promises make handling asynchronous code easier to understand and less prone to mistakes, enabling programmers to create reliable and effective applications. Thus, utilise Promises in your JavaScript applications to fully utilise asynchronous programming!

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1712778286879/7721d6da-1f5d-43d4-bae7-261e346725c7.jpeg align="center")

---