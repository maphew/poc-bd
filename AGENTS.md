# Agent Instructions

This repository is a proof of concept for making Matt Pocock's agent skills work with Beads as a first-class issue tracker.

## Agent skills

### Issue tracker

Issues live in Beads (`bd`), not GitHub Issues, local markdown tickets, TodoWrite, or ad hoc task files. External PRs are not a triage surface for this repo. See `docs/agents/issue-tracker.md`.

### Triage labels

Matt Pocock's five triage roles map directly to Beads labels: `needs-triage`, `needs-info`, `ready-for-agent`, `ready-for-human`, and `wontfix`. Category labels are `bug` and `enhancement`. See `docs/agents/triage-labels.md`.

### Domain docs

This is a single-context repo: read `CONTEXT.md` and relevant ADRs in `docs/adr/` before changing workflow conventions. See `docs/agents/domain.md`.

## Beads workflow

Run `bd prime` when starting or after context reset. Use Beads for durable project state:

```bash
bd ready
bd show <id> --json
bd update <id> --claim
bd create --title="..." --description="..." --type=task --priority=2
bd dep add <issue> <depends-on>
bd close <id> --reason="..."
```

Prefer non-interactive `bd` flags over commands that open editors. Use `--json` when another tool or script will parse output.

Beads is the source of truth for task status and dependencies. Local execution checklists are fine for the current turn, but do not create markdown TODO lists as shared project tracking.

## Session boundaries

The default profile is conservative:

- Do not commit, push, or run `bd dolt push` unless the user explicitly asks.
- Do close completed beads when the tracked work is actually complete.
- File follow-up beads for discovered work that should survive handoff.
- Report changed files, validation commands, and any blocked sync/publish step at handoff.

## Validation

Run this after changing the adapter or local tool setup:

```bash
scripts/check-agent-integration
```
