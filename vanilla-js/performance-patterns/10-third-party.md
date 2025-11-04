## 3️⃣ Optimize Loading Third-Parties

- **Purpose:** Minimize the performance impact of third-party scripts and resources by managing when and how they load.
- **How it works:** Third-party assets (scripts, embeds, analytics) are identified, then loaded using strategies like async, defer, preconnect or lazy loading.
- **Result:** Reduced blocking, faster interactivity and rendering, improved metrics (CWV) while retaining the benefit of the third-party features.

### ⚖️ Pros & Cons

- ✅ Keeps your page faster by reducing blocking from third-party code.
- ✅ Helps you maintain better control over performance despite external dependencies.
- ✅ Works hand-in-hand with other loading/rendering optimizations (resource hints, lazy loads, etc.).
- ❌ Some third-party features might need to load early (trade-off).
- ❌ Self-hosting scripts means you must handle updates/security/maintenance.
- ❌ Lazy or delayed loading might affect functionality if fallback or timing isn’t handled properly.
- ❌ It adds complexity: you have to audit 3P usage, determine critical vs non-critical, and monitor performance.

---

### 🧩 Example

```html
<head>
  <!-- early connection setup for a critical third-party domain -->
  <link rel="preconnect" href="https://third-party-cdn.com" />
  <link rel="dns-prefetch" href="https://third-party-cdn.com" />
</head>
<body>
  <!-- Non-critical script loaded with defer so it does not block DOM parsing -->
  <script src="https://third-party-analytics.com/analytics.js" defer></script>

  <!-- Embedding a map below the fold, lazy loaded -->
  <div
    class="map-container"
    data-src="https://maps.third-party.com/embed"
  ></div>
  <script>
    if ("IntersectionObserver" in window) {
      let obs = new IntersectionObserver((entries) => {
        if (entries[0].isIntersecting) {
          let div = entries[0].target;
          div.innerHTML = `<iframe src="${div.dataset.src}" loading="lazy"></iframe>`;
          obs.disconnect();
        }
      });
      obs.observe(document.querySelector(".map-container"));
    }
  </script>
</body>
```
