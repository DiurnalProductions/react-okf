---
type: Concept
title: JSX
description: Syntax extension for describing UI structure in JavaScript
tags: [react, jsx, syntax]
related:
  - concepts/components
resource: "https://react.dev/learn/writing-markup-with-jsx"
timestamp: 2026-01-01
---

## Summary

JSX is a syntax extension that lets you write HTML-like markup inside JavaScript. React transforms JSX into function calls that create element descriptions. It is not HTML — it is sugar over `React.createElement` (or the modern JSX runtime equivalent).

## Mental model

Think of JSX as a **template literal for UI trees**. Each tag becomes a function call with a type, props object, and children. Curly braces `{}` escape back into JavaScript expressions. JSX must return a single root (or a fragment `<>...</>`). Attribute names follow camelCase (`className`, `onClick`) because they are JavaScript object keys.

## Example

```jsx
function Greeting({ name }) {
  const hour = new Date().getHours();
  const salutation = hour < 12 ? 'Good morning' : 'Hello';

  return (
    <div className="greeting">
      <h1>{salutation}, {name}!</h1>
      <p>Welcome to React.</p>
    </div>
  );
}
```

## Common mistakes

- Using `class` instead of `className`, or `for` instead of `htmlFor`.
- Forgetting that JSX expressions must be a single expression (use ternaries, not `if` statements, inside `{}`).
- Treating JSX as HTML — self-closing tags are required (`<img />`, `<input />`).
- Returning multiple adjacent elements without a wrapping fragment or parent element.

## Related concepts

- [Components](/concepts/components.md) — JSX is how you express component trees.
