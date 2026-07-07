---
type: Concept
title: Effects
description: Synchronizing components with external systems via useEffect
tags: [react, effects, useEffect]
prerequisites:
  - concepts/hooks
related:
  - concepts/hooks
resource: "https://react.dev/learn/synchronizing-with-effects"
timestamp: 2026-01-01
---

## Summary

Effects let a component synchronize with an external system — fetching data, subscribing to events, manipulating the DOM, or starting timers. In function components, `useEffect` runs after render and can return a cleanup function. Effects express "keep this in sync with that" rather than "do this once on mount."

## Mental model

An effect is a **reaction to rendered output**. After React paints the DOM, effects run. If dependencies change on a subsequent render, React runs the previous cleanup, then the new effect. Think of effects as bridging React's declarative world and imperative APIs (browser, network, third-party libraries). Not everything belongs in an effect — event handlers and derived state often belong elsewhere.

## Example

```jsx
import { useState, useEffect } from 'react';

function UserProfile({ userId }) {
  const [user, setUser] = useState(null);

  useEffect(() => {
    let cancelled = false;

    fetch(`/api/users/${userId}`)
      .then(res => res.json())
      .then(data => {
        if (!cancelled) setUser(data);
      });

    return () => { cancelled = true; };
  }, [userId]);

  if (!user) return <p>Loading…</p>;
  return <h1>{user.name}</h1>;
}
```

## Common mistakes

- Using an empty dependency array `[]` when the effect actually depends on props or state.
- Omitting cleanup for subscriptions, timers, or fetch requests (causes memory leaks and race conditions).
- Putting data-fetching logic in effects when a dedicated data library or server component is more appropriate.
- Running expensive work in effects that should run in event handlers.

## Related concepts

- [Hooks](/concepts/hooks.md) — `useEffect` is a hook; effects are one hook capability among many.
- [Context](/concepts/context.md) — often combined with effects to subscribe to shared state.
