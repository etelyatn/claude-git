---
model: haiku
allowed-tools: Bash(gh pr list:*), Bash(gh pr merge:*), Bash(gh pr view:*)
description: Merge one or more GitHub pull requests
---

## Context

- Open PRs: !`gh pr list --state open`
- Current branch: !`git branch --show-current`

## Task

${ARGUMENTS}

- PR number given → merge that PR
- Branch name given → find its PR and merge
- "current" or no argument → merge the PR for the current branch
- "all" → merge all open PRs one by one, reporting each result

Default strategy: `--merge`. Use `--squash` or `--rebase` if specified.

Report success or failure for each.
