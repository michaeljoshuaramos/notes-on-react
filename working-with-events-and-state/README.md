# React: Working With Events and State

## Key Points

- Don’t set state manually (I.e. don’t use the variable directly to update itself), use the setter function provided by the `useState` hook.
  - Why use the setter function provided by the `useState` hook?
    - It ensures that React is aware of state changes and can properly manage the component's rendering lifecycle. When you use the setter function, React knows that the state has changed and triggers a re-render of the component. This keeps the UI in sync with the state.
- In React, when updating the state based on the current state, it is important to use the callback function form of the state setter.
  - When is it better to use callback function form of the state setter?
    - It is because state updates are asynchronous and can be batched for performance reasons.
    - When you call the setState function, React schedules an update rather than immediately applying the changes. This allows React to batch multiple state updates together, minimizing unnecessary re-renders and improving overall efficiency.
- Don’t set state in the render logic.
