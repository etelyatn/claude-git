---
model: haiku
allowed-tools: Bash(git push:*)
description: Push current branch to remote
---

## Context

- Current branch: !`git branch --show-current`
- Remote tracking: !`git status -sb`

## Your task

Push the current branch to the remote repository. If the branch doesn't have an upstream set, use `git push -u origin <branch-name>`.

You have the capability to call multiple tools in a single response. Execute the push in a single message. Do not use any other tools or do anything else. Do not send any other text or messages besides these tool calls.

## Important: Bash syntax requirements

When executing git commands in bash, use correct bash syntax:
- Use `cd /path/to/repo` with forward slashes (NOT `cd /d D:\path` - the `/d` flag is Windows cmd syntax)
- For Windows paths in Git Bash, use forward slashes: `cd D:/path` works fine
- Never use Windows cmd-specific flags or syntax
