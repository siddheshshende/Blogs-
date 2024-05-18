---
title: "Asynchronous JavaScript with Promise APIs (all, allSettled, race and any)"
seoTitle: "Asynchronous JavaScript with Promise APIs(all, allSettled, race & any)"
datePublished: Sat May 18 2024 21:35:27 GMT+0000 (Coordinated Universal Time)
cuid: clwcmnlyq000408lecls61tlr
slug: asynchronous-javascript-with-promise-apis-all-allsettled-race-and-any
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1716067869390/c610c377-543d-4b20-846e-765fd6b7d24f.png
tags: programming-blogs, javascript, web-development, hashnode, 2articles1week, wemakedevs

---

## Introduction

JavaScript asynchronous programming is an essential ability for recent developers. Promises have made it easier to handle asynchronous tasks and reduced the likelihood of errors. With promises, handling callbacks is simplified, improving the readability and maintainability of your code. Four significant <mark> Promise API's</mark> are `Promise.all, Promise.allSettled , Promise.race and Promise.any` will be discussed in this article.This promise API's are used basically to make multiple API calls in parallel way. Gaining a knowledge of them will provide you the ability to manage several asynchronous jobs successfully and efficiently.

---

## 1.Promise.all()

Promise.all() provides a single promise after accepting an array or iterable of promises. When every promise in the array resolves, this one resolves as well; if any of the promises reject, it rejects.

consider,there are multiple API calls or promises to be fetched. So, it will handle multiple promises together.It will wait for all of them(API calls) to finish and result is displayed at same time in console in resolve case.

But, in reject case, if any one of the promise is reject, then promise.all() will throw an error and it will not wait for other promise results (that can be success or failure).  
  
**Use Case:**

Promise.all is used when you need to make multiple API calls at once and wait for each one to finish. For example, retrieving information concurrently from several sources.

Promise.all(\[p1, p2, p3\]) -&gt; Lets assume we are making 3 API call to fetch data. Also assume p1 takes 3 seconds, p2 takes 1 second, p3 takes 2 seconds.

In first scenario let's assume all 3 promises are successful. So Promise.all will take 3secs and will give promise value of result like \[val1, val2, val3\]. It will wait for all of them to finish then it will collect the results and give array as output.

What if any of the promise gets rejected, for eg: Promise.all(\[p1, p2, p3\]). But this time, p2 get rejected after 1 sec. Thus Promise.all will throw same error as p2 immediately as soon as error happened. It will not wait for other promise to either become success or failure.

```javascript
// First case

const p1 = new Promise((resolve, reject) => {
  setTimeout(() => {
    resolve('P1 Success');
  }, 3000);
});
const p2 = new Promise((resolve, reject) => {
  setTimeout(() => {
    resolve('P2 Success');
  }, 1000);
});
const p3 = new Promise((resolve, reject) => {
  setTimeout(() => {
    resolve('P3 Success');
  }, 2000);
});

Promise.all([p1, p2, p3]).then((results) => {
  console.log(results); 
});
// o/p: ['P1 Success', 'P2 Success', 'P3 Success'] -> took 3 secs
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1716063420275/38cc7ac4-d598-4298-9db8-537f1723db24.jpeg align="center")

```javascript
// Second case
const p1 = new Promise((resolve, reject) => {
  setTimeout(() => {
    resolve('P1 Success');
  }, 3000);
});
const p2 = new Promise((resolve, reject) => {
  setTimeout(() => {
    reject('P2 Fail');
  }, 1000);
});
const p3 = new Promise((resolve, reject) => {
  setTimeout(() => {
    resolve('P3 Success');
  }, 2000);
});

Promise.all([p1, p2, p3])
  .then(results => console.log(results))
  .catch(err => console.error(err)); 
