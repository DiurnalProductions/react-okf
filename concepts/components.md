---
id: react.components
type: concept
title: Components
description: Reusable, composable units that describe pieces of UI
tags: [react, components]
prerequisites:
  - react.jsx
related:
  - react.props
  - react.rendering
resource: https://react.dev/learn/your-first-component
timestamp: 2026-01-01
---

## Summary

Components are the building blocks of a React application. A component is a JavaScript function (or, historically, a class) that accepts props and returns JSX describing what should appear on screen. Components compose — you build complex UIs by nesting simple components.

## Mental model

Picture components as **custom HTML tags you define**. Each component encapsulates a piece of UI and its behavior. Parent components render child components like `<Avatar user={user} />`. React calls your function, takes the returned JSX, and reconciles it with the DOM. Components should be pure with respect to their props: same props in, same JSX out.

## Example

```jsx
function Avatar({ user }) {
  return <img src={user.avatarUrl} alt={user.name} />;
}

function ProfileCard({ user }) {
  return (
    <article>
      <Avatar user={user} />
      <h2>{user.name}</h2>
      <p>{user.bio}</p>
    </article>
  );
}
```

## Common mistakes

- Defining components inside other components (causes remounting on every parent render).
- Using PascalCase inconsistently — only capitalized names are treated as components.
- Putting side effects directly in the render body instead of event handlers or effects.
- Creating overly large "god components" instead of composing smaller ones.

## Related concepts

- [JSX](/concepts/jsx.md) — prerequisite syntax for writing components.
- [Props](/concepts/props.md) — how data flows into components.
- [Rendering](/concepts/rendering.md) — how React processes component output.
