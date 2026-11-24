# agents — agent instructions

Personal collection of Claude Code subagents, installed by copying into `~/.claude/agents/`. What the repo
is and the catalog: [README.md](README.md). This file is the rules for editing or adding an agent.

## Structure

```
agents/<name>.md   one file per agent: frontmatter + body
```

Flat repo. No scripts, no build, no CI, no CHANGELOG (no versioned releases yet).

## House style for an agent

- **Frontmatter:** `name` (kebab-case, matches the file name), `description`, `tools`, `model`.
  `description` says what it does on which input, and what it never does.
- **Agnostic.** No project, company, person, path, stack command or host. Anything project-specific belongs
  in that project's `AGENTS.md`, which the agent reads.
- **Precedence line at the top:** the repo's own rules win; this file is the default.
- **Never acts in public.** No push, PR, comment, review, merge, tag, issue change. The report goes back to
  the main session.
- **Least tools.** A reviewer gets no `Edit`/`Write`.
- **Ends with a report format** the main session can act on (`file:line`, verdict, draft text).
- **Keep it under ~120 lines.** Long tables or checklists that only some repos need do not go in.

## Adding or changing an agent

1. Write or edit `agents/<name>.md`.
2. Add or update its row in README.md's `## Agents` table.
3. A rename updates the file, the `name:` and every README mention (`grep -rn <old-name> .`).

## Privacy

Public repo. Never commit real project names, clients, hosts, IPs, tokens or keys, including in examples.

## Verification

- `grep -rn '^name:' agents/` matches each file name.
- Every README link resolves (`agents/<name>.md`, `LICENSE`, `AGENTS.md`).
- Copy the changed agent into `~/.claude/agents/` and run it once on a real repo before committing.

## Don't

- Restate commit or PR conventions; they live in the user's global `~/.claude/CLAUDE.md`.
- Split one agent into lite/full variants; one agent per role.
