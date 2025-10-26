## 🔃 Loading Sequence

- **Purpose:** Optimize the order and timing in which resources (CSS, fonts, images, JS) are loaded so the page becomes usable and interactive as quickly as possible.
- **How it works:** Prioritize critical resources (for first content, hero image, interactivity) and sequence their loading intelligently, delaying or deferring less critical resources.
- **Result:** Better performance metrics (e.g., First Contentful Paint, Largest Contentful Paint, First Input Delay) and improved user experience.

### ⚖️ Pros & Cons

- ✅ Maximises performance for initial view and interactivity.
- ✅ Better alignment between resource loading and browser render/interactivity phases.
- ✅ Improves user-perceived speed and key metrics.
- ❌ Requires careful planning and monitoring of resource dependencies and priorities.
- ❌ Browser and network behaviour may differ from expectations (complex environment).
- ❌ Over-optimisation can add complexity (e.g., too many preload tags, many special cases).
- ❌ Needs custom build/asset strategy (e.g., inline CSS, manage fonts, chunking JS).

---

### 🧩 Ideal Loading Sequence (Simplified)

1. Parse HTML.
2. Execute small inline first-party (1P) scripts.
3. Inline critical CSS (or preload).
4. Inline or preconnect critical fonts.
5. Load hero image / main above-the-fold image. (Start LCP)
6. Load non-critical CSS (async) and below-the-fold images.
7. Load and execute first-party JS for interactivity. (Prepare FID)
8. Load lazy-loaded JS chunks, third-party resources, further interactions.
