# CLAUDE.md — AAO Lab Docs

Instructions for Claude when working in the `aao-lab-docs` repository.

---

## What This Repo Is

`aao-lab-docs` contains the contributor documentation for **AAO Data Lab** (All Aboard Ohio Data Lab). Every `.md` file is automatically fetched and rendered on [lab.allaboardohio.org](https://lab.allaboardohio.org) in the Dev Docs section.

This is a documentation-only repository — no application code, no `package.json`, no build step. Changes here are live as soon as they are merged to `main`.

---

## The Project

**AAO Data Lab** is a volunteer civic tech initiative building open-source tools that support the case for investing in passenger rail and connected public transit in Ohio and beyond.

### Core framing (always apply this)

- **Economics and quality of life** are the argument — commute times, job access, housing costs, regional GDP, fiscal outcomes for connected municipalities
- **Rail is the spine; transit is the system** — the tools cover intercity rail, local buses/BRT, bike infrastructure, and station-area development
- **Reusable beyond Ohio** — data pipelines and models are designed to be parameterized for any corridor or state
- **Visualization-first** — the best analysis means nothing if it cannot be communicated; every tool prioritizes legibility and shareability

### What to avoid

- Do not frame transit advocacy in primarily environmental terms — that is not our angle
- Do not reference personal data collection, user tracking, or analytics — all tools are privacy-first
- Do not use deprecated repo names: `aao-dev-components` → `aao-lab-components`, `aao-dev-docs` → `aao-lab-docs`, `aao-dev-homepage` → `aao-lab-homepage`

---

## Repository Layout

```
README.md               ← Docs index (three sections: Start Here / Contributing / Reference)
mission-ethos.md        ← Philosophy, rail+multimodal vision, disciplines table
onboarding.md           ← 4-step checklist for new contributors
roles.md                ← 7 volunteer disciplines with skills and progression paths
code-of-conduct.md      ← Contributor Covenant v2.1 adapted for AAO
getting-started.md      ← Local dev setup: React/Vite + Python/FastAPI + Jupyter
contributing.md         ← Full contribution workflow, issue labels, Conventional Commits, DoD
requirements.md         ← Mandatory standards: shared header/notification, privacy, a11y, perf
style-guide.md          ← Design tokens, typography, component patterns, data viz standards
architecture.md         ← Repo structure and system design patterns
tool-stack.md           ← Tech stack, external data sources, env variables
academic-guide.md       ← For professors and students using AAO challenges as coursework
.github/
  copilot-instructions.md  ← GitHub Copilot workspace instructions
CLAUDE.md                  ← This file
```

---

## Writing Guidelines

### Format

- All docs use Markdown with optional YAML frontmatter:
  ```yaml
  ---
  title: Display Title
  excerpt: One sentence used as the card preview on the homepage.
  ---
  ```
- File names: lowercase, hyphenated (`getting-started.md`), no spaces
- Cross-link with relative paths: `[Contributing Guidelines](./contributing.md)`
- Update `README.md` whenever a new file is added

### Style

- **Plain language first.** Write for a capable newcomer — a first-year CS student or a policy researcher with no coding background.
- **Tables for options and reference data.** Never write a wall of bullets when a table is cleaner.
- **Numbered steps for sequences.** Ordered lists (`1.`, `2.`) for anything that must happen in order.
- **Code blocks with language tags** for all commands, config, and code samples.
- **Active voice.** "Run `npm install`" — not "Dependencies can be installed by running…"
- **Start with the useful content.** No filler paragraphs before the first heading.

---

## Key Technical Details

### Shared web components (required on every public AAO tool)

```html
<script type="module" src="https://all-aboard-ohio.github.io/aao-lab-components/aao-banner.js"></script>
```

```jsx
<aao-site-header mode="compact" dev-url="https://lab.allaboardohio.org"></aao-site-header>
<aao-notification
  config-url="https://raw.githubusercontent.com/all-aboard-ohio/aao-lab-components/main/banner.json"
></aao-notification>
```

### Brand tokens

| Token | Hex | Use |
|---|---|---|
| `aao-dark-blue` | `#012345` | Backgrounds, headings |
| `aao-dark-red` | `#B72717` | CTAs, accents |
| `aao-light-blue` | `#388CBB` | Links, hover states |
| `aao-beige` | `#FBF3E3` | Alternate section backgrounds |

### Commit format

```
<type>(<scope>): <description>
```

Types: `feat`, `fix`, `docs`, `style`, `refactor`, `test`, `chore`, `data`

---

## Volunteer Disciplines

AAO Data Lab has contributors across 7 disciplines — all are considered in documentation:

1. **Software Developers** — React, Python, Node, APIs, maps
2. **Data Analysts / Engineers** — pandas, geopandas, Jupyter, dbt, SQL
3. **UI/UX Designers** — Figma, WCAG 2.1, design systems
4. **Policy Analysts** — legislative context, source credibility, framing
5. **Researchers** — literature review, comparable programs, citations
6. **Project Managers / Coordinators** — issue scoping, milestones, cross-discipline coordination
7. **Technical Writers / Communicators** — docs, READMEs, outreach materials

When drafting documentation that has discipline-specific content (e.g., a new role, a new workflow), make sure it is scoped correctly and does not assume all contributors are developers.

---

## Common Tasks

### Add a new doc

1. Create `new-topic.md` with frontmatter (`title` + `excerpt`)
2. Add it to the correct section in `README.md`
3. Cross-link from any related existing docs
4. Commit with `docs(new-topic): add initial draft`

### Update an existing doc

1. Read the current file content before making changes
2. Preserve frontmatter — only update `excerpt` if the doc's purpose meaningfully changes
3. Check for cross-references in other files that may need updating
4. Commit with `docs(<filename>): <what changed and why>`

### Fix a broken reference

Search for old repo names with:
```powershell
Select-String -Path "*.md" -Pattern "aao-dev-components|aao-dev-docs|aao-dev-homepage"
```
Replace all matches with the `aao-lab-*` equivalents.
