## 🧋 Mixin Pattern

- **Purpose:** Add reusable functionality to another class/object.
- **How it works:** We assign a mixin to a class/object, or to another mixin.
- **Result:** New instances of the class/object will have the mixin's functionality.

### ⚡ In JavaScript

- Can be implemented with Object.assign()

---

### 🧩 Example

```js
// We have a class called Dog
class Dog {
  constructor(name) {
    this.name = name;
  }
}

// `animalFunctionality` is a mixin
const animalFunctionality = {
  walk: () => console.log("Walking!"),
  sleep: () => console.log("Sleeping!"),
};

// `dogFunctionality` is a mixin too
const dogFunctionality = {
  bark: () => console.log("Woof!"),
  wagTail: () => console.log("Wagging my tail!"),
  play: () => console.log("Playing!"),
  walk() {
    super.walk();
  },
  sleep() {
    super.sleep();
  },
};

// We ass the animalFunctionality to the dogFunctionality mixin
Object.assign(dogFunctionality, animalFunctionality);
// And then the dogFunctionality to the Dog class
Object.assign(Dog.prototype, dogFunctionality);

const dog = new Dog("Fido");

// The instance has the mixin's functionality
dog.name; // Fido
dog.bark(); // Woof!
dog.wagTail(); // Wagging my tail!
pet1.walk(); // Walking!
pet1.sleep(); // Sleeping!
```
