## 1. What is Callbacks in JavaScript?


A **JavaScript callback** is a function which is to be executed **after another function has finished execution**.

---

### 🔹 Simply Said:
Any function that is passed as an argument to another function so that it can be executed in that other function is called a **callback function**. This often leads to **callback hell** when nested deeply.

---

### 🔸 Example (Callback Hell):

```js
// callbacks and callback hell
let fruits = ["apple", "banana", "kiwi"];

const animateAll = (animate) => {
  // below is the callback hell
  setTimeout(() => {
    animate(fruits[0]);
    setTimeout(() => {
      animate(fruits[1]);
      setTimeout(() => {
        animate(fruits[2]);
      }, 1000);
    }, 1000);
  }, 1000);
};

const animate = (fruit) => {
  console.log("animating", fruit);
};

animateAll(animate);
```

**Output**
---
animating apple  
animating banana  
animating kiwi
#### Note
This is an example of callback hell where multiple nested callbacks make the code harder to read and maintain. Modern alternatives include Promises and Async/Await.

## 2. What are Promises in JavaScript?

A **Promise** is an object in JavaScript that will produce a single value sometime in the future. If the operation is successful, it will produce a resolved value. If it fails, it will produce a reason for the failure.

---

### 🔹 Simply Said:
It behaves very similarly to real-life promises — either fulfilled (resolved) or broken (rejected).

---

### 🔸 Example (Using Promises):

```js
let fruits = ["apple", "banana", "kiwi"];

const animateOne = (fruit, animate) => {
  return new Promise((res, rej) => {
    setTimeout(() => {
      animate(fruit);
      res(true);
    }, 1000);
  });
};

const animateAll = (animate) => {
  animateOne(fruits[0], animate)
    .then(() => animateOne(fruits[1], animate))
    .then(() => animateOne(fruits[2], animate))
    .catch((err) => console.log("some error occurred", err));
};

const animate = (fruit) => {
  console.log("animating", fruit);
};

animateAll(animate);
```
Output

animating apple
animating banana
animating kiwi



#### Note
TPromises help make asynchronous code more readable and manageable than using nested callbacks. They are the basis for using async and await in modern JavaScript.