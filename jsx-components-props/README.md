# JSX, Components, and Props

## Table of Contents

1. [JSX](#jsx)
1. [Components](#components)
1. [Props](#Props)

## JSX

JSX is a declarative syntax used in React to describe what the UI should look like. It allows developers to write HTML-like code within JavaScript, which React then transforms into React elements. It also allows for integration of JavaScript expressions, used for building dynamic user interfaces.

Here's a succinct example of JSX in React:

```jsx
import React, { useState } from "react";

function Greeting() {
  const [name, setName] = useState("");

  return (
    <div>
      <h1>Hello, {name || "Stranger"}!</h1>
      <input
        type="text"
        placeholder="Enter your name"
        value={name}
        onChange={(e) => setName(e.target.value)}
      />
    </div>
  );
}

export default Greeting;
```

This simple JSX component renders a greeting that updates as the user types a name.
