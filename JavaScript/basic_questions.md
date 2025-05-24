## 1. What is Strict Mode in JavaScript

The `"use strict"` directive enables JavaScript's strict mode.  
This was introduced in **ECMAScript 5**. It enforces stricter parsing and error handling on the code at runtime.  
It also helps you write cleaner code and catch errors and bugs that might otherwise go unnoticed.

---

### 🔹 Example:

```js
// strict mode
"use strict";
x = 56;
console.log(x);
```
**Output**
```
ReferenceError: x is not defined
    at Object.<anonymous> (.../js_practice.js:86:2)
    ...
```
#### 🔸 Explanation:

In strict mode, you must declare variables using let, const, or var.
In the above example, x was not declared before assignment, so JavaScript throws a ReferenceError.




