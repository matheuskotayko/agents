# agents

Subagents for Claude Code that work in any repository. They read the repo's own `AGENTS.md` / `CLAUDE.md`
first and fall back to the defaults written here.

| Agent | What it does |
|---|---|
| [issue-implementer](agents/issue-implementer.md) | Implements one issue on a new branch, with a code style, targeted tests and a regression proof. Commits; never pushes or opens a PR. |
| [pr-reviewer](agents/pr-reviewer.md) | Checks a PR against its linked issue (not the PR text), runs the targeted tests, returns a verdict. Never approves or merges. |

Companion to [skills](https://github.com/matheuskotayko/skills).

## Install

Every project:

```bash
git clone https://github.com/matheuskotayko/agents.git
cp agents/agents/*.md ~/.claude/agents/
```

One project only: copy into that repo's `.claude/agents/`.

## Use

- "Use issue-implementer on #42."
- "Run pr-reviewer on PRs 57 and 58."

The agent reports back to the main session, which decides on push, PR, approval and merge.

## Customizing

Project rules belong in the project's `AGENTS.md`, not here: test commands, migration paths, invariants,
changelog format. The agents read them before working.

## License

MIT
