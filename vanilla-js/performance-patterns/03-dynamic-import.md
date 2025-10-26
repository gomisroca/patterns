## 🧨 Dynamic Import

- **Purpose:** Load modules on demand instead of bundling them into the initial download.
- **How it works:** Use `import()` to dynamically import a module only when it’s needed.
- **Result:** Smaller initial bundle size, improved initial loading/performance, and better user experience.

### 🌐 In JavaScript / React

- Use `const LazyComp = React.lazy(() => import('./MyComp')).`
- Wrap the lazy component in `<React.Suspense fallback={...}>` so you handle loading state.

### ⚖️ Pros & Cons

- ✅ Smaller initial download → faster page load / perceived performance.
- ✅ You avoid loading code that the user may never use.
- ✅ Works well for features toggled after initial render (like modals, optional widgets).
- ❌ Delay when the user triggers the feature (because module has to download).
- ❌ Over-splitting everything can increase complexity (many small chunks, many network requests).
- ❌ Must manage fallback UI/loading state (via Suspense or similar).
- ❌ If the module is very likely to be used, maybe it makes sense to import it statically.

---

### 🧩 Example

```js
import React, { Suspense, lazy } from "react";

const Send = lazy(() => import("./icons/Send"));
const Emoji = lazy(() => import("./icons/Emoji"));
const Picker = lazy(() => import("./EmojiPicker"));

const ChatInput = () => {
  const [pickerOpen, togglePicker] = React.useReducer((state) => !state, false);

  return (
    <Suspense fallback={<p id="loading">Loading...</p>}>
      <div className="chat-input-container">
        <input type="text" placeholder="Type a message..." />
        <Emoji onClick={togglePicker} />
        {pickerOpen && <Picker />}
        <Send />
      </div>
    </Suspense>
  );
};

console.log("ChatInput loaded", Date.now());

export default ChatInput;
```
