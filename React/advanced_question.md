## 1. How do you implement routing in React
**Answer**
Use **React Router** for client-side routing.
1. Install React Router:
```bash
npm install react-router-dom
```
2. Set Up Routing
```jsx
import { BrowserRouter, Routes, Route } from 'react-router-dom';
import Home from './Home';
import About from './About';

function App() {
    return (
        <BrowserRouter>
        <Routes>
            <Route path="/" element={<Home />} />
            <Route path="/about" element={<About />} />
            </Routes>
            </BrowserRouter>
        );
    }
```
3. This allows navigation without reloading the page in a Single Page Application (SPA).




## 2. Difference bwtween react router and traditional routing

**Answer**

| Feature              | React Router                             | Traditional Routing                      |
|----------------------|-------------------------------------------|------------------------------------------|
| **Page Reload**      | No full-page reload (SPA)                | Full-page reload on every route change   |
| **Speed**            | Faster, smoother navigation              | Slower due to page reloads               |
| **State Persistence**| Maintains state between routes           | State resets on each reload              |
| **Routing Type**     | Client-side routing                      | Server-side routing                      |
| **Use Case**         | Single Page Applications (SPA)           | Multi-page websites                      |

**Summary:**  
React Router is client-side and enables seamless, fast navigation in SPAs, while traditional routing reloads the whole page and is used in multi-page apps.

## 3  How do you optimize performance in React?

- **Use React.memo** to prevent unnecessary re-renders of functional components.
- **Use useCallback and useMemo** to memoize functions and values.
- **Lazy load components** using `React.lazy` and `Suspense`.
- **Code splitting** with dynamic `import()` to reduce initial bundle size.
- **Avoid inline functions/objects** in props.
- **Use keys** correctly in lists to avoid extra rendering.
- **Use virtualization** (e.g., `react-window`) for large lists.
- **Keep component state minimal** and lift state only when needed.

## 4. What are React Fragments?

**React Fragments** let you group multiple elements without adding extra nodes to the DOM.Avoid unnecessary wrapper elements and keep the DOM clean.

Instead of using a `<div>`, use:

```jsx
<>
  <h1>Title</h1>
  <p>Description</p>
</>
```
**OR**
```jsx
<React.Fragment>
  <h1>Title</h1>
  <p>Description</p>
</React.Fragment>
```

## 5. Explain the useMemo and useCallback Hooks

 **useMemo**   
`useMemo` memoizes the **result** of a function to avoid expensive recalculations on every render.

```jsx
const expensiveValue = useMemo(() => computeExpensiveValue(a, b), [a, b]);
```
 **useCallback**

`useCallback` memoizes the **function itself**, preventing it from being recreated on every render.
```jsx
const handleClick = useCallback(() => {
  doSomething();
}, [dependency]);
```

## 6. What is React Fiber?

**React Fiber** is the **reconciliation engine** in React (since React 16) that enables:

- **Incremental rendering**: breaking rendering work into units and pausing/resuming as needed.
- **Better performance**: especially for animations and complex UI updates.
- **Prioritization**: assigning priority to different updates.
- **Concurrency**: lays the foundation for features like **Concurrent Mode**.

**Summary:** React Fiber makes React faster, more responsive, and able to handle complex UI updates efficiently.

## 7. How does Server-Side Rendering (SSR) work in React?

**Server-Side Rendering (SSR)** in React means rendering components to HTML on the server and sending that HTML to the browser.

#### How it works:
1. Server runs React code and generates HTML.
2. HTML is sent to the client (faster initial load).
3. React "hydrates" the HTML to make it interactive.

#### Tools:
- **Next.js** – most popular React framework for SSR.

**Benefits:**  
- Faster initial load  
- Better SEO  
- Improved performance on slow devices

## 8. What are error boundaries in React
Error boundaries are React components that catch JavaScript errors anywhere in their child component tree, log those errors, and display a fallback UI instead of the component tree that crashed.

## Key Characteristics

- **Class Components Only**: Error boundaries must be class components (not functional components)
- **Catch Errors During**: Rendering, lifecycle methods, and constructors of the whole tree below them
- **Don't Catch Errors In**: Event handlers, asynchronous code, server-side rendering, or errors thrown in the error boundary itself

## Implementation

```javascript
class ErrorBoundary extends React.Component {
  constructor(props) {
    super(props);
    this.state = { hasError: false };
  }

  static getDerivedStateFromError(error) {
    // Update state to show fallback UI
    return { hasError: true };
  }

  componentDidCatch(error, errorInfo) {
    // Log error to error reporting service
    console.log('Error caught:', error, errorInfo);
  }

  render() {
    if (this.state.hasError) {
      return <h1>Something went wrong.</h1>;
    }
    return this.props.children;
  }
}
```

## Usage

```javascript
<ErrorBoundary>
  <MyComponent />
</ErrorBoundary>
```

## Lifecycle Methods

- **`getDerivedStateFromError()`**: Updates state to render fallback UI
- **`componentDidCatch()`**: Logs error information for debugging

## Best Practices

- Place error boundaries at strategic levels in your component tree
- Use them to prevent entire app crashes
- Log errors for monitoring and debugging
- Provide meaningful fallback UIs
- Don't overuse - place them where recovery makes sense


