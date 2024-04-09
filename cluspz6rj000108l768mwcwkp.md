---
title: "all about JavaScript's callback function."
seoTitle: "all about callback function in javascript."
datePublished: Tue Apr 09 2024 18:33:21 GMT+0000 (Coordinated Universal Time)
cuid: cluspz6rj000108l768mwcwkp
slug: all-about-javascripts-callback-function
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1712687133672/e9825739-9c90-4324-a914-11a4aa520c46.png
tags: programming-blogs, javascript, web-development, hashnode, 2articles1week, wemakedevs

---

## Introduction

In the world of JavaScript programming, callback functions are essential, especially when managing asynchronous operations. They are essential tools that enable the execution of code smoothly and efficiently by carrying out activities without stopping the program as a whole.  
We'll examine the dual nature of <mark>callback functions</mark> in this article, looking at both their advantages and disadvantages. We'll go into details of callback functions and their significance in asynchronous code, as well as how they affect contemporary JavaScript development. We'll also discuss about <mark>Callback Hell </mark> and <mark>Inversion of Control</mark>.

---

## Callback Functions: An Overview of the Good and the Bad

### **The Good Part of Callback Functions**

In JavaScript, callback functions are crucial when working with asynchronous programming. They ensure seamless and effective performance by enabling the completion of tasks without waiting for the completion of the preceding one.

JavaScript is a synchronous, single-threaded language. However, callbacks allow us to accomplish async things in JavaScript.It is used with closures and often passed as an argument in functional programming.

callback functions are functions that are included as arguments to other functions and then performed when a specified event occurs or an asynchronous operation is completed. In short, **a function passed inside another function as an argument is called as callback function.**

### How we can create a callback function ??

\=&gt; however, we will first wrap certain statement inside a function and then, we will passed it onto setTimeout or any other function. Now, job of setTimeout will be to execute the function which is passed after some time(interval).

consider the *example* which is mentioned below to understand it properly.

Here, we are using the callback method of setTimeout in order to delay the execution.

```javascript
console.log('you');
setTimeout(function () {
  console.log('wealthy');
}, 5000);
console.log('are');
/* o/p: 
you
are
wealthy (it will get printed after 5 sec)*/
```

### The Bad Part of Callback Functions

Callback functions are useful, but they have drawbacks of their own. There are two main problems that come up frequently:

**1\. Callback Hell:**  
The code can easily become complicated and challenging to manage when working with nested callback methods, and code grows horizontally instead of vertically, resulting in what is sometimes referred to as "Callback Hell" or the "Pyramid of Doom."

When we have a huge codebase and many apis and have dependency on each other, then we fall into callback hell. Then, the code becomes tough to maintain and read.

```javascript
//E-commerce website example 
const products =[" shoes", "airpods", "headphones"];

Api.createorder( cart, function(){
    api.paymentprocess(function(){
        api.ordersummary(function(){
            api.checkout()
        })
    })
})
/*
See the pyramid shape and all the }) at the end repeating? This is affectionately known as callback hell.

The cause of callback hell is when people try to write JavaScript in a way where execution happens visually from top to bottom. 
Lots of people make this mistake! In other languages like C, Ruby or Python there is the expectation that whatever happens on line 1 will finish before the code on line 2 starts running and so on down the file. 
As you will learn, JavaScript is different.
*/
```

**2\. Inversion of Control**:

Because callback functions depend on parent functions to correctly execute them, developers may lose control over the flow of the code as a result of using callback functions. This reliance may result in unexpected mistakes and maintenance issues.

In short, We give authority to the function that calls our callback function; possibly it will never be invoked, or our function may be called twice due to something that is present in their function. **Inversion of control is like that you lose the control of code,when we are using callback.**

```javascript
api.createOrder(cart, function () {
  api.proceedToPayment();
});
//here, proceedToPayment function is dependent on createOrder function.
//So,we don't know proceedToPayment function will get invoked or not.
```

## How to Avoid callback hell ??

Developers can use more manageable and cleaner code structures by using alternative tactics like async/await syntax, modularization, or promises to avoid slipping into the hole of Callback Hell.

---

## Conclusion

Although callback functions are necessary for JavaScript asynchronous programming, they have certain drawbacks. It is essential for developers to comprehend callback functions' advantages and disadvantages in order to design effective and manageable code.

> Research Further  
> Visit [callbackhell.com](http://callbackhell.com) to learn more about asynchronous programming and callback functions.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1712686479528/6770acaf-2159-4953-aea8-3c8b31da98f4.jpeg align="center")

---