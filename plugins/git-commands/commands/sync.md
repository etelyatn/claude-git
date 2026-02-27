---
model: haiku
allowed-tools: Bash(git fetch:*), Bash(git branch:*), Bash(git log:*), Bash(git status:*), Bash(git rev-list:*)
description: Check sync status — what's ahead, behind, or diverged vs remote and main. No changes made.
---

## Context

- Current branch: !`git branch --show-current`
- Fetch remote (no changes): !`git fetch --dry-run 2>&1 || true`

## Your task

Run these checks in parallel, then report a concise summary:

1. **vs remote**: `git status -sb` — is the branch ahead/behind its remote tracking branch?
2. **vs main**: `git rev-list --left-right --count main...HEAD 2>/dev/null || git rev-list --left-right --count master...HEAD 2>/dev/null` — how many commits is this branch ahead/behind main?
3. **main vs origin/main**: `git rev-list --left-right --count origin/main...main 2>/dev/null || git rev-list --left-right --count origin/master...master 2>/dev/null` — is main itself out of date?
4. **Stash**: `git stash list` — any stashed changes?

Report format (be concise):
- Current branch and whether it's up to date, ahead, behind, or diverged — for both remote and main
- Whether main needs pulling
- Any stash entries
- What action would fix any issues (e.g. "run /update to rebase on main")

Do NOT make any changes. Read-only.
