# GitHub + Claude Code: A Practical Guide

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![Made with Claude Code](https://img.shields.io/badge/Made%20with-Claude%20Code-blueviolet)](https://docs.anthropic.com/en/docs/claude-code)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](CONTRIBUTING.md)

A comprehensive, hands-on reference for developers learning to use **GitHub** and **Claude Code** together effectively. Covers core concepts, real workflows, prompt patterns, and professional best practices — from your first commit to shipping production features.

---

## Table of Contents

1. [What Is This?](#what-is-this)
2. [Core Concepts](#core-concepts)
3. [Setting Up Your Environment](#setting-up-your-environment)
4. [GitHub Workflow](#github-workflow)
5. [Claude Code Workflow](#claude-code-workflow)
6. [Working Together: GitHub + Claude Code](#working-together-github--claude-code)
7. [What You Can Build](#what-you-can-build)
8. [Best Practices](#best-practices)
9. [Common Commands Reference](#common-commands-reference)
10. [Example Workflows](#example-workflows)

---

## What Is This?

This repository is a **living guide** — a structured reference you can return to at any stage of your development journey. Whether you are committing code for the first time or looking to tighten up your workflow, this guide covers the essentials.

| Topic | Coverage |
|---|---|
| **GitHub** | Version control, branching, pull requests, collaboration |
| **Claude Code** | AI-assisted coding in the terminal, slash commands, prompt patterns |
| **Combined Workflow** | End-to-end feature development using both tools together |
| **Best Practices** | Commit conventions, PR standards, security habits, code review |

### Who This Is For

- Developers new to GitHub who want to build good habits from day one
- Developers already using GitHub who want to add Claude Code to their workflow
- Teams looking for a shared reference on conventions and best practices

---

## Core Concepts

### GitHub

| Concept | What It Means |
|---|---|
| **Repository (repo)** | A folder that tracks all versions of your project |
| **Commit** | A saved snapshot of your changes with a description |
| **Branch** | A parallel version of your code to work on features safely |
| **Pull Request (PR)** | A request to merge your branch into another, with review |
| **Fork** | Your own copy of someone else's repository |
| **Clone** | Downloading a repo to your local machine |
| **Push / Pull** | Sending your changes to GitHub / Getting changes from GitHub |
| **Merge** | Combining changes from one branch into another |

### Claude Code

| Concept | What It Means |
|---|---|
| **Claude Code** | An AI assistant that lives in your terminal and understands your codebase |
| **Context** | The files and conversation Claude uses to understand your project |
| **Tool use** | Claude can read files, run commands, edit code, search the web |
| **Slash commands** | Built-in shortcuts like `/commit`, `/help`, `/review-pr` |
| **Hooks** | Shell commands that run automatically on events (e.g., before a commit) |
| **MCP Servers** | Extensions that give Claude new capabilities (databases, APIs, etc.) |

---

## Setting Up Your Environment

### 1. Install Git

```bash
# macOS
brew install git

# Ubuntu/Debian
sudo apt install git

# Windows — download from: https://git-scm.com
```

### 2. Configure Git

```bash
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
```

### 3. Install Claude Code

```bash
npm install -g @anthropic-ai/claude-code
```

### 4. Authenticate Claude Code

```bash
claude
# Follow the prompts to log in with your Anthropic account
```

### 5. Start Claude Code in a Project

```bash
cd your-project
claude
```

---

## GitHub Workflow

The standard GitHub flow for any project:

```
main branch (stable, production-ready)
    |
    └── feature/my-new-feature  (your working branch)
            |
            ├── commit: "add login form"
            ├── commit: "validate email input"
            └── Pull Request → reviewed → merged into main
```

### Step-by-Step

```bash
# 1. Clone a repo to your machine
git clone https://github.com/username/repo-name.git
cd repo-name

# 2. Create a new branch for your work
git checkout -b feature/my-feature

# 3. Make changes, then stage them
git add filename.txt         # stage a specific file
git add .                    # stage all changed files

# 4. Commit with a clear message
git commit -m "add user authentication with JWT tokens"

# 5. Push your branch to GitHub
git push -u origin feature/my-feature

# 6. Open a Pull Request on GitHub.com
# Go to your repo → "Compare & pull request" button

# 7. After review and approval, merge into main
```

### Branch Naming Conventions

```
feature/user-authentication     # new features
fix/login-redirect-bug          # bug fixes
docs/update-api-reference       # documentation only
refactor/extract-auth-service   # code restructuring
chore/update-dependencies       # maintenance tasks
```

---

## Claude Code Workflow

### Starting a Session

```bash
# Open Claude Code in your project directory
claude

# Ask it to understand your codebase first
> Explore this codebase and give me an overview of how it's structured
```

### Core Things You Can Ask Claude Code

**Understand code:**
```
> Explain how authentication works in this project
> Where is the database connection configured?
> What does the processPayment function do?
```

**Write code:**
```
> Add a function to validate email addresses in src/utils.js
> Create a REST endpoint for user profile updates
> Write unit tests for the Cart component
```

**Fix bugs:**
```
> I'm getting a TypeError on line 42 of server.js — can you fix it?
> The login form doesn't redirect after success, find out why
```

**Refactor:**
```
> Refactor the UserService class to use dependency injection
> Extract the email validation logic into a shared utility
```

**Git operations:**
```
> /commit        — Claude writes a commit message and commits for you
> /review-pr     — Claude reviews an open pull request
```

### Slash Commands

| Command | What It Does |
|---|---|
| `/help` | Show available commands and features |
| `/commit` | Stage, write, and commit your changes |
| `/review-pr <number>` | Review a GitHub pull request |
| `/clear` | Clear conversation context |
| `/compact` | Summarize conversation to save context |
| `/fast` | Toggle fast mode |
| `/cost` | Show token usage for this session |

---

## Working Together: GitHub + Claude Code

Here is a complete real-world workflow combining both tools:

### Scenario: Adding a New Feature

```bash
# 1. Start with a fresh branch
git checkout -b feature/user-profile-page

# 2. Open Claude Code
claude

# 3. Describe what you want to build
> I need to add a user profile page.
> It should show the user's name, email, avatar, and recent activity.
> Use the existing patterns in this codebase.

# Claude reads your code, understands patterns, and writes the feature.

# 4. Review what Claude wrote, test it
npm test

# 5. Commit using Claude's slash command
> /commit

# Claude analyzes all changes and writes a descriptive commit message automatically.

# 6. Push your branch
git push -u origin feature/user-profile-page

# 7. Create a PR on GitHub, then have Claude review it
> /review-pr 42
```

### Scenario: Fixing a Bug from a GitHub Issue

```bash
# 1. Read the issue on GitHub
# Issue #87: "Users can't reset their password if email has capital letters"

# 2. Create a fix branch
git checkout -b fix/password-reset-case-sensitivity

# 3. Ask Claude to investigate
> There's a bug where password reset fails if the email has capital letters.
> Find where email comparison happens and fix it.

# Claude searches the codebase, finds the bug, and fixes it.

# 4. Verify the fix
> Write a test that covers the capital letter edge case

# 5. Commit and push
> /commit
git push -u origin fix/password-reset-case-sensitivity
```

---

## What You Can Build

With GitHub + Claude Code you can build virtually anything. Here are common project types and how Claude Code helps:

### Web Applications
- Claude understands React, Vue, Angular, Next.js, and more
- Can scaffold components, pages, API routes, and database models
- Helps debug frontend/backend integration issues

### APIs and Backend Services
- Writes REST and GraphQL endpoints
- Handles authentication, middleware, and error handling
- Understands Express, FastAPI, Django, Rails, and more

### Command-Line Tools
- Builds CLI apps with argument parsing
- Adds shell completion, config files, and help docs

### Data Scripts and Automation
- Writes scripts to process files, call APIs, transform data
- Automates repetitive workflows with scheduled jobs

### Browser Extensions, Mobile Apps, Games
- Claude adapts to whatever tech stack you're using

---

## Best Practices

### With Git and GitHub

**Commit often and clearly:**
```bash
# Bad
git commit -m "stuff"
git commit -m "fix"

# Good
git commit -m "fix: handle empty cart state in checkout flow"
git commit -m "feat: add pagination to product listing page"
```

**Use Conventional Commits format:**
```
feat:     a new feature
fix:      a bug fix
docs:     documentation changes only
style:    formatting, no logic change
refactor: code change that neither fixes nor adds
test:     adding or fixing tests
chore:    build process or tooling changes
```

**Never commit secrets:**
```bash
# Add a .gitignore for sensitive files
echo ".env" >> .gitignore
echo "*.pem" >> .gitignore
echo "secrets.json" >> .gitignore
```

**Keep branches short-lived:**
- A branch should represent one unit of work
- Merge frequently to avoid large, painful conflicts

**Write good PR descriptions:**
- What changed and why
- How to test it
- Screenshots for UI changes
- Reference the issue it closes: `Closes #42`

---

### With Claude Code

**Give context, not just commands:**
```
# Less effective
> Add a button

# More effective
> Add a "Save Draft" button to the post editor (src/components/Editor.jsx).
> It should call the /api/posts/draft endpoint and show a success toast.
> Match the style of the existing "Publish" button.
```

**Read before you ask Claude to write:**
- Ask Claude to explore and explain before making big changes
- This helps Claude match your existing patterns

**Review everything Claude writes:**
- Claude is very good but not perfect
- Run tests, read the diff, understand the changes
- You are responsible for the code in your repo

**Use Claude for exploration:**
```
> What's the most complex part of this codebase?
> Where are the performance bottlenecks likely to be?
> How is error handling done across this project?
```

**Iterate in conversation:**
```
> Generate the component
> Now add loading and error states
> Now write tests for it
> Now make it accessible (add ARIA labels)
```

**Let Claude handle boilerplate:**
- Tests, configuration files, type definitions, documentation
- These are tedious for humans but easy for Claude

---

## Common Commands Reference

### Git Essentials

```bash
git init                          # initialize a new repo
git clone <url>                   # copy a remote repo locally
git status                        # see what's changed
git diff                          # see exact line-by-line changes
git add <file>                    # stage a file
git add .                         # stage all changes
git commit -m "message"           # commit staged changes
git push origin <branch>          # push to remote
git pull origin <branch>          # pull latest from remote
git checkout -b <branch>          # create and switch to new branch
git checkout <branch>             # switch to existing branch
git merge <branch>                # merge branch into current
git log --oneline                 # see commit history
git stash                         # temporarily save uncommitted work
git stash pop                     # restore stashed work
```

### GitHub CLI (`gh`)

```bash
gh repo create                    # create a new repo
gh pr create                      # create a pull request
gh pr list                        # list open PRs
gh pr view <number>               # view a PR
gh pr merge <number>              # merge a PR
gh issue create                   # create an issue
gh issue list                     # list open issues
gh issue close <number>           # close an issue
```

### Claude Code

```bash
claude                            # start Claude Code in current directory
claude "explain this codebase"    # start with a prompt
/help                             # show all commands
/commit                           # commit changes
/review-pr <number>               # review a pull request
/clear                            # clear context
/cost                             # show usage
```

---

## Example Workflows

### Starting a New Project from Scratch

```bash
# 1. Create repo on GitHub.com (click "New repository")

# 2. Clone it locally
git clone https://github.com/yourname/my-project.git
cd my-project

# 3. Open Claude Code
claude

# 4. Have Claude scaffold the project
> I want to build a web app that lets users track their reading list.
> Use Node.js with Express for the backend, vanilla HTML/CSS/JS for frontend.
> Set up the project structure and create a basic working app.

# 5. Review, test, then commit
> /commit
git push origin main
```

### Contributing to an Open Source Project

```bash
# 1. Fork the repo on GitHub.com

# 2. Clone YOUR fork
git clone https://github.com/yourname/forked-repo.git
cd forked-repo

# 3. Add the original as "upstream"
git remote add upstream https://github.com/originalowner/repo.git

# 4. Create a branch for your contribution
git checkout -b fix/typo-in-readme

# 5. Make changes with Claude's help
claude
> Fix the grammatical errors in README.md and improve the Getting Started section

# 6. Commit and push to YOUR fork
> /commit
git push origin fix/typo-in-readme

# 7. Open a PR from your fork to the original repo on GitHub.com
```

### Daily Development Loop

```bash
# Morning: sync with the team
git pull origin main
git checkout -b feature/todays-task

# Work: use Claude Code throughout
claude
> Continue working on the user notifications feature

# End of day: commit and push your progress
> /commit
git push origin feature/todays-task

# When ready: open a PR for review
gh pr create --title "feat: add user notification preferences"
```

---

## Learning Resources

| Resource | Description |
|---|---|
| [GitHub Docs](https://docs.github.com) | Official GitHub documentation |
| [Claude Code Docs](https://docs.anthropic.com/en/docs/claude-code) | Official Claude Code documentation |
| [Pro Git Book](https://git-scm.com/book/en/v2) | Free, comprehensive Git reference (highly recommended) |
| [Conventional Commits](https://www.conventionalcommits.org) | Commit message standard used industry-wide |
| [GitHub Flow Guide](https://docs.github.com/en/get-started/using-github/github-flow) | GitHub's recommended branching strategy |
| [GitHub Skills](https://skills.github.com) | Free interactive GitHub learning courses |

---

## Quick Tips

| Situation | What to Do |
|---|---|
| Stuck on an error | Paste the full error into Claude Code: "what does this mean and how do I fix it?" |
| Don't know where to start | Ask Claude: "explore this codebase and tell me where I should look to implement X" |
| Bad commit message | Use `git commit --amend` (before pushing) to rewrite it |
| Accidentally committed to main | Create a branch from main, reset main — ask Claude Code to walk you through it |
| PR getting too large | Break it into smaller PRs — one feature per PR |
| Claude wrote something incorrect | Say: "That's not quite right, here's what I actually need..." and iterate |
| Need to undo a pushed commit | Use `git revert <hash>` — it's safe and preserves history |

---

## Contributing

This is a living guide. If you find something unclear, out of date, or missing — open a PR. Contributions of any size are welcome.

1. Fork the repository
2. Create a branch: `git checkout -b docs/your-improvement`
3. Make your changes and commit: `/commit`
4. Open a pull request with a clear description

---

## License

Released under the [MIT License](LICENSE). Free to use, share, and adapt.

---

*Built with [Claude Code](https://docs.anthropic.com/en/docs/claude-code). As you grow your skills, come back and add your own notes, examples, and discoveries.*
