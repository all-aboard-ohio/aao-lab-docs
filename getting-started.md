---
title: Getting Started
excerpt: Set up your local development environment and make your first contribution to AAO Data Lab.
---

# Getting Started

This guide walks you through everything you need to run AAO Data Lab projects locally and submit your first contribution.

> Already set up? Head to [Contributing Guidelines](./contributing.md) to find and claim your first issue.

---

## Prerequisites

| Tool | Version | How to check |
|---|---|---|
| Git | Any recent | `git --version` |
| Node.js | 18 or higher | `node --version` |
| npm | 9+ (bundled with Node) | `npm --version` |
| Python | 3.10+ (data projects only) | `python --version` |

We recommend [VS Code](https://code.visualstudio.com/) with these extensions:

- **ESLint** — JavaScript linting
- **Prettier** — code formatting
- **Tailwind CSS IntelliSense** — autocomplete for utility classes
- **GitLens** — enhanced Git history

---

## Step 1 — Join the Community

1. [Join the AAO Slack workspace](https://join.slack.com/t/all-aboard-ohio/shared_invite/zt-3wgj180pu-eWAJoGn4_6~y9YHR9Lq3qA)
2. Introduce yourself in `#welcome` — your background and what you want to build
3. Join `#dev-general` and `#dev-resources`
4. Request any API keys you need in `#dev-resources`

---

## Step 2 — Fork and Clone

1. Go to the [All Aboard Ohio GitHub organization](https://github.com/all-aboard-ohio)
2. Open the repo you want to contribute to
3. Click **Fork** then **Create fork** to copy it to your account
4. Clone your fork:

```bash
git clone https://github.com/<your-username>/<repo-name>.git
cd <repo-name>
```

5. Add the upstream remote so you can pull future changes:

```bash
git remote add upstream https://github.com/all-aboard-ohio/<repo-name>.git
git remote -v   # should show both origin and upstream
```

---

## Step 3 — Install Dependencies

### React / Vite projects (frontend)

```bash
npm install
cp .env.example .env.local
```

Open `.env.local` and fill in the required values. Get API keys from `#dev-resources` on Slack.

### Python / data projects

```bash
python -m venv venv
source venv/bin/activate       # macOS / Linux
venv\Scripts\activate          # Windows

pip install -r requirements.txt
cp .env.example .env
```

---

## Step 4 — Run Locally

### AAO Data Lab homepage (React / Vite)

```bash
npm run dev
# Open http://localhost:5173
```

### FastAPI backend

```bash
uvicorn main:app --reload
# Open http://localhost:8000/docs for the interactive API explorer
```

### Jupyter notebooks (data projects)

```bash
jupyter lab
# Opens in your browser automatically
```

---

## Step 5 — Create a Branch

Never commit directly to `main`. Always create a branch:

```bash
git checkout -b feature/your-short-description
```

See [Contributing Guidelines](./contributing.md) for branch naming conventions.

---

## Step 6 — Stay in Sync

As the project evolves, keep your fork's `main` up to date:

```bash
git fetch upstream
git checkout main
git merge upstream/main
git push origin main
```

Do this regularly — especially before creating a new branch or opening a PR.

---

## Step 7 — Open Your First PR

When your work is ready:

```bash
git add .
git commit -m "feat: describe what you changed"
git push origin feature/your-short-description
```

Go to GitHub. You should see a banner offering to open a pull request. Click it, fill in the PR template, and submit.

See [Contributing Guidelines](./contributing.md) for the full PR process and merge criteria.

---

## Troubleshooting

**`npm install` fails with a Node version error**

Use [nvm](https://github.com/nvm-sh/nvm) (Linux/macOS) or [nvm-windows](https://github.com/coreybutler/nvm-windows) to switch Node versions:

```bash
nvm install 18
nvm use 18
npm install
```

**Port 5173 is already in use**

```bash
npm run dev -- --port 5174
```

**Environment variable not found at runtime**

Make sure you copied `.env.example` to `.env.local` (not just edited the example file) and restarted the dev server.

**Python module not found**

Make sure your virtual environment is active (`which python` should point inside your `venv/` folder) and that you ran `pip install -r requirements.txt` after activating it.

**Something else?**

Post in `#dev-general` on Slack with a clear description of what command you ran and what error you saw. Screenshots are very helpful.
