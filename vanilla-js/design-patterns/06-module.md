## 🪫 Module Pattern

- **Purpose:** Encapsulate code into smaller, reusable pieces.
- **How it works:** Export code from a module file.
- **Result:** Modular code that can be reused. Private code can't be accessed outside of the module.

### ⚡ In JavaScript

- ES2015 introduced built-in JS modules.
- `export` is used to export code from a module.

---

### 🧩 Example

Create a module file called `math.js` with the following code:

```js
// Not exported, can't use it outside of the module
const privateValue = "This is a value private to the module!";

export function add(x, y) {
  return x + y;
}

export function multiply(x) {
  return x * 2;
}

export function subtract(x, y) {
  return x - y;
}

export function square(x) {
  return x * x;
}
```

Then import the functions in another file:

```js
import { add, multiply, subtract, square } from "./math.js";

subtract(10, 3);
square(3);

console.log(privateValue);
/* Error: privateValue is not defined (we don't export it) */
```
