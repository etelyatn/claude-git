---
model: haiku
allowed-tools: Bash(git checkout:*), Bash(git merge:*), Bash(git branch:*), Bash(git fetch:*), Bash(git status:*)
description: Merge git branches — single branch or all feature branches into main
---

## Context

- Branches: !`git branch -a`
- Current: !`git branch --show-current`
- Status: !`git status -sb`

## Task

${ARGUMENTS}

- Specific branch named → merge into current branch
- "into main/master" → checkout main first, then merge
- No branch / "all" → checkout main, merge each feature branch one by one

Stop on conflict — report conflicting files, do not resolve.
