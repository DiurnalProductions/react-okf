---
id: react.hooks
type: concept
title: Hooks
description: Functions that let function components use state, context, and lifecycle features
tags: [react, hooks]
prerequisites:
  - react.state
related:
  - react.effects
  - react.context
resource: https://react.dev/reference/react
timestamp: 2026-01-01
---

## Summary

Hooks are functions that let you "hook into" React features from function components. They replace the need for class component lifecycle methods. Built-in hooks include `useState`, `useEffect`, `useContext`, `useRef`, `useMemo`, and `useCallback`. Custom hooks let you extract reusable stateful logic.

## Mental model

Hooks are **composable state machines** attached to a component instance. They must be called at the top level of a function component (or custom hook) — never inside loops, conditions, or nested functions. React relies on call order to associate hook state with the correct component. Each hook call returns a slice of capability: state setter, effect cleanup, context value, etc.

## Example

```jsx
import { useState, useCallback } from 'react';

function useCounter(initial = 0) {
  const [count, setCount] = useState(initial);
  const increment = useCallback(() => setCount(c => c + 1), []);
  const reset = useCallback(() => setCount(initial), [initial]);
  return { count, increment, reset };
}

function Counter() {
  const { count, increment, reset } = useCounter(0);
  return (
    <div>
      <span>{count}</span>
      <button onClick={increment}>+</button>
      <button onClick={reset}>Reset</button>
    </div>
  );
}
```

## Common mistakes

- Calling hooks conditionally or inside loops (breaks the rules of hooks).
- Using `useEffect` for everything that should be an event handler or derived value.
- Creating custom hooks that do not start with `use` or that hide side effects unexpectedly.
- Overusing `useMemo`/`useCallback` without measuring — premature optimization adds complexity.

## Related concepts

- [State](/concepts/state.md) — `useState` is the foundational state hook.
- [Effects](/concepts/effects.md) — `useEffect` handles side effects and synchronization.
- [Context](/concepts/context.md) — `useContext` reads shared values from providers.
