---
model: sonnet
allowed-tools: Bash(git branch:*), Bash(git log:*), Bash(git diff:*), Bash(git status:*), Bash(git push:*), Bash(gh pr create:*), Bash(gh pr view:*)
description: Push current branch and open a pull request
---

## Context

- Current branch: !`git branch --show-current`
- Remote tracking: !`git status -sb`
- Commits ahead of main: !`git log main..HEAD --oneline 2>/dev/null || git log master..HEAD --oneline 2>/dev/null || git log --oneline -10`
- Diff summary: !`git diff main...HEAD --stat 2>/dev/null || git diff --stat HEAD~5..HEAD`

## Your task

${ARGUMENTS}

1. Push the current branch — use `git push -u origin <branch>` if no upstream is set
2. Check if a PR already exists for this branch — if so, report the URL and stop
3. Write a concise PR title (under 70 characters) based on the commits
4. Write a short PR body with a summary bullet list and a test plan checklist
5. Run `gh pr create` with `--title` and `--body`
6. Report the PR URL

Do all operations in a single message using parallel tool calls where possible.
