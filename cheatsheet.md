# Quick Reference Cheatsheet

Keep this open while you work.

---

## Git — Daily Commands

```bash
git status                          # what's changed?
git diff                            # what exactly changed?
git add <file>                      # stage a file
git add .                           # stage everything
git commit -m "type: description"   # commit
git push origin <branch>            # push to GitHub
git pull origin main                # get latest from main
git checkout -b <branch>            # new branch
git checkout <branch>               # switch branch
git log --oneline -10               # last 10 commits
git stash / git stash pop           # temp save / restore
```

---

## Commit Message Types

```
feat:      new feature
fix:       bug fix
docs:      documentation only
style:     formatting, no logic change
refactor:  restructuring, no behavior change
test:      add or fix tests
chore:     build, tooling, dependencies
```

---

## Claude Code — Key Prompts

| Goal | What to Say |
|---|---|
| Understand a project | "Explore this codebase and give me an overview" |
| Before building | "Where would I add X in this codebase?" |
| Build a feature | "Implement X using the patterns you see in this project" |
| Debug | "Here's the error: [paste]. Find and fix it." |
| Write tests | "Write tests for [component/function]" |
| Code review | "Review these changes for bugs and issues" |
| Commit | `/commit` |
| Review a PR | `/review-pr <number>` |

---

## Branch Naming

```
feature/what-youre-building
fix/what-youre-fixing
docs/what-youre-documenting
refactor/what-youre-restructuring
chore/what-youre-maintaining
```

---

## The Golden Rules

1. **Never commit to main directly** — always use branches
2. **Never commit secrets** — use `.env` files and `.gitignore`
3. **Commit early, commit often** — small commits are easier to review and revert
4. **One branch = one thing** — keep PRs focused
5. **Read before you edit** — understand code before changing it
6. **Review what Claude writes** — you're responsible for your code
7. **Test before you push** — don't break main for your teammates

---

## Undoing Things

```bash
# Undo last commit (keep changes)
git reset --soft HEAD~1

# Discard unstaged changes to a file
git checkout -- filename.txt

# Remove a file from staging
git restore --staged filename.txt

# See what a commit changed
git show <commit-hash>

# Revert a pushed commit (safe — creates a new commit)
git revert <commit-hash>
```

---

## When You're Stuck

1. Read the full error message — the answer is usually there
2. Ask Claude: paste the error + what you expected
3. Check `git status` — you may have uncommitted/unstaged changes
4. Check `git log` — something might have been committed you didn't expect
5. Google the exact error message in quotes
