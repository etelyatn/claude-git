# claude-git

A [Claude Code](https://claude.com/claude-code) plugin for fast git operations. Uses **Haiku** for speed on simple commands and **Sonnet** for quality PR descriptions.

## Installation

```
/plugin marketplace add https://github.com/etelyatn/claude-git
/plugin install git@claude-git
```

Restart Claude Code after installation.

## Commands

| Command | Model | Description |
|---------|-------|-------------|
| `/git:commit` | Haiku | Stage changes and create a commit |
| `/git:push` | Haiku | Push current branch to remote |
| `/git:commit-push-pr` | Sonnet | Commit, push, and open a pull request |
| `/git:clean-branches` | Haiku | Delete local branches removed from remote |

## Skill: Quick Git

The **quick-git** skill triggers on natural language — no slash command needed.

| You say | What happens |
|---------|-------------|
| "just commit", "commit this", "save my work" | Commit only |
| "just push", "push it", "push my changes" | Push only |
| "commit and push", "save and push" | Commit + push |

Runs on Haiku for instant responses.

## Why Different Models?

- **Haiku** — Fast and cheap. Perfect for straightforward git operations like commits and pushes.
- **Sonnet** — Used only for `/git:commit-push-pr` where better reasoning produces higher quality PR titles and descriptions.

## Customization

To change a command's model, edit the `model:` field in the command's frontmatter:

```yaml
---
model: sonnet  # or haiku, opus
---
```

Command files are in `plugins/git-commands/commands/`.

## License

MIT
