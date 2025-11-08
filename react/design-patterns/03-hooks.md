## 🪝 Hooks Pattern

- **Purpose:** Share stateful logic among multiple components without using classes or complex wrapper patterns.
- **How it works:** Use built-in hooks (like `useState`, `useEffect`, `useContext`) and/or custom hooks (functions prefixed with use…) to extract reusable logic.
- **Result:** Functional components become simpler, logic is more modular and re-usable, and you avoid “wrapper hell” many HOCs/Render Props patterns caused.

### ⚖️ Pros & Cons

- ✅ Less boilerplate than class components (no constructor, no `this`, no binding).
- ✅ Logic can be split into small reusable hooks → better modularity and testability.
- ✅ Avoids complex patterns like heavy HOC composition or render-props wrappers.
- ❌ Rules of hooks must be followed (e.g., only call hooks at top level, not inside loops/conditions) — breaking them leads to bugs.
- ❌ Custom hooks can still become complex; logic may become hard to trace if overused.
- ❌ Some patterns (legacy code, class-based libraries) may still require HOCs or other approaches.

---

### 🧩 Example

```js
// Built-in hooks
const [value, setValue] = useState(initial);
useEffect(() => {
  // side-effect logic here
}, [dependencies]);
```

```js
// Custom hooks
function useKeyPress(targetKey) {
  const [pressed, setPressed] = useState(false);
  useEffect(() => {
    function down({ key }) {
      if (key === targetKey) setPressed(true);
    }
    function up({ key }) {
      if (key === targetKey) setPressed(false);
    }
    window.addEventListener("keydown", down);
    window.addEventListener("keyup", up);
    return () => {
      window.removeEventListener("keydown", down);
      window.removeEventListener("keyup", up);
    };
  }, []);
  return pressed;
}
```
