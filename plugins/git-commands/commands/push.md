---
model: haiku
allowed-tools: Bash(git push:*)
description: Push current branch to remote
---

## Context

- Branch: !`git branch --show-current`
- Tracking: !`git status -sb`

## Task

Push the current branch. Use `git push -u origin <branch>` if no upstream is set.
