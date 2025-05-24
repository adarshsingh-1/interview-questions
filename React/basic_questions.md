## 1. What is React?

**Answer:**  
React is a JavaScript library developed by Facebook for building user interfaces, especially single-page applications where data changes frequently. It allows developers to create large web applications that can update and render efficiently in response to data changes. React uses a virtual DOM to optimize rendering performance and supports component-based architecture, making code more reusable and easier to maintain.


## 2. What are the features of React?

**Answer:**

- **JSX (JavaScript XML):** React uses JSX, a syntax extension that allows mixing HTML with JavaScript.
- **Component-Based Architecture:** UI is broken down into reusable components, making development and maintenance easier.
- **Virtual DOM:** React uses a virtual DOM to efficiently update and render components by minimizing direct DOM manipulation.
- **Unidirectional Data Flow:** Data flows in one direction (from parent to child), making the code more predictable and easier to debug.
- **Declarative UI:** React makes it easier to design interactive UIs by describing what the UI should look like for different states.
- **Performance Optimization:** Features like virtual DOM and code-splitting help improve app performance.
- **Rich Ecosystem:** React has a vast ecosystem of tools, libraries, and community support.

## 3. What is JSX?

**Answer:**

JSX (JavaScript XML) is a syntax extension for JavaScript used in React. It allows you to write HTML-like code inside JavaScript files. This makes the code more readable and easier to write, especially when building UI components.

### Key Points:
- Looks like HTML but gets transpiled to JavaScript.
- Makes it easier to visualize the UI structure within components.
- JSX must have one parent element (use fragments or a single wrapper).
- You can embed JavaScript expressions using `{}` inside JSX.

**Example:**
```jsx
const element = <h1>Hello, world!</h1>;
```

## 4. What are the components in React?

**Answer:**

Components are the building blocks of a React application’s UI. They allow you to split the UI into independent, reusable pieces, and think about each piece in isolation.

### Types of Components:
- **Functional Components:**  
  These are simple JavaScript functions that return JSX. From React 16.8 onwards, functional components can use hooks to manage state and lifecycle.

  **Example:**
  ```jsx
  function Welcome(props) {
    return <h1>Hello, {props.name}</h1>;
  }
  ```
- **Class Components:**

    These are ES6 classes that extend `React.Component` and must include a `render()` method. Class components can manage their own state and have access to React lifecycle methods.

    **Example:**
    ```jsx
    import React, { Component } from 'react';

    class Welcome extends Component {
        render() {
            return <h1>Hello, {this.props.name}</h1>;
        }
    }
    ```

## 5. Explain the lifecycles methods of a react component?

**Answer:**

Lifecycle methods are special methods in React class components that are invoked at specific points in a component’s life — from creation to unmounting. These methods give you control over what happens when the component is initialized, updated, or removed from the DOM.

### 📌 Phases of Component Lifecycle:

---

#### 1. **Mounting Phase** (Component is being added to the DOM)

- **constructor()**  
  Initializes state and binds methods.

- **static getDerivedStateFromProps(props, state)**  
  Sync state with props before rendering. Rarely used.

- **render()**  
  Returns the JSX to render the UI.

- **componentDidMount()**  
  Invoked once after the component is mounted. Used for API calls, DOM manipulation, etc.

---

#### 2. **Updating Phase** (Component is being re-rendered due to state/prop changes)

- **static getDerivedStateFromProps(props, state)**  
  Called before every re-render.

- **shouldComponentUpdate(nextProps, nextState)**  
  Determines whether the component should re-render. Used for performance optimization.

- **render()**  
  Re-renders the UI based on new props/state.

- **getSnapshotBeforeUpdate(prevProps, prevState)**  
  Captures some information (like scroll position) before the DOM is updated.

- **componentDidUpdate(prevProps, prevState, snapshot)**  
  Invoked after the component updates. Used for DOM operations or data fetching on updates.

---

#### 3. **Unmounting Phase** (Component is being removed from the DOM)

- **componentWillUnmount()**  
  Clean up tasks (e.g., removing event listeners, canceling timers, etc.)

---

#### 4. **Error Handling Phase** (When an error occurs)

- **componentDidCatch(error, info)**  
  Catches errors in child components and logs them.

- **static getDerivedStateFromError(error)**  
  Used to update the UI in case of an error.

---

#### 🔔 Note:
React recommends using **functional components with Hooks** (`useEffect`, `useState`, etc.) for new code, which simplifies lifecycle management.



## 6. What is the difference between State and Props?

**Answer:**

In React, **state** and **props** are both plain JavaScript objects used to control component data, but they serve different purposes and behave differently.

#### 🔹 Props (Short for Properties):
- Props are **read-only**.
- Passed **from parent to child** component.
- Used to **configure a component** or pass data.
- Cannot be modified by the receiving component.
- Helps make components **reusable** and **dynamic**.

**Example:**
```jsx
function Greeting(props) {
  return <h1>Hello, {props.name}!</h1>;
}
```
#### 🔹 State:

