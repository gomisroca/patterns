## 🍚 Prefetch

- **Purpose:** Fetch resources ahead of time that might be needed soon (but aren’t required immediately).
- **How it works:** Use declarative HTML, HTTP headers or custom means so the browser fetches resources when idle, caches them, and then they’re ready when needed.
- **Result:** Faster perceived performance when a user navigates or triggers a feature, because the resource is already loaded. But you trade bandwidth and cache space for potential savings.

### ⚖️ Pros & Cons

- ✅ Reduces wait time for features the user will likely use.
- ✅ Improves perceived responsiveness of your app.
- ✅ Works well in combination with patterns like Dynamic Import (so you split code) and Prefetch (so you load it just-in-time).
- ❌ If overused, can waste bandwidth and slow down devices/slow networks.
- ❌ Browser support and heuristics vary (prefetch is a hint, not a guarantee).
- ❌ Requires analytics or user-behaviour insight to know which resources to prefetch.
- ❌ Caching strategy must be correct so the prefetched resource actually helps when needed.

---

### 🧩 Example

```js
<link rel="prefetch" href="emoji-picker.bundle.js" as="script" />
```

```js
const EmojiPicker = import(/* webpackPrefetch: true */ "./EmojiPicker");
```
