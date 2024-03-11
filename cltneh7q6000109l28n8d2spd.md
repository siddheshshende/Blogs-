---
title: "JS Engine Details in Google's V8 Architecture Explained"
seoTitle: "Explained JS Engine Details in Google's V8 Architecture"
datePublished: Mon Mar 11 2024 20:32:53 GMT+0000 (Coordinated Universal Time)
cuid: cltneh7q6000109l28n8d2spd
slug: js-engine-details-in-googles-v8-architecture-explained
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1710189091221/60334d71-38d7-4692-ab44-6e1edb0ad406.png
tags: programming-blogs, javascript, web-development, hashnode, 2articles1week, wemakedevs

---

## Introduction

In the ever-changing world of web development, understanding the complexities of Javascript (JS) and its engines is essential. Today, we'll look at the <mark>Javascript Runtime Environment (JRE)</mark>, which is at the heart of JS execution, as well as Google's extraordinary <mark> V8 architecture</mark>, which powers everything from smart watches to web browsers. Join us as we deconstruct the JS engine's key components, including its parsing, compilation, and execution processes, and learn about the powerful V8 architecture. Let us begin on a mission to discover the inner workings of the code that governs the digital universe.

---

## JS Engine: The Heart of Javascript Runtime Environment (JRE)

Javascript (JS) is already widespread, powering devices ranging from smartwatches to robots to web browsers, thanks to its Javascript Runtime Environment (JRE). The JRE functions as a comprehensive container, containing everything required to run Javascript code.

## Figuring out JRE Components: The Core Element (JS Engine)

The JS Engine, often known as the environment's heart, is located at the centre of JRE. It includes critical components like as APIs for interacting with the external environment, event loops, callback queues, microtask queues, and more.

## ECMAScript: Controlling JavaScript Rules

JS is governed by ECMAScript and follows a set of standards that are obeyed by all JS engines, including Chakra (Edge), Spidermonkey (Firefox), and the focus of our talk, Google's V8 in Chrome.

## Understanding the JavaScript Engine

JS Engine is not a physical engine, but rather software written in low-level languages such as C++. It converts high-level JavaScript code into low-level machine code in three steps:   

1. parsing
    
2. compilation
    
3. execution.
    

* Parsing: Breaking down the code. During parsing, the code is broken down into tokens. For example, in the sentence "let a = 7," the words "let," "a," "=," and "7" are tokens. A syntax parser also turns the code into an abstract syntax tree (AST), which is similar to a JSON structure.
    

> You can use the [**AST Explorer**](https://astexplorer.net/) [tool to see](https://astexplorer.net/) how code written by you gets parsed into an *Abstract Syntax Tree(AST)*.

* JS uses Just-in-Time (JIT) compilation, which combines interpreter and compiler functionality. The AST passes to the interpreter, which converts high-level code to bytecode, while the compiler optimises the code at runtime. JavaScript, a JIT-compiled language, provides the best of both worlds.
    
* Execution: memory and call stack dynamics Execution consists of two important components: Memory Heap (storage for all memory) and Call Stack. A garbage collector implements the Mark and Sweep method to perform memory cleanup.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1710188083933/f589813c-f0c3-441d-895f-984dc684a09c.jpeg align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1710188131882/67aa12eb-6238-4c8a-aeaa-890545c8ced0.avif align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1710188164139/85028995-d5af-4e33-9f55-ce2d369476cd.png align="center")

## Knowing Google's V8 Architecture.

Google's V8 stands out for its Interpreter (Ignition), Compiler (Turbo Fan), and Garbage Collector (Orinoco). This architecture promotes V8 as a powerful JavaScript engine that can be used on a variety of platforms.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1710188021561/65cdc579-7d6c-432c-a5ce-ea32952f9e51.png align="center")

## Companies are embracing JS engines.

Diverse firms choose different JS engines, each attempting to perfect its implementation. Google's V8, with its unique components, remains a key participant in this competitive landscape.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1710188286784/8909b2b8-e3f8-4889-a23c-0a584ce436cd.jpeg align="center")

---