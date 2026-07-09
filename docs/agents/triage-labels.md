# Triage Labels

Matt Pocock's skills speak in canonical triage roles. This file maps those roles to Beads labels used in this repo.

| Label in mattpocock/skills | Label in Beads | Meaning |
| --- | --- | --- |
| `needs-triage` | `needs-triage` | Maintainer needs to evaluate this issue |
| `needs-info` | `needs-info` | Waiting on reporter or user for more information |
| `ready-for-agent` | `ready-for-agent` | Fully specified and ready for an AFK agent |
| `ready-for-human` | `ready-for-human` | Requires human implementation or judgment |
| `wontfix` | `wontfix` | Will not be actioned |

Category labels:

| Role | Label in Beads | Meaning |
| --- | --- | --- |
| `bug` | `bug` | Something is broken |
| `enhancement` | `enhancement` | New feature or improvement |

Every triaged issue should carry exactly one state label and, when applicable, exactly one category label. Remove stale state labels when moving an issue to a new state.

When a skill says "apply the AFK-ready triage label", use:

```bash
bd label add <id> ready-for-agent
```
