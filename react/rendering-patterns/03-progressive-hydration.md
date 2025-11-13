## 🌱 Progressive Hydration

- **Purpose:** Delay or stagger the hydration of interactive parts of a server-rendered UI so that critical parts become interactive quickly, while less critical parts hydrate later.
- **How it works:** Instead of hydrating the entire application immediately after the JS bundle loads, you hydrate portions (nodes/segments) over time based on priority, visibility, or user interaction.
- **Result:** Faster perceived interactivity (Time to Interactive), reduced JavaScript and hydration cost upfront, better performance on slower devices or large apps.

### ⚖️ Pros & Cons

- ✅ Reduces upfront JS/hydration work → faster interactive parts.
- ✅ Better user experience in large apps or on slow devices.
- ✅ Enables selective hydration of non-critical components.
- ❌ Need to identify which parts to prioritise/hydrate later — wrong choices hurt UX.
- ❌ More complex architecture: chunking, hydration orchestration, logic for when to hydrate.
- ❌ If too many parts are deferred, user might perceive non-interactive parts as broken.
- ❌ Not ideal for apps where everything must respond immediately (like full dashboards).

---

### 🧩 Example

```js
// Server sends fully rendered HTML.

// Client side bootstrap:
import App from "./App";

// Mount root fast:
hydrateRoot(document.getElementById("root"), <App />);

// But within App:
// The Hero, Navigation components hydrate immediately.
// The CommentsList or RelatedArticles components only hydrate when they scroll into view or after idle.

// e.g., using IntersectionObserver:
const commentSection = document.querySelector("#comments");
const observer = new IntersectionObserver(
  (entries) => {
    if (entries[0].isIntersecting) {
      import("./CommentsList").then((module) => {
        module.default().hydrate(commentSection);
      });
      observer.disconnect();
    }
  },
  { rootMargin: "200px" }
);
observer.observe(commentSection);
```
