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
**Output**

animating apple
animating banana
animating kiwi



#### Note

TPromises help make asynchronous code more readable and manageable than using nested callbacks. They are the basis for using async and await in modern JavaScript.

---
## 3. What is Async/Await in JavaScript?

**Async/Await** makes it easier to work with **Promises**.

- The keyword `async` before a function makes it return a Promise.
- The keyword `await` is used inside async functions and pauses the execution until the Promise resolves.

---

### 🔹 Simply Said:
Async/Await behaves like synchronous code but works asynchronously under the hood, making it easier to read and maintain than chained `.then()` calls.

---

### 🔸 Example:

```js
// async/await
let fruits = ["apple", "banana", "kiwi"];

const animateOne = (fruit, animate) => {
  return new Promise((res, rej) => {
    setTimeout(() => {
      animate(fruit);
      res(true);
    }, 1000);
  });
};

const animateAll = async (animate) => {
  await animateOne(fruits[0], animate);
  await animateOne(fruits[1], animate);
  await animateOne(fruits[2], animate);
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

## 4.What are Higher Order Function 

Functions can be assigned to variables in the same way that strings or arrays can.  
They can be passed into other functions as parameters or returned from them as well.

---

### 🔹 Simple Words:
It is a function that **accepts functions as parameters** and/or **returns a function**.

---

### 🔸 Examples:
`map`, `filter`, `reduce`, `some`, `every`, `forEach`, `sort`, etc.

---

### 🧠 Example Code (with `map()` and `filter()`):

```js
// Higher order function with Array.map() and Array.filter()
const ages = [23, 45, 12, 67, 18];

const doubleAges = ages.map((age) => age * 2);
console.log(doubleAges);      // [46, 90, 24, 134, 36]

const ageLessThan40 = ages.filter((age) => age < 40);
console.log(ageLessThan40);   // [23, 12, 18]
```

#### ✅ Explanation:
map() takes a function and applies it to every element of the array.  
filter() takes a function that returns true or false and filters elements accordingly.


## 5. What is Call, Apply, Bind 

**Call** is a function that helps you change the context of the invoking function. In layperson's terms, it helps you replace the value of this inside a function with whatever value you want.

**Apply** is very similar to the call function. The only difference is that in apply you can pass an array as an argument list.

**Bind** is a function that helps you create another function that you can execute later with the new context of this that is provided.

## Code Example

```javascript
// call, apply, bind
function fullName(greet) {
    console.log(greet + " " + this.firstName + " " + this.lastName);
}

const person1 = {
    firstName: "Elon",
    lastName: "Musk",
};

const person2 = {
    firstName: "Ratan",
    lastName: "Tata",
};

fullName.call(person1, "Hello"); // Hello Elon Musk
fullName.call(person2, "Hi");    // Hi Ratan Tata

fullName.apply(person1, ["Hello"]); // Hello Elon Musk
fullName.apply(person2, ["Hi"]);    // Hi Ratan Tata

const person1FullName = fullName.bind(person1); // Hello Elon Musk
const person2FullName = fullName.bind(person2); // Hi Ratan Tata

console.log("execute some other code here");
person1FullName("Hello"); // Hello Elon Musk
person2FullName("Hi");    // Hi Ratan Tata
```

## Output

```
Hello Elon Musk
Hi Ratan Tata
Hello Elon Musk
Hi Ratan Tata
execute some other code here
Hello Elon Musk
Hi Ratan Tata
```

## 5. What is Closures

A **closure** is the combination of a function bundled together (enclosed) with references to its surrounding state (the **lexical environment**).

**Simple words:** A closure gives you access to an outer function's variables and functions from an inner function.

## Code Example

```javascript
// closures
function createHustler(name){
    let greetHi = 'Hi ';
    function greet(){
        return greetHi + name + ', welcome to hustlers group';
    }
    return greet;
}

let greetFn = createHustler('Ankit');
console.log(greetFn());
```

## Output

```
Hi Ankit, welcome to hustlers group
```

## 6. What is Hoisting


A javascript mechanism where variables with **var** and **function declarations** are moved to the top of their scope before code execution.

👉 **function declarations** are properly hoisted (not arrow functions)
👉 **var** is hoisted.

## Code Example

```javascript
// hoisting
myPlace = 'Bengaluru'; // var is hoisted
console.log(myPlace);
var myPlace;

let myName = "Subhajit";
sayHi(); // valid

function sayHi() {
    let greet = "hi";
    console.log(greet, myName);
}

sayHello(); // error
let sayHello = function() {
    console.log(myName);
};
```

## Output

```
Bengaluru
hi Subhajit
d:\web_dev_recap\js_prep\js_youtube_explain\js_practice.js:200
sayHello(); // error
^

ReferenceError: Cannot access 'sayHello' before initialization
```

## 7. What is Currying

It involves breaking down a function that takes multiple arguments into a series of functions that take one argument each.

**Simple words:** This creates a chain of functions, where each function returns another function until the final result is achieved.

## Code Example

```javascript
// currying
// basic use case
function sum(a){
    return function(b){
        return function(c){
            return a+b+c;
        }
    }
}
console.log(sum(3)(4)(5));

// real life use case of event logger with time, type, message
const logger = (time) => (type) => (message) => `At time: ${time}, an event of type: ${type} occurred with full details as: ${message}`;

const eventsNow = logger('5am');
const errorEvent = eventsNow('error');
console.log(errorEvent('cannot set properties of null'))
```

## Output

```
12
At time: 5am, an event of type: error occurred with full details as: cannot set properties of null
```

## 7. What is Debouncing

**Debouncing** is a strategy used to improve the performance of a feature by controlling the time at which a function should be executed.

**Simple words:** It delays the execution of your code until the user stops performing a certain action for a specified amount of time. It is a practice used to improve browser performance.

## JavaScript Code

```javascript
// debouncing
// js file
const inputElement = document.getElementById('fruits');

function printInputText(text) {
    console.log(text);
}

function debounce(fx, delay){
    let timeoutId = null;
    return function(text){
        clearTimeout(timeoutId);
        timeoutId = setTimeout(() => {
            fx(text);
        }, delay);
    }
}

const debounceFn = debounce(printInputText, 2000);

inputElement.addEventListener('input', (event) => {
    debounceFn(event.target.value);
});
```
## 7. What is Throttling


**Throttling** is a mechanism that allows a function execution for a limited number of times after that it will block its execution.

**Simple words:** It limits the execution of your code to once in every specified time interval. It is a practice used to improve browser performance.

## JavaScript Code

```javascript
let count = 0;
function printScroll(){
  coint+=1;
  console.log("scroll called", count);
}
function throttle(dx, delay){
  let timeoutId = null;
  return function(){
    if(!timeoutId){
      timeoutId = setTimeout(() => {
        fx();
        clearTimeout(timeoutId);
        timeoutId = null;
      }, delay)
    }
  }
}

const throttleFn = throttle(printScroll, 2000);

document.addEventListener('scroll', (e) => {
  throttleFn
});
```


## 7. What is Polyfills

Polyfill is a way of providing futuristic API not available in browser.
We might need to do the native prototype modifications, so that we can get a feature/API.
There might be situations when we have a method not supported for specific browsers, in such cases we can use polyfills.

```javascript
// polyfills
if(!Array-prototype.contains){
  Array. prototype.contains = function(searchElement){
    return this.indexOf(searchElement) >= 0 ? true : false
  }
}
```