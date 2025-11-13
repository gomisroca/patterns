## 📄 Static Rendering

- **Purpose:** Generate fully rendered HTML pages at build time, so the client can load a pre-built HTML file rather than waiting for server rendering or heavy client-side logic.
- **How it works:** During your build process, each route is rendered to HTML using your app’s components + data (if applicable). The resulting HTML files are stored (e.g., on a CDN) and served directly to users.
- **Result:** Fast “Time to First Byte” (TTFB) and “First Contentful Paint” (FCP) because the HTML is ready-to-go, minimal server overhead, good caching. But works best when content is relatively static (not user-personalized or extremely volatile).

### ⚖️ Pros & Cons

- ✅ Very fast initial load since HTML is ready and cached.
- ✅ Excellent for SEO since full content exists in HTML.
- ✅ Low server runtime cost per request (as it’s mostly static).
- ❌ Build time can grow large if many pages or data variants.
- ❌ Not suitable for highly personalized or user-specific content.
- ❌ If content changes often, you might need frequent rebuilds or rerenders.

---

### 🧩 Example

```js
// pages/about.js (React / Next.js)
export default function About() {
  return (
    <div>
      <h1>About Us</h1>
      <p>We build awesome stuff.</p>
    </div>
  );
}
```

- At build time, about.html is generated for route /about.

- On user request, the server (or CDN) serves this pre-rendered HTML. Client loads minimal JS/hydration.
