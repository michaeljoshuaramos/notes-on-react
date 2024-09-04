# React Testing: Unit Testing With Vitest and End-to-end Testing With Playwright

## Table of Contents

1. [Testing Functions](#testing-functions)
1. [Testing Components](#testing-components)
1. [Testing useState Hook](#testing-usestate-hook)
1. [Testing useEffect Hook With API Calls](#testing-useeffect-hook-with-api-calls)

## Testing Functions

utils.js

```javascript
export const range = (start, end) => {
  return [...Array(end - start).keys()].map((el) => el + start);
};
```

utils.test.js

```javascript
import { describe, expect, it } from "vitest";
import { range } from "./utils";

describe("utils", () => {
  describe("range", () => {
    it("returns correct result from 1-6 range", () => {
      const result = range(1, 6);
      expect(result).toEqual([1, 2, 3, 4, 5]);
    });
    it("returns correct result from 41-45 range", () => {
      const result = range(41, 45);
      expect(result).toEqual([41, 42, 43, 44]);
    });
  });
});
```

**[⬆ back to top](#table-of-contents)**

## Testing Components

ErrorMessage.jsx

```javascript
import React from "react";

const ErrorMessage = ({ message = "Something went wrong" }) => {
  return <div data-testid="message-container">{message}</div>;
};

export default ErrorMessage;
```

ErrorMessage.test.jsx

```javascript
import { render, screen } from "@testing-library/react";
import { describe, expect, it } from "vitest";
import ErrorMessage from "./ErrorMessage";

describe("ErrorMessage", () => {
  it("render default error state", () => {
    render(<ErrorMessage />);
    expect(screen.getByTestId("message-container")).toHaveTextContent(
      "Something went wrong"
    );
  });
  it("render custom error state", () => {
    render(<ErrorMessage message="Email is already taken" />);
    expect(screen.getByTestId("message-container")).toHaveTextContent(
      "Email is already taken"
    );
  });
});
```

**[⬆ back to top](#table-of-contents)**

## Testing `useEffect` Hook With API Calls

Avoid executing real API calls inside your tests because:

1. **Unreliable Tests**: Network issues or server downtime can cause tests to fail unpredictably, even if the code is correct.
2. **Speed**: Real API calls slow down tests, making the test suite longer to run.
3. **Cost**: Making repeated API calls during testing can consume resources or incur costs, especially with rate-limited or paid APIs.
4. **Side Effects**: Real API calls can alter data on the server, leading to inconsistent test results and potential data corruption.
5. **Isolation**: Tests should focus on the component’s behavior, not the external system's reliability, ensuring that failures are related to code changes, not external factors.

Instead, mocking API calls in tests allows you to control the environment, making tests faster, more reliable, and cost-effective. [^1]

### Mocking API Calls

[React Testing Library](https://testing-library.com/docs/react-testing-library/example-intro#mock) recommends using the [Mock Service Worker (MSW)](https://github.com/mswjs/msw) library to declaratively mock API communication in your tests.

Tags.jsx

```javascript
import axios from "axios";
import { useEffect, useState } from "react";

const Tags = () => {
  const [tags, setTags] = useState([]);
  console.log("tags", tags);
  useEffect(() => {
    console.log("useEffect");
    axios.get("http://localhost:3004/tags").then((response) => {
      console.log("response", response.data);
      setTags(response.data);
    });
  }, []);

  return (
    <>
      {tags.map((tag) => (
        <div key={tag.id} data-testid="tag">
          {tag.name}
        </div>
      ))}
    </>
  );
};

export default Tags;
```

Tags.test.jsx

```javascript
import { render, screen } from "@testing-library/react";
import { http, HttpResponse } from "msw";
import { setupServer } from "msw/node";
import { afterEach, beforeAll, describe, expect, it } from "vitest";
import Tags from "./Tags";

describe("Tags", () => {
  const server = setupServer(
    http.get("http://localhost:3004/tags", () => {
      return HttpResponse.json([{ id: "1", name: "bar" }]);
    })
  );

  beforeAll(() => server.listen());
  afterEach(() => server.resetHandlers());
  afterAll(() => server.close());

  it("renders tags", async () => {
    render(<Tags />);
    const tags = await screen.findAllByTestId("tag");
    expect(tags).toHaveLength(1);
  });
});
```

### The Approach

1. Simulate API Calls with MSW:
   - **MSW (Mock Service Worker)** is used to mock the network requests that `axios` makes in the `useEffect`. This allows you to simulate the API response without making actual network requests.
2. Setup the Mock Server:
   - `setupServer()` creates a mock server that intercepts the `axios.get` request to `http://localhost:3004/tags`.
   - The server is configured to return a predefined JSON response (`[{ id: "1", name: "bar" }]`), simulating what the real API would return.
3. Manage the Server Lifecycle:
   - `beforeAll()` starts the server before any tests run, ensuring it intercepts network requests during testing.
   - `afterEach()` resets any request handlers that may have been modified during individual tests, keeping tests isolated and repeatable.
   - `afterAll()` stops the server after all tests complete, cleaning up resources.
4. Test the Component Behavior:
   - **Render the Component**: The `Tags` component is rendered as usual.
   - **Await and Assert**: `screen.findAllByTestId("tag")` is used to find all elements with the `data-testid="tag"` attribute. Since `findAllByTestId` waits for the elements to appear asynchronously, it aligns with the async nature of the API call in `useEffect`.
   - **Assertion**: The test checks that exactly one tag is rendered (`expect(tags).toHaveLength(1)`), which corresponds to the mock response.

**[⬆ back to top](#table-of-contents)**

[^1]: Oleksandr Kocherhin, "React Testing: Unit Testing React and E2E Testing," Udemy, [https://www.udemy.com/course/react-testing-unit-testing-react-and-e2e-testing/](https://www.udemy.com/course/react-testing-unit-testing-react-and-e2e-testing/).
