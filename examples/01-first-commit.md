# Example 1: Making Your First Commit

This example walks through making your very first commit on a real project.

## Scenario

You just cloned a repo and want to add your name to a contributors list.

## Steps

### 1. Check your status first

```bash
git status
```

You'll see something like:
```
On branch main
nothing to commit, working tree clean
```

### 2. Make a change

Edit `CONTRIBUTORS.md` and add your name.

### 3. See what changed

```bash
git diff
```

This shows you the exact lines added (green/+) and removed (red/-).

### 4. Stage your change

```bash
git add CONTRIBUTORS.md
```

Check the status again:
```bash
git status
# Changes to be committed:
#   modified: CONTRIBUTORS.md
```

### 5. Commit it

```bash
git commit -m "docs: add my name to contributors list"
```

You'll see:
```
[main a1b2c3d] docs: add my name to contributors list
 1 file changed, 1 insertion(+)
```

### 6. Push to GitHub

```bash
git push origin main
```

**Congratulations — you just made your first commit!**

## What Claude Code Can Do Here

Instead of step 5, you could open Claude Code and type:
```
/commit
```

Claude will:
1. Read all your changes
2. Write a clear, descriptive commit message
3. Stage and commit for you

This is especially useful when you have many files changed and want a thoughtful message.
