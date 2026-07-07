---
type: Concept
title: Rendering
description: How React reconciles component trees and commits updates to the DOM
tags: [react, rendering, reconciliation]
prerequisites:
  - concepts/components
related:
  - concepts/components
resource: "https://react.dev/learn/render-and-commit"
timestamp: 2026-07-06
---

## Summary

Rendering is the process by which React turns component functions into a UI description and updates the DOM. React maintains a virtual representation of the UI, diffs it against the previous tree (reconciliation), and applies minimal DOM mutations in the commit phase. Re-renders occur when state or props change, or when a parent re-renders.

## Mental model

Rendering has three phases: **trigger** (state/props change), **render** (call components, produce a new element tree), and **commit** (apply DOM changes, run layout effects). With concurrent rendering (React 18+), non-urgent renders started inside `startTransition` can be interrupted and restarted so urgent updates like typing stay responsive. Re-rendering does not always mean the DOM changes — React may bail out if output is identical. Keys help React match list items across renders. Strict Mode double-invokes renders in development to surface side effects.

## Example

```jsx
function List({ items }) {
  return (
    <ul>
      {items.map(item => (
        <li key={item.id}>{item.label}</li>
      ))}
    </ul>
  );
}

// When items changes, React:
// 1. Re-runs List()
// 2. Diffs the new <ul> tree against the previous one
// 3. Adds, removes, or updates only the <li> nodes that changed
```

## Common mistakes

- Using array index as `key` for lists that reorder, insert, or delete items.
- Assuming a child re-render means DOM nodes are recreated (React reuses nodes when possible).
- Calling setState during render in the same component (causes infinite loops).
- Confusing "render" with "paint" — rendering is pure computation; commit touches the DOM.

## Related concepts

- [Components](/concepts/components.md) — rendering is how component output becomes visible UI.
- [State](/concepts/state.md) — state changes are the most common render trigger.
- [Hooks](/concepts/hooks.md) — hook state updates schedule re-renders.
