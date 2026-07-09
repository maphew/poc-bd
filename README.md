# poc-bd

A proof of concept for using Matt Pocock's agent skills with Beads as the issue tracker.

## What Is Wired Up

- Matt Pocock's skills are installed globally for Codex via `skills add mattpocock/skills`.
- Beads is initialized locally with issue prefix `pocbd`.
- `AGENTS.md` and `CLAUDE.md` point agents at the same Beads-backed workflow.
- `docs/agents/` contains the adapter docs expected by Matt Pocock's setup pattern.
- `CONTEXT.md` and `docs/adr/0001-use-beads-as-matt-skills-issue-tracker.md` capture the domain terms and decision.

## Daily Commands

```bash
bd prime
bd ready
bd show <id> --json
bd update <id> --claim
bd close <id> --reason="..."
```

Run the integration check after changing setup files:

```bash
scripts/check-agent-integration
```

## Current Tracker State

The completed bootstrap work is recorded as `pocbd-8q5`.

The next useful validation step is `pocbd-nr5`: exercise a real Matt-skill workflow against the Beads adapter and record any gaps as Beads issues.
