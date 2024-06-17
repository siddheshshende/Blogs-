---
title: "Top Ways to Use "this" Keyword in JavaScript."
seoTitle: "Top Ways to Use "this" Keyword in JavaScript."
datePublished: Mon Jun 17 2024 13:43:20 GMT+0000 (Coordinated Universal Time)
cuid: clxj100mi000x0amg43bl6wc3
slug: top-ways-to-use-this-keyword-in-javascript
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1718631473658/c6dbb7f3-6c4e-4215-9042-bbf075870250.png
tags: programming-blogs, javascript, web-development, hashnode, 2articles1week, wemakedevs

---

## Introduction

JavaScript is a strong and flexible programming language, yet its peculiar ideas and actions sometimes confuse engineers. The <mark>"this" keyword</mark> stands out among them as one of the trickiest yet most important to learn. The object that "this" in JavaScript refers to can vary significantly depending on the context in which it is used. We shall examine every scenario in which "this" is used in this post and try to solve the enigma surrounding its behaviour.

---

## 1\. "this" in the global context(space)

The global object is referred to when the "this" keyword is used in the global space.

global object is different in different javascript runtime environment like js is differrent on smart bulbs,smart watches, node.js, browser etc. It depends on where you run the js code.

```javascript
console.log(this); // refers to global object i.e. window in a browser or global in node.js
```

## 2."this" inside a function

The behavior of "this" inside a function varies based on strict mode and non-strict mode(i.e it works differently in both mode).

```javascript
function x() {
    console.log(this);
    // In strict mode:o/p is undefined
    // In non-strict mode:o/p is global object
}
x();
```

When "use strict" is used at the beginning of the script, "this" acts differently inside functions. "this" inside a function is undefined in strict mode, but it points to the global object in non-strict mode.  

## 3."this" Substitution

In non-strict mode, the global object is used(replaced) in place of "this" if the value is null or undefined.

`this` keyword value depends on how the `function` is called.

```javascript
"use strict";
console.log(this);
  function x() {
        console.log(this);
    }
x();
// o/p: window(object)
//      undefined 

//without using strict-mode
console.log(this);
  function x() {
        console.log(this);
    }
x();
// o/p: window(object)
//     window(object)  
//in non strict mode, "this substitution" takes place and "this" points to globalObject
```

## 4."this" in the Method of an Object:

"This" refers to the object itself in the context of its method.

```javascript
const obj = {
    a: 10,
    x: function () {
        console.log(this); // o/p: {a: 10, x: f()}
        console.log(this.a); // o/p: 10
    }
}
obj.x();
```

**Difference between function and method:**

When you make a function as a part of of object , then it is know as method.

when you create a function inside an object, then function x will be a method. So, "x" is a method of object "obj".

## 5.call, apply & bind Methods

The value of "this" can be explicitly set via the call, apply, and bind methods. Basically, they are used to control the value of "this" inside a function.

call, apply & bind are used to share a method with another object (hence,the "this" keyword reference would also change accordingly).

`call` and `apply`Both methods immediately invoke the function.But, bind method does not invoke immediately.

call () takes arguments separately (fixed number of arguments.),whereas apply() takes arguments as an array.

```javascript
const student = {
    name: 'siddhesh',
    printName: function () {
        console.log(this.name);
    }
}
student.printName(); // o/p: siddhesh

const student2 = {
    name: 'Karan',
}
student.printName.call(student2); 
// o/p: Karan
//In this case, the call method modifies "this" to refer to student2.
```

## 6."this" inside arrow function

Arrow functions do not have their own "this" context. Instead, they inherit "this" from the enclosing lexical context. (lexical context: it depends on where it is present).

In short, they take the value of their lexical context which is enclosed.

```javascript
const student ={
    name: "siddhesh",
    printname:  function() {
        console.log(this);
    }
}
student.printname();
//o/p: { name: 'siddhesh', printname: [Function: printname] }
 //now, using arrow function
const student ={
    name: "siddhesh",
    printname:()=> {
        console.log(this);
    }
}
student.printname();
//o/p: window(object) as it is lexical scope of "this".
//but, actually is is not present/written in global space. "this" in arrow function behaves differently than regular functions.
```

## 7."this" Inside the DOM

"this" in DOM refers to the HTML element itself on which it is being used.

```javascript
<button onclick="alert(this)">Click Me</button>
//o/p: <!-- [object HTMLButtonElement] Button element -->
//here, "this" will be referred to buttons.
//another example:
<button onclick="alert(this.tagName)">Click Me</button>
//o/p: alert box will be displayed with "Buttton" tag.
```

## Conclusion:

JavaScript's "this" keyword behaves differently depending on the context. Writing efficient JavaScript code requires an understanding of how "this" changes depending on where and how it is used. Whether you use "this" in global space, inside functions, methods or arrow functions etc which will improve your JavaScript significantly.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1718631137782/3cf1c9c7-c71f-4411-8e1e-03cad3192e13.jpeg align="center")

---