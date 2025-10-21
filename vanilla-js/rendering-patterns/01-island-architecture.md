## 🏝️ Island Architecture

- **Purpose:** Ship pages as mostly static HTML, with small interactive “islands” of JS only where needed.
- **How it works:** A server-rendered page contains static content + embedded interactive components (islands). Each island is hydrated (or activated) independently.
- **Result:** Much less JS shipped up-front; faster load times; interactivity where needed without full SPA overhead.

---

### ⚖️ Pros & Cons

- ✅ Smaller JS bundles => faster TTI
- ✅ Static HTML is SEO-friendly and accessible
- ✅ Interactive parts don’t block the whole page.
- ❌ Not very mature yet, not widely adopted.
- ❌ For highly interactive apps (many islands) the overhead may increase.
- ❌ Implementation complexity: need careful orchestration of islands and hydration scheduling.

---

### 🧩 Example

```js
<!-- Static part of the page rendered on server -->
<section class="intro">
  <h1>Post title (static)</h1>
  <p>This is the post content with images…</p>
</section>

<!-- Interactive island embedded -->
<section class="social">
  <div id="social-buttons-widget">
    <!-- Placeholder for SocialButtons component -->
  </div>
  <script type="module">
    import { SocialButtons } from './components/SocialButtons.js';
    SocialButtons.hydrate(document.getElementById('social-buttons-widget'));
  </script>
</section>
```
