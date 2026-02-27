---
model: haiku
allowed-tools: Bash(git branch:*), Bash(git log:*), Bash(git status:*), Bash(gh pr create:*), Bash(gh pr view:*)
description: Create a pull request from the current branch
---

## Context

- Branch: !`git branch --show-current`
- Ahead of main: !`git log main..HEAD --oneline 2>/dev/null || git log master..HEAD --oneline 2>/dev/null`
- Status: !`git status -sb`

## Task

${ARGUMENTS}

Check if a PR already exists for this branch — if so, report the URL and stop.

If the branch has unpushed commits, report that and stop.

Otherwise: create a PR with a concise title (<70 chars) and short body (summary bullets + test plan checklist). Report the PR URL.
