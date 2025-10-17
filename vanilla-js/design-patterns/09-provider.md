## 🎁 Provider Pattern

- **Purpose:** Share data or state across component trees without prop drilling.
- **How it works:** A Provider component supplies data to all nested consumers.
- **Result:** Any component under the Provider can access shared context data.

### ⚡ In JavaScript / 🌐 React

- Create context with `createContext()`.
- The **Provider** makes data available via a `value` prop.
- The **Consumer** (or `useContext()`) reads the nearest Provider’s value.

---

### 🧩 Example

```js
import React from "react";

const DataContext = React.createContext();

function App() {
  const data = {
    listItem: "Task 1",
    text: "Hello Context!",
    title: "Dashboard",
  };

  return (
    <DataContext.Provider value={data}>
      <SideBar />
      <Content />
    </DataContext.Provider>
  );
}

function SideBar() {
  return <List />;
}

function List() {
  return <ListItem />;
}

function ListItem() {
  const data = React.useContext(DataContext);
  return <span>{data.listItem}</span>;
}

function Content() {
  return (
    <div>
      <Header />
      <Text />
    </div>
  );
}

function Header() {
  const data = React.useContext(DataContext);
  return <h1>{data.title}</h1>;
}

function Text() {
  const data = React.useContext(DataContext);
  return <p>{data.text}</p>;
}
```
