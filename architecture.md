---
title: Architecture & Design Patterns
excerpt: Recommended architecture patterns, component design principles, and state management approaches.
---

# Architecture & Design Patterns

## Frontend Architecture

AAO React projects follow a **feature-based folder structure**:

```
src/
  components/     # Shared UI components
  features/       # Feature-specific modules (each with own components, hooks, utils)
  data/           # Static data, constants, mock fixtures
  hooks/          # Shared custom React hooks
  utils/          # Pure utility functions
  App.jsx
  main.jsx
```

## Component Design Principles

- **Small and focused**: Each component does one thing well.
- **Props over global state**: Prefer prop drilling for simple trees; use Context or Zustand only when state is truly global.
- **Accessible by default**: Use semantic HTML (`<nav>`, `<main>`, `<section>`, `<article>`) and ARIA attributes where needed.
- **Responsive**: Mobile-first Tailwind classes (`sm:`, `md:`, `lg:` breakpoints).

## State Management

| Use Case | Recommended Approach |
|---|---|
| UI state (modals, toggles) | `useState` |
| Async server data | `useEffect` + `useState` or React Query |
| Cross-component state | React Context |
| Complex global state | Zustand |

## API Design

Backend services should follow REST conventions. Use `/api/v1/` prefixes and return consistent JSON shapes:

```json
{
  "data": { ... },
  "meta": { "page": 1, "total": 100 },
  "error": null
}
```
