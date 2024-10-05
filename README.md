# React.js Features Explained with Examples

This document provides an in-depth look at key React.js features, with explanations and code examples for each.

## 1. Component-Based Architecture

**Explanation:** React's core philosophy is building UIs using reusable, encapsulated components. This approach promotes modularity, reusability, and easier maintenance.

**Example:**

```jsx
// Button.js
function Button({ label, onClick }) {
  return <button onClick={onClick}>{label}</button>;
}

// App.js
function App() {
  return (
    <div>
      <h1>My App</h1>
      <Button label="Click me" onClick={() => alert('Button clicked!')} />
    </div>
  );
}
```

## 2. JSX (JavaScript XML)

**Explanation:** JSX is a syntax extension for JavaScript, allowing you to write HTML-like code in your JavaScript files. It makes the structure of UI components more readable and expressive.

**Example:**

```jsx
function Greeting({ name }) {
  return <h1>Hello, {name}!</h1>;
}

const element = <Greeting name="React" />;
```

## 3. Virtual DOM

**Explanation:** React uses a virtual DOM to optimize rendering performance. It creates a lightweight copy of the actual DOM in memory and uses efficient diffing algorithms to update only the parts of the DOM that have changed.

**Note:** This feature is built into React and doesn't require specific code examples.

## 4. One-Way Data Flow

**Explanation:** React implements a unidirectional data flow, making the code more predictable and easier to debug. Data is passed down from parent to child components via props.

**Example:**

```jsx
function Parent() {
  const [count, setCount] = useState(0);

  return (
    <div>
      <h1>Count: {count}</h1>
      <Child count={count} onIncrement={() => setCount(count + 1)} />
    </div>
  );
}

function Child({ count, onIncrement }) {
  return <button onClick={onIncrement}>Increment {count}</button>;
}
```

## 5. State Management

**Explanation:** React provides built-in state management for components, allowing them to keep track of changing data. Hooks like `useState` make state management in functional components easy.

**Example:**

```jsx
import React, { useState } from 'react';

function Counter() {
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>Click me</button>
    </div>
  );
}
```

## 6. Lifecycle Methods (Class Components)

**Explanation:** Class components in React have lifecycle methods that allow you to run code at particular times in the component's life.

**Example:**

```jsx
class Clock extends React.Component {
  constructor(props) {
    super(props);
    this.state = { date: new Date() };
  }

  componentDidMount() {
    this.timerID = setInterval(() => this.tick(), 1000);
  }

  componentWillUnmount() {
    clearInterval(this.timerID);
  }

  tick() {
    this.setState({ date: new Date() });
  }

  render() {
    return <div>It is {this.state.date.toLocaleTimeString()}.</div>;
  }
}
```

## 7. Hooks (Functional Components)

**Explanation:** Hooks allow you to use state and other React features without writing a class. They provide a more direct API to the React concepts you already know: props, state, context, refs, and lifecycle.

**Example:**

```jsx
import React, { useState, useEffect } from 'react';

function Example() {
  const [count, setCount] = useState(0);

  useEffect(() => {
    document.title = `You clicked ${count} times`;
  });

  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>Click me</button>
    </div>
  );
}
```

## 8. Context API

**Explanation:** Context provides a way to pass data through the component tree without having to pass props down manually at every level. This is useful for sharing data that can be considered "global" for a tree of React components.

**Example:**

```jsx
const ThemeContext = React.createContext('light');

function App() {
  return (
    <ThemeContext.Provider value="dark">
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
  const theme = useContext(ThemeContext);
  return <button theme={theme}>I am styled by theme context!</button>;
}
```

## 9. Error Boundaries

**Explanation:** Error boundaries are React components that catch JavaScript errors anywhere in their child component tree, log those errors, and display a fallback UI instead of the component tree that crashed.

**Example:**

```jsx
class ErrorBoundary extends React.Component {
  constructor(props) {
    super(props);
    this.state = { hasError: false };
  }

  static getDerivedStateFromError(error) {
    return { hasError: true };
  }

  render() {
    if (this.state.hasError) {
      return <h1>Something went wrong.</h1>;
    }
    return this.props.children;
  }
}

// Usage
<ErrorBoundary>
  <MyWidget />
</ErrorBoundary>
```

## 10. Fragments

**Explanation:** Fragments let you group a list of children without adding extra nodes to the DOM.

**Example:**

```jsx
function Table() {
  return (
    <table>
      <tr>
        <Columns />
      </tr>
    </table>
  );
}

function Columns() {
  return (
    <React.Fragment>
      <td>Hello</td>
      <td>World</td>
    </React.Fragment>
  );
}
```

## 11. Refs

**Explanation:** Refs provide a way to access DOM nodes or React elements created in the render method.

**Example:**

```jsx
function TextInputWithFocusButton() {
  const inputEl = useRef(null);
  const onButtonClick = () => {
    inputEl.current.focus();
  };
  return (
    <>
      <input ref={inputEl} type="text" />
      <button onClick={onButtonClick}>Focus the input</button>
    </>
  );
}
```

## 12. Higher-Order Components (HOCs)

**Explanation:** A higher-order component is a function that takes a component and returns a new component. This technique can be used for code reuse, logic abstraction, and state manipulation.

**Example:**

```jsx
function withLoading(WrappedComponent) {
  return function({ isLoading, ...props }) {
    if (isLoading) return <div>Loading...</div>;
    return <WrappedComponent {...props} />;
  }
}

// Usage
const ComponentWithLoading = withLoading(MyComponent);
```

## 13. Render Props

**Explanation:** The term "render prop" refers to a technique for sharing code between React components using a prop whose value is a function.

**Example:**

```jsx
class Mouse extends React.Component {
  state = { x: 0, y: 0 };

  handleMouseMove = (event) => {
    this.setState({
      x: event.clientX,
      y: event.clientY
    });
  }

  render() {
    return (
      <div style={{ height: '100%' }} onMouseMove={this.handleMouseMove}>
        {this.props.render(this.state)}
      </div>
    );
  }
}

// Usage
<Mouse render={({ x, y }) => (
  <h1>The mouse position is ({x}, {y})</h1>
)}/>
```

## 14. Strict Mode

**Explanation:** StrictMode is a tool for highlighting potential problems in an application. It activates additional checks and warnings for its descendants.

**Example:**

```jsx
import React from 'react';

function ExampleApplication() {
  return (
    <React.StrictMode>
      <div>
        <Header />
        <Main />
      </div>
    </React.StrictMode>
  );
}
```

## 15. Portals

**Explanation:** Portals provide a first-class way to render children into a DOM node that exists outside the DOM hierarchy of the parent component.

**Example:**

```jsx
import ReactDOM from 'react-dom';

const Modal = ({ children }) => {
  return ReactDOM.createPortal(
    children,
    document.getElementById('modal-root')
  );
};

// Usage
function App() {
  return (
    <div>
      <h1>My App</h1>
      <Modal>
        <h2>This is a modal</h2>
      </Modal>
    </div>
  );
}
```

These examples and explanations cover the key features of React.js, demonstrating its power and flexibility in building user interfaces. React's component-based architecture, along with features like JSX, state management, hooks, and more, make it a powerful library for creating interactive and efficient web applications.
