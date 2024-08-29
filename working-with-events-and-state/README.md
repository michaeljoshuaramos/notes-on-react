# Working With Events and State

## Table of Contents

1. [Key Points](#key-points)
1. [Knowledge Questions](#knowledge-questions)

## Key Points

- Don’t set state manually (i.e. don’t use the variable directly to update itself), use the set function provided by the `useState` hook.
- Don’t set state in the render logic.

**[⬆ back to top](#table-of-contents)**

## FAQ

- Why use the set function provided by the `useState` hook?

  - It ensures that React is aware of state changes and can properly manage the component's rendering lifecycle. When you use the set function, React knows that the state has changed and triggers a re-render of the component. This keeps the UI in sync with the state.

- Why should we use the callback function form of the set function when a state depends on a previous state?

  - We use the callback function form of the set function to ensure that state updates based on the current state receive the most recent value.
  - In React, state updates are asynchronous and can be batched for performance reasons.
  - When you call the setState function, React schedules an update rather than immediately applying the changes.

  **[⬆ back to top](#table-of-contents)**
