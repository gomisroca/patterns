## 🌊 Streaming Server-Side Rendering

- **Purpose:** Send HTML to the browser in chunks — as it’s generated on the server — rather than waiting for the entire page to render before sending it.
- **How it works:** Use a streaming API (e.g.,` renderToNodeStream()` or `renderToReadableStream()` in React) on the server to start piping HTML chunks immediately. Browser can parse and render while more HTML is still being sent.
- **Result:** Reduced Time to First Byte (TTFB), earlier First Contentful Paint (FCP), and better perceived performance especially for large pages.

### ⚖️ Pros & Cons

- ✅ Faster delivery of meaningful HTML → earlier paint and better user experience.
- ✅ Better for large pages or heavy components because you don’t wait for everything before sending something.
- ✅ Improved server responsiveness under load (thanks to streaming/back-pressure handling).
- ❌ Implementation complexity; streaming SSR isn’t simply “change `renderToString` to `renderToNodeStream`” in many cases.
- ❌ Some CSS-in-JS or head-management libraries may struggle or need adjustments when HTML is streamed.
- ❌ The client still needs hydration logic; streaming HTML alone doesn’t guarantee interactivity until hydration is done.

---

### 🧩 Example

```js
import express from "express";
import React from "react";
import { renderToNodeStream } from "react-dom/server";
import App from "./src/App";

const app = express();

app.get("/", (req, res) => {
  const stream = renderToNodeStream(<App />);
  res.writeHead(200, {
    "Content-Type": "text/html",
    "Transfer-Encoding": "chunked",
  });
  res.write(
    `<!DOCTYPE html><html><head><title>My App</title></head><body><div id="root">`
  );

  stream.pipe(res, { end: false });
  stream.on("end", () => {
    res.write(`</div></body></html>`);
    res.end();
  });
});
```

- The server sends an initial shell (`<!DOCTYPE html>...<div id="root">`) immediately.

- Then it streams the React-rendered HTML chunk by chunk.

- Once done, sends the closing tags and ends the response.
