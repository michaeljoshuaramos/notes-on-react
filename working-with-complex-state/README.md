# Working With Complex State

## Table of Contents

1. [A Look at useReducer Hook](#a-look-at-usereducer-hook)
2. [Summary: useState vs. useReducer Hook](#summary-usestate-vs-usereducer-hook)
3. [Context API: Passing State to Multiple Deeply Nested Components](#context-api-passing-state-to-multiple-deeply-nested-components)

## A Look at useReducer Hook

The useReducer hook in React is an alternative to useState for managing more complex state logic. It takes a **reducer function** and an **initial state**, and returns the current state and a dispatch function to trigger state updates.

A reducer function defines how the state should change in response to actions, which are dispatched.

Here's a succinct example using `useReducer` hook in React:

```jsx
import React, { useReducer } from "react";

const initialState = { count: 0 };

function reducer(state, action) {
  switch (action.type) {
    case "increment":
      return { count: state.count + 1 };
    case "decrement":
      return { count: state.count - 1 };
    default:
      return state;
  }
}

const Counter = () => {
  const [state, dispatch] = useReducer(reducer, initialState);

  return (
    <div>
      <p>Count: {state.count}</p>
      <button onClick={() => dispatch({ type: "increment" })}>+</button>
      <button onClick={() => dispatch({ type: "decrement" })}>-</button>
    </div>
  );
};

export default Greeting;
```

### Explanation:

- `reducer`: Defines how state changes based on action types (`increment`, `decrement`).
- `useReducer`: Returns the current state and a `dispatch` function.
- `dispatch`: Triggers state changes by passing an action object (e.g., `{ type: 'increment' }`).

Use useReducer for more complex state management, especially when state updates depend on previous states or involve multiple actions.

## Summary: useState vs. useReducer Hook

![alt text](image.png)

## Context API: Passing State to Multiple Deeply Nested Components

The **Context API** in React is a way to pass data through the component tree without having to pass props manually at every level, solving the problem of "prop drilling." It allows you to share state across deeply nested components without passing it down through multiple layers.

### Explanation:

The Context API creates a context object that holds the data you want to share. A provider component makes this data available to any component in the tree, while a consumer component can access this data wherever needed.

### Basic Example:

```jsx
import React, { createContext, useContext, useState } from "react";

// Create context
const MyContext = createContext();

function Parent() {
  const [value, setValue] = useState("Hello from Context!");

  return (
    <MyContext.Provider value={value}>
      <Child />
    </MyContext.Provider>
  );
}

function Child() {
  const contextValue = useContext(MyContext);
  return <div>{contextValue}</div>;
}

export default Parent;
```

Here, the `Parent` component provides a value through the `MyContext.Provider`, and the `Child` component accesses that value using `useContext`. This avoids the need to pass props through intermediate components.

**Note: Only the components that consume the context directly will re-render** if the context value changes. However, the nested children of these consuming components will also re-render, but only if they depend on the consuming component's state or props.

To clarify:

- **Direct consumers** of the context (i.e., components that use `useContext` or the `Context.Consumer` component) will re-render when the context value changes.
- **Nested components** within those consumers will only re-render if they are affected by the re-render of their parent (e.g., through updated props).
