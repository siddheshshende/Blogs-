---
title: "JavaScript Hoisting Unveiled: Mastering the Art of Code Elegance."
seoTitle: "JavaScript Hoisting Unveiled: Mastering the Art of Code Elegance"
datePublished: Tue Jan 23 2024 19:00:55 GMT+0000 (Coordinated Universal Time)
cuid: clrqq21ti000009l29uthamqd
slug: javascript-hoisting-unveiled-mastering-the-art-of-code-elegance
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1706036088773/b1720720-7894-4b1b-8785-ce5e5c259211.png
tags: programming-blogs, javascript, web-development, hashnode, wemakedevs

---

## Introduction: Unravel the Magic of Hoisting

JavaScript, the language that drives the dynamic world of web development, contains a fascinating notion known as <mark>Hoisting</mark>. This phenomena permits variables and function declarations to be accessed prior to their official definition in the code. As we begin our journey to grasp the complexities of hoisting, Part 2 gives an intuitive basis for those wanting a deeper understanding...

---

## Grasping Hoisting Essentials. 🙃

Hoisting offers a novel dance between memory allocation and execution, radically changing how we interact with variables and functions in JavaScript.

1. Variables are initialized as undefined during the memory allocation step.
    
2. Function declarations find a place in memory and are ready for execution.
    
3. Hoisting allows variables and function calls to be used prior to their formal declaration, providing a level of flexibility not seen in other programming languages.
    

## Unravel the Magic: Behind the Scenes of Hoisting

To understand the mesmerising nature of hoisting, let's look into the mechanics that take place behind the scenes:

1. Variable declarations are painstakingly inspected and marked as undefined.
    
2. Function declarations go through a similar scan, placing themselves in memory, ready for execution.
    

### **Examples of hoisting:**

**Example 1-**

```javascript
getName(); // Namaste Javascript
console.log(x); // undefined
var x = 7;
function getName() {
    console.log('Namaste Javascript');
}
```

Deciphering Magic:

* 'getName()' executes gracefully before its official declaration, demonstrating the power of hoisting.
    
* Variable 'x' is hoisted, but it remains undefined until assigned the value 7.
    
    **Example 2-**
    
    Untangling Technicalities:
    
* The mystical power of hoisting allows 'getName()' to execute flawlessly before declaration.
    
* Accessing an undeclared variable 'x' results in an error, emphasizing the subtle nature of hoisting.
    
* Console.log(getName) smoothly displays the function definition, a nuanced ballet in the world of hoisting.
    

```javascript
getName(); // Namaste JavaScript
console.log(x); // Uncaught Reference: x is not defined.
console.log(getName); // f getName(){ console.log("Namaste JavaScript); }
function getName() {
    console.log('Namaste JavaScript');
}
```

**Example 3-**

```javascript
getName(); // Uncaught TypeError: getName is not a function
console.log(getName);
var getName = function () {
    console.log('Namaste JavaScript');
};
// The code won't execute as the first line itself throws a TypeError.
```

Technical insights:

* Calling 'getName()' before the variable declaration throws a TypeError, emphasizing the complexities of function expressions and variable hoisting.
    
* The value of the undefined variable is beautifully outputted by console.log(getName), but the code execution stops after the first line owing to a TypeError.
    

---

## Navigating the Hoisting Landscape in JavaScript: Variables and Functions (summary)

As we investigate the next code block, the delicate dance of hoisting begins:

```javascript
getName(); // Namaste Javascript
console.log(x); // undefined
var x = 7;
function getName() {
    console.log("Namaste Javascript");
}
```

In traditional programming languages, attempting to access something that had not yet been created resulted in an error. However, during the memory construction phase, JavaScript assigns variables to undefined and stores function contents. The succeeding line-by-line code run produces undefined without error. Removing **var x = 7**; turns the scenario into an error. **Uncaught ReferenceError: x was not defined**.

In essence, hoisting in JavaScript is more than a concept; it is a magical power that provides access to variables and functions prior to initialization, revealing the full potential of JavaScript creation.

Stay Tuned!! Happy Learning!!

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1706035490060/462e6fab-e314-4fb2-ae71-4b3b4ada4fdc.jpeg align="center")

---