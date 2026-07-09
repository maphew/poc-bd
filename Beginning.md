I found **real overlap, but not a mature ecosystem yet**. The current pattern is: people like `mattpocock/skills`’ planning/triage discipline and want Beads as the durable tracker, but the integration is still mostly hand-rolled or proposed.

## Best direct examples

### 1. `mattpocock/skills` issue #116 — “please add Beads support”

This is the clearest upstream discussion. The request is to add Beads support to `/setup-matt-pocock-skills`; it is still open.

What happened there:

* Matt replied positively: “Agree!” and later “Sounds reasonable!”
* One contributor proposed actual changes adding **Beads** as an issue tracker target and a Beads-specific `issue-tracker-beads.md`. The proposed commands include `bd create`, `bd show`, `bd ready`, `bd blocked`, `bd update --claim`, `bd comments`, labels, close, and Dolt sync.
* Another contributor mapped Matt’s five canonical triage roles onto Beads statuses/labels: `needs-triage`, `needs-info`, `ready-for-agent`, `ready-for-human`, `wontfix`.
* The tribulation: the original requester later said they had “given up with Beads” as too unpredictable/error-prone, while another user pushed back saying they had used Beads for months with no issues and liked it more than `gh` for issue tracking because of dependencies, epics/subtasks, structured task fields, local-first speed, and less context pollution.

My read: **this is the center of gravity**. Beads support is desired, sketched, and socially validated by Matt, but not merged into the current upstream setup skill.

### 2. `TheFermiSea/CrystalMath` — actual project using both

This is the strongest “in the wild” project example I found. Its `AGENTS.md` has a Beads section and an `Agent skills` section explicitly referencing `mattpocock/skills`.

It uses Beads as the canonical tracker, with commands like `bd ready`, `bd show`, `bd create`, `bd update`, `bd close`, and `bd dolt push/pull`; it explicitly says not to use TodoWrite or markdown task files.

Later in the same file, it says the per-repo config is consumed by `mattpocock/skills` engineering/productivity skills including `triage`, `to-issues`, `to-prd`, `improve-codebase-architecture`, `diagnose`, `tdd`, and `zoom-out`, and that issues live in Beads rather than GitHub Issues/TodoWrite/markdown TODOs.

It also has the expected `docs/agents/issue-tracker.md` and `docs/agents/triage-labels.md` glue files. The tracker doc says issues/PRDs live in Beads, maps “publish to issue tracker” to `bd create`, “fetch ticket” to `bd show`, and label work to `bd label add`.   The triage-labels doc maps Matt’s canonical roles to Beads labels.

My read: **this is exactly the combined pattern you’re asking about**. It appears to work by making Matt’s skills tracker-agnostic through `docs/agents/*`, then teaching those docs that Beads is the tracker.

### 3. `vessux/dotfiles` — smaller, solo Beads + Agent skills setup

This repo also has an `Agent skills` block saying issues live in Beads and there is no GitHub issue tracker. It uses a simplified Beads-native lifecycle: raw capture → `stage:ready` → closed/`wontfix`.

Its issue tracker doc says Beads is the backlog even though the remote is GitHub, and explicitly says not to create GitHub issues. It treats `bd ready` plus dependencies/epics as the work driver.   It also adapts Matt’s five-role triage vocabulary into a simpler solo workflow, folding away `needs-info` and `ready-for-human`.

My read: this is a nice “solo project” variant: don’t overfit Beads to GitHub-like labels; map Matt’s roles into the simplest local lifecycle that actually gets used.

### 4. `mj-meyer/.dotfiles` — modified setup skill that auto-detects Beads

This is not a target project so much as a modified copy of `/setup-matt-pocock-skills`. It adds `.beads/` and `bd list` as discovery signals, proposes Beads by default when present, and says Beads is the best fit because “Blocked by” becomes real dependency edges and AFK-ready slices map onto `bd ready`.