//o/p: throws error after 1 sec i.e. 'P2 Fails'
```

But, Its ok if one of our promise fails.I want other 9 out of 10 promises to be displayed. In this situation, promise.all() will not work. So, promise.allsettled() is introduced.

## 2.Promise.AllSettled()

Once all of the input promises have settled, either resolved or refused, Promise.allSettled() gives a promise that resolves. It offers a thorough analysis of every promise's performance.

If one of our promise is failed, then Promise.AllSettled() will wait for all other promises to settled.This Promises API is the safest of all.

> Promise.all() -&gt; Very Quick Failure(fail fast)  
> Promise.AllSettled() -&gt; Promise Will await and deliver final outcomes

**Use Case:**

when you have to wait for every promise—regardless of whether it was accepted or rejected—to be fulfilled.

Promise.allSettled(\[p1, p2, p3\]) -&gt; Lets assume we are making 3 API call to fetch data. Also assume **p1** takes **3 seconds**, **p2** takes **1 second**, **p3** takes **2 seconds**.

In first scenario let's assume all 3 promises are successful. So Promise.allSettled will take **3secs** and will give promise value of result like \[val1, val2, val3\]. It will wait for all of them to finish then it will collect the results and give array as output.

What if any of the promise gets rejected, for eg: Promise.all(\[p1, p2, p3\]). But this time, p2 get rejected after 1 sec. Thus Promise.allSettled will still wait for all promises to get settled. So After 3 secs, it will be \[val1, err, val3\]

```javascript
const p1 = new Promise((resolve, reject) => {
  setTimeout(() => {
    resolve('P1 Success');
  }, 3000);
});
const p2 = new Promise((resolve, reject) => {
  setTimeout(() => {
    resolve('P2 Success');
  }, 1000);
});
const p3 = new Promise((resolve, reject) => {
  setTimeout(() => {
    reject('P3 Fail');
  }, 2000);
});

Promise.allSettled([p1, p2, p3])
  .then((results) => console.log(results))
  .catch(err => console.error(err));//we can also do (err.errors) for detailed output.

// Over here, it will wait for all promises to be either settled or rejected and then return,
  /*
    [
      {status: 'fulfilled', value: 'P1 Success'},
      {status: 'fulfilled', value: 'P2 Success'},
      {status: 'rejected', reason: 'P3 Fail'}
    ]
  */
```

## 3.Promise.race()

As soon as one of the input promises resolves or rejects, Promise.race() returns a promise that does the same. It truly is a race between the promises.It will not wait for other promises to finish because its a race.

It basically give us value of first settled promise.And if the first promise which should be settled is rejected ,then it will throw an error.  
  
**Use Case:**  
  
When you require the fastest promise's result, no matter how quickly it happens.

Promise.race(\[p1, p2, p3\]) -&gt; Lets assume we are making 3 API call to fetch data. Also assume **p1** takes **3 seconds**, **p2** takes **1 second**, **p3** takes **2 seconds**. So as soon as first promise will resolve or reject, it will give the output.

So in Happy scenario, Promise.race will give (val2) as output after 1sec as p2 got resolved at the earliest. Whereas if it would have been failed Promise.race would have still given output after 1 sec but this time with error.

```javascript
//First case
const p1 = new Promise((resolve, reject) => {
  setTimeout(() => {
    resolve('P1 Success');
  }, 3000);
});
const p2 = new Promise((resolve, reject) => {
  setTimeout(() => {
    resolve('P2 Success');
  }, 1000);
});
const p3 = new Promise((resolve, reject) => {
  setTimeout(() => {
    reject('P3 Fail');
  }, 2000);
});

Promise.race([p1, p2, p3])
  .then((results) => console.log(results))
  .catch(err => console.error(err));

 // It will return as soon as first promise is resolved or rejected.
 // O/P: "P2 Success"
```

```javascript
//Second case
const p1 = new Promise((resolve, reject) => {
  setTimeout(() => {
    resolve('P1 Success');
  }, 3000);
});
const p2 = new Promise((resolve, reject) => {
  setTimeout(() => {
    resolve('P2 Success');
  }, 5000);
});
const p3 = new Promise((resolve, reject) => {
  setTimeout(() => {
    reject('P3 Fail');
  }, 2000);
});

