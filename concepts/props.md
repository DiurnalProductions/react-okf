---
type: Concept
title: Props
description: Read-only inputs passed from parent components to children
tags: [react, props, data-flow]
prerequisites:
  - concepts/components
related:
  - concepts/state
  - concepts/context
resource: "https://react.dev/learn/passing-props-to-a-component"
timestamp: 2026-07-06
---

## Summary

Props (short for properties) are read-only arguments passed from a parent component to a child. They enable one-way data flow down the component tree. A child cannot modify its own props — if new data is needed, the parent must pass updated props.

## Mental model

Props are like **function parameters for UI**. The parent owns the data; the child receives a snapshot. When props change, React re-renders the child with the new values. Props can be any JavaScript value: strings, numbers, objects, arrays, or even other components (the `children` prop). Since React 19, `ref` is also just a prop — function components receive it directly without `forwardRef`.

## Example

```jsx
function Button({ label, onClick, disabled = false }) {
  return (
    <button onClick={onClick} disabled={disabled}>
      {label}
    </button>
  );
}

function App() {
  return (
    <Button
      label="Save"
      onClick={() => console.log('saved')}
    />
  );
}
```

## Common mistakes

- Mutating props or objects received via props (breaks one-way data flow).
- Spreading unknown props onto DOM elements without filtering (can cause React warnings).
- Passing new object or function literals inline on every render, causing unnecessary child re-renders.
- Confusing props with state — props come from outside; state is owned internally.

## Related concepts

- [Components](/concepts/components.md) — props are the primary input mechanism for components.
- [State](/concepts/state.md) — internal mutable data that complements props.
- [Context](/concepts/context.md) — alternative to passing props through many layers.
