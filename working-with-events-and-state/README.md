# Working With Events and State

## Table of Contents

1. [State: A Component's Memory](#state-a-components-memory)
1. [Lifting State Up](#lifting-state-up)
1. [State vs. Props](#state-vs-props)
1. [Key Points](#key-points)
1. [Test Yourself](#test-yourself)
1. [Exercises](#exercises)

## State: A Component's Memory

Components often need to change what’s on the screen as a result of an interaction. Components update based on new data. In React, this kind of component-specific memory is called state.

To update a component with new data, two things need to happen:

1. Retain the data between renders.
1. Trigger React to render the component with new data (re-rendering).

The `useState` Hook provides those two things:

1. A state variable to retain the data between renders.
1. A state setter function to update the variable and trigger React to render the component again.

When you call `useState`, you are telling React that you want this component to remember something.

**[⬆ back to top](#table-of-contents)**

## Lifting State Up

Having multiple components depend on some shared piece of state is a scenario you will face frequently when working with React. This problem can be solved by _lifting state up._

Lifting state up in React means moving shared state to the closest common ancestor of components that need it. This ensures a single source of truth and allows components to stay in sync with each other.

**[⬆ back to top](#table-of-contents)**

## State vs. Props

- State is internal data owned by the component. Props are external data owned by the parent component.
- State can be updated by the component itself. Props are read-only. Props cannot be modified by the component receiving them.

**Note:** Whenever a piece of state is passed as a prop, when that state updates, both components are re-rendered - both the component owning the state
and the component receiving the state as a prop.

**[⬆ back to top](#table-of-contents)**

## Key Points

- Don’t set state manually (i.e. don’t use the variable directly to update itself), use the set function provided by the `useState` hook.
- Don’t set state in the render logic.
- Each component has and manages **its own state**, no matter how many times we render the same component on a screen. States are isolated inside of each instance of component.
- For data that should not trigger component re-renders, **don't use state.** Use a regular variable instead.
- Whenever a piece of state is passed as a prop, when that state updates, both components are re-rendered - both the component owning the state and the component receiving the state as a prop.
- _Lift the state up_ when multiple components need to share and synchronize state.

**[⬆ back to top](#table-of-contents)**

## Test Yourself

- Why use the set function provided by the `useState` hook?

  - Using the set function ensures that React is aware of state changes and can properly manage the component's rendering lifecycle. When you use the set function, React knows that the state has changed and triggers a re-render of the component. This keeps the UI in sync with the state.

- Why use the callback function form of the set function when a state depends on a previous state?

  - Using the callback function form ofw the set function ensures that state updates based on the current state receive the most recent value.
  - In React, state updates are asynchronous, which means when you call the set function, React schedules an update rather than immediately applying the changes.

**[⬆ back to top](#table-of-contents)**

## Exercises

**Exercise 1: Basic State Management**

**Objective**: Create a simple counter application.

**Instructions**:

1. Create a functional component with a button and a display for the count.
2. Use the `useState` hook to manage the count state.
3. Implement functionality to increment the count when the button is clicked.

**Expected Solution:**

```
import { `useState` } from "react";

export default function Home() {
  const [count, setCount] = `useState`(0);

  const handleStep = () => {
    setCount((c) => c + 1);
  };

  return (
    <div>
      <button onClick={handleStep}>Step</button>
      <p>Current step: {count}</p>
    </div>
  );
}
```

**Exercise 2: Managing Complex State**

**Objective**: Create a form with multiple inputs and manage their state.

**Instructions**:

1. Create a form with inputs for name and email.
2. Use the `useState` hook to manage the state of the form inputs.
3. Display the current state of the form inputs below the form.

**Expected Solution:**

```
import { `useState` } from "react";

export default function Form() {
  const [formData, setFormData] = `useState`({ name: "", email: "" });

  const handleChange = (event) => {
    const { name, value } = event.target;
    setFormData((prevData) => ({ ...prevData, [name]: value }));
  };

  return (
    <div>
      <form>
        <div>
          <div>
            <label>
              Name:
              <input
                type="text"
                name="name"
                value={formData.name}
                onChange={handleChange}
              />
            </label>
          </div>
          <div>
            <label>
              Email:
              <input
                type="text"
                name="email"
                value={formData.email}
                onChange={handleChange}
              />
            </label>
          </div>
        </div>
      </form>
      <p>Current User: {JSON.stringify(formData)}</p>
    </div>
  );
}
```

**[⬆ back to top](#table-of-contents)**
