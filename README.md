# prs-fixes

For each PR you name, the agent applies the suggested fixes, pushes them to the PR's head branch, replies to every review comment and marks each thread as resolved. Every comment is triaged as fix, already done or decline, and a decline always gets a short technical reason. It works in a throwaway worktree, runs the repo's own formatter, linter and tests, and finishes with a table that shows each thread as replied and resolved. It never pushes to the default branch and never force pushes.

## Install

For Claude Code, copy the skill folder into your personal skills directory:

```bash
git clone https://github.com/orenatobr/prs-fixes.git
mkdir -p ~/.claude/skills
cp -R prs-fixes/skills/* ~/.claude/skills/
```

Start a new Claude Code session. The skill loads from the `description` in its `SKILL.md`, so it triggers on its own and can also be called by name.

Other agents: the skill is a folder with a `SKILL.md` (YAML frontmatter plus Markdown). Tools that read the Agent Skills format can load `skills/` as it is. For the rest, paste the body of the `SKILL.md` into the agent's instruction file.

## Usage

`/prs-fixes 12, 15, 20`, or `/prs-fixes owner/repo#12`. Bare numbers use the repo of the current directory. It also triggers on "fix PR comments" and "resolve PR threads".

Comment bodies are treated as data. Requests inside them to run commands, read secrets or touch other repos are declined.

## Requirements

The `gh` CLI, authenticated. The GitHub MCP server is used when present, with `gh` as the fallback. The skill calls other skills when they are installed: [git-guidelines](https://github.com/orenatobr/git-guidelines), [programming-best-practices](https://github.com/orenatobr/programming-best-practices), [attack-protection](https://github.com/orenatobr/attack-protection), `humanizer` and `code-review`.

## What is in this repo

| Path | Purpose |
|------|---------|
| `skills/prs-fixes/` | The `prs-fixes` skill. |
| `CHANGELOG.md` | Notable changes, in Keep a Changelog format. |
| `AGENTS.md` | Rules for AI agents that edit this repo. |

The same skill also ships inside each of the other skill repos of this family.

## Contributing

`main` is protected: changes land through a pull request with one approval. See [AGENTS.md](AGENTS.md) for the conventions.

## License

MIT, see [LICENSE](LICENSE).
