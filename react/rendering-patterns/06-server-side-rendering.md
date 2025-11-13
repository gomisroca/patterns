## 🌐 Server-Side Rendering

- **Purpose:** Generate the full HTML for a page on each user request (on the server) so the client receives a fully rendered page.
- **How it works:** The server fetches data, builds HTML using the React component tree (via rendering methods), and sends the HTML to the browser. The client may then hydrate or attach interactivity.
- **Result:** Users and crawlers get rendered content immediately; improved SEO and faster first meaningful paint, but increased server cost and latency for each request.

### ⚖️ Pros & Cons

- ✅ Fast first render for users (HTML ready) → better perceived performance.
- ✅ Good for SEO and pages where content is dynamic or personalized per user.
- ✅ Ensures that the HTML content is viewable even if JS fails.
- ❌ Higher server load and latency per request → may scale less well than static generation.
- ❌ Slower TTFB especially if data fetching or server processing is heavy.
- ❌ Client still needs JS for interactivity/hydration → initial render may look correct but not be interactive until JS loads.
- ❌ Implementation complexity: management of caching, routing logic, and possibly many states/variants.

---

### 🧩 Example

```js
// pages/users/[id].js
export async function getServerSideProps({ params }) {
  const res = await fetch(`https://api.example.com/user/${params.id}`);
  const user = await res.json();
  return {
    props: { user }, // passed to the component
  };
}

export default function UserPage({ user }) {
  return (
    <section>
      <h1>{user.name}</h1>
      <p>{user.bio}</p>
    </section>
  );
}
```

- On each request, getServerSideProps runs, fetches the user data, and returns props.
- The page is rendered on server and sent to browser with the user’s content.
- Client receives HTML containing that data, then may hydrate for interactivity.
