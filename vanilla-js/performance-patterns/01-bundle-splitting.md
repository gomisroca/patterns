## 📦 Bundle Splitting

- **Purpose:** Break a large JavaScript bundle into smaller, more manageable pieces to improve loading and execution performance.
- **How it works:** Instead of shipping one giant bundle with all code, you split the bundle into multiple smaller chunks (e.g., by feature, library, route). The browser loads only what’s needed initially.
- **Result:** Reduced initial load time, better perceived performance (First Contentful Paint, Largest Contentful Paint), and greater efficiency for users on slower devices or networks.

### ⚖️ Pros & Cons

- ✅ Smaller initial JS download → faster load & start.
- ✅ Less work for JS engine (parse/compile) for unused code.
- ✅ Better user-experience for slower networks/devices.
- ❌ Complexity: build config, chunk naming, caching, dependency graphs.
- ❌ Over-splitting can cause fragmentation, many small files, loading overhead.
- ❌ Need to manage when and how chunks are loaded (e.g., interactions, routes).

### 🧩 Example

```js
// main entry
import React from "react";
import App from "./App";

// large component used only on a specific feature
const ChatModule = React.lazy(() => import("./ChatModule"));

// Vendor libraries might go into a separate bundle by the bundler
```

At build time the bundler might produce:

- vendors.bundle.js (React, ReactDOM, etc.)
- main.bundle.js (foundation/app code)
- chat.bundle.js (only loaded when ChatModule is used)

Result: Initial load downloads vendors.bundle.js + main.bundle.js, deferring chat.bundle.js until needed.
