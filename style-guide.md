---
title: UI & Code Style Guide
excerpt: Conventions for visual design, component styling, and code formatting across AAO projects.
---

# UI & Code Style Guide

## Design Tokens

AAO projects use a consistent set of brand colors defined as Tailwind custom tokens:

| Token | Hex | Usage |
|---|---|---|
| `aao-dark-blue` | `#012345` | Primary backgrounds, headings |
| `aao-dark-red` | `#B72717` | Accents, CTAs, error states |
| `aao-light-blue` | `#388CBB` | Links, hover states, highlights |
| `aao-light-red` | `#D55855` | Secondary accents |
| `aao-beige` | `#FBF3E3` | Section backgrounds, tags |

## Typography

| Role | Font | Tailwind Class |
|---|---|---|
| Headings | Poppins | `font-heading` |
| Body / UI | Montserrat | `font-body` |

Always use `font-heading` for `<h1>`–`<h3>` and `font-body` for paragraphs, labels, and buttons.

## Spacing & Layout

- Max content width: `max-w-7xl mx-auto`
- Section padding: `py-16 md:py-24 px-4`
- Card radius: `rounded-2xl`
- Card shadow: `shadow-sm` (default), `shadow-md hover:shadow-xl` (interactive)

## Button Variants

```jsx
// Primary
<button className="bg-aao-dark-blue hover:bg-aao-light-blue text-white font-body font-semibold px-5 py-2.5 rounded-lg transition-colors duration-200">
  Action
</button>

// Danger / CTA
<button className="bg-aao-dark-red hover:bg-red-700 text-white font-body font-semibold px-5 py-2.5 rounded-lg transition-colors duration-200">
  Join Slack
</button>

// Ghost
<button className="text-aao-light-blue hover:text-aao-dark-blue font-body font-semibold text-sm transition-colors duration-200">
  Learn more →
</button>
```

## Component Conventions

- Use `article` for card-like content items
- Use `section` with an `id` for scrollable page sections
- Always include `aria-label` on icon-only buttons
- Prefer `flex flex-col flex-1` inside cards to push CTAs to the bottom

## Code Formatting

- **Indentation**: 2 spaces
- **Quotes**: Single quotes in JS/JSX, double quotes in JSX attributes
- **Semicolons**: Omit (handled by ESLint)
- **Imports**: React first, then third-party, then local — separated by blank lines
- **Commit messages**: Follow [Conventional Commits](https://www.conventionalcommits.org/)