Promise.race([p1, p2, p3])
  .then((results) => console.log(results))
  .catch(err => console.error(err));

 //After 2 secs O/P: "P3 Fail"
```

> Insights:  
> As soon as a promise is fulfilled, the outcome is obtained.
> 
> Furthermore, settled can be broadly classified into two categories:
> 
> 1.reject, failure, rejected
> 
> 2.resolve, success, fulfilled
> 
> ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1716065747003/32015554-7ffb-4cc4-8430-efddfcad8198.jpeg align="center")

## 4.Promise.any()

A promise that resolves as soon as any of the input promises resolves is returned by Promise.any(). An aggregated error is nothing but array of all error like \[err1, err2, err3\] is returned if every promise/API call is rejected/failed.

It is similar to promise.race(). But, it will wait for first success/resolved /fulfilled promise. It is a **success seeking** promise means it will return result only after/whenever it is successful.

  
**Use case:**  
  
when you require the first of multiple promises to be fulfilled successfully.

Promise.any(\[p1, p2, p3\]) -&gt; Lets assume we are making 3 API call to fetch data. Also assume **p1** takes **3 seconds**, **p2** takes **1 second**, **p3** takes **2 seconds**. So as soon as first promise will be successful, it will give the output.

If in above situation what if p2 got rejected, nothing will happen as Promise.any seek for success, so the moment first success will happen that will become the result.

```javascript
// First case
const p1 = new Promise((resolve, reject) => {
  setTimeout(() => {
    resolve('P1 Success');
  }, 3000);
});
const p2 = new Promise((resolve, reject) => {
  setTimeout(() => {
    resolve('P2 Success');
  }, 5000);
});
const p3 = new Promise((resolve, reject) => {
  setTimeout(() => {
    reject('P3 Fail');
  }, 2000);
});

Promise.any([p1, p2, p3])
  .then((results) => console.log(results))
  .catch(err => console.error(err));

// It will wait for first settled **success**
// In above, p3 will settled first, but since it is rejected, 
//so it will wait further and at 3rd second it will print "P1 Success"
```

```javascript
// second case
const p1 = new Promise((resolve, reject) => {
  setTimeout(() => {
    reject('P1 Fail');
  }, 3000);
});
const p2 = new Promise((resolve, reject) => {
  setTimeout(() => {
    resolve('P2 Success');
  }, 5000);
});
const p3 = new Promise((resolve, reject) => {
  setTimeout(() => {
    reject('P3 Fail');
  }, 2000);
});

Promise.any([p1, p2, p3])
  .then((results) => console.log(results))
  .catch(err => console.error(err));

// o/p: After 5 secs: 'P2 Success'
```

```javascript
//Third case
const p1 = new Promise((resolve, reject) => {
  setTimeout(() => {
    reject('P1 Fail');
  }, 3000);
});
const p2 = new Promise((resolve, reject) => {
  setTimeout(() => {
    reject('P2 Fail');
  }, 5000);
});
const p3 = new Promise((resolve, reject) => {
  setTimeout(() => {
    reject('P3 Fail');
  }, 2000);
});

Promise.any([p1, p2, p3])
  .then((results) => console.log(results))
  .catch(err => {
    console.error(err);
    console.error(err.errors); 
  });
// o/p: ['P1 Fail', 'P2 Fail', 'P3 Fail']
// Since all are rejected, so it will give "aggregate error" as output
// AggregateError: All promises were rejected
// To get AggregateError array you need to write "err.errors"
```

## Conclusion:

Gain more proficiency managing asynchronous processes in JavaScript by learning and utilising these Promise APIs: Promise.all, Promise.allSettled, Promise.race and Promise.any. Every API has a distinct function, such as Promise.all to concurrently process multiple promises, Promise.allSettled to handle all promise states, Promise.race for executing the fastest promise, and Promise.any for managing the first resolved promise.Making use of these will greatly enhance your asynchronous programming abilities.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1716067238305/97606e7b-a078-4f10-af92-8c77efa4436f.jpeg align="center")

---