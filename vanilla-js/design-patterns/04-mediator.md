## 🧭 Mediator Pattern

- **Purpose:** Centralize communication between components to reduce direct dependencies.
- **How it works:** Components send messages or events to a **Mediator**, not directly to each other.
- **Mediator:** Receives, routes, or transforms communication.
- **Result:** Decoupled, modular system where components don’t need to know each other.

### ⚡ In JavaScript

- Can be implemented using an **object literal** or **function** acting as a hub.
- Common in frameworks or event-driven systems (e.g., Node.js `EventEmitter`).

---

### 🧩 Example 1 — Conceptual

```js
class Mediator {
  constructor() {
    this.channels = {};
  }

  subscribe(channel, fn) {
    if (!this.channels[channel]) this.channels[channel] = [];
    this.channels[channel].push(fn);
  }

  publish(channel, data) {
    (this.channels[channel] || []).forEach((fn) => fn(data));
  }
}

const mediator = new Mediator();

mediator.subscribe("userLoggedIn", (user) => console.log(`Welcome ${user}`));
mediator.publish("userLoggedIn", "Alice");
```

---

### 🧩 Example 2 — Express Analogy

In Express, middleware acts like a mediator.

```js
app.use("/", (req, res, next) => {
  req.headers["test-header"] = 1234;
  next();
});

app.use("/", (req, res, next) => {
  console.log(`Request has test header: ${!!req.headers["test-header"]}`);
  next();
});
```
