## 📽️ Animating View Transitions

- **Purpose:** Animate changes between two visual states in the UI (e.g., page navigation, layout changes) to provide smoother user experience.
- **How it works:** Use document.startViewTransition(callback) to let the browser capture the “before” snapshot of the DOM, execute DOM changes in the callback, then animate between the old and new states using built-in or custom animations.
- **Result:** More visually-coherent transitions, reduced perceived latency, improved UX for UI changes or navigations.

### 🗝️ Key Concepts

- The API takes two states: “old” and “new”. During the transition, pseudo-elements ::view-transition-old(root) and ::view-transition-new(root) represent the two snapshots.
- Can assign view-transition-name (and containment like contain: layout | paint) to DOM elements so that shared elements across states animate smoothly (like a photo growing into place).
- For navigation (especially SPAs) you should ideally call startViewTransition after data is fetched but before DOM update, so the UI isn’t stuck in a frozen state.

---

### 🧩 Example

```js
if (document.startViewTransition) {
  document.startViewTransition(() => {
    // perform DOM changes here
    document.querySelector("#details").toggleAttribute("open");
  });
} else {
  // fallback: just perform the change normally
  document.querySelector("#details").toggleAttribute("open");
}
```

```html
<div id="details" open>
  <img src="photo.jpg" alt="Example" view-transition-name="photo-hero" />
  <p>Details</p>
</div>
```

```css
/* Target the snapshots of the element during transition */
::view-transition-old(photo-hero),
::view-transition-new(photo-hero) {
  animation-duration: 300ms;
}
```
