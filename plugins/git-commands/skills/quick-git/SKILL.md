---
name: quick-git
description: This skill should be used when the user asks to "just commit", "commit this", "save my work", "commit and push", "just push", "push it", "push my changes", "save and push", "commit push", or wants to quickly perform git operations without detailed discussion. Handles commit-only, push-only, and commit+push workflows.
model: haiku
---

# Quick Git

Fast git workflow skill that determines intent from the user's request and executes the appropriate git operations.

## Intent Detection

Determine which operations to perform based on the user's words:

| User says | Action |
|-----------|--------|
| "just commit", "commit this", "save my work", "commit it" | Commit only |
| "just push", "push it", "push my changes" | Push only |
| "commit and push", "save and push", "commit push", "just commit and push" | Commit then push |

**Rules:**
- If the request mentions only "commit" or "save" without "push" → commit only
- If the request mentions only "push" → push only
- If the request mentions both, or says "save and push" → commit then push
- Never create a PR unless the user explicitly asks for one

## Context Gathering

Before executing, gather context in parallel:
- `git status`
- `git diff HEAD`
- `git branch --show-current`
- `git log --oneline -10`

## Operations

### Commit
1. Stage changes using `git add` (stage specific files based on changes, not blind `git add .`)
2. Create a commit with an appropriate message matching the project's recent commit style

### Push
1. Push to remote using `git push`
2. If no upstream is set, use `git push -u origin <branch-name>`

## Execution

Perform all operations in a single message using multiple tool calls where possible. Be fast and concise — no extra commentary beyond confirming what was done.
