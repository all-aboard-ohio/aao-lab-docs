---
title: Contributing to AAO Data Lab
excerpt: A complete guide to contributing — from your first issue to your first merged PR.
---

# Contributing to AAO Data Lab

Welcome! AAO Data Lab is a volunteer-driven civic tech initiative building open-source tools for passenger rail advocacy in Ohio. Whether you're a developer, data analyst, designer, or researcher, there's a place for you here.

> **New contributor?** Start with the [Onboarding Checklist](./onboarding.md) before reading this guide.

## Table of Contents

- [Who Can Contribute](#who-can-contribute)
- [Ways to Contribute](#ways-to-contribute)
- [Before You Start](#before-you-start)
- [Your First Contribution](#your-first-contribution-step-by-step)
- [Working on Issues](#working-on-issues)
- [Pull Request Process](#pull-request-process)
- [Commit Message Standards](#commit-message-standards)
- [Definition of Done](#definition-of-done)
- [Code Review](#code-review)
- [Communication](#communication)
- [Getting Help](#getting-help)

---

## Who Can Contribute

Everyone is welcome. You do not need to be an expert — you need to be curious, respectful, and willing to learn. We especially welcome:

- **Students** working on capstone or independent study projects
- **Professionals** giving back through civic tech volunteering
- **Domain experts** in transit, policy, GIS, or public data analysis
- **First-time open source contributors** (we love first PRs!)

See [Volunteer Roles](./roles.md) to find where your skills fit best.

---

## Ways to Contribute

Contributing is not just writing code. You can also help by:

| Contribution Type | Where to Start |
|---|---|
| Fixing bugs | Issues labeled `bug` |
| Building features | Issues labeled `feature` or `enhancement` |
| Data analysis / cleaning | Issues labeled `data` |
| UI/UX design | Issues labeled `design` |
| Writing / improving docs | Issues labeled `documentation` |
| Research | Issues labeled `research` |
| Writing tests | Issues labeled `testing` |
| Reviewing PRs | Any open pull request |

---

## Before You Start

Make sure you have:

- [ ] A [GitHub account](https://github.com/join)
- [ ] Git installed locally (`git --version`)
- [ ] Node.js 18+ installed (`node --version`)
- [ ] Joined the [AAO Slack](https://join.slack.com/t/all-aboard-ohio/shared_invite/zt-3wgj180pu-eWAJoGn4_6~y9YHR9Lq3qA) and introduced yourself in `#welcome`
- [ ] Read the [Code of Conduct](./code-of-conduct.md)

---

## Your First Contribution (Step by Step)

### 1. Find an Issue

- Browse [open issues](https://github.com/all-aboard-ohio) and look for ones labeled **`good first issue`**
- Read the issue description thoroughly before claiming it
- Ask questions in the issue thread if anything is unclear

### 2. Claim the Issue

Comment: **"I'd like to work on this."**

A maintainer will assign it to you within 1-2 business days. **Do not open a PR for an issue not assigned to you.** If an issue has been assigned for 2+ weeks with no activity, it may be reopened for others.

### 3. Fork and Branch

```bash
# Fork the repo on GitHub, then clone your fork:
git clone https://github.com/<your-username>/<repo-name>.git
cd <repo-name>

# Add upstream so you can pull future updates:
git remote add upstream https://github.com/all-aboard-ohio/<repo-name>.git

# Create your branch:
git checkout -b feature/your-short-description
```

Branch naming conventions:

| Prefix | When to use |
|---|---|
| `feature/` | New functionality |
| `fix/` | Bug fixes |
| `docs/` | Documentation only |
| `data/` | Data processing or analysis |
| `chore/` | Maintenance, dependency updates |

### 4. Set Up Your Environment

See [Getting Started](./getting-started.md) for full environment setup instructions.

### 5. Make Your Changes

- Keep changes **focused on the issue**. One issue = one PR.
- Write clear commit messages (see [Commit Standards](#commit-message-standards))
- Add or update tests where applicable
- Test your changes locally before pushing

### 6. Open a Pull Request

```bash
git push origin feature/your-short-description
```

Then open a PR from your fork against `main` on the upstream repo.

In your PR description:
- Link the issue: `Closes #123`
- Describe what changed and why
- Include screenshots for any UI changes
- Check off every item in the PR checklist

---

## Working on Issues

### Issue Labels

| Label | Meaning |
|---|---|
| `good first issue` | Well-scoped, great for newcomers |
| `bug` | Something is broken |
| `feature` | New capability |
| `enhancement` | Improvement to existing feature |
| `documentation` | Docs, READMEs, guides |
| `data` | Data cleaning, analysis, ETL |
| `design` | UI/UX work |
| `research` | Background research needed |
| `help wanted` | Maintainers need support |
| `P0` | Critical, blocking others |
| `P1` | High priority |
| `P2` | Nice to have |
| `size: small` | ~1-2 hours |
| `size: medium` | ~3-6 hours |
| `size: large` | ~1 day or more |

### Issue Etiquette

- **Do not start work on an unassigned issue.** If you do and someone else's PR lands first, yours may not be merged.
- **Give progress updates** if you hit a blocker. A comment like "still working on this, ETA Friday" is enough.
- **Unassign yourself** if you can no longer complete the work. No judgment — it frees the issue for someone else.

---

## Pull Request Process

1. **One PR per issue.** Do not bundle unrelated changes.
2. **Keep PRs small.** Reviewers move faster on focused PRs. Aim for `size: small` or `size: medium`.
3. **Fill out the PR template completely.** Incomplete PRs will be returned.
4. **Do not submit a PR that breaks CI.** Verify all checks pass before requesting review.
5. **Respond to review feedback within 5 business days.** PRs with no response after 10 days may be closed.
6. **Squash commits before merge.** Maintainers will handle this for you if needed.

---

## Commit Message Standards

We follow [Conventional Commits](https://www.conventionalcommits.org/):

```
<type>(<optional scope>): <short description>

[optional body]

[optional footer: Closes #123]
```

### Types

| Type | When to use |
|---|---|
| `feat` | New feature |
| `fix` | Bug fix |
| `docs` | Documentation only |
| `style` | Formatting, no logic change |
| `refactor` | Code restructure, no behavior change |
| `test` | Adding or updating tests |
| `chore` | Build tooling, dependency updates |
| `data` | Data processing, cleaning, or analysis |

### Examples

```
feat(ridership-map): add county-level choropleth layer

fix(api): handle null values returned from ODOT endpoint
Closes #88

docs(contributing): clarify PR review timeline

data(census): normalize tract IDs to 11-digit FIPS format
```

---

## Definition of Done

A contribution is complete when:

- [ ] The feature or fix works as described in the issue
- [ ] No existing functionality is broken
- [ ] Tests pass locally and in CI (where applicable)
- [ ] PR description is complete, with screenshots for UI changes
- [ ] Code follows the [Style Guide](./style-guide.md)
- [ ] Any new environment variables are documented in `.env.example`
- [ ] At least one maintainer has approved the PR

---

## Code Review

Code review is a learning opportunity, not a performance evaluation. Our maintainers aim to:

- Review all PRs within **5 business days**
- Leave constructive, specific, and actionable comments
- Approve or request changes clearly, not go silent

As a contributor, please:

- Address every review comment before re-requesting review
- Ask for clarification if a comment is unclear
- Mark resolved threads after you have addressed them

---

## Communication

| Channel | Purpose |
|---|---|
| GitHub Issues | Bug reports, feature ideas, scoping discussions |
| GitHub PR comments | Code review, implementation questions |
| `#dev-general` (Slack) | General developer conversation |
| `#dev-resources` (Slack) | API keys, datasets, environment help |
| `#announcements` (Slack) | Project updates from maintainers |

**We are async-first.** Everyone here is a volunteer with a day job. Most discussions happen over 24-48 hours. That is normal and expected.

---

## Getting Help

1. **Search existing issues and PRs** — your question may already be answered.
2. **Post in `#dev-general`** on Slack with a clear description of the problem.
3. **Comment on the issue** you are working on — maintainers monitor all active issues.
4. **Tag a maintainer** in your PR if you have not heard back after 5 business days.

No question is too basic. We want you to succeed.
