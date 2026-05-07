---
title: Architecture & Design Patterns
excerpt: Recommended architecture patterns, component design principles, state management approaches, and platform deployment guidelines.
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

---

## Deployment & Platform

### Hosting: GitHub Pages First

The preferred deployment target for all AAO Data Lab projects is **GitHub Pages**. It is free, version-controlled, and requires no ongoing infrastructure management. Use it whenever the project can be served as a static site.

| Project Type | Preferred Deployment |
|---|---|
| Static sites, landing pages | GitHub Pages |
| React / Vite SPAs (no backend) | GitHub Pages |
| Tools requiring a database or server | Google Cloud (see below) |

**Deploy to GitHub Pages via GitHub Actions:**

```yaml
# .github/workflows/deploy.yml
name: Deploy to GitHub Pages
on:
  push:
    branches: [main]
jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-node@v4
        with:
          node-version: 20
      - run: npm ci
      - run: npm run build
      - uses: peaceiris/actions-gh-pages@v4
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: ./dist
```

Set `base` in `vite.config.js` to match the repo name if deploying to a `*.github.io/<repo>` URL. For custom subdomains (see below) no base path adjustment is needed.

---

### Database & Backend: Google Cloud

When a project genuinely requires persistent storage or serverside logic, Google Cloud Platform is the approved infrastructure:

| Need | GCP Service |
|---|---|
| Relational data | **Cloud SQL** (PostgreSQL) |
| Document / flexible data | **Firestore** |
| Serverless API | **Cloud Run** (containerized) |
| File / asset storage | **Cloud Storage** |

GCP usage carries real cost. Any project that requires paid infrastructure **must** include the AAO donation component (see below) to help the organization offset those costs.

---

### Donation Component Requirement

Projects running on paid infrastructure are required to integrate the `<aao-donation>` Web Component from [`aao-lab-components`](https://github.com/all-aboard-ohio/aao-lab-components). This keeps the project transparent about its operational costs and gives users a direct way to support it.

```html
<!-- Load from CDN -->
<script
  type="module"
  src="https://all-aboard-ohio.github.io/aao-lab-components/aao-donation.js"
></script>

<!-- Place in your layout — typically footer or sidebar -->
<aao-donation></aao-donation>
```

If the `<aao-donation>` component does not yet exist in `aao-lab-components`, open an issue in that repo to request it before launching on paid infrastructure.

---

### Subdomain Hosting

Live projects can be served under the `lab.allaboardohio.org` domain hierarchy:

```
lab.allaboardohio.org                 ← Data Lab homepage
stations.lab.allaboardohio.org        ← example project subdomain
ridership.lab.allaboardohio.org       ← example project subdomain
```

**To request a subdomain:**

1. Build and deploy your project (GitHub Pages or GCP).
2. Post a request in the **#infrastructure** channel on the [AAO Slack](https://join.slack.com/t/all-aboard-ohio/shared_invite/zt-3wgj180pu-eWAJoGn4_6~y9YHR9Lq3qA) with:
   - Requested subdomain (e.g. `stations.lab.allaboardohio.org`)
   - Deployment URL the subdomain should point to
   - Project GitHub repo link
3. A maintainer will configure the DNS record and confirm in the thread.

> Subdomain requests are reviewed on a rolling basis. There is no formal SLA, but most requests are handled within a few days.

