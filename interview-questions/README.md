# React Interview Questions

## Table of Contents

1. [Basic React Concepts](#basic-react-concepts)
1. [Advanced React Concepts](#advanced-react-concepts)
1. [Redux and State Management](#redux-and-state-management)
1. [Testing in React](#testing-in-react)
1. [Performance and Optimization](#performance-and-optimization)
1. [Ecosystem and Tooling](#ecosystem-and-tooling)
1. [Practical and Behavioral Questions](#practical-and-behavioral-questions)

## Basic React Concepts

1. **What is React and why is it used?**

   React is a JavaScript library developed by Meta for building user interfaces, primarily for single-page applications. It allows developers to create reusable UI components, which can manage their own state and render efficiently when data changes. React is used because it simplifies the process of building complex, interactive, and dynamic user interfaces by using a component-based architecture. Additionally, React's use of a virtual DOM improves performance by minimizing direct manipulation of the actual DOM, resulting in faster and more efficient updates.

2. **Explain the difference between a class component and a functional component.**

   A class component in React is a component defined using ES6 class syntax. It can hold and manage its own state and has access to lifecycle methods, like componentDidMount and componentDidUpdate. A functional component, on the other hand, is a simpler way to create components using plain JavaScript functions. Initially, functional components were stateless, but with the introduction of hooks like useState and useEffect in React 16.8, they can now manage state and side effects, making them as powerful as class components but with less boilerplate.

3. **What is JSX and why is it used in React?**

   JSX is a declarative syntax used in React to describe what the UI should look like. It allows developers to write HTML-like code within JavaScript, which React then transforms into React elements. It also allows for integration of JavaScript expressions, used for building dynamic user interfaces.

4. **How do you create a React component?**

   To create a React component, you can use either a function or a class.

   Functional Component:

   ```javascript
   function MyComponent() {
     return (
       <div>
         <h1>Hello, World!</h1>
       </div>
     );
   }
   ```

   Class Component:

   ```javascript
   import React, { Component } from "react";

   class MyComponent extends Component {
     render() {
       return (
         <div>
           <h1>Hello, World!</h1>
         </div>
       );
     }
   }

   export default MyComponent;
   ```

   Functional components are simpler and preferred for most cases, especially with the introduction of hooks, which allow them to manage state and side effects.

5. **What is the Virtual DOM and how does it work?**

   Virtual DOM is a representation of the real DOM elements generated by React components.

   When a component's state changes, React creates a new Virtual DOM tree and compares it with the previous one using a process called "reconciliation."

   You might wonder, "Why not update the entire DOM when state changes?" Updating the DOM is slow, and often only a small part needs to change. React's reconciliation process calculates the minimal changes needed to update the current DOM to match the new Virtual DOM, optimizing performance by reducing direct DOM manipulation.

6. **What are props in React? How are they different from state?**

   - State is internal data owned by the component. Props are external data owned by the parent component.
   - State can be updated by the component itself. Props are read-only. Props cannot be modified by the component receiving them.

7. **Explain state management in React. How do you update the state?**

   State management in React involves maintaining and updating the state of components to reflect changes in the UI. Each component can have its own state, which is an object that holds data that may change over time.

   To update the state, you use the setState method in the useState hook in functional components. This schedules an update to the component's state and trigger a re-render to reflect the changes in the UI.

8. **What are lifecycle methods in React? Name some of them.**
9. **What are hooks in React? Name some commonly used hooks.**

   Hooks in React are special functions that simplify component logic and make it easier to reuse stateful logic across components.

   Commonly used hooks include:

   - useState: Manages state in functional components.
   - useEffect: Handles side effects like data fetching, subscriptions, or manually changing the DOM.
   - useContext: Accesses context values without needing a context consumer.
   - useRef: Persists values between renders and can reference DOM elements.
   - useReducer: Manages complex state logic with a reducer function.
   - useMemo: Memoizes expensive calculations to optimize performance.
   - useCallback: Memoizes functions to prevent unnecessary re-creations during renders.

   Hooks enable more powerful and flexible functional components, improving code readability and reuse.

10. **What is the useEffect hook and how is it different from lifecycle methods in class components?**

    The `useEffect` hook in React allows you to perform side effects in functional components, such as data fetching. It runs after the render phase and can be controlled to run only when certain dependencies change.

    Difference from lifecycle methods:

    - In class components, you use lifecycle methods like `componentDidMount`, `componentDidUpdate`, and `componentWillUnmount` for handling side effects at different points of the component's life cycle.
    - `useEffect` combines all these into one function. You can mimic `componentDidMount` by providing an empty dependency array `[]`, and `componentDidUpdate` by specifying dependencies in the array. Cleanup logic can be handled inside the effect to mimic `componentWillUnmount`.

    Example:

    ```javascript
    useEffect(() => {
      // Side effect (e.g., data fetch)
      return () => {
        // Cleanup (e.g., unsubscribe)
      };
    }, [dependencies]);
    ```

    `useEffect` simplifies the way side effects are handled in functional components compared to lifecycle methods in class components.

**[⬆ back to top](#table-of-contents)**

## Advanced React Concepts

1. What are higher-order components (HOCs)? Give an example.
2. What is the context API and when would you use it?
3. Explain the concept of “lifting state up” in React.
4. What are React fragments and why are they used?
5. What is React.memo and when would you use it?
6. How does the useRef hook work? Give an example.
7. What are controlled and uncontrolled components in React?
8. Explain React portals and when you might use them.
9. What are render props and how are they different from HOCs?
10. What is code splitting and how does React support it?

**[⬆ back to top](#table-of-contents)**

## Redux and State Management

1. What is Redux and why is it used?
2. Explain the three core principles of Redux.
3. What are actions, reducers, and the store in Redux?
4. How do you connect a React component to a Redux store?
5. What is middleware in Redux? Give an example.
6. Explain the purpose of the Redux DevTools.
7. What is the difference between Redux and the Context API?
8. What is the useSelector and useDispatch hook in Redux?
9. Explain how you would handle asynchronous actions in Redux.
10. What are thunks in Redux?

**[⬆ back to top](#table-of-contents)**

## Testing in React

1. What tools do you use for testing React applications?
2. Explain the difference between unit tests, integration tests, and end-to-end tests.
3. How do you test a React component?
4. What is Jest and how is it used with React?
5. What is the purpose of Enzyme in React testing?
6. Explain the difference between shallow rendering and full rendering in Enzyme.
7. What is the React Testing Library and how does it differ from Enzyme?
8. How do you mock API calls in your tests?
9. Explain snapshot testing and its benefits.
10. How do you handle testing hooks in React?

**[⬆ back to top](#table-of-contents)**

## Performance and Optimization

1. What are some common performance issues in React applications?
2. How do you optimize the performance of a React application?
3. What is lazy loading and how do you implement it in React?
4. How does React’s reconciliation algorithm work?
5. What are PureComponents in React?
6. How do you prevent unnecessary re-renders in React?
7. What is the useMemo hook and how does it help with performance?
8. Explain the purpose of the shouldComponentUpdate lifecycle method.
9. How do you measure the performance of a React application?
10. What is code splitting and why is it important for performance?

**[⬆ back to top](#table-of-contents)**

## Ecosystem and Tooling

1. What build tools have you used with React?
2. How do you set up a new React project?
3. What is the purpose of webpack in a React application?
4. Explain the purpose of Babel in a React project.
5. What is Create React App and why would you use it?
6. How do you handle styling in React applications?
7. What are CSS-in-JS solutions and how do they compare to traditional CSS?
8. What is the purpose of a linter in a React project?
9. How do you handle environment variables in a React application?
10. What version control systems have you used?

**[⬆ back to top](#table-of-contents)**

## Practical and Behavioral Questions

1. Can you walk me through a recent project you worked on? What challenges did you face?
2. How do you approach debugging issues in a React application?
3. Explain a situation where you had to optimize a React application. What steps did you take?
4. How do you keep up-to-date with the latest developments in the React ecosystem?
5. Describe a time when you had to work with a difficult team member. How did you handle it?
6. How do you manage your time when working on multiple tasks or projects?
7. Can you explain a complex problem you solved in a previous project?
8. How do you ensure your code is maintainable and scalable?
9. What is your approach to writing documentation?
10. What do you enjoy most about working with React?

**[⬆ back to top](#table-of-contents)**
