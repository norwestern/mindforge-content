# Verify protocol

Run after generating, before opening a PR. Two independent subagent passes —
dispatch both in parallel. Neither sees the other's output.

## Pass 1 — blind solve (questions only)

For each generated question, give a fresh subagent ONLY: `type`, `prompt`,
`options` (mcq). Strip `answerIndex`/`answer`/`acceptable`, `pitfall`, `hints`,
difficulty. The solver must (a) answer, (b) flag ambiguity or a second
defensible answer if it sees one. A finding is: solver's answer ≠ answer key,
or an ambiguity flag.

## Pass 2 — rubric review (all content)

A fresh subagent gets `authoring/RUBRIC.md`, the generated items, and the
concept's existing content (for R6/R8). It returns findings only.

## Fix loop

Regenerate ONLY the items with findings, then re-verify those items (both
passes). Maximum 3 rounds. Items still failing after round 3 are dropped —
list every dropped item and its last finding in the PR body. Never silently
trim, never PR an unverified item. A subagent that dies or times out counts
as findings-for-everything-it-covered: regenerate or drop.

## PR body template

- Generated: <n> questions across <concepts>, <n> hints backfilled
- Verify: <n>/<n> solved blind on round 1, <n> regenerated, <n> dropped
- Dropped: <id> — <last finding> (or "none")
