---
title: Project Requirements Guide
excerpt: Mandatory technical requirements every AAO Data Lab project must satisfy — shared components, privacy, accessibility, and data standards.
---

# Project Requirements Guide

All AAO Data Lab projects must satisfy these requirements before being published or accepted as a pull request to a production repository. These are not suggestions — they are the minimum bar.

---

## 1. Shared Header and Notification System

Every publicly facing AAO Data Lab project must include the shared site header and notification web component from the `aao-dev-components` library.

### Loading the Library

Add this script tag to your HTML `<head>`, **before** any other scripts:

```html
<script
  type="module"
  src="https://all-aboard-ohio.github.io/aao-dev-components/aao-banner.js"
></script>
```

### Required Elements

Both of these elements must appear in your app root, **before** any page content:

```jsx
<aao-site-header
  mode="compact"
  dev-url="https://lab.allaboardohio.org"
></aao-site-header>

<aao-notification
  config-url="https://raw.githubusercontent.com/all-aboard-ohio/aao-dev-components/main/banner.json"
></aao-notification>
```

**Why this matters:** The shared header ensures every tool is identifiably part of the AAO Data Lab ecosystem. The notification component lets maintainers broadcast updates, maintenance windows, and announcements to all tools simultaneously without a code deploy.

### Header Modes

| Mode | When to Use |
|---|---|
| `compact` | Standard pages — a slim persistent banner without site nav |
| `standard` | Full-width branded header with navigation links |
| `footer` | Placed at the bottom of the page for attribution/footer branding |

---

## 2. Privacy and Data Handling

AAO Data Lab tools handle **no personal user data**. This is not a feature limitation — it is a core design constraint.

### What This Means in Practice

- **No user accounts or authentication** unless explicitly scoped and approved by maintainers
- **No cookies** beyond essential session state (and none at all if the project has no session)
- **No analytics trackers** (no Google Analytics, Meta Pixel, or similar third-party tracking scripts)
- **No forms that collect names, emails, phone numbers, or addresses** unless the project is explicitly a contact/intake tool approved for that purpose
- **No API calls that transmit user-identifiable data** to third-party services
- **No local storage of user behavior data**

### What Is Allowed

- Caching public API responses in `sessionStorage` or `localStorage` (no personal data, maximum 24-hour TTL)
- Logging aggregated, anonymized usage counts (e.g., "this page was loaded") via server-side logging only — no client-side analytics library
- Storing user-chosen UI preferences (e.g., dark mode) in `localStorage` with the key clearly namespaced (`aao-pref-*`)

### Environment Variables

Secrets must never be committed to the repository. Always:

1. Copy `.env.example` to `.env.local` (gitignored)
2. Document every required variable in `.env.example` with a description comment
3. Validate that required environment variables are present at startup

```bash
# .env.example
VITE_MAPBOX_TOKEN=       # Get from #dev-resources on Slack
VITE_SUPABASE_URL=       # Get from #dev-resources on Slack
VITE_SUPABASE_ANON_KEY=  # Get from #dev-resources on Slack
```

---

## 3. Accessibility

All AAO Data Lab tools must meet **WCAG 2.1 Level AA** accessibility standards.

### Mandatory Checks

- [ ] Color contrast: 4.5:1 for body text, 3:1 for large text (18px+ or 14px+ bold)
- [ ] All images have meaningful `alt` text (`alt=""` for decorative images)
- [ ] All form inputs have associated `<label>` elements
- [ ] All icon-only interactive elements have `aria-label`
- [ ] Keyboard navigation works for all interactive elements (tab order, focus management)
- [ ] No element uses `outline: none` without a custom visible focus style
- [ ] All `target="_blank"` links include `rel="noopener noreferrer"`
- [ ] Page has a single `<h1>`, with logical heading hierarchy below it
- [ ] All data visualizations have text alternatives (table, caption, or description)

Use [axe DevTools](https://www.deque.com/axe/) browser extension to run an automated check before submitting a PR.

---

## 4. Responsive Design

All tools must work on screens from 320px wide upward.

- Build **mobile-first**: use Tailwind base classes for mobile, then `sm:`, `md:`, `lg:` breakpoints for larger screens
- Test at 375px (iPhone SE), 768px (tablet), 1280px (laptop), and 1920px (desktop)
- Tables and data grids must scroll horizontally on small screens — never clip content
- Maps must not lock viewport scroll on mobile (use two-finger gesture requirements or a dedicated drawer UI)

---

## 5. Performance

| Metric | Target |
|---|---|
| Lighthouse Performance | ≥ 85 on desktop |
| Largest Contentful Paint | < 2.5 seconds |
| Total Blocking Time | < 300ms |
| Bundle Size (initial JS) | < 250 KB compressed |

- Lazy-load images and below-the-fold sections
- No unused third-party libraries in the production bundle
- Use `vite build --minify` for all production builds
- Compress all static image assets before committing (use `squoosh.app` or `sharp`)

---

## 6. Code Quality

### Linting and Formatting

All JS/JSX/TS must pass ESLint with no errors. Run before every PR:

```bash
npm run lint
```

For Python projects, all files must pass `flake8` and `black`:

```bash
flake8 .
black --check .
```

### Testing

- Unit tests required for all utility functions and data transformation logic
- Integration tests required for all API endpoints
- Test coverage must not regress — do not submit a PR that lowers coverage
- Run tests locally before opening a PR: `npm test` or `pytest`

---

## 7. Documentation

Every project repository must include:

- [ ] `README.md` with: project description, local setup instructions, and a link back to [lab.allaboardohio.org](https://lab.allaboardohio.org)
- [ ] `CONTRIBUTING.md` linking to [aao-dev-docs contributing guidelines](https://github.com/all-aboard-ohio/aao-dev-docs/blob/main/contributing.md)
- [ ] `.env.example` documenting all required environment variables
- [ ] Inline comments for any non-obvious logic (the "why", not the "what")

---

## 8. Branch and Merge Standards

- **Never commit directly to `main`** — all changes come through pull requests
- PRs must have at least **one maintainer approval** before merging
- All CI checks (lint, test, build) must pass before merge
- PR titles must follow Conventional Commits format

See [Contributing Guidelines](./contributing.md) for the full PR and branch naming guide.
