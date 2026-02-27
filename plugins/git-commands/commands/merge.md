---
model: haiku
allowed-tools: Bash(git checkout:*), Bash(git merge:*), Bash(git branch:*), Bash(git fetch:*), Bash(git status:*), Bash(git log:*)
description: Merge branches — single branch, or all feature branches into main
---

## Context

- All branches: !`git branch -a`
- Current branch: !`git branch --show-current`
- Git status: !`git status -sb`
- Recent log: !`git log --oneline -5`

## Your task

${ARGUMENTS}

Based on context and the request above:

1. **No branch specified / "all branches"**: Identify all non-main/master feature branches, then merge each into main/master one by one. Checkout main first.
2. **Specific branch named**: Merge it into the current branch.
3. **"into main" / "into master"**: Checkout main/master first, then merge the named branch.

After each merge:
- If clean: report `Merged <branch> ✓`
- If conflict: list the conflicting files and stop — do not attempt to resolve

Use parallel tool calls where operations are independent. Be concise.
