---
model: haiku
allowed-tools: Bash(git fetch:*), Bash(git pull:*), Bash(git rebase:*), Bash(git branch:*), Bash(git status:*)
description: Update current branch from remote — pull if on main, rebase on main if on a feature branch
---

## Context

- Branch: !`git branch --show-current`
- Tracking: !`git status -sb`

## Task

${ARGUMENTS}

1. `git fetch origin`
2. On main/master → `git pull`
3. On feature branch → `git rebase origin/main`; on conflict: `git rebase --abort`, report files, stop
4. Report commits applied or "Already up to date"
