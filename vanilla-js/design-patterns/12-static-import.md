## 🗿 Static Import Pattern

- **Purpose:** Load all required modules at build time.
- **How it works:** `import X from '...'` is resolved statically at compile time and included in the main bundle.
- **Result:** Simpler dependency graph, but larger initial bundle (slower first load).

### ⚖️ Pros & Cons

- ✅ Predictable dependencies
- ✅ Ideal for essential, always-needed modules
- ❌ Increases initial bundle size
- ❌ Loads code even if it’s not immediately used

---

### 🧩 Example

```js
import React from "react";
import UserInfo from "./components/UserInfo";
import ChatList from "./components/ChatList";
import ChatInput from "./components/ChatInput";
import "./styles.css";

console.log("App loading", Date.now());

const App = () => (
  <div className="App">
    <UserInfo />
    <ChatList />
    <ChatInput />
  </div>
);

export default App;
```
