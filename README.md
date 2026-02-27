# claude-git

A [Claude Code](https://claude.com/claude-code) plugin for fast git operations. All commands run on **Haiku** for speed.

## Installation

```
/plugin marketplace add https://github.com/etelyatn/claude-git
/plugin install git@claude-git
```

Restart Claude Code after installation.

## Commands

| Command | Description |
|---------|-------------|
| `/git:commit` | Stage changes and create a commit |
| `/git:push` | Push current branch to remote |
| `/git:commit-push-pr` | Smart PR — commits if needed, pushes if needed, opens PR |
| `/git:merge` | Merge a branch or GitHub PR — asks if not specified |
| `/git:sync` | Read-only status check vs remote and main |
| `/git:update` | Pull (on main) or rebase on main (on feature branch) |
| `/git:clean-branches` | Delete local branches removed from remote |

## Skill: Quick Git

The **quick-git** skill triggers on natural language — no slash command needed.

| You say | What happens |
|---------|-------------|
| "commit this", "save my work" | Commit |
| "push it", "push my changes" | Push |
| "commit and push" | Commit + push |
| "open a PR", "ship it", "full PR" | Smart PR (commit/push/open as needed) |
| "merge feature-x", "merge PR #42" | Merge branch or GitHub PR |
| "merge" (no target) | Shows branches + open PRs, asks what to merge |
| "are we up to date?", "check sync" | Sync status report |
| "get latest", "update from main" | Pull / rebase from main |

## License

MIT
