---
model: haiku
allowed-tools: Bash(git add:*), Bash(git status:*), Bash(git commit:*)
description: Stage and commit changes
---

## Context

- Status: !`git status`
- Diff: !`git diff HEAD`
- Recent commits: !`git log --oneline -5`

## Task

Stage relevant files and create a commit matching the project's recent commit message style.
