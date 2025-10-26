## 🫣 Import on Visibility

- **Purpose:** Load components (or modules) only when they become visible in the viewport — not just on interaction.
- **How it works:** Use something like the `IntersectionObserver` API (or libraries built on it) to detect when an element enters the viewport; then dynamically import or lazy-load the associated module.
- **Result:** Smaller initial bundle, faster page load, and features/modules that only load when they’re needed visually.

### ⚖️ Pros & Cons

- ✅ Reduces initial JavaScript bundle size.
- ✅ Improves performance metrics like First Contentful Paint (FCP), Time to Interactive (TTI) for initial view.
- ✅ Defers non-essential modules until they become relevant visually.
- ❌ If the module loads too late when in view, user may see a delay or placeholder for longer.
- ❌ Many visibility-triggered modules may complicate build/monitoring.
- ❌ Needs proper placeholder UI to avoid layout shift or content “jump.”
- ❌ Not always worth it if the component is very likely to be used immediately.

---

### 🧩 Example

```js
import { lazy, Suspense } from "react";
import { useInView } from "react-intersection-observer";

const HeavyComponent = lazy(() => import("./HeavyComponent"));

function ListingCard(props) {
  const { ref, inView } = useInView({
    triggerOnce: true,
    rootMargin: "200px", // preload a bit before full visibility
  });

  return (
    <div ref={ref}>
      <Suspense fallback={<div>Loading…</div>}>
        {inView && <HeavyComponent />}
      </Suspense>
    </div>
  );
}

export default ListingCard;
```
