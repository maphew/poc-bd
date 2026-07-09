# ADR 0001: Use Beads as the Matt Skills Issue Tracker

## Status

Accepted

## Context

Matt Pocock's skills expect each repo to define an issue tracker, triage labels, and domain documentation. Upstream does not yet provide Beads as a built-in tracker option, but the skills support "other" trackers through repo-local documentation.

This repo needs the combination to be practical, not just described in research notes.

## Decision

Use Beads as the durable issue tracker and configure Matt Pocock's skills through `docs/agents/issue-tracker.md`, `docs/agents/triage-labels.md`, and `docs/agents/domain.md`.

Use native Beads dependency edges for blocking relationships. Use Beads labels for Matt Pocock's triage roles. Keep session-close behavior conservative: no commits, Git pushes, or Dolt pushes unless the user explicitly asks.

## Consequences

Agents can use Matt Pocock's skills without translating tickets into markdown or GitHub issues.

The adapter docs must stay aligned with the installed `bd` CLI. `scripts/check-agent-integration` exists to catch missing docs, unavailable Beads state, or missing installed skills.

If upstream adds official Beads support later, compare it with this adapter before replacing the local convention.
