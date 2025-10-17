## 🖇️ Proxy Pattern

- **Purpose:** Add control, validation, or extra behavior when accessing or modifying an object.
- **How it works:** Instead of interacting with an object directly, use a _proxy_ that intercepts operations.
- **Result:** You can run custom logic on reads/writes without modifying the original object.

### ⚡ In JavaScript

- Create a proxy with `new Proxy(target, handler)`.
- The **handler** defines "traps" like `get()` and `set()` that intercept property access or assignment.
- The **Reflect** API is used to safely forward operations to the original object.

---

### 🧠 Common Use Cases

- Access control
- Validation
- Logging / debugging
- Caching or lazy initialization

---

### 🧩 Example

```js
const person = {
  name: "John Doe",
  age: 42,
  nationality: "American",
};

const personProxy = new Proxy(person, {
  get: (obj, prop) => {
    console.log(`The value of ${prop} is ${Reflect.get(obj, prop)}`);
  },
  set: (obj, prop, value) => {
    console.log(`Changed ${prop} from ${obj[prop]} to ${value}`);
    Reflect.set(obj, prop, value);
  },
});

personProxy.name; // Logs: "The value of name is John Doe"
personProxy.age = 43; // Logs: "Changed age from 42 to 43"
```
