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