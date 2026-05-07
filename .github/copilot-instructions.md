# GitHub Copilot Instructions — AAO Lab Docs

This repository contains the contributor documentation for **AAO Data Lab** (All Aboard Ohio Data Lab), a volunteer-driven civic technology initiative building open-source tools for passenger rail and connected mobility advocacy.

Every `.md` file in this repo is automatically fetched and rendered in the Dev Docs section of [lab.allaboardohio.org](https://lab.allaboardohio.org) via the GitHub Contents API.

---

## Project Context

**What AAO Data Lab builds:** Interactive visualizations, economic models, ridership analyses, and dashboards that help advocates, government officials, and the public make the case for investing in passenger rail and connected public transit.

**Mission framing:** Focus on economic impact and quality of life — commute times, housing costs, job access, regional GDP, and fiscal outcomes for connected communities. Rail is the spine, but the tools cover the full multimodal system (local transit, bike infrastructure, station-area walkability). Tools are designed to be reusable beyond Ohio.

**What to avoid in documentation:**
- Do not frame transit benefits primarily in environmental terms — focus on economics and quality of life
- Do not reference personal user data collection — all tools are privacy-first, zero tracking
- Do not use the old names: `aao-dev-components`, `aao-dev-docs`, `aao-dev-homepage` — use `aao-lab-components`, `aao-lab-docs`, `aao-lab-homepage`

---

## Repository Structure and Doc Conventions

### Frontmatter

Every doc should begin with YAML frontmatter used for display on the homepage:

```yaml
---
title: Short Display Title
excerpt: One sentence shown as the card preview on the homepage.
---
```

If a doc has no frontmatter, the homepage derives the title from the first `# heading` and the excerpt from the first non-heading paragraph.

### File Naming

- Lowercase, hyphenated: `getting-started.md`, `mission-ethos.md`
- No spaces or underscores in filenames
- Descriptive and specific — a new contributor should know what a file contains from the name alone

### Writing Style

- **Plain language.** Write for a first-year computer science student or a policy researcher with no coding background. Explain jargon the first time it appears.
- **Tables for reference data.** Use Markdown tables for comparisons, option lists, and parameter documentation.
- **Numbered steps for procedures.** Use ordered lists (`1.`, `2.`, `3.`) for anything sequential.
- **Code blocks for all commands and code.** Always specify the language (` ```bash `, ` ```jsx `, ` ```yaml `).
- **Active voice.** "Run `npm install`" not "Dependencies should be installed by running `npm install`."
- **No filler.** Do not add a "Getting Started" preamble to every doc. Start with the useful content.

---

## Docs Inventory

| File | Purpose |
|---|---|
| `README.md` | Docs index — links to all other files in three groups |
| `mission-ethos.md` | Project philosophy, transit system vision, disciplines table |
| `onboarding.md` | 4-step checklist for new contributors |
| `roles.md` | 7 volunteer disciplines with skills, good first issues, progression |
| `code-of-conduct.md` | Contributor Covenant v2.1 adapted for AAO |
| `getting-started.md` | Local dev setup (React/Vite + Python/FastAPI) |
| `contributing.md` | Full contribution workflow, PR process, Conventional Commits |
| `requirements.md` | Mandatory standards: shared header, privacy, accessibility, perf |
| `style-guide.md` | Design tokens, typography, components, data viz standards |
| `architecture.md` | Repo structure and system design patterns |
| `tool-stack.md` | Tech stack, external APIs, environment variables |
| `academic-guide.md` | For professors and capstone students |

---

## Technical Standards Referenced in Docs

### Shared Components (Required on Every Project)

```html
<!-- In index.html -->
<script type="module" src="https://all-aboard-ohio.github.io/aao-lab-components/aao-banner.js"></script>
```

```jsx
// In root layout
<aao-site-header mode="compact" dev-url="https://lab.allaboardohio.org"></aao-site-header>
<aao-notification
  config-url="https://raw.githubusercontent.com/all-aboard-ohio/aao-lab-components/main/banner.json"
></aao-notification>
```

### Brand Colors (Tailwind Tokens)

| Token | Hex |
|---|---|
| `aao-dark-blue` | `#012345` |
| `aao-dark-red` | `#B72717` |
| `aao-light-blue` | `#388CBB` |
| `aao-beige` | `#FBF3E3` |

### Commit Convention

```
feat|fix|docs|style|refactor|test|chore|data(<scope>): <description>
```

---

## When Writing or Editing a Doc

1. Check whether the topic is already covered in another file before creating a new one
2. Add or update YAML frontmatter to keep the homepage card preview accurate
3. If adding a new file, update `README.md` to include it in the appropriate section
4. Cross-link related docs using relative paths: `[Contributing Guidelines](./contributing.md)`
5. Run a quick spell-check and review for old repo names before committing
