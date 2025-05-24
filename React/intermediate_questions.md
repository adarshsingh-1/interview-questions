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


## 6. What are the most commomly used hooks in React?
**Answer:**
### 📘 Most Commonly Used React Hooks

React hooks are functions that let you "hook into" React state and lifecycle features from function components.

---

### 🔹 1. `useState`
- **Purpose**: Adds local state to functional components.
- **Syntax**:
  ```js
  const [count, setCount] = useState(0);
  ```
  **Use Case**: Managing input fields, toggles, counters, etc.


### 🔹 2. `useEffect`
- **Purpose**: Handles side effects like API calls, subscriptions, or manually changing the DOM.
- **Syntax**:
```js
  useEffect(() => {
  // Side effect logic
  return () => {
    // Cleanup (optional)
  };
}, [dependency]);
```

**Use Case**: Fetching data on mount, updating title, cleaning intervals.



### 🔹 3. `useContext`
- **Purpose**: Consumes context data without using <Context.Consumer>.
- **Syntax**:
```js
const value = useContext(MyContext);
```
  **Use Case**: Accessing global state like auth, theme, or user data.


### 🔹 4. `useRef`
- **Purpose**: Creates a reference to a DOM element or value that persists across renders.
- **Syntax**:
```js
const inputRef = useRef(null);
```
  **Use Case**: Accessing DOM nodes, tracking previous values.


### 🔹 5. `useMemo`
- **Purpose**: Memoizes the result of a calculation to avoid expensive re-renders.
- **Syntax**:
```js
const result = useMemo(() => computeExpensiveValue(a, b), [a, b]);
```
  **Use Case**:  Performance optimization.


### 🔹 6. `useCallback`
- **Purpose**: Returns a memoized version of a callback function.
- **Syntax**:
```js
const memoizedCallback = useCallback(() => {
  doSomething(a, b);
}, [a, b]);
```
  **Use Case**:   Prevents unnecessary re-renders in child components.



### 🔹 6. `useReducer`
- **Purpose**: An alternative to useState for complex state logic.
- **Syntax**:
```js
const [state, dispatch] = useReducer(reducer, initialState);
```
  **Use Case**:  Complex state management, multiple state updates.


## 7. Explain useState and useEffect hooks?

### `useState` – Manage State in Functional Components

### 📌 What is it?
`useState` is a React Hook that lets you add **state variables** to functional components.

### 🧠 Syntax:
```js
const [state, setState] = useState(initialValue);
```
state: The current state value.  
setState: A function to update the state.  
initialValue: The starting value of the state.
```javascript
import React, { useState } from 'react';

function Counter() {
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>Clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>Click Me</button>
    </div>
  );
}
```
**Use Cases:**
- Handling form inputs. 
- Toggling modals.   
- Counter logic

### `useEffect` – Perform Side Effects

### 📌 What is it?
`useEffect` is a React Hook that lets you **perform side effects** in functional components.

Side effects can include:
- Fetching data from APIs
- Subscribing to events
- Setting up timers
- Manually interacting with the DOM

---


### 🧠 Syntax:
```js
useEffect(() => {
  // Code to run (effect)

  return () => {
    // Optional cleanup logic
  };
}, [dependencies]);
```
useEffect runs after the component renders.  
It can optionally return a cleanup function.  
The effect runs again if any value in the dependencies array changes.

```javascript
import React, { useState, useEffect } from 'react';

function Timer() {
  const [count, setCount] = useState(0);

  useEffect(() => {
    const interval = setInterval(() => {
      setCount(prev => prev + 1);
    }, 1000);

    // Cleanup when component unmounts
    return () => clearInterval(interval);
  }, []); // Runs only once when component mounts

  return <h1>Timer: {count}s</h1>;
}
```
**Usecase**

- Fetching data from APIs
- Starting and clearing timers or intervals
- Adding event listeners (e.g., scroll, resize)
- Triggering animations or DOM updates


##  8. What is Context API in React?

The **Context API** is a feature in React that allows you to **share state (data) globally** across your application, without having to manually pass props down through every level of the component tree.

It's like a **global state manager** but built into React — no need for Redux or any external library for simpler use cases.

---

