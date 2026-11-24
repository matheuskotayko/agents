<h1 align="center">agents</h1>

> Claude Code subagents that take an issue to a tested commit and review the PR against the issue,
> in any repository. They follow the repo's own rules first and stop before anything public.

[![License](https://img.shields.io/badge/license-MIT-blue)](LICENSE)

## Why these agents

- **The repo's rules win.** Each agent reads `AGENTS.md` / `CLAUDE.md` and the docs they point to before
  touching code. The defaults here only apply when the repo says nothing.
- **The issue is the spec, not the PR text.** `pr-reviewer` lists what the linked issue asks and checks each
  item in the code with `file:line`, instead of trusting the PR description.
- **Fixes are proved.** Both agents restore the production file from the base branch, run the new test and
  confirm it fails before accepting a regression test.
- **They never act in public.** No push, PR, comment, approval or merge. The report goes back to your main
  session, and you decide.
- **One code style travels with them.** `task-implementer` carries a default style (function and file size,
  explicit types, no duplication, early returns, WHY comments, F.I.R.S.T tests) for repos that don't define one.

## How it works

```
you: "task-implementer on #42"
  └─▶ reads issue + repo rules ─▶ new branch ─▶ code + targeted tests ─▶ commits ─▶ report + PR draft
you: push, open PR, "pr-reviewer on 57"
  └─▶ reads linked issue ─▶ checks each item in diff ─▶ runs touched tests ─▶ verdict + approval text
```

## Agents

| Agent | Model | What it does |
|---|---|---|
| [task-implementer](agents/task-implementer.md) | sonnet | Implements one issue on a new branch from the default branch, tests what changed and commits. Stops and asks when a decision is open. |
| [pr-reviewer](agents/pr-reviewer.md) | opus | Reviews one or more PRs against their linked issues, runs the targeted tests, checks conflicts between PRs, returns `merge` / `merge with caveat` / `don't merge`. Read-only tools. |

Companion to [skills](https://github.com/matheuskotayko/skills).

## Quick start

Requires [Claude Code](https://docs.claude.com/en/docs/claude-code) and an authenticated
[`gh`](https://cli.github.com/) CLI.

```bash
git clone https://github.com/matheuskotayko/agents.git
cp agents/agents/*.md ~/.claude/agents/
```

For a single project, copy them into that repo's `.claude/agents/` instead.

## Everyday use

- "Use task-implementer on #42." You get a branch, commits, a per-item checklist and a PR body draft.
- "Run pr-reviewer on PRs 57 and 58." You get a verdict per PR and a summary to paste into the approval.
- "Run pr-reviewer on the open PRs from alice." Reviewed one at a time, in order.

## Customizing

Project rules belong in the project's `AGENTS.md`, not in these files: test commands, migration paths,
invariants, changelog format, read access to production. The agents read them before working, so one copy
here serves every repo.

## Contributing

Rules for editing an agent are in [AGENTS.md](AGENTS.md).

## License

MIT. See [LICENSE](LICENSE).
