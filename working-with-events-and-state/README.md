# Working With Events and State

## Table of Contents

1. [Key Points](#key-points)
1. [Knowledge Questions](#knowledge-questions)
1. [Exercises](#exercises)

## Key Points

- Don’t set state manually (i.e. don’t use the variable directly to update itself), use the set function provided by the `useState` hook.
- Don’t set state in the render logic.

**[⬆ back to top](#table-of-contents)**

## Knowledge Questions

- Why use the set function provided by the `useState` hook?

  - Using the set function ensures that React is aware of state changes and can properly manage the component's rendering lifecycle. When you use the set function, React knows that the state has changed and triggers a re-render of the component. This keeps the UI in sync with the state.

- Why use the callback function form of the set function when a state depends on a previous state?

  - Using the callback function form of the set function ensures that state updates based on the current state receive the most recent value.
  - In React, state updates are asynchronous and can be batched for performance reasons.
  - When you call the setState function, React schedules an update rather than immediately applying the changes.

**[⬆ back to top](#table-of-contents)**

## Exercises

**Exercise 1: Basic State Management**

**Objective**: Create a simple counter application.

**Instructions**:

1. Create a functional component with a button and a display for the count.
2. Use the useState hook to manage the count state.
3. Implement functionality to increment the count when the button is clicked.

**Expected Solution:**

```
import { useState } from "react";

export default function Home() {
  const [count, setCount] = useState(0);

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
2. Use the useState hook to manage the state of the form inputs.
3. Display the current state of the form inputs below the form.

**Expected Solution:**

```
import { useState } from "react";

export default function Form() {
  const [formData, setFormData] = useState({ name: "", email: "" });

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
