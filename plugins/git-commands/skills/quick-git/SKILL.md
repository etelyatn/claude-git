---
name: quick-git
description: Use when user wants to commit, push, merge, sync, update, open a PR, save work, or run quick git operations without extended discussion
---

# Quick Git

Detects git intent and dispatches a haiku sub-agent for execution. Never do git work directly — always delegate.

## Intent Detection

| User says | Operation | Model |
|-----------|-----------|-------|
| "commit", "save my work", "just commit", "commit this" | commit | haiku |
| "push", "just push", "push it", "push my changes" | push | haiku |
| "commit and push", "save and push", "commit push" | commit+push | haiku |
| "merge", "merge branches", "merge into main", "merge all" | merge | haiku |
| "open a PR", "create a PR", "make a PR", "open PR" | pr | sonnet |
| "push and PR", "push then PR", "push + PR" | push+pr | sonnet |
| "commit push PR", "commit and push and PR", "full PR" | commit+push+pr | sonnet |
| "sync", "check sync", "are we up to date", "what's new" | sync | haiku |
| "update", "update from main", "pull main", "rebase on main", "get latest" | update | haiku |

## Execution — ALWAYS dispatch a sub-agent

PR operations need quality titles/descriptions → use **sonnet**.
All other git operations → use **haiku**.

Gather context in parallel first:
- `git status`
- `git branch -a`
- `git log --oneline -5`

Then dispatch:
```
Task(
  subagent_type: "general-purpose",
  model: "haiku" | "sonnet",   ← per table above
  prompt: "Git operation: <detected operation>
User request: <exact words>
Context:
- Status: <git status output>
- Branches: <git branch -a output>
- Log: <git log --oneline -5 output>

<operation instructions below>"
)
```

## Operation Instructions (include in Task prompt)

### commit
1. Stage specific relevant files (not blind `git add .`)
2. Commit message matching recent project style

### push
Push current branch; add `-u origin <branch>` if no upstream set.

### commit+push
Commit then push sequentially.

### merge
1. If "merge all": merge each feature branch into main one by one (checkout main first)
2. If specific branch named: merge into current branch
3. Stop on conflicts — report conflicting files, do not auto-resolve

### pr
1. Check if PR already exists for this branch — if so, report URL and stop
2. Write concise title (<70 chars) from commits
3. Write body with summary bullets + test plan checklist
4. Run `gh pr create --title "..." --body "..."`
5. Report PR URL

### push+pr
Push first (`-u origin <branch>` if needed), then follow pr steps above.

### commit+push+pr
Commit, push, then follow pr steps above — all sequentially.

### sync
Read-only. Run in parallel:
1. `git fetch origin` (no apply)
2. `git status -sb` — ahead/behind remote
3. `git rev-list --left-right --count main...HEAD` — ahead/behind main
4. `git rev-list --left-right --count origin/main...main` — is main itself stale?
5. `git stash list` — any stashes?
Report status and suggested action. Make no changes.

### update
1. `git fetch origin`
2. If on main/master: `git pull`
3. If on feature branch: `git rebase origin/main` (abort + report on conflict)
4. Report commits pulled/rebased or "Already up to date"

## Rules
- Never create a PR unless explicitly asked
- Report only what was done — no extra commentary
- On conflict during merge: report details and stop