- **State is mutable** (can be changed).
- Managed **within the component itself**.
- Used to store **data that may change over time** (e.g., user input, toggle status).
- Updating state **triggers a re-render** of the component.
```jsx
class Counter extends React.Component {
  constructor(props) {
    super(props);
    this.state = { count: 0 };
  }

  increment = () => {
    this.setState({ count: this.state.count + 1 });
  };

  render() {
    return (
      <div>
        <p>Count: {this.state.count}</p>
        <button onClick={this.increment}>Increment</button>
      </div>
    );
  }
}
```

#### 🆚 Key Differences Between Props and State

| **Feature**      | **Props**                        | **State**                          |
|------------------|----------------------------------|------------------------------------|
| **Mutability**   | Immutable (read-only)            | Mutable (can change)               |
| **Ownership**    | Passed from parent               | Managed within component           |
| **Use Case**     | Component configuration          | Managing dynamic data              |
| **Modification** | Cannot be modified by child      | Can be updated with `setState()`   |



## 6. What are Controlled Components?

**Answer:**

Controlled Components are form elements in React (like `<input>`, `<textarea>`, `<select>`) whose value is **controlled by React state**. This means that the form data is handled by the component, not the DOM.

### 🔹 Key Features:
- React **controls the value** of the input through state.
- You must provide an `onChange` handler to update the state.
- Ensures a **single source of truth** for form data.
- Makes validation and conditional rendering easier.

#### ✅ Example of a Controlled Component:
```jsx
import React, { useState } from 'react';

function ControlledForm() {
  const [name, setName] = useState('');

  const handleChange = (e) => {
    setName(e.target.value);
  };

  const handleSubmit = (e) => {
    e.preventDefault();
    alert(`Submitted Name: ${name}`);
  };

  return (
    <form onSubmit={handleSubmit}>
      <input type="text" value={name} onChange={handleChange} />
      <button type="submit">Submit</button>
    </form>
  );
}
```
#### How this example explains Controlled Components:

- The input’s **value** is tied to the React state variable `name`. This means React controls what is shown inside the input box.
- The `onChange` handler updates the React state every time you type something, keeping the input value and state in sync.
- Because React state is the **single source of truth**, the input doesn’t manage its own data internally.
- On form submission, the React state `name` is used, showing that the component fully controls the form data.

This pattern ensures the form input is controlled by React, making it easier to validate, modify, or reset form data programmatically.


## 7. What are Uncontrolled Components?

**Answer:**

Uncontrolled Components are form elements in React where the **DOM handles the form data** instead of React. These components use **refs** to access the values, meaning the data is stored in the actual HTML input element rather than in React state.

### 🔹 Key Features:
- Form data is handled by the **DOM**, not React.
- You use **`ref`** to directly access form values.
- Simpler for quick forms where React control isn't needed.
- Not ideal for validation, but useful for integrating with non-React code or simple use cases.

### ✅ Example of an Uncontrolled Component:
```jsx
import React, { useRef } from 'react';

function UncontrolledForm() {
  const inputRef = useRef(null);

  const handleSubmit = (e) => {
    e.preventDefault();
    alert(`Submitted Name: ${inputRef.current.value}`);
  };

  return (
    <form onSubmit={handleSubmit}>
      <input type="text" ref={inputRef} />
      <button type="submit">Submit</button>
    </form>
  );
}
```
#### How this example explains Uncontrolled Components:

- Here, the `ref` (`inputRef`) is attached to the input field.
- Instead of tracking the value using `state` and `onChange`, we read the input value directly from the DOM using `inputRef.current.value`.
- React is **not controlling** the input field — hence, it is called an **uncontrolled component**.


## 8. What is a Higher Order Component (HOC)?

**Answer:**

A **Higher Order Component (HOC)** is an advanced technique in React for **reusing component logic**.  
It is a **function** that takes a component and returns a **new enhanced component**.

> **HOC = A function that takes a component and returns a new component**

### 🔹 Purpose:
- Code reuse and logic abstraction
- Add common functionalities (e.g., authentication, theming, logging)
- Works like higher-order functions in JavaScript

### ✅ Syntax:
```js
const EnhancedComponent = higherOrderComponent(WrappedComponent);
```



## 9. Explain the concept of Virtual DOM?

**Answer:**

The **Virtual DOM (VDOM)** is a lightweight, in-memory representation of the **real DOM** used by React to optimize performance and rendering.

### 🔹 Key Concepts:
- React creates a **virtual copy** of the actual DOM.
- When changes occur (like user input), React updates the **Virtual DOM first**, not the real DOM directly.
- It then **compares (diffs)** the new VDOM with the previous one to find the minimal number of changes.
- Only the **necessary parts of the real DOM** are updated (this is called *reconciliation*).

### 💡 Benefits of Virtual DOM:
- Improves **performance** by reducing direct DOM manipulations.
- Leads to **faster updates** and **better user experience**.
- Helps in building **efficient UIs**, especially for dynamic content.

### ✅ Real-World Analogy:
Think of the Virtual DOM as a **blueprint** of a house. Instead of rebuilding the whole house every time you want to change something, you update the blueprint and only make changes where needed.

### 🔄 Process Overview:
1. UI changes → New Virtual DOM created
2. React compares new VDOM with old VDOM
3. Calculates the difference (diffing algorithm)
4. Updates only the changed elements in the real DOM

---

