# Domain Docs

This is a single-context repo. Before changing the workflow contract, read:

- `CONTEXT.md`
- relevant ADRs in `docs/adr/`
- `docs/agents/issue-tracker.md`
- `docs/agents/triage-labels.md`

If a future repo using this pattern has multiple bounded contexts, add a `CONTEXT-MAP.md` and point each context to its own `CONTEXT.md` and ADR directory.

## Use the Glossary

Use the domain terms in `CONTEXT.md` when naming issues, labels, scripts, docs, or validation checks. If a term is missing, update the glossary or file a Beads issue to clarify it.

## Flag ADR Conflicts

If a proposed change contradicts an ADR, surface it explicitly in the issue or implementation notes before changing the convention.
