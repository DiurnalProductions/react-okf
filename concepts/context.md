---
type: Concept
title: Context
description: Sharing values across the component tree without prop drilling
tags: [react, context]
prerequisites:
  - concepts/effects
related:
  - concepts/props
resource: "https://react.dev/learn/passing-data-deeply-with-context"
timestamp: 2026-07-06
---

## Summary

Context provides a way to pass data through the component tree without manually passing props at every level. A provider component supplies a value; any descendant can consume it with `useContext` (or React 19's `use`, which may also be called conditionally). Since React 19 the context object itself can be rendered as the provider — `<ThemeContext value={...}>` instead of `<ThemeContext.Provider value={...}>`. Context is ideal for globally relevant, infrequently changing data like themes, locale, or authentication.

## Mental model

Context is a **broadcast channel** for a subtree. The provider publishes a value; consumers anywhere below subscribe to it. When the provider's value changes, all consuming components re-render. Context is not a state management replacement — it is a transport mechanism. Pair it with `useState` or `useReducer` in the provider for mutable shared state.

## Example

```jsx
import { createContext, useContext, useState } from 'react';

const ThemeContext = createContext('light');

function ThemeProvider({ children }) {
  const [theme, setTheme] = useState('light');
  return (
    <ThemeContext.Provider value={{ theme, setTheme }}>
      {children}
    </ThemeContext.Provider>
  );
}

function ThemedButton() {
  const { theme, setTheme } = useContext(ThemeContext);
  return (
    <button
      className={theme}
      onClick={() => setTheme(t => t === 'light' ? 'dark' : 'light')}
    >
      Toggle theme
    </button>
  );
}
```

## Common mistakes

- Putting frequently changing values in context, causing large re-render subtrees.
- Using context when simple prop passing or component composition would suffice.
- Creating a new object literal as the provider value on every render (forces all consumers to re-render).
- Splitting unrelated concerns into a single context instead of separate focused contexts.

## Related concepts

- [Props](/concepts/props.md) — context is an alternative to deep prop drilling; compare when to use each.
- [Hooks](/concepts/hooks.md) — `useContext` is the hook for reading context values.
- [Effects](/concepts/effects.md) — prerequisite path through the core learning chain.
