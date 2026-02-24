# Example 5: Building a Real Feature End-to-End

This example simulates building a complete feature from GitHub issue to merged PR.

---

## The Scenario

**GitHub Issue #12:**
> **Title:** Add "dark mode" toggle to the settings page
>
> **Description:**
> Users have requested a dark mode option. The toggle should:
> - Appear in Settings > Appearance
> - Persist across sessions (save to localStorage)
> - Apply to the entire app immediately on toggle
>
> **Acceptance criteria:**
> - [ ] Toggle visible in settings
> - [ ] Preference saved and restored on reload
> - [ ] All pages respect the dark mode class

---

## Step 1: Create a Branch

```bash
git checkout main
git pull origin main
git checkout -b feature/dark-mode-toggle
```

---

## Step 2: Understand the Codebase with Claude

```bash
claude

> I'm working on GitHub issue #12 — adding a dark mode toggle.
> Before writing any code, explore the codebase and tell me:
> 1. Where is the Settings page?
> 2. How are user preferences currently stored?
> 3. Where is the app's root CSS/theme defined?
> 4. What CSS framework or theming approach is being used?
```

Claude responds with the relevant files and patterns. Now you know where to work.

---

## Step 3: Implement with Claude

```bash
> Now implement the dark mode toggle based on what you found.
>
> Requirements from issue #12:
> - Add a toggle in the Settings > Appearance section
> - Save preference to localStorage under key "theme"
> - On load, read localStorage and apply "dark" class to <body> if set
> - The toggle should update immediately without page reload
>
> Make sure to match the existing code style and component patterns.
```

Claude writes:
- The toggle component
- The localStorage read/write logic
- The CSS dark mode variables
- Updates to the Settings page

---

## Step 4: Review the Changes

```bash
git diff
```

Read through everything Claude wrote. Ask questions if something is unclear:

```bash
> Why did you put the localStorage logic in a custom hook instead of in the component directly?
```

---

## Step 5: Test It

```bash
npm run dev         # start the dev server
# Open browser, go to Settings > Appearance
# Toggle dark mode
# Reload the page — preference should persist
```

If something's wrong:
```bash
> The dark mode class is being applied but the colors aren't changing.
> Here's the CSS file: [paste or let Claude read it]
> What's missing?
```

---

## Step 6: Write Tests

```bash
> Write tests for the dark mode toggle.
> Test:
> 1. Toggle switches from light to dark
> 2. Preference is saved to localStorage
> 3. On mount, it reads localStorage and applies the saved theme
```

---

## Step 7: Commit

```bash
> /commit
```

Claude writes something like:
```
feat: add dark mode toggle with localStorage persistence

Adds a dark mode toggle to Settings > Appearance. The user's
preference is saved to localStorage and restored on page load.
Applies a "dark" class to the body element which triggers CSS
variable overrides for the dark theme.

Closes #12
```

---

## Step 8: Push and Open a PR

```bash
git push -u origin feature/dark-mode-toggle

gh pr create \
  --title "feat: add dark mode toggle to settings" \
  --body "Closes #12

## What changed
- Added DarkModeToggle component in src/components/settings/
- Theme preference persisted in localStorage
- CSS dark mode variables added to src/styles/theme.css

## Test
1. Go to Settings > Appearance
2. Toggle dark mode
3. Reload page — preference should persist"
```

---

## Step 9: Address Review Comments

If a reviewer says:
> "Can you also add a keyboard shortcut (Ctrl+Shift+D) for power users?"

```bash
claude
> A reviewer asked me to add a keyboard shortcut Ctrl+Shift+D to toggle dark mode globally.
> The current toggle is in src/components/settings/DarkModeToggle.jsx.
> Where's the best place to add a global keyboard listener?
```

Make the change, then:
```bash
git add .
git commit -m "feat: add Ctrl+Shift+D keyboard shortcut for dark mode toggle"
git push origin feature/dark-mode-toggle
```

---

## Step 10: Merge

Once approved, merge on GitHub. Delete the branch.

```bash
git checkout main
git pull origin main
git branch -d feature/dark-mode-toggle
```

**You just shipped a feature the professional way.**

---

## What Made This Workflow Effective

1. **Branch isolation** — main stayed clean throughout
2. **Exploration first** — Claude understood the codebase before writing
3. **Incremental commits** — each logical step is a separate commit
4. **Tests included** — not an afterthought
5. **Clear PR description** — reviewer knew exactly what to look at
6. **Addressed feedback** — as new commits, not force pushes
