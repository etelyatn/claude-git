---
name: quick-git
description: Use when user wants to commit, push, merge branches, merge PRs, open a PR, sync, update, or do any quick git operation in natural language
---

# Quick Git

Detect intent from natural language and dispatch a **haiku** sub-agent. Never run git commands directly.

## Intent Detection

| Intent | Example phrases | Operation |
|--------|----------------|-----------|
| Commit | "commit this", "save my work", "just commit" | commit |
| Push | "push it", "push my changes", "just push" | push |
| Commit + push | "commit and push", "save and push" | commit+push |
| Open PR | "open a PR", "create a PR", "make a PR" | pr |
| Push + PR | "push and open a PR", "push then PR" | push+pr |
| Commit + push + PR | "full PR", "commit push and PR", "ship it" | commit+push+pr |
| Merge branches | "merge into main", "merge all branches", "merge feature-x" | merge |
| Merge PRs | "merge the PR", "merge PR #42", "merge all open PRs" | merge-pr |
| Sync | "are we up to date?", "check sync", "what's new on main" | sync |
| Update | "update from main", "get latest", "rebase on main", "pull main" | update |

## Execution

Gather context in parallel first, then dispatch a haiku Task:

```
Task(
  subagent_type: "general-purpose",
  model: "haiku",
  prompt: "Git operation: <operation>
User said: <exact words>
Context:
  Status: <git status>
  Branches: <git branch -a>
  Log: <git log --oneline -5>

<instructions from section below>"
)
```

## Operation Instructions

### commit
Stage specific files (not `git add .`), commit matching recent project style.

### push
Push current branch; `-u origin <branch>` if no upstream.

### commit+push
Commit then push.

### pr
Check for existing PR — if found, report URL and stop. If unpushed commits exist, report and stop. Otherwise create PR: title <70 chars, body with summary + test plan.

### push+pr
Push, then create PR as above.

### commit+push+pr
Commit, push, then create PR. Branch off main if currently on main.

### merge (branches)
Specific branch → merge into current. "into main" → checkout main first. "all" → merge each feature branch into main one by one. Stop and report on conflict.

### merge-pr (GitHub PRs)
By number/branch → merge that PR. "current" or no arg → merge PR for current branch. "all" → merge all open PRs. Default `--merge`; honor `--squash` or `--rebase` if asked.

### sync
Read-only — run in parallel: `git status -sb`, ahead/behind main, is main itself stale, stash list. Report status and suggested fix. No changes.

### update
`git fetch origin`, then pull (on main) or `git rebase origin/main` (on feature branch). Abort and report on conflict.

## Rules
- Haiku for everything
- Never create a PR unless explicitly asked
- On conflict: report and stop, never auto-resolve
- Concise output only
