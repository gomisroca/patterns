## 🐌 PRPL Pattern

- **Purpose:** Build web apps that load fast and perform well globally, including on slow networks or low-end devices.
- **How it works:** Based on 4 principles: Push, Render, Pre-cache, and Lazy-load.
- **Result:** A fast first load, cached assets, and deferred load of less important resources.

### 🪨 The Four Pillars

| Pillar        | Description                                                                                                  |
| ------------- | ------------------------------------------------------------------------------------------------------------ |
| **Push**      | “Push” or preload critical resources (e.g., CSS, JS) so they load with minimal round trips.                  |
| **Render**    | Render the initial route as quickly as possible (first meaningful content + interactivity) to improve UX.    |
| **Pre-cache** | Use service workers or caching to fetch and store assets for routes likely to be visited, in the background. |
| **Lazy-load** | Defer loading of routes or assets that are less frequently used or not needed immediately.                   |
