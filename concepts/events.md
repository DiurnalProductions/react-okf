---
id: react.events
type: concept
title: Events
description: Handling user interactions with synthetic events in React
tags: [react, events, interactions]
prerequisites:
  - react.state
related:
  - react.state
resource: https://react.dev/learn/responding-to-events
timestamp: 2026-01-01
---

## Summary

React wraps native browser events in **SyntheticEvents** — a cross-browser normalization layer. Event handlers are passed as props (`onClick`, `onChange`, `onSubmit`) and receive a synthetic event object. Handlers typically update state, which triggers a re-render reflecting the new UI.

## Mental model

Events are **the bridge between user action and state change**. Unlike effects (which synchronize after render), events respond to explicit user gestures. React 17+ attaches listeners at the root, not per element. Event handlers should be lean — perform the action, update state, and delegate heavy work elsewhere. Use `e.preventDefault()` and `e.stopPropagation()` when needed, same as native events.

## Example

```jsx
import { useState } from 'react';

function SearchForm() {
  const [query, setQuery] = useState('');

  function handleSubmit(e) {
    e.preventDefault();
    console.log('Searching for:', query);
  }

  return (
    <form onSubmit={handleSubmit}>
      <input
        value={query}
        onChange={e => setQuery(e.target.value)}
        placeholder="Search…"
      />
      <button type="submit">Search</button>
    </form>
  );
}
```

## Common mistakes

- Calling the handler immediately (`onClick={handleClick()}`) instead of passing a reference (`onClick={handleClick}`).
- Forgetting `e.preventDefault()` on form submit, causing full page reloads.
- Putting data-fetching or complex side effects in click handlers that belong in effects or dedicated modules.
- Relying on `e.target.value` after an async gap without capturing the value first.

## Related concepts

- [State](/concepts/state.md) — events are the primary trigger for state updates.
- [Components](/concepts/components.md) — event handlers are passed as props to child components.
- [Props](/concepts/props.md) — callback props (`onSave`, `onDelete`) propagate events up the tree.
