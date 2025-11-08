## 👝 Compound Pattern

- **Purpose:** Enable a set of related components to work together under a shared state or API, while providing a clean and flexible public interface.
- **How it works:** A parent component provides shared state (via context or props) and exposes child components as its properties (e.g., Parent.Toggle, Parent.List). Consumers import only the parent and use the children in composition.
- **Result:** Clean API, decoupled internals, easier component library development — you avoid prop-drilling and keep logic encapsulated.

### ⚖️ Pros & Cons

- ✅ Encapsulates state and logic inside the parent; consumer only composes.
- ✅ Cleaner public API: you import one component and use its children, rather than importing many separate pieces.
- ❌ If implemented via children cloning (React.cloneElement) then the children must be direct descendants (no wrapper elements) which limits composability.
- ❌ Prop name collisions: when cloning elements, existing props may get overwritten inadvertently.

---

### 🧩 Example

```js
// FlyOut.js
const FlyOutContext = createContext();

function FlyOut({ children }) {
  const [open, setOpen] = useState(false);
  const toggle = () => setOpen((o) => !o);

  return (
    <FlyOutContext.Provider value={{ open, toggle }}>
      {children}
    </FlyOutContext.Provider>
  );
}

function Toggle() {
  const { toggle } = useContext(FlyOutContext);
  return <button onClick={toggle}>Toggle Menu</button>;
}

function List({ children }) {
  const { open } = useContext(FlyOutContext);
  return open ? <ul>{children}</ul> : null;
}

function Item({ children }) {
  return <li>{children}</li>;
}

FlyOut.Toggle = Toggle;
FlyOut.List = List;
FlyOut.Item = Item;

export { FlyOut };
```

```js
// Usage
import { FlyOut } from "./FlyOut";

function Menu() {
  return (
    <FlyOut>
      <FlyOut.Toggle />
      <FlyOut.List>
        <FlyOut.Item>Edit</FlyOut.Item>
        <FlyOut.Item>Delete</FlyOut.Item>
      </FlyOut.List>
    </FlyOut>
  );
}
```