## 9. Difference Between `useEffect` and `useLayoutEffect`

| Feature              | `useEffect`                                     | `useLayoutEffect`                                |
|----------------------|--------------------------------------------------|--------------------------------------------------|
| Execution Timing     | Runs **after** the DOM is painted               | Runs **before** the DOM is painted              |
| Use Case             | Non-blocking side effects (e.g., API calls)     | Synchronous DOM reads/writes (e.g., measuring layout) |
| Performance Impact   | Doesn’t block browser painting                  | Blocks painting until effect runs               |
| Common Usage         | Data fetching, subscriptions                    | Animations, reading layout measurements         |

Use `useEffect` for most side effects.  
Use `useLayoutEffect` when DOM measurement or synchronous updates are required.

### Example of `useEffect`

```jsx
import { useEffect, useState } from "react";

function UserComponent() {
  const [user, setUser] = useState(null);

  useEffect(() => {
    // Fetching data after component renders
    fetch("/api/user")
      .then(res => res.json())
      .then(data => setUser(data));
  }, []);

  return <div>{user ? user.name : "Loading..."}</div>;
}
```

### Example of `useLayoutEffect`
```jsx
import { useLayoutEffect, useRef, useState } from "react";

function MeasureComponent() {
  const boxRef = useRef();
  const [width, setWidth] = useState(0);

  useLayoutEffect(() => {
    // Measuring DOM before paint
    const boxWidth = boxRef.current.getBoundingClientRect().width;
    setWidth(boxWidth);
  }, []);

  return (
    <div>
      <div ref={boxRef} style={{ width: "50%" }}>Resizable Box</div>
      <p>Width: {width}px</p>
    </div>
  );
}
```

## 10. How to Handle Forms in React

### 1. **Controlled Components**
- Form inputs are tied to component state.
- Updates are handled via `onChange`.

```jsx
import { useState } from "react";

function MyForm() {
  const [name, setName] = useState("");

  const handleSubmit = (e) => {
    e.preventDefault();
    console.log("Submitted:", name);
  };

  return (
    <form onSubmit={handleSubmit}>
      <input
        type="text"
        value={name}
        onChange={(e) => setName(e.target.value)}
      />
      <button type="submit">Submit</button>
    </form>
  );
}
```
### Uncontrolled Components (less common)
-	Use useRef to access DOM elements directly.

```jsx
import { useRef } from "react";

function UncontrolledForm() {
  const nameRef = useRef();

  const handleSubmit = (e) => {
    e.preventDefault();
    console.log("Submitted:", nameRef.current.value);
  };

  return (
    <form onSubmit={handleSubmit}>
      <input type="text" ref={nameRef} />
      <button type="submit">Submit</button>
    </form>
  );
}
```

## 11. What are some Best Practices for Writing React Components

### 1. **Keep Components Small and Focused**
- Each component should do **one thing well**.
- Easier to test, reuse, and maintain.

### 2. **Use Functional Components with Hooks**
- Prefer **functional** over class components.
- Use `useState`, `useEffect`, etc., for logic.

### 3. **Use Meaningful and Consistent Naming**
- Name components and variables clearly (e.g., `UserCard`, `handleClick`).

### 4. **Lift State Up When Needed**
- Share state by lifting it to the **nearest common ancestor**.

### 5. **Avoid Prop Drilling**
- Use **Context API** or state management tools like Redux/Zustand for deeply nested data.

### 6. **Use PropTypes or TypeScript**
- Add type safety with `PropTypes` or better: **TypeScript**.

### 7. **Use Keys in Lists**
- Always use **unique `key` props** when rendering lists.

### 8. **Separate Logic from UI**
- Keep logic (hooks/functions) separate from rendering for cleaner code.

### 9. **Use Destructuring for Props**
```jsx
function Greeting({ name }) {
  return <h1>Hello, {name}</h1>;
}
```


## 12. What is Code Splitting in React?

**Code Splitting** is a technique to split your React app into smaller bundles (chunks), so only the necessary code is loaded when needed.

###  Why Use Code Splitting?
- Improves **performance** by reducing initial load time.
- Loads code **on demand** (lazy loading).
- Essential for **large applications**.

###  How to Implement in React?

#### Using `React.lazy()` and `Suspense`
```jsx
import React, { Suspense } from "react";

const LazyComponent = React.lazy(() => import("./MyComponent"));

function App() {
  return (
    <Suspense fallback={<div>Loading...</div>}>
      <LazyComponent />
    </Suspense>
  );
}
```


## 13. How to Lazy Load Components in React

### ✅ Use `React.lazy()` with `Suspense`

Lazy loading lets you load components **only when needed**, reducing initial load time.

### 📦 Syntax:

```jsx
import React, { Suspense } from "react";

// Lazy load the component
const LazyComponent = React.lazy(() => import('./MyComponent'));

function App() {
  return (
    <Suspense fallback={<div>Loading...</div>}>
      <LazyComponent />
    </Suspense>
  );
}
```

**Key Points**.   
	•	React.lazy() takes a function that returns a dynamic import().     
	•	Suspense shows a fallback UI until the lazy component is loaded.