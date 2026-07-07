---
type: Concept
title: State
description: Mutable data owned by a component that triggers re-renders when updated
tags: [react, state]
prerequisites:
  - concepts/props
related:
  - concepts/hooks
  - concepts/events
resource: "https://react.dev/learn/state-a-components-memory"
timestamp: 2026-07-06
---

## Summary

State is data that a component owns and can change over time. When state updates, React schedules a re-render of that component and its descendants. State is private to the component that declares it and is initialized and updated through React's state APIs.

## Mental model

Think of state as a component's **internal memory**. Unlike props (which flow down from parents), state is local. Updating state does not modify the existing value in place — React replaces it with a new value and re-runs the component function. State updates are asynchronous, and since React 18 they are automatically batched everywhere — event handlers, promises, timeouts — so multiple `set` calls in one tick produce a single re-render.

## Example

```jsx
import { useState } from 'react';

function Counter() {
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={() => setCount(count + 1)}>
        Increment
      </button>
    </div>
  );
}
```

## Common mistakes

- Mutating state directly (`state.items.push(x)`) instead of creating a new object or array.
- Assuming state updates are synchronous — reading state immediately after `setState` shows the old value.
- Storing derived data in state that could be computed from props or other state.
- Lifting state too late or not at all, causing sibling components to fall out of sync.

## Related concepts

- [Props](/concepts/props.md) — external inputs that complement internal state.
- [Hooks](/concepts/hooks.md) — `useState` is the primary hook for state in function components.
- [Events](/concepts/events.md) — user interactions typically trigger state updates.