My read: this is probably the shape that should land upstream: detect `.beads/`, generate `docs/agents/issue-tracker.md`, map the labels, then stay out of the way.

## Adjacent but useful: Beads-side “skills” discussions

The broader Beads repo has lots of signal about skills + agents, even when not specifically `mattpocock/skills`.

A key Beads issue says Claude was “struggling to use bd consistently”; the report shows the model ignoring repo instructions, failing to run `bd ready`, using TodoWrite, and not updating/closing Beads issues.  The comments suggest that a structured end-of-session protocol helps, and another user says the `superpowers`-style skills workflow works well, especially brainstorming → writing plans → executing plans → finishing branch; they also say using brainstorming to create a Beads epic and subtasks “does a great job.”

Another Beads issue reports “basically incompatible” behavior with Claude Code + Opus 4.5, but the discussion narrows the problem to discoverability and Claude choosing TodoWrite instead of `bd`. One user says onboarding was confusing but “now that it’s set up I’m flying”; another says the dedicated Beads Claude Code skill is the missing piece; another says even the skill conflicted for them and they preferred Claude’s Todo tool.

## Wins

The strongest wins are:

**Dependency-aware work breakdown.** The Beads model maps naturally to Matt-style “break this into tickets” and “AFK-ready slices”: `bd ready` is a better primitive than a flat issue list when dependencies matter. The modified setup skill in `mj-meyer/.dotfiles` makes this point directly.

**Local-first, low-context tracker.** In the `mattpocock/skills` issue, one user says Beads is faster, less context-polluting than `gh`, and has good separation between description, design, acceptance criteria, and additional context.

**The adapter-doc pattern works.** CrystalMath and vessux show that you do not necessarily need to rewrite Matt’s skills. You can add `docs/agents/issue-tracker.md`, `triage-labels.md`, and `domain.md`, then let Matt’s skills read those as the tracker abstraction.

## Losses / tribulations

**Not merged upstream yet.** Current `setup-matt-pocock-skills` still offers GitHub, GitLab, local markdown, or “Other”; it does not list Beads as a first-class option.

**Beads docs / skill drift has bitten people.** Beads has had issues where skill docs were out of sync with CLI commands and missing many newer commands.  There is also an issue proposing auto-generating `SKILL.md` version/CLI surface from `bd` because manual refresh drifted by multiple minor versions.

**Agents forget or fight the tracker.** Multiple Beads discussions show agents ignoring `bd`, defaulting back to TodoWrite, or needing stronger hooks/skills/templates to stay consistent.

**Beads-generated instructions can be too aggressive.** One issue complains that the injected Beads block can push agents into committing/pushing unexpectedly, including trivial changes and partial micro-commits.  That lines up with my concern: “Land the plane” is useful, but it needs consent boundaries.

**Skill packaging / validation issues.** A user reported Beads skills failing to load in Copilot because command metadata had `argument-hint` syntax issues; `bd` still worked, but they were unsure whether the skills did.

## Bottom line

The combination is promising, but still **pre-standard**.

The best current recipe is:

1. Use `mattpocock/skills` for **thinking/workflow discipline**: grill, triage, specs, tickets, TDD, code review.
2. Use Beads for **durable task state**: dependency graph, ready work, comments, design/acceptance criteria, local-first session continuity.
3. Add a thin project adapter:

   * `docs/agents/issue-tracker.md`
   * `docs/agents/triage-labels.md`
   * `docs/agents/domain.md`
   * one `AGENTS.md` / `CLAUDE.md` section pointing both systems at those docs.
4. Keep Beads instructions **less aggressive** than upstream defaults: no unconditional push/commit, no forced TodoWrite ban unless the agent actually honors it, and explicit consent before destructive or publishing steps.

I would treat CrystalMath and vessux/dotfiles as the most useful patterns to copy, and issue #116 as the upstream place to watch or contribute to.

