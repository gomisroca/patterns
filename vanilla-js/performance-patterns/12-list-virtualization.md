## 📺 List Virtualization

- **Purpose:** Efficiently render very large lists by only rendering the items that are visible in the viewport (plus a buffer), instead of all items at once.
- **How it works:** Maintain a “window” of visible items based on scroll position. Use a container for scrolling, a large element representing full size, and absolutely position only the visible children.
- **Result:** Much better scroll and render performance, especially on low-end devices or when lists are thousands of items long.

### ⚖️ Pros & Cons

- ✅ Greatly improves rendering & scrolling performance for long lists.
- ✅ Reduces number of DOM nodes, memory usage, layout cost.
- ✅ More performant on slower devices / large lists.
- ❌ Implementation more complex than simple list rendering.
- ❌ Item sizes variable → harder to compute positions.
- ❌ Overscanning (rendering slightly more than visible) needed to avoid blanks when scrolling fast.
- ❌ If list is small or items are heavy/complex, virtualization might not help (or even hurt).

---

### 🧩 Example

```js
import React from "react";
import { FixedSizeList as List } from "react-window";

const items = [
  /* large array of items */
];

const Row = ({ index, style }) => <div style={style}>{items[index].name}</div>;

function App() {
  return (
    <List
      height={400}
      width={300}
      itemCount={items.length}
      itemSize={35} // each row 35px tall
    >
      {Row}
    </List>
  );
}
```
