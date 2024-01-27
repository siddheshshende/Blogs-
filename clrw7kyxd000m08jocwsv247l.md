---
title: "JavaScript's Scope Chain and Lexical Environment: An Overview"
seoTitle: "JavaScript's Scope Chain and Lexical Environment: An Overview"
datePublished: Sat Jan 27 2024 15:10:22 GMT+0000 (Coordinated Universal Time)
cuid: clrw7kyxd000m08jocwsv247l
slug: javascripts-scope-chain-and-lexical-environment-an-overview
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1706367972903/6df73310-1b3f-4a99-ae60-3d400a9e0f9b.png
tags: programming-blogs, javascript, web-development, hashnode, 2articles1week, wemakedevs

---

### Introduction

JavaScript, the driving force behind dynamic web pages, contains an interesting interplay between <mark> scope, the scope chain, and the lexical environment</mark>. Understanding these notions is critical for mastering the language and writing efficient, error-free code. In this investigation, we will unravel the mysteries of the <mark>Scope Chain, Scope, and Lexical Environment</mark>, figuring out the complexities that regulate variable access and execution context.

---

### Understanding the Basics: Scope and Lexical Environment.

In the world of Javascript, scope is tightly tied to the Lexical Environment. Let's look at some examples to shed light on this link.

**Case 1: Accessing the Global Scope.**

```javascript
function a() {
  console.log(b); // 10
  // Instead of printing undefined, it prints 10. This function can access the variable b outside its scope.
}
var b = 10;
a();
```

**Case 2: Nesting and Global Scope Access.**

```javascript
function a() {
  c();
  function c() {
    console.log(b); // 10
  }
}
var b = 10;
a();
```

**Case 3: Local Priority Over Global**

```javascript
function a() {
  c();
  function c() {
    var b = 100;
    console.log(b); // 100
  }
}
var b = 10;
a();
```

**Case 4: Global vs. Local Scopes**

```javascript
function a() {
  var b = 10;
  c();
  function c() {
    console.log(b); // 10
  }
}
a();
console.log(b); // Error, Not Defined
```

### Understanding the output:

In Case 1, the function 'a' has access to the variable 'b' from the global scope. Case 2 demonstrates that the global scope variable can be accessed from within nested functions. Moving on to Case 3, a local variable takes precedence over a global one, yielding a value of 100. Case 4 shows that a function can access a global variable, but the global execution context cannot access any local variables.

### Understanding the Execution Context

To summarize the points in terms of execution context, look at the call stack:

**\[GEC, a(), c()\]**.

Let us allocate memory portions to each execution context in the call stack.

* `c()`: `[lexical environment pointer pointing to a()]`
    
* `a()`: `[b:10, c:{}, [lexical environment pointer pointing to GEC]]`
    
* `GEC`: `[a:{}, [lexical environment pointer pointing to null]]`
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1706366873323/5ab902a7-fca7-4d84-b827-d167f3b9ae3e.jpeg align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1706366982859/ef6bc6b6-1f72-4a34-9c0c-3df5a3b9c083.jpeg align="center")

### simplifying the Lexical Environment:

The lexical environment is a combination of local memory and the lexical environment of the parent. It follows a hierarchical structure, progressing from one parent to the next, establishing the scope chain or Lexical Environment chain.

```javascript
function a() {
  function c() {
    // logic here
  }
  c(); // 'c' is lexically inside 'a'
} // 'a' is lexically inside the global execution
```

The accessibility of variables, functions, and objects is determined by their physical position in the source code, also known as lexical or static scope. It's a hierarchical structure, with the inner encircled by the outer's lexical scope.

---

### TLDR: Understanding Lexical Scope

In simple terms, an inner function can access variables in outer functions, no matter how deeply nested they are. In all other cases, a function cannot access variables outside of its scope.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1706368056058/7b4e0abe-538b-4eae-91b0-cd889a2609db.jpeg align="center")

---