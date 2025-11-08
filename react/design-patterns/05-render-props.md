## 🖼️ Render Props Pattern

- **Purpose:** Enable component logic reuse by passing a function prop that controls what gets rendered.
- **How it works:** A component takes a prop (often named `render`, or even uses its `children` as a function) which is a function returning JSX. That component calls this function instead of rendering fixed UI.
- **Result:** You decouple component logic from rendering, making the logic reusable across different UIs without rewriting it.

### ⚖️ Pros & Cons

- ✅ Logic and data fetching/handling lives in one place, but UI rendering is flexible.
- ✅ Avoids prop‐collision problems common in HOCs (since you explicitly pass what you render).
- ❌ Can lead to “wrapper hell” if many nested render props are used (lots of nesting).
- ❌ With many render functions created inline, performance might suffer (new functions each render).
- ❌ In modern React, many of the use‐cases for render props are now often solved by custom hooks.

---

### 🧩 Example

```js
function Input(props) {
  const [value, setValue] = useState("");
  return (
    <>
      <input
        type="text"
        value={value}
        onChange={(e) => setValue(e.target.value)}
        placeholder="Temp in °C"
      />
      {props.render(value)}
    </>
  );
}

function Kelvin({ value }) {
  return <div>{value + 273.15}K</div>;
}
function Fahrenheit({ value }) {
  return <div>{(value * 9) / 5 + 32}°F</div>;
}

export default function App() {
  return (
    <div className="App">
      <h1>☃️ Temperature Converter 🌞</h1>
      <Input
        render={(value) => (
          <>
            <Kelvin value={parseFloat(value || 0)} />
            <Fahrenheit value={parseFloat(value || 0)} />
          </>
        )}
      />
    </div>
  );
}
```
