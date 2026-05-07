---
title: UI & Code Style Guide
excerpt: Conventions for visual design, component architecture, accessibility, and code formatting across all AAO Data Lab projects.
---

# UI & Code Style Guide

This guide defines the look, feel, and coding standards for every AAO Data Lab project. Consistency here is what lets volunteers pick up any repository and feel at home.

---

## Design Tokens

AAO projects use a consistent set of brand colors defined as Tailwind custom tokens in `tailwind.config.js`:

| Token | Hex | Usage |
|---|---|---|
| `aao-dark-blue` | `#012345` | Primary backgrounds, headings, `<aao-site-header>` |
| `aao-dark-red` | `#B72717` | Accents, CTAs, error states, warning indicators |
| `aao-light-blue` | `#388CBB` | Links, hover states, interactive highlights |
| `aao-light-red` | `#D55855` | Secondary accents, badge backgrounds |
| `aao-beige` | `#FBF3E3` | Alternate section backgrounds, tag chips |

**Never use raw hex values in component code.** Always reference the token name. This ensures global theming works correctly.

---

## Typography

| Role | Font | Tailwind Class |
|---|---|---|
| Headings (h1–h3) | Poppins | `font-heading` |
| Body, UI labels, buttons | Montserrat | `font-body` |

Both fonts are loaded via Google Fonts in `index.html`. Do not add alternative font imports.

**Usage rules:**
- `font-heading font-extrabold` for `<h1>` page titles
- `font-heading font-bold` for `<h2>` section headers and `<h3>` card titles
- `font-body font-semibold` for buttons, labels, and navigation links
- `font-body` for all body text, descriptions, and captions

---

## Spacing & Layout

| Property | Value | Notes |
|---|---|---|
| Max content width | `max-w-7xl mx-auto` | All sections |
| Section vertical padding | `py-16 md:py-24 px-4` | Standard section spacing |
| Card border radius | `rounded-2xl` | Cards, modals, dialogs |
| Card shadow | `shadow-sm` (default) | `shadow-md hover:shadow-xl` for interactive cards |
| Grid gap | `gap-6` (default), `gap-8` (spacious) | Use `gap-8` for lg-grid layouts |

---

## Button Variants

```jsx
// Primary — main CTAs
<button className="bg-aao-dark-blue hover:bg-aao-light-blue text-white font-body font-semibold px-5 py-2.5 rounded-lg transition-colors duration-200">
  Action
</button>

// Danger / Join CTA
<button className="bg-aao-dark-red hover:bg-red-700 text-white font-body font-semibold px-5 py-2.5 rounded-lg transition-colors duration-200">
  Join Slack
</button>

// Pill CTA (for hero / community sections)
<a className="inline-flex items-center gap-2 bg-aao-light-blue hover:bg-blue-500 text-white font-body font-semibold px-6 py-3 rounded-full transition-colors duration-200">
  Get Started <ArrowRight size={18} />
</a>

// Ghost / text link
<button className="text-aao-light-blue hover:text-aao-dark-blue font-body font-semibold text-sm transition-colors duration-200">
  Learn more →
</button>
```

---

## Web Component Usage

Every page must include the AAO shared header and notification system. See the [Requirements Guide](./requirements.md) for implementation details.

```html
<!-- In index.html — loads the shared component library from CDN -->
<script type="module" src="https://all-aboard-ohio.github.io/aao-dev-components/aao-banner.js"></script>
```

```jsx
// In App.jsx or your root layout component
<aao-site-header mode="compact" dev-url="https://lab.allaboardohio.org"></aao-site-header>
<aao-notification
  config-url="https://raw.githubusercontent.com/all-aboard-ohio/aao-dev-components/main/banner.json"
></aao-notification>
```

---

## Component Conventions

### Semantic HTML
- `<section id="...">` with a meaningful `id` for all scrollable page sections
- `<article>` for card-like self-contained content items
- `<nav>` for navigation elements
- `<main>` wrapping all primary page content

### Accessibility
- All icon-only buttons must have `aria-label`
- All images must have descriptive `alt` text (or `alt=""` if purely decorative)
- Color contrast must pass WCAG AA (4.5:1 for body text, 3:1 for large text)
- Interactive elements must have visible focus rings — do not use `outline-none` without adding a custom focus style
- Use `rel="noopener noreferrer"` on all `target="_blank"` links

### Card Pattern
```jsx
// Standard card layout — pushes CTA to the bottom with flex
<div className="rounded-2xl p-6 border border-gray-100 bg-white shadow-sm hover:shadow-md transition-shadow duration-200 flex flex-col">
  {/* Icon */}
  <div className="w-11 h-11 rounded-xl flex items-center justify-center mb-4 bg-aao-light-blue/10 text-aao-light-blue">
    <SomeIcon size={22} />
  </div>
  {/* Content */}
  <h3 className="font-heading text-aao-dark-blue text-lg font-bold mb-2">Title</h3>
  <p className="font-body text-gray-600 text-sm leading-relaxed mb-4 flex-1">Description</p>
  {/* CTA pushed to bottom */}
  <a href="..." className="mt-auto ...">Action →</a>
</div>
```

### Eyebrow Label Pattern
```jsx
<p className="font-body text-aao-dark-red font-semibold text-sm uppercase tracking-widest mb-2">
  Section Category
</p>
<h2 className="font-heading text-aao-dark-blue text-3xl md:text-4xl font-extrabold mb-4">
  Section Title
</h2>
```

---

## Code Formatting

| Rule | Value |
|---|---|
| Indentation | 2 spaces |
| JS/JSX quotes | Single quotes (`'`) in logic, double quotes in JSX attributes |
| Semicolons | Omitted (ESLint handles) |
| Line length | 100 characters max |
| Import order | React → third-party → local (separated by blank lines) |
| Component files | PascalCase (`MyComponent.jsx`) |
| Utility files | camelCase (`formatRidership.js`) |
| CSS class order | Layout → sizing → color → state → animation |

---

## Data Visualization Standards

For all charts, maps, and data displays:

- **Use AAO brand colors** as your primary palette. Avoid red-green only contrast (accessibility).
- **Always label axes** — never rely on a tooltip alone to convey axis meaning.
- **Include a data source citation** below every chart: `Source: [Bureau of Transportation Statistics, 2023]`
- **Choropleth maps**: use a sequential single-hue scale (light `aao-beige` → dark `aao-dark-blue`)
- **Bar/line charts**: `aao-dark-blue` primary series, `aao-light-blue` secondary, `aao-dark-red` highlight/comparison
- **Responsive**: all visualizations must reflow or scroll gracefully on mobile — never clip data

---

## Commit Messages

Follow [Conventional Commits](https://www.conventionalcommits.org/):

```
feat(ridership-map): add county-level choropleth layer
fix(api): handle null values from ODOT endpoint
data(census): normalize tract IDs to 11-digit FIPS
docs(style-guide): add visualization standards section
```

See [Contributing Guidelines](./contributing.md) for the full type table.
