## 💽 React Server Components

- **Purpose:** Execute parts of a React component tree on the server so those components' code doesn't get included in the client-side bundle—reducing client-bundle size and improving performance.
- **How it works:** Mark a component (or file) as a server component, run it on the server, and combine its output with client components. The client only receives the parts that need interactivity.
- **Result:** Smaller JavaScript on the client, potentially faster load/interactivity, better scalability for large React apps.

### ⚖️ Pros & Cons

- ✅ Reduces client-side JavaScript bundle size (because server components code isn’t sent to the client).
- ✅ Enables access to server-only resources directly inside components.
- ✅ Combines benefits of server-rendered logic + interactive client UI.
- ❌ Complexity: you need toolchain/framework support (bundlers, routing) to separate server vs client components.
- ❌ Still evolving: not fully stable in all environments yet. Patterns.dev notes this is “worth keeping on your radar”.
- ❌ Some limitations: server components cannot have client-side hooks/state; mixing must be done carefully.
- ❌ Might require changes in how your app is structured (file naming, component boundaries, data-fetching strategy).

---

### 🧩 Example

```js
// MyComponent.server.js   (Server Component)
import { fetchData } from "./data";
export default async function MyComponent({ id }) {
  const data = await fetchData(id);
  return (
    <div>
      <h1>{data.title}</h1>
      <InteractivePart clientId={id} />
    </div>
  );
}

// InteractivePart.client.js   (Client Component)
"use client";
import { useState } from "react";
export default function InteractivePart({ clientId }) {
  const [count, setCount] = useState(0);
  return (
    <button onClick={() => setCount(c => c + 1)}>
      Count for {clientId}: {count}
    </button>
  );
}

```

- `MyComponent.server.js` fetches data server-side and returns markup (or JSX that gets converted) without sending the fetch logic to the client.

- `InteractivePart.client.js` runs in the browser; it includes interactivity.

- The result: only the interactive part is shipped to the client; the rest stays on the server, reducing bundle size.
