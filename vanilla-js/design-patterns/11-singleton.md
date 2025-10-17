## 🐪 Singleton Pattern

- **Purpose:** Ensure only one instance of a class exists and provide a global point of access to it.
- **How it works:** Controls object instantiation by storing and returning a single shared instance.
- **Result:** A single source of truth for state or configuration across the app.

### ⚡ In JavaScript

- Use a static property or closure to store the single instance.
- Optionally use `Object.freeze()` to prevent modification.

---

### 🧠 Common Use Cases

- Global app configuration
- Database connections
- Logging utilities
- Shared cache or API client

---

### 🧩 Example

```js
let instance;
let counter = 0;

class Counter {
  constructor() {
    if (instance) {
      throw new Error("You can only create one instance!");
    }
    instance = this;
  }

  getInstance() {
    return this;
  }

  getCount() {
    return counter;
  }

  increment() {
    return ++counter;
  }

  decrement() {
    return --counter;
  }
}

const singletonCounter = class Counter {
  constructor() {
    if (Counter.instance) {
      return Counter.instance;
    }
    this.count = 0;
    Counter.instance = this;
    Object.freeze(this);
  }

  increment() {
    return ++this.count;
  }

  decrement() {
    return --this.count;
  }

  getCount() {
    return this.count;
  }
};

// Usage
const counter1 = Object.freeze(new Counter());
const counter2 = Object.freeze(new Counter());

counter1.increment();
console.log(counter2.getCount()); // 1 (same instance!)

export default singletonCounter;
```
