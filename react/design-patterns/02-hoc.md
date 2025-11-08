## 🔊 HOC (Higher-Order Component) Pattern

- **Purpose:** Reuse component logic by wrapping components with extra functionality.
- **How it works:** A function takes a component as input and returns a new component that adds or modifies behaviour.
- **Result:** Shared logic in one place; wrapped components pick up the behaviour without modifying their internals.

### ⚖️ Pros & Cons

- ✅ Encapsulates reusable logic in one place.
- ✅ Keeps wrapped components focussed on presentation, not logic.
- ❌ Can result in many nested wrappers (wrapper hell) making component tree harder to reason about.
- ❌ Naming collisions: HOCs might pass props that conflict with existing props of wrapped component.
- ❌ With modern React (hooks, functional components) other patterns may be more ergonomic.

---

### 🧩 Example

```js
// Define a HOC
function withLoader(Element, url) {
  return (props) => {
    const [data, setData] = useState(null);

    useEffect(() => {
      fetch(url)
        .then((res) => res.json())
        .then((json) => setData(json));
    }, []);

    if (!data) {
      return <div>Loading…</div>;
    }
    return <Element {...props} data={data} />;
  };
}
```

```js
// Use the HOC
export default withLoader(
  DogImages,
  "https://dog.ceo/api/breed/labrador/images/random/6"
);
```
