---
title: "Elevate Code Skills: First Class Functions in JavaScript"
seoTitle: "Elevate Code Skills: First Class Functions in JavaScript"
datePublished: Mon Feb 19 2024 17:54:10 GMT+0000 (Coordinated Universal Time)
cuid: clst8k7x9000309l7bnkvcwd0
slug: elevate-code-skills-first-class-functions-in-javascript
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1708364806525/11120b77-631b-4f21-83c0-531ed5fe2569.png
tags: programming-blogs, javascript, web-development, hashnode, 2articles1week, wemakedevs

---

## Introduction:

JavaScript, the language that gives life to the web, is a domain where functions reign supreme. These functions, known as the "heartbeat" of JavaScript, significantly impact code dynamics. In this adventure across the code cosmos, let us discover the enchantment hidden inside <mark> First Class Functions</mark> and <mark>Anonymous Functions</mark>.

---

## Understanding Functional Statements:

Function statements serve as the core building blocks of JavaScript. Consider the following example.

```javascript
function a() {
  console.log("Hello");
}
a(); // Hello
```

a() is a function statement that produces the intended output when invoked.

## Understanding Function Expressions:

Function expressions involve applying a function to a variable while treating functions as values.

```javascript
var b = function() {
  console.log("Hello");
}
b();
```

In this case, b() is a function expression that provides flexibility and serves as a value.

## Addressing the Hoisting Dilemma

The notion of Hoisting helps you understand the difference between function statements and expressions. Consider this specific example

```javascript
a(); // "Hello A"
b(); // TypeError
function a() {
  console.log("Hello A");
}
var b = function() {
  console.log("Hello B");
}
// Why? During memory creation phase a is created in memory and function assigned to a. 
//But b is created like a variable (b:undefined) and until code reaches the function()  part, it is still undefined. So it cannot be called.
```

Hoisting treats function statements uniquely than expressions, which affects their accessibility.

## Understanding Function Declarations :

Function declarations are an alternate name for function statements, which expands your coding vocabulary.

## Enigma of Anonymous Functions:

A function without name is anonymous function. They don't have their identity and they are used in place where functions are used as values.

```javascript
function () {

}
// this is going to throw Syntax Error - Function Statement requires function name.
```

An anonymous function without code returns an error due to a lack of identity. They find benefit when functions are used as values, as in function expressions.

## Named Function Expressions: Balancing Identity.

Same as Function Expression but function has a name instead of being anonymous.

```javascript
var b = function xyz() {
  console.log('b called');
};
b(); // "b called"
xyz(); // Throws ReferenceError:xyz is not defined.
// xyz function is not created in global scope. So it can't be called.
```

Named functions, on the other hand, have a limited scope, which limits their global accessibility.

## Learning Parameters and Arguments

Understanding the distinction between parameters and arguments is crucial.

```javascript
 function info(name, age){ // labels/identifiers are like parameters
    console.log ("Hi "+ name + ",you are " + age +" years old now.");
}
info("Siddhesh", 20);// arguments are values passed inside function call
// output: Hi Siddhesh,you are 20 years old now.
```

Here, name and age are parameters and Siddhesh and 20 are arguments, which represent values in a function call.

## Understanding first class functions or First Class Citizens:

Functions can be passed as arguments or returned from a function. The ability to utilise functions as values is known as first-class function. It is a programming idea that is also accessible in a few other languages.

```javascript
var b = function (param1) {
  console.log(param1); 
};
b(function () {
});// output: f() {}

// Other way of doing the same thing.But, it is named.
var b = function (param1) {
  console.log(param1);
};
function xyz() {}
b(xyz); // output: f xyz() {} 


// again doing the same thing. we can return a function from a function:
var b = function (param1) {
  return function xyz() {
};
};
console.log(b()); //we log the entire fun within b. output: f xyz() {}
```

---

## Conclusion: Improving Your JavaScript Understanding

In the complex world of JavaScript, understanding every aspect of functions, from statements to expressions, and embracing the power of First Class Functions is critical. These notions not only improve code readability, but they also pave the way for new development approaches.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1708364936801/7ecd513f-da11-4bfb-a1b2-fd004a97ab55.jpeg align="center")

---