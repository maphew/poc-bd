# Context

This repo explores a first-class combination of Matt Pocock's agent skills and Beads.

## Glossary

- **Agent skills**: Installed skill prompts from `mattpocock/skills`, such as `to-tickets`, `triage`, `implement`, `tdd`, and `code-review`.
- **Adapter docs**: The files under `docs/agents/` that tell Matt Pocock's skills how this repo tracks issues, labels, and domain context.
- **Beads**: The local-first issue tracker accessed through the `bd` CLI. Beads is the source of truth for issues, dependencies, state, and handoff notes in this repo.
- **Durable tracker**: Project task state that survives context resets and can be resumed by another person or agent. In this repo, that means Beads.
- **Frontier**: The set of unblocked issues returned by `bd ready`.
- **Triage role**: One of Matt Pocock's canonical issue states: `needs-triage`, `needs-info`, `ready-for-agent`, `ready-for-human`, or `wontfix`.

## Operating Model

Matt Pocock's skills provide workflow discipline: grilling, specs, ticket slicing, triage, TDD, implementation, and review.

Beads provides durable state: issue IDs, dependencies, comments, priorities, status, and session continuity.

The integration point is intentionally thin: the skills read `docs/agents/*`; those docs map tracker-agnostic skill instructions onto concrete `bd` commands.
