# React Testing: Unit Testing and End-to-end Testing

## Table of Contents

1. [Key Points](#key-points)

## Key Points

## Testing `useEffect` With API Calls

Avoid executing real API calls inside your tests because:

1. **Unreliable Tests**: Network issues or server downtime can cause tests to fail unpredictably, even if the code is correct.
2. **Speed**: Real API calls slow down tests, making the test suite longer to run.
3. **Cost**: Making repeated API calls during testing can consume resources or incur costs, especially with rate-limited or paid APIs.
4. **Side Effects**: Real API calls can alter data on the server, leading to inconsistent test results and potential data corruption.
5. **Isolation**: Tests should focus on the component’s behavior, not the external system's reliability, ensuring that failures are related to code changes, not external factors.

Instead, mocking API calls in tests allows you to control the environment, making tests faster, more reliable, and cost-effective.

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

**[⬆ back to top](#table-of-contents)**
