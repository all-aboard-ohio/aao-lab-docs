---
title: Project Management & GitHub Projects Board
excerpt: How we use GitHub Projects to coordinate across aao-lab-planning proposal issues and individual project implementation tasks.
---

# Project Management & GitHub Projects Board

## The Two-Tier System

AAO Data Lab uses a two-tier issue structure, both tracked on one org-level GitHub Projects board:

| Tier | Repository | What lives here |
|---|---|---|
| **Proposals** | aao-lab-planning | New tool and analysis ideas -- from concept through approval |
| **Implementation tasks** | Individual project repos | Features, bug fixes, data work for active projects |

---

## The GitHub Projects Board

The board is the canonical view of all in-flight work across the org. It auto-pulls all issues from aao-lab-planning and issues labeled (task) from each individual project repo.

Board: https://github.com/orgs/all-aboard-ohio/projects

### Status Field

| Status | Meaning |
|---|---|
| **Proposed** | Issue opened in aao-lab-planning, awaiting maintainer review |
| **Scoping** | Maintainer reviewing -- clarifying scope, disciplines needed |
| **Approved** | Scope accepted; ready for a contributor to pick up |
| **In Progress** | Repo created or issue claimed; active work underway |
| **Review** | PR open, awaiting review |
| **Shipped** | Tool deployed or analysis published; homepage updated |

### Recommended Board Views

| View | Use |
|---|---|
| Board (Kanban) | Day-to-day status overview |
| Roadmap | Timeline across milestones |
| Grouped by repository | Per-project standups |

---

## Workflow: Proposing a New Project

1. Check open issues and the board to avoid duplicates
2. Mention your idea in #projects on Slack first
3. Open an issue in aao-lab-planning using the right template (New Tool or App / New Analysis or Research)
4. Issue auto-appears on the board as Proposed
5. A maintainer moves it to Scoping and sharpens scope with you

---

## Workflow: Starting a New Repository

Once a proposal reaches Approved:

1. Create a repo from the right template:
   - aao-lab-template-tool -- React + Vite + Tailwind, AAO components, GitHub Pages deploy
   - aao-lab-template-analysis -- Python + Jupyter, standard folder structure
2. Comment the new repo URL on the planning issue; link back from the new repo README
3. Open implementation issues in the new repo labeled (task) -- they auto-populate the board

In GitHub Project settings, enable Workflows to auto-add:
- All issues from aao-lab-planning
- Issues labeled (task) from each project repo

---

## Workflow: Shipping

1. Close implementation issues in the project repo
2. Comment live URL on the planning issue and close it
3. Set board item to Shipped
4. If a deployed tool: update aao-lab-homepage src/data/projects.js to show status Live

---

## Labels (aao-lab-planning)

| Label | Description |
|---|---|
| new-tool | Web tool or app proposal |
| research | Data model or analysis proposal |
| in-scoping | Under maintainer review |
| approved | Ready for a contributor |
| good first issue | Well-scoped for a new contributor |
| needs-discipline | Blocked on finding a specific skill |
