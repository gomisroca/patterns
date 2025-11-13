## 🌻 Selective Hydration

- **Purpose:** Prioritise hydration of interactive or visible UI components first, deferring less-critical parts, so the page becomes interactive quicker.
- **How it works:** Rather than hydrating the entire server-rendered UI at once, React hydrates critical sections immediately (e.g., where a user clicks), and schedules the rest later (idle, visibility, lower priority).
- **Result:** Faster Time to Interactive (TTI), better responsiveness especially on slower devices, while still using SSR/SSG advantages.

### ⚖️ Pros & Cons

- ✅ Improves perceived responsiveness and interactivity.
- ✅ Better experience on slower devices / networks.
- ✅ Combines SSR/SSG with performant hydration strategy.
- ❌ More complex to architect (splitting, chunking, `<Suspense>` boundaries).
- ❌ Need to ensure server and client render structure match to avoid hydration errors.
- ❌ If hydration is delayed too much for parts the user expects to be interactive, you might hurt UX.

---

### 🧩 Example

```js
// Server renders full HTML quickly.

// Client side hydration:
hydrateRoot(
  document.getElementById('root'),
  <Suspense fallback={<Spinner />}>
    <App />
  </Suspense>
);

// In App:
<Navigation/>         // top priority, hydrates early
<Suspense fallback={<Placeholder/>}>
  <HeavyWidget/>     // lower-priority: hydrates later or when visible/interaction occurs
</Suspense>

```
