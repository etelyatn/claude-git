---
model: haiku
allowed-tools: Bash(git checkout:*), Bash(git add:*), Bash(git status:*), Bash(git push:*), Bash(git commit:*), Bash(gh pr create:*)
description: Commit, push, and open a pull request
---

## Context

- Status: !`git status`
- Diff: !`git diff HEAD`
- Branch: !`git branch --show-current`
- Recent commits: !`git log --oneline -5`

## Task

1. Create a new branch if currently on main/master
2. Stage relevant files and commit
3. Push the branch
4. Create a PR with a concise title (<70 chars) and short body (summary bullets + test plan checklist)
5. Report the PR URL
