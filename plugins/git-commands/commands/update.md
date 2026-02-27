---
model: haiku
allowed-tools: Bash(git fetch:*), Bash(git pull:*), Bash(git rebase:*), Bash(git merge:*), Bash(git branch:*), Bash(git log:*), Bash(git status:*), Bash(git stash:*)
description: Update current branch from remote and/or main — pull if on main, rebase on main if on a feature branch
---

## Context

- Current branch: !`git branch --show-current`
- Remote tracking: !`git status -sb`
- Behind main by: !`git rev-list --left-right --count main...HEAD 2>/dev/null || git rev-list --left-right --count master...HEAD 2>/dev/null`
- Stash: !`git stash list`

## Your task

${ARGUMENTS}

1. **Fetch** from remote first: `git fetch origin`

2. **If on main or master**:
   - `git pull` to fast-forward
   - Report how many commits were pulled

3. **If on a feature branch**:
   - Rebase onto `origin/main` (or `origin/master`): `git rebase origin/main`
   - If rebase conflicts: abort with `git rebase --abort`, report the conflicting files, and stop
   - If clean: report how many commits from main were incorporated

4. If the branch has no new commits behind main/remote — report "Already up to date" and stop

Report what changed (commits pulled/rebased) or what blocked the update (conflicts).
