## 📦 Presentational Container Pattern

- **Purpose:** Separate UI (how things look) from application logic/data (how things work).
- **How it works:** Presentational components receive data and callbacks via props, focus solely on rendering. Container components manage state, logic, data fetching and pass data down to presentational components.
- **Result:** More modular, reusable UI components; easier to test the view part; logic is isolated.

### ⚖️ Pros & Cons

- ✅ Clear separation of concerns: view vs logic.
- ✅ Presentational components are simpler, mostly stateless → easier to reuse and test.
- ✅ Team members (e.g., designers) can modify UI without touching logic parts.
- ❌ With modern React (hooks, functional components) the pattern may feel over-engineered for smaller apps.
- ❌ Requires managing two layers (container + presentational) which can add complexity.
- ❌ If containers become too large, they can still become difficult to maintain.

---

### 🧩 Example

```js
// Presentational component
function DogImages({ dogs }) {
  return dogs.map((dog, i) => <img src={dog} key={i} alt="Dog" />);
}
```

```js
// Container component
import React from "react";
import DogImages from "./DogImages";

class DogImagesContainer extends React.Component {
  state = { dogs: [] };

  componentDidMount() {
    fetch("https://dog.ceo/api/breed/labrador/images/random/6")
      .then((res) => res.json())
      .then(({ message }) => this.setState({ dogs: message }));
  }

  render() {
    return <DogImages dogs={this.state.dogs} />;
  }
}
```
