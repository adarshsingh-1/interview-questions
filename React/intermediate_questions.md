## 1. What is the difference between Functional and Class Components?

**Answer:**

### 🆚 Key Differences Between Functional and Class Components:

| Feature                 | Functional Component            | Class Component                      |
|-------------------------|----------------------------------|--------------------------------------|
| Syntax                  | Function                         | Class                                |
| State Management        | `useState`, `useEffect` (Hooks) | `this.state`, `this.setState()`      |
| Lifecycle Methods       | Via Hooks                        | Traditional lifecycle methods        |
| Simplicity              | Simple and concise               | More verbose                         |
| Performance             | Slightly better                  | Slightly heavier                     |
| Usage (Modern React)    | Recommended                      | Less preferred                       |

---

## 2. How do you handle events in React?

**Answer:**

In React, **event handling** is similar to handling events in plain HTML/JavaScript, but with a few key differences:

- Events are named using **camelCase** instead of lowercase.
- You pass a **function reference**, not a string.
- You can access the event object like in native DOM, but React uses a wrapper called `SyntheticEvent`.

### ✅ Example: Handling a Click Event
```jsx
import React from 'react';

function ClickButton() {
  const handleClick = () => {
    alert('Button clicked!');
  };

  return <button onClick={handleClick}>Click Me</button>;
}
```

#### 🔹 Explanation:
-	onClick={handleClick} attaches the event handler to the button.
-	handleClick is the function that runs when the button is clicked.
-	You don’t need to use addEventListener — React takes care of that internally.

---

## 3. What are Keys in React and Why are they Important?

**Answer:**

In React, **keys** are special string attributes used to **identify elements in a list**. They help React **track which items have changed, been added, or removed**, and optimize the re-rendering process.

### 🔹 Why Keys are Important:
- Improve **performance** by helping React avoid unnecessary re-renders.
- Enable **efficient diffing** in the Virtual DOM.
- Maintain the **identity of components** across updates.

### ✅ Example:
```jsx
const items = ['Apple', 'Banana', 'Cherry'];

const ItemList = () => (
  <ul>
    {items.map((item, index) => (
      <li key={index}>{item}</li>
    ))}
  </ul>
);
```
## 4. How do you pass data between components in React?

**Answer:**

In React, data is usually passed **between components** using **props**, **callbacks**, and **context**, depending on the direction of the data flow.

---

### 🔸 1. From Parent to Child (via **props**)
You pass data from a **parent** component to a **child** component using `props`.



### 🔸 2. From Child to Parent (via **callback function**)
Pass a function from parent to child, and call it from the child with the data you want to send.



### 🔸 3. Between Sibling Components (via **lifting state up**)
Use the parent component to hold the shared state and pass it down to the children.


### 🔸 4. Between Sibling Components (via **lifting state up**)
When data needs to be accessible by many components, use React.createContext().

---
## 5. What are React Hooks?

**Answer:**

**React Hooks** are special functions introduced in React 16.8 that let you **use state and other React features** in **functional components** — without writing a class.

---

### 🔹 Why Hooks?
- Avoid writing class components just for using state or lifecycle methods.
- Make code **cleaner, reusable**, and **easier to test**.
- Enable **sharing logic** across components using custom hooks.

---

### 🔸 Commonly Used Built-in Hooks:

| Hook         | Purpose                                      |
|--------------|----------------------------------------------|
| `useState`   | Adds state to functional components          |
| `useEffect`  | Performs side effects (e.g., fetch, timer)   |
| `useContext` | Access context values                        |
| `useRef`     | Access/manipulate DOM elements or persist values |
| `useMemo`    | Optimize performance by memoizing values     |
| `useCallback`| Memoize functions                            |
| `useReducer` | Alternative to `useState` for complex state logic |


