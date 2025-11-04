## 🦥 Preload

- **Purpose:** Tell the browser to fetch a critical resource early, before it's naturally discovered in the page.
- **How it works:** Use declarative HTML or custom means such as Webpack so the browser gives the resource a high priority and fetches it sooner.
- **Result:** The resource is available sooner when needed, improving interactivity and key metrics.

### ⚖️ Pros & Cons

- ✅ Lets you control early fetching of important assets.
- ✅ Can improve interactivity (Time to Interactive) if critical script or component is needed soon.
- ❌ If used on the wrong resource, you may delay more important ones (hero image, CSS) and hurt performance.
- ❌ Over-using preload can waste bandwidth or cache space.
- ❌ Requires good understanding of what’s “critical” vs “can wait”.

---

### 🧩 Example

```js
<link rel="preload" href="emoji-picker.bundle.js" as="script">
<script src="emoji-picker.bundle.js" defer></script>
```

```js
const EmojiPicker = import(/* webpackPreload: true */ "./EmojiPicker");
```
