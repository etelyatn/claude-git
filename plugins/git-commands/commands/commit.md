---
model: haiku
allowed-tools: Bash(git add:*), Bash(git status:*), Bash(git commit:*)
description: Create a git commit
---

## Context

- Current git status: !`git status`
- Current git diff (staged and unstaged changes): !`git diff HEAD`
- Current branch: !`git branch --show-current`
- Recent commits: !`git log --oneline -10`

## Your task

Based on the above changes, create a single git commit.

You have the capability to call multiple tools in a single response. Stage and create the commit using a single message. Do not use any other tools or do anything else. Do not send any other text or messages besides these tool calls.

## Important: Bash syntax requirements

When executing git commands in bash, use correct bash syntax:
- Use `cd /path/to/repo` with forward slashes (NOT `cd /d D:\path` - the `/d` flag is Windows cmd syntax)
- For Windows paths in Git Bash, use forward slashes: `cd D:/path` works fine
- Never use Windows cmd-specific flags or syntax
