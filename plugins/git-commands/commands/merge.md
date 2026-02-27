---
model: haiku
allowed-tools: Bash(git checkout:*), Bash(git merge:*), Bash(git branch:*), Bash(git fetch:*), Bash(git status:*), Bash(gh pr list:*), Bash(gh pr merge:*), Bash(gh pr view:*)
description: Merge a branch or GitHub PR — if not specified, asks the user what to merge
---

## Context

- Branches: !`git branch -a`
- Current branch: !`git branch --show-current`
- Open PRs: !`gh pr list --state open 2>/dev/null || echo "(gh unavailable)"`

## Task

${ARGUMENTS}

**No argument given** → show the branches and open PRs from context above, then ask:
"What would you like to merge? Provide a branch name or PR number."

**Argument is a PR** (a number, "#N", "PR N", or "all PRs"):
- Single PR → `gh pr merge <number> --merge` (or `--squash`/`--rebase` if specified)
- "all" → merge all open PRs one by one
- Report success or failure for each

**Argument is a branch name:**
- Specific branch → merge into current branch
- "into main/master" → checkout main first, then merge
- "all" → checkout main, merge each feature branch one by one
- Stop on conflict — report conflicting files, do not resolve
