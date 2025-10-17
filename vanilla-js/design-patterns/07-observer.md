## 👁️ Observer Pattern

- **Purpose:** Subscribe an object to another.
- **How it works:** An observable object sends notifications to other objects that are interested in its state.
- **Result:** Observers can react to changes in the observable object.

### ⚡ In JavaScript

An observable obj usually has 3 parts:

- observers: array of objs interested in the observable obj
- subscribe()/unsubscribe(): add/remove observers
- notify(): notify all observers on specific event

---

### 🧩 Example 1 - Conceptual

```js
class Observable {
  constructor() {
    this.observers = [];
  }

  subscribe(observer) {
    this.observers.push(observer);
  }

  unsubscribe(observer) {
    this.observers = this.observers.filter((o) => o !== observer);
  }

  notify(event) {
    this.observers.forEach((observer) => observer(event));
  }
}
```

### 🧩 Example 2 - React User Interaction

In this example, we have `logger` and `toastify` functions that subscribe to the observable object. When the observable object notifies, the logger function logs the data to the console and the toastify function displays a toast notification.

```js
import React from "react";
import { Button, Switch, FormControlLabel } from "@material-ui/core";
import { ToastContainer, toast } from "react-toastify";
import observable from "./Observable";

function handleClick() {
  observable.notify("User clicked button!");
}

function handleToggle() {
  observable.notify("User toggled switch!");
}

function logger(data) {
  console.log(`${Date.now()} ${data}`);
}

function toastify(data) {
  toast(data, {
    position: toast.POSITION.BOTTOM_RIGHT,
    closeButton: false,
    autoClose: 2000,
  });
}

observable.subscribe(logger);
observable.subscribe(toastify);

export default function App() {
  return (
    <div className="App">
      <Button variant="contained" onClick={handleClick}>
        Click me!
      </Button>
      <FormControlLabel
        control={<Switch name="" onChange={handleToggle} />}
        label="Toggle me!"
      />
      <ToastContainer />
    </div>
  );
}
```
