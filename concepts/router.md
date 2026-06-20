---
id: react.router
type: concept
title: Router
description: Client-side routing that maps URLs to components in single-page applications
tags: [react, routing, spa]
prerequisites:
  - react.components
  - react.hooks
related:
  - react.components
resource: https://reactrouter.com
timestamp: 2026-01-01
---

## Summary

A React router maps URL paths to components, enabling multi-page-like navigation without full server round-trips. Libraries such as React Router provide declarative routing via components (`<Routes>`, `<Route>`) or data APIs. The router listens to history changes and renders the matching component tree.

## Mental model

The router is a **conditional renderer driven by the URL**. The address bar is application state. Navigating updates the history stack; the router matches the new path against a route table and mounts the corresponding component. Nested routes render outlet components, mirroring UI layout hierarchy. Link components intercept clicks to prevent full page reloads.

## Example

```jsx
import { BrowserRouter, Routes, Route, Link } from 'react-router-dom';

function App() {
  return (
    <BrowserRouter>
      <nav>
        <Link to="/">Home</Link>
        <Link to="/about">About</Link>
      </nav>
      <Routes>
        <Route path="/" element={<Home />} />
        <Route path="/about" element={<About />} />
        <Route path="/users/:id" element={<UserDetail />} />
      </Routes>
    </BrowserRouter>
  );
}
```

## Common mistakes

- Using `<a href>` instead of `<Link to>` for internal navigation (causes full page reloads).
- Forgetting to wrap the app in a router provider (`BrowserRouter` or equivalent).
- Putting data-fetching only in `useEffect` when the router's loader/action APIs can handle it.
- Hard-coding paths in multiple places instead of centralizing route definitions.

## Related concepts

- [Components](/concepts/components.md) — routes render components based on URL.
- [Hooks](/concepts/hooks.md) — `useParams`, `useNavigate`, and `useLocation` are common router hooks.
- [Effects](/concepts/effects.md) — sometimes used to sync URL params with local state.
