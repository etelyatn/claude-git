---
model: haiku
allowed-tools: Bash(git checkout:*), Bash(git add:*), Bash(git status:*), Bash(git diff:*), Bash(git push:*), Bash(git commit:*), Bash(git log:*), Bash(gh pr create:*), Bash(gh pr view:*)
description: Smart PR command — commits if needed, pushes if needed, then opens a pull request
---

## Context

- Branch: !`git branch --show-current`
- Status: !`git status -sb`
- Diff: !`git diff HEAD`
- Ahead of main: !`git log main..HEAD --oneline 2>/dev/null || git log master..HEAD --oneline 2>/dev/null`
- Recent commits: !`git log --oneline -5`

## Task

${ARGUMENTS}

Check if a PR already exists for this branch — if so, report the URL and stop.

Then work through the chain as needed based on current state:

1. **Uncommitted changes?** → create a new branch if on main/master, stage relevant files, commit
2. **Unpushed commits?** → push the branch (`-u origin <branch>` if no upstream)
3. **Ready to PR** → create a PR with a concise title (<70 chars) and short body (summary bullets + test plan checklist)

Report the PR URL.