### 🧠 When to Use It?
- When you have **data that needs to be accessed by many components** at different nesting levels.
- Avoiding "prop drilling" — passing props through intermediate components that don't use them, just to get data to deeply nested ones.

---

### 🔧 Key Functions:
- `React.createContext()` – Creates a context object.
- `<Context.Provider>` – Wraps components and provides the value.
- `useContext(Context)` – Allows any child component to consume the context.

---

### ✅ Example:

```javascript
import React, { createContext, useContext, useState } from 'react';

// 1. Create the context
const ThemeContext = createContext();

function App() {
  const [theme, setTheme] = useState('light');

  return (
    // 2. Provide context to children
    <ThemeContext.Provider value={{ theme, setTheme }}>
      <Toolbar />
    </ThemeContext.Provider>
  );
}

function Toolbar() {
  return (
    <div>
      <ThemedButton />
    </div>
  );
}

function ThemedButton() {
  // 3. Consume the context
  const { theme, setTheme } = useContext(ThemeContext);

  return (
    <button
      onClick={() => setTheme(theme === 'light' ? 'dark' : 'light')}
    >
      Current Theme: {theme}
    </button>
  );
}
```

## 9. How Does Context API Help in Managing State?

The **Context API** in React helps manage **global or shared state** across multiple components, especially when:

- The state needs to be accessed by deeply nested components.
- Passing props manually becomes repetitive and messy (called "prop drilling").

---

### 📌 What Problem Does It Solve?

In large applications, passing data through multiple levels of components can look like this:

```js
<App>
  <Header>
    <UserMenu>
      <ProfileButton user={user} />
    </UserMenu>
  </Header>
</App>
```

🔁 If user is needed in ProfileButton, it has to be passed down through Header and UserMenu even though they don’t use it.

This is inefficient and hard to maintain.

**How Context API Helps**  
1.	Create a central “store” (context) that holds your state.  
2.	Wrap your component tree with a Provider, which gives access to that state.  
3.	Use useContext hook to read and update the state from anywhere in the component tree.

###  Benefits of Using Context API for State

|  Benefit                     |  Description                                                  |
|-------------------------------|-----------------------------------------------------------------|
| Avoids Prop Drilling          | No need to pass props through intermediate components           |
| Global State Sharing          | Easily share state like user info, theme, language, etc.        |
| Simple to Use                 | Uses built-in React APIs — no need for Redux or extra tools     |
| Easy Access with `useContext` | Consume state anywhere inside the provider’s component tree     |


## 10. What is Redux?

**Redux** is a **predictable state management library** for JavaScript applications.  
It is commonly used with **React** to manage **global application state** in a centralized store.


### 🧠 Why Use Redux?

In large apps, passing data via props becomes messy (called **prop drilling**).  
Also, managing state across unrelated components becomes difficult.  
**Redux solves this** by providing:

- A **single source of truth** (centralized state store)
- A **predictable way** to update state (via actions and reducers)

### 🔧 Core Concepts:

| Concept     | Description                                                                 |
|-------------|-----------------------------------------------------------------------------|
| **Store**   | Holds the entire state of the application                                    |
| **Action**  | A plain JS object that describes what happened (`{ type: "INCREMENT" }`)     |
| **Reducer** | A function that takes current state and action, returns new state            |
| **Dispatch**| A method used to send actions to the reducer                                 |
| **useSelector** | React-Redux hook to read data from the store                            |
| **useDispatch** | React-Redux hook to dispatch actions                                    |

---

### ✅ Redux Flow:

1. **User interacts** with the UI (e.g., clicks a button)
2. Component **dispatches an action**
3. **Reducer** receives the action and updates the state
4. **Store** holds the new state
5. UI automatically **re-renders** with updated data

---

### 💡 Example:

```js
// Action
const increment = { type: 'INCREMENT' };

// Reducer
function counterReducer(state = 0, action) {
  switch (action.type) {
    case 'INCREMENT':
      return state + 1;
    default:
      return state;
  }
}

// Store
import { createStore } from 'redux';
const store = createStore(counterReducer);

// Dispatching Action
store.dispatch({ type: 'INCREMENT' });
console.log(store.getState()); // Output: 1

```