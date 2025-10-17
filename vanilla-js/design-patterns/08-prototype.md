## 🤖 Prototype Pattern

- **Purpose:** Reuse behavior by delegating to a shared prototype object.
- **How it works:** Objects inherit from a prototype, forming a prototype chain.
- **Result:** Methods are shared; each instance doesn’t duplicate them.

### ⚡ In JavaScript

- JS uses **prototypal inheritance**, not classical inheritance.
- All class methods are stored on the prototype.
- Access via `<Constructor>.prototype` or `Object.getPrototypeOf(obj)`.
- Every prototype has its own prototype (the **prototype chain**) until reaching `Object.prototype`.

---

### 🧩 Example

```js
class Dog {
  constructor(name) {
    this.name = name;
  }

  bark() {
    console.log("Woof!");
  }
}

class SuperDog extends Dog {
  fly() {
    console.log("Flying!");
  }
}

const dog1 = new SuperDog("Daisy");

dog1.bark(); // From Dog prototype
dog1.fly(); // From SuperDog prototype

console.log(Object.getPrototypeOf(dog1) === SuperDog.prototype); // true
console.log(Object.getPrototypeOf(SuperDog.prototype) === Dog.prototype); // true
```

#### 🧠 Prototype Chain

`dog1 → SuperDog.prototype → Dog.prototype → Object.prototype → null`
