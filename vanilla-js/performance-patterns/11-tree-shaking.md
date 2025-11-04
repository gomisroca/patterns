## 🌲 Tree Shaking

- **Purpose:** Remove unused (dead) code from your JavaScript bundle so you ship less to the browser.
- **How it works:** Using ES 2015+ module syntax (import/export), the bundler analyzes which parts of your code are actually referenced and marks others as removable.
- **Result:** Smaller bundle size → faster downloads, less parsing/compiling, improved performance.

### ⚖️ Pros & Cons

- ✅ Reduces bundle size by removing code you don’t use.
- ✅ Improves network performance (smaller downloads), parsing and execution overhead.
- ✅ Especially useful for large libraries or modules where you only use a part.
- ❌ Not effective if modules aren’t authored in a tree-shakable way (e.g., default exports that include many properties, side-effects heavy modules).
- ❌ If bundler/transpiler converts ESM to CommonJS or mixes module types, tree-shaking may fail.
- ❌ Requires correct configuration (sideEffects, module syntax) and awareness of library packaging.
- ❌ Doesn’t help if you import whole modules unnecessarily — you still need to only import what you need.

---

### 🧩 Example

```js
// utilities.js
export function read(props) {
  return props.book;
}

export function nap(props) {
  return props.winks;
}
```

```js
// index.js
import { read } from "./utilities";

eventHandler = (e) => {
  read({ book: e.target.value });
};
```
