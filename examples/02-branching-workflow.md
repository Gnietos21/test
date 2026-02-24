# Example 2: Feature Branching Workflow

The most important habit in professional development: **never work directly on main**.

## Why Branches Matter

Imagine two developers working on the same project:
- Alice is adding a payment feature
- Bob is fixing a login bug

If both work on `main`, their changes constantly conflict. Branches solve this.

```
main ─────────────────────────────────────── (always stable)
       │                         │
       └── feature/payment ──────┘  (Alice's work, merged when done)
       │                         │
       └── fix/login-bug ────────┘  (Bob's work, merged when done)
```

## The Workflow

### Create a branch

```bash
# Always branch from an up-to-date main
git checkout main
git pull origin main

# Create and switch to your feature branch
git checkout -b feature/user-notifications
```

### Work on your branch

```bash
# ... make changes ...
git add .
git commit -m "feat: add email notification on new message"

# ... more changes ...
git add .
git commit -m "feat: add in-app notification badge"
```

### Push and open a PR

```bash
git push -u origin feature/user-notifications
# GitHub will show a "Compare & pull request" button
```

### After merge, clean up

```bash
git checkout main
git pull origin main
git branch -d feature/user-notifications   # delete local branch
```

## With Claude Code

```bash
# 1. Create the branch
git checkout -b feature/user-notifications

# 2. Open Claude Code
claude

# 3. Describe the full feature
> I need to add user notifications.
> When a user gets a new message, they should:
> 1. Get an email (use the existing EmailService)
> 2. See a red badge on the bell icon in the nav
> Look at the existing codebase and implement this end-to-end.

# Claude will explore the codebase, understand the patterns, and build it.

# 4. Test and commit
> /commit
git push -u origin feature/user-notifications
```

## Key Rules

| Rule | Why |
|---|---|
| Never commit directly to `main` | Keeps main stable and deployable |
| Keep branches focused | One feature/fix per branch |
| Pull from main before branching | Avoid merge conflicts |
| Delete branches after merging | Keeps the repo tidy |
