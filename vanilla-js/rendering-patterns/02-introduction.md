## 🎉 Rendering Patterns

- **Purpose:** Decide how and where to render content — on build, server, edge or client. The choice strongly affects user experience (UX) and developer experience (DX).
- **How it works:** Different patterns (static rendering, server-side rendering, edge/streaming rendering, client rendering) trade off initial load time, interactivity, cacheability, complexity.
- **Result:** Choosing the right pattern leads to faster builds, better Core Web Vitals (CWV), improved performance; choosing the wrong one can hamper app success.

---

### 🗝️ Key Rendering Patterns

| Pattern                                   | Description                                                                           | Best Use Case                                                       |
| ----------------------------------------- | ------------------------------------------------------------------------------------- | ------------------------------------------------------------------- |
| **Plain Static Rendering**                | HTML is generated at build time; served from CDN/edge; no build-time data variation.  | Pages with constant content, many users, high cacheability.         |
| **Static + Client-Side Fetch**            | HTML is pre-rendered, then client fetches dynamic data after load.                    | Mostly static pages with some dynamic parts (e.g., latest data).    |
| **Static with Build-Time Data Fetch**     | HTML includes dynamic data fetched at build time (e.g., via `getStaticProps`).        | Pages where data changes infrequently and build time is acceptable. |
| **Incremental Static Regeneration (ISR)** | Pages are statically generated but can be regenerated later or on-demand.             | Sites with lots of pages and moderate data update needs.            |
| **Server-Side Rendering (SSR)**           | HTML is generated on each request based on dynamic/user-specific data.                | Highly personalized pages, user dashboards, auth-based content.     |
| **Edge SSR / HTTP Streaming**             | Rendering at edge region + streaming parts of HTML as ready; hybrid static + dynamic. | Very dynamic content with global scale and performance needs.       |

### ⚖️ Pros & Cons

- ✅ Static patterns ofer fast Time To First Byte, better caching and lower runtime costs.
- ❌ Static may fail when personalized, per-used data is needed.
- ⚠️ Many apps will require mixed rendering patterns.

---

### 🧩 Example

1. A blog uses Plain Static Rendering: pages generated at build, served from CDN.
2. The same blog adds “latest comments” via Static + Client-Side Fetch.
3. A product catalog uses ISR: pages pre-built and regenerated every X minutes.
4. A user dashboard uses SSR: content unique to each logged-in user.
