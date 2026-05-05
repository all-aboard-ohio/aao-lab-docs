---
title: Contributing Guidelines
excerpt: How to open issues, submit pull requests, and follow the code review process for AAO projects.
---

# Contributing Guidelines

## Code of Conduct

All contributors are expected to follow our [Code of Conduct](https://github.com/all-aboard-ohio). Be respectful, inclusive, and constructive.

## Opening an Issue

Before writing code, open a GitHub Issue to describe what you want to build or fix. Use the appropriate issue template:

- 🐛 **Bug Report** — Something is broken.
- ✨ **Feature Request** — A new capability you'd like to see.
- 📖 **Documentation** — Improvements to docs or READMEs.
- 💬 **Discussion** — General questions or ideas.

## Pull Request Process

1. **Branch naming**: `feature/<short-description>`, `fix/<short-description>`, `docs/<short-description>`
2. **Commit style**: Use [Conventional Commits](https://www.conventionalcommits.org/) — e.g., `feat: add ridership chart component`
3. **Tests**: Include unit tests for new logic. Use Vitest for React projects.
4. **PR description**: Link the related issue, describe what changed, and attach screenshots if UI is affected.
5. **Review**: At least one maintainer approval is required before merge.

## Branch Protection

The `main` branch is protected. All changes must come through a PR. Direct pushes are not permitted.
