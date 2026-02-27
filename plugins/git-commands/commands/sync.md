---
model: haiku
allowed-tools: Bash(git fetch:*), Bash(git branch:*), Bash(git log:*), Bash(git status:*), Bash(git rev-list:*), Bash(git stash:*)
description: Check sync status — what's ahead, behind, or diverged vs remote and main. Read-only.
---

## Context

- Branch: !`git branch --show-current`

## Task

Run in parallel, then report a concise summary:

1. `git status -sb` — ahead/behind remote
2. `git rev-list --left-right --count main...HEAD 2>/dev/null || git rev-list --left-right --count master...HEAD 2>/dev/null` — ahead/behind main
3. `git rev-list --left-right --count origin/main...main 2>/dev/null` — is main itself stale?
4. `git stash list` — any stashed changes?

Report: branch status vs remote + main, whether main needs pulling, stash entries, and suggested action. No changes.
