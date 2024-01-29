---
title: "JavaScript Scope War: Showdown Between Block Scope and Shadowing..."
seoTitle: "JavaScript Scope War: Showdown Between Block Scope and Shadowing..."
datePublished: Mon Jan 29 2024 11:57:05 GMT+0000 (Coordinated Universal Time)
cuid: clryvk423000209jj6uri4glr
slug: javascript-scope-war-showdown-between-block-scope-and-shadowing
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1706529361956/142f9b5a-dbd4-4e6d-a563-4ee92f277d60.png
tags: programming-blogs, javascript, web-development, hashnode, 2articles1week, wemakedevs

---

## Introduction

JavaScript's dynamic capabilities keep developers on their toes. Two key aspects demand our attention as we work to understand the complexities of JavaScript: <mark>Block Scope and Shadowing</mark>. Understanding these ideas is essential for not only producing better code, but also reaching JavaScript's full potential. So, let's dig deep into the world of Block Scope and Shadowing to improve our coding abilities.

---

## Understanding the Basics: What is a Block in JavaScript?

In JavaScript, a block, also known as a compound statement, is a powerful tool for grouping statements together. These statements are enclosed in curly braces {...}.

```javascript
{
    var a = 10;
    let b = 20;
    const c = 30;
    // Let and const are hoisted in Block scope,
    // While var is hoisted in Global scope.
}
```

### Exploring Block Scope and Accessibility.

```javascript
{
    var a = 10;
    let b = 20;
    const c = 30;
}
console.log(a); // 10
console.log(b); // Uncaught ReferenceError: b is not defined
```

## Learning the Reason behind It

Variables b and c in the **BLOCK SCOPE** field are initialised as undefined due to hoisting, and they exist in a separate memory area known as a block. Meanwhile, variable an is stored in the global scope. This basic difference means that let and const are **BLOCK SCOPED**, meaning they are only available within the block in which they are defined, but var is global and accessible elsewhere.

## Figuring out the Secret: What is Shadowing???

```javascript
var a = 100;
{
    var a = 10; // Same name as global var
    let b = 20;
    const c = 30;
    console.log(a); // 10
    console.log(b); // 20
    console.log(c); // 30 
}
console.log(a); // 10, modifying the value of the global "a"
```

When using var, if another variable with the same name exists outside the block, the variable inside the block takes place of the external one. This problem does not occur with let or const.

## Understanding the Behavior of Let and Const.

```javascript
let b = 100;
{
    var a = 10;
    let b = 20;
    const c = 30;
    console.log(b); // 20
}
console.log(b); // 100, separate spaces for both b's (Block: 20, Script: 100)
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1706528592998/165212de-9c14-4535-9e2f-86f9ece4691c.jpeg align="center")

## Understanding Function's Block Scope.

```javascript
const c = 100;
function x() {
    const c = 10;
    console.log(c); // 10
}
x();
console.log(c); // 100
```

## Take precautions of Illegal Shadowing.

```javascript
let a = 20;
{
    var a = 20;
}
// Uncaught SyntaxError: Identifier 'a' has already been declared
```

Remember that it is not OK to use shadow let with var, but the converse is true. In addition, let can shadow another let, whereas var cannot.

---

Understanding Block Scope and Shadowing is critical in JavaScript, where correctness is everything. Understanding these notions enables developers to design strong, error-free programs.

Stay Tuned!! Happy Learning!!

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1706528163592/c28ffc8e-a9ee-48ee-8316-8bc12ff6f3df.jpeg align="center")

---