# Example 4: Writing Great Pull Requests

A pull request (PR) is how you propose changes to a codebase. Writing a good PR description makes the review process faster and smoother.

## Anatomy of a Good PR

### Title

```
feat: add password strength indicator to registration form
```

- Short (under 70 characters)
- Uses conventional commit prefix
- Describes what changed, not how

### Description Template

```markdown
## What changed
- Added a `PasswordStrength` component that evaluates password strength in real time
- Strength is calculated based on length, special characters, and common patterns
- Visual indicator shows weak/medium/strong with color coding

## Why
Closes #34 — users were setting weak passwords and getting locked out after breaches.

## How to test
1. Go to /register
2. Type in the password field
3. Observe the strength indicator updating in real time
4. Verify: < 8 chars = weak (red), 8-12 mixed = medium (yellow), 12+ complex = strong (green)

## Screenshots
[attach before/after screenshots for UI changes]

## Notes for reviewer
- The strength algorithm is in `src/utils/passwordStrength.js` — worth a close look
- I chose not to block weak passwords, just warn. We can make it blocking in a follow-up.
```

---

## The PR Review Process

```
Author opens PR
       │
       ▼
Reviewer reads description + code
       │
       ▼
Reviewer leaves comments:
  - "This looks good"
  - "Can you add a test for the edge case where..."
  - "Suggestion: extract this into a helper function"
       │
       ▼
Author addresses comments, pushes new commits
       │
       ▼
Reviewer approves
       │
       ▼
PR merged into main
```

---

## Using Claude Code for PR Reviews

### Ask Claude to review a PR

```bash
claude
> /review-pr 42
```

Claude will:
1. Fetch the PR diff from GitHub
2. Analyze the changes
3. Identify bugs, security issues, logic errors
4. Check for missing tests or edge cases
5. Give specific, line-level feedback

### Ask Claude to review YOUR OWN PR before submitting

```bash
claude
> Review the changes I'm about to submit as a PR.
> Check for: bugs, security vulnerabilities, missing error handling,
> missing tests, and anything that would get flagged in a code review.
```

---

## PR Size Guidelines

| PR Size | Lines Changed | Verdict |
|---|---|---|
| Tiny | < 50 | Perfect |
| Small | 50–200 | Great |
| Medium | 200–500 | Acceptable |
| Large | 500–1000 | Break it up if possible |
| Huge | 1000+ | Always break up |

**Smaller PRs get reviewed faster and merged with fewer bugs.**

---

## Common PR Mistakes

| Mistake | Better Approach |
|---|---|
| "Various fixes" title | Describe the actual change |
| No description | Always explain what and why |
| 50 files changed | One PR per feature/fix |
| Mixing unrelated changes | Separate PRs for separate things |
| No tests | Add tests for new behavior |
| Force-pushing after review | Push new commits instead |
