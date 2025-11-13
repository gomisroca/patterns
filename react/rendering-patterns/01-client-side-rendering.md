## 👤 Client-side Rendering

- **Purpose:** Render the application UI entirely in the browser, after loading a minimal HTML shell.
- **How it works:** The server sends a basic HTML file (often just `<div id="root"></div>`). JavaScript bundle fetches, executes, builds the UI, handles routing, data-fetching, etc.
- **Result:** Rich interactive experience like a single-page application (SPA), but initial load may be delayed while bundles download and execute.

### ⚖️ Pros & Cons

- ✅ Fast subsequent navigations since client controls routing and view updates (no full page reloads).
- ✅ Great for highly interactive apps, dashboards, user-specific experiences where much logic occurs in the browser.
- ✅ Clear separation between server (static host) and client logic.
- ❌ Larger initial JavaScript bundle → delays First Contentful Paint (FCP) and Time to Interactive (TTI).
- ❌ Potential SEO issues: because content is rendered in the browser, crawlers may struggle (or index later) unless SSR or prerendering used.
- ❌ Depends on client’s device capability and network speed; slower devices may suffer noticeable delay.

### Performance Optimizations

- Keep the initial JavaScript bundle small (< ~100-170 KB gzipped) to reduce load/parse/compile cost.
- Use code-splitting, lazy loading of less-critical modules.
- Preload critical resources; defer non-essential scripts.
- Consider service-worker caching of the app shell.
- Optimize data-fetching to avoid delayed content.
