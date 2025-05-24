## 1. What are Scopes

The scope is the current context of execution in which values and expressions are "visible".

JavaScript variables have 3 types of scope:

**Block scope:** Variables declared inside a `{ }` block cannot be accessed from outside the block. `let` and `const` have block scope.

**Function scope:** Variables defined inside a function are not accessible (visible) from outside the function. `let`, `const` and `var` have function scope.

**Global scope:** Variables declared Globally (outside any function) have Global Scope. `let`, `const` and `var` have global scope.

## Code Example - let with different scopes


### let with different scopes
```javascript


// * let creates a block scope
// * Re-declaration in NOT allowed (in same scope)
// * Re-assignment is allowed

{ // block scope
    let x = 0;
    console.log(x); // 0
    let x = 1; // Error
}

{
    let x = 1;
    x = 2;
    console.log(x); // 2
}

console.log(x); // Error in global Scope
```


### var with different scopes
```javascript
// var with different scopes

// * No block scope, and can be re-declared
// * Only had function scope
// * var are hoisted, so they can be used before the declaration

var x = 1;
var x = 2; // valid

console.log(y) // valid
var y = 3

z=4
console.log(z) // valid
var z;
```

### const with different scopes

```javascript
// const with different scopes

// * const creates a block scope
// * Re-declaration in NOT allowed
// * Re-assignment is NOT allowed
// * Must be assigned at declaration time.

{ // block scope
    const x; //Error
    const y=0;
    y=3;
}

console.log(x); // Error in global scope
```

## Key Points:

### `let`:
- Creates a block scope
- Re-declaration is NOT allowed (in same scope)
- Re-assignment is allowed

### `var`:
- No block scope, and can be re-declared
- Only had function scope
- var are hoisted, so they can be used before the declaration

### `const`:
- const creates a block scope
- Re-declaration in NOT allowed
- Re-assignment is NOT allowed
- Must be assigned at declaration time


## 2. What is IIFE(Immediately Invoked Functional Expressions)

An **IIFE** is a function that is called immediately after it is defined.

## Use cases of IIFE:

👉 Avoid polluting the global namespace.
👉 Execute async/await functions.
👉 Provides encapsulation, allowing you to create private scopes for variables and functions.

## Code Example

```javascript
// IIFE (Immediately Invoked Functional Expression)
const pr = () => {
    return new Promise((res, rej) => {
        setTimeout(() => {
            res("resolved");
        }, 1500);
    });
};

(async () => {
    const a = await pr();
    console.log(a);
    
    const b = await pr();
    console.log(b);
    
    const c = await pr();
    console.log(c);
})();
```