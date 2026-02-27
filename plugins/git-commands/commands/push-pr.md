---
model: haiku
allowed-tools: Bash(git branch:*), Bash(git log:*), Bash(git status:*), Bash(git push:*), Bash(gh pr create:*), Bash(gh pr view:*)
description: Push the current branch and open a pull request
---

## Context

- Branch: !`git branch --show-current`
- Tracking: !`git status -sb`
- Ahead of main: !`git log main..HEAD --oneline 2>/dev/null || git log master..HEAD --oneline 2>/dev/null`

## Task

${ARGUMENTS}

1. Push the branch (`-u origin <branch>` if no upstream)
2. Check if a PR already exists — if so, report URL and stop
3. Create a PR with a concise title (<70 chars) and short body (summary bullets + test plan checklist)
4. Report the PR URL
