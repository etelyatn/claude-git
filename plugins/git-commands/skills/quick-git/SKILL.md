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
| PR (any stage) | "open a PR", "make a PR", "push and PR", "ship it", "full PR" | commit+push+pr |
| Merge | "merge feature-x", "merge PR #42", "merge into main", "merge all" | merge |
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

### commit+push+pr
Smart PR: check for existing PR first — if found, report URL and stop. Then commit if there are uncommitted changes, push if there are unpushed commits, open PR. Branch off main if currently on main.

### merge
No target given → show available branches and open PRs, ask user what to merge.
PR (number or "#N") → `gh pr merge`; "all PRs" → merge all open PRs.
Branch name → merge into current; "into main" → checkout main first; "all" → merge all feature branches into main.
Stop on conflict — report files, do not resolve.

### sync
Read-only — run in parallel: `git status -sb`, ahead/behind main, is main itself stale, stash list. Report status and suggested fix. No changes.

### update
`git fetch origin`, then pull (on main) or `git rebase origin/main` (on feature branch). Abort and report on conflict.

## Rules
- Haiku for everything
- Never create a PR unless explicitly asked
- On conflict: report and stop, never auto-resolve
- Concise output only
