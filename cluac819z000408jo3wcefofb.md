---
title: "Higher-Order Functions in Functional Programming"
seoTitle: " Higher-Order Functions in Functional Programming "
datePublished: Wed Mar 27 2024 21:48:28 GMT+0000 (Coordinated Universal Time)
cuid: cluac819z000408jo3wcefofb
slug: higher-order-functions-in-functional-programming
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1711575972384/c2c24293-ba5a-4800-844a-b3483871fc47.png
tags: programming-blogs, javascript, web-development, hashnode, 2articles1week, wemakedevs

---

## Introduction: Understanding Functional Programming's Potential

<mark>Functional programming </mark> stands out as a shining example of efficiency and elegance in the ever-changing field of software development. The fundamental idea behind higher-order functions is to provide programmers with an extensive toolkit to write clear, modular code. Stay with us, as we explore the world of <mark> higher-order functions </mark> and how they may transform modern development approaches.

---

## What's a Higher Order Function, Exactly?

Higher-order functions are an essential component of functional programming; they are not just theoretical ideas. However, what sets a higher-order function apart from what it resembles precisely?  
  
Higher-order functions are essentially regular functions with an additional feature: they can return functions as results or accept other functions as arguments.

This adaptability gives programmers a strong tool for composition and abstraction, enabling flexible and reusable programmes.

1. Higher-order functions are basically functions which takes/accepts other functions as arguments and/or returns a function as a result.
    
2. The function which is passed into Higher-order function is called as callback function, which is called latter in program.
    
3. And all this is possible only due to First class citizens, functions are first class citizens in js.
    

To give an example, think about this one:

```javascript
function greet() {
  console.log('Hi');
}
function caller(func) {
  func();
}
caller(greet); // Outputs: Hi
```

This sample shows how caller is a higher-order function, can be used by passing in greet as an argument and using it within its body. The fact that greet is called a callback function in turn illustrates how dynamic higher-order functions are.

## Handling Higher-Order Function Problems

Let's attempt to understand the proper way to approach a solution during an interview. I have to find the area, circumference, and diameter  using an array of radius values and store the results in an array.

```javascript
const radius = [3,6,5,2,];
//code to calculate area of a circle.
const calculatearea = function(radius){
    const output =[];
    for (let i = 0; i <radius.length; i++)  {
output.push(Math.PI* radius[i] * radius[i]);
    }
    return output;
}
console.log(calculatearea(radius));
//code to calculate circumference of a circle.
const calculatecircumference = function(radius){
    const output =[];
    for (let i = 0; i <radius.length; i++)  {
output.push( 2 * Math.PI* radius[i]);
    }
    return output;
}
console.log(calculatecircumference(radius));
//code to calculate diameter of a circle.
const calculatediameter = function(radius){
    const output=[];
    for (let i = 0; i <radius.length; i++)  {
output.push( 2 * radius[i]);
    }
    return output;
}
console.log(calculatediameter(radius));
//output: 
//[28.274333882308138,113.09733552923255, 78.53981633974483,12.566370614359172]
//[18.84955592153876,37.69911184307752,31.41592653589793,12.566370614359172]
//[ 6, 12, 10, 4 ]
```

This solution behaves flawlessly. But what if our specifications also included the need to calculate anything else? If we kept going in the same direction, we would have redundant code.  
However, this is where the problem lies: repetition conflicts with the ***DRY (Don't Repeat Yourself)*** Principle.

we have to make our code more modular and less repetitive. So, we need to abstract our code/logic due to which we don't require to write the whole code or copy the whole code/function again and again.  
So, Let's evaluate a more effective and efficient alternatives,now:

```javascript
const radius = [3,6,5,2,];

const area = function (radius){
    return Math.PI * radius * radius;
}
const circumference = function (radius){
    return 2 * Math.PI * radius;
}
const diameter = function (radius){
    return 2 * radius;
}

const calculate = function(radius, logic ){
    const output=[];
    for (let i = 0; i <radius.length; i++)  {
output.push(logic(radius[i]));
    }
    return output;
}
console.log(calculate(radius, area));
console.log(calculate(radius, circumference));
console.log(calculate(radius, diameter));
//output will be same as mentioned in above code.
```

Calculate occurs as a Higher-Order Function in this case. CalculateArea , CalculateCircumference and calculatediameter are some separate functions that we might pass in order to reuse the same logic for different calculations.

## Making the Most of Functional Programming's Power :

Furthermore, this method effectively captures the principles of functional programming. We promote modularity and maintainability in our program's code by abstracting logic into distinct functions.

### Expanding the map function :

Let's continue with our functional approach by turning our calculate function into a <mark>polyfill </mark> for the native map function:

Let's try using the above calculate function changed to a map function. Thus,

```javascript
Array.prototype.calculate = function(logic) {
    const output = [];
    for (let i = 0; i < this.length; i++) {
        output.push(logic(this[i]));
    }
    return output;
}
console.log(radius.calculate(area))
console.log(radius.map(area))// another way
//calculate will be available for all arrays in code. 
//prototype: when we put something on prototype, it appears on all arrays. 
//Here,calculate is nothing but polyfill of map function.
//console.log(radiusArr.map(area)) == console.log(calculate(radiusArr, area));
```

**Polyfills** is used to fill the gap between older browers and modern features in js.

polyfills are a piece of code that provides functionality which is not not support by some browers.Popular polyfills exist for features like promises, fetch API , object.assign() etc.....

---

## conclusion:

Finally, the key to maximising the potential of functional programming is to become proficient with higher-order functions. We may unleash a world of efficiency, scalability, and elegance in our code by adopting these ideas.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1711575998750/81866d7d-9c5d-4cbe-9e28-524439b27fec.jpeg align="center")

---