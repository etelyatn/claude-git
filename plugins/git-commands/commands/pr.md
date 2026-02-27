---
model: sonnet
allowed-tools: Bash(git branch:*), Bash(git log:*), Bash(git diff:*), Bash(git status:*), Bash(gh pr create:*), Bash(gh pr view:*)
description: Create a pull request from the current branch
---

## Context

- Current branch: !`git branch --show-current`
- Commits ahead of main: !`git log main..HEAD --oneline 2>/dev/null || git log master..HEAD --oneline 2>/dev/null || git log --oneline -10`
- Diff summary: !`git diff main...HEAD --stat 2>/dev/null || git diff --stat HEAD~5..HEAD`
- Current status: !`git status -sb`

## Your task

${ARGUMENTS}

Create a pull request for the current branch:

1. Check if a PR already exists for this branch — if so, report the URL and stop
2. Write a concise PR title (under 70 characters) based on the commits
3. Write a short PR body with a summary bullet list and a test plan checklist
4. Run `gh pr create` with `--title` and `--body`
5. Report the PR URL

If the branch has no upstream or has unpushed commits, report that and stop — do not push automatically.
