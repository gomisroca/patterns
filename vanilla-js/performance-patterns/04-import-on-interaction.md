## 🎭 Import on Interaction

- **Purpose:** Lazy-load non-critical resources when a user interacts with UI requiring them.
- **How it works:** Instead of loading code eagerly on initial page load, the module or script is fetched when a user action triggers it.
- **Result:** Faster initial page load, reduced blocking of main thread, improved responsiveness by delaying rarely used code.

### 🗝️ Key Concepts

- Use placeholders to represent non-critical resources until they're loaded.
- Applies for features not needed on initial render.
- Loading strategies:
  - Eager: load resource right away.
  - Lazy (route-based): load resource when user navigates to route.
  - Lazy (interaction-based): load resource when user interacts with UI.
  - Lazy (viewport-based): load resource when user scrolls to it.
  - Prefetch: load prior to need, but after critical resources are loaded.
  - Preload: load eagerly, greater level of urgency.

### ⚖️ Pros & Cons

- ✅ Better initial load performance (less JS upfront).
- ✅ Saves bandwidth and CPU for users who don’t use the feature.
- ✅ Improves metrics like Time to Interactive, First Input Delay by reducing upfront work.
- ❌ Feature load may lag: user might wait when they trigger it.
- ❌ More complexity: extra logic to load on interaction, placeholders/facades needed.
- ❌ If the feature is actually used frequently, the benefit may diminish.
- ❌ Requires careful UX handling so interaction doesn’t feel broken.

---

### 🧩 Example

```js
import React, { useState } from "react";

function MyComponent() {
  const [FeatureComponent, setFeatureComponent] = useState(null);

  // Only import the heavy feature when the user clicks the button
  const handleClick = () => {
    import(/* webpackChunkName: "heavy-feature" */ "./HeavyFeature")
      .then((mod) => setFeatureComponent(() => mod.default))
      .catch((err) => console.error(err));
  };

  return (
    <div>
      <button onClick={handleClick}>Load Feature</button>
      {FeatureComponent && <FeatureComponent />}
    </div>
  );
}
```
