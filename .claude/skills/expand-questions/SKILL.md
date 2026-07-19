---
name: expand-questions
description: Generate verified question variants + hint ladders for existing concepts. Use when asked to expand, deepen, or add questions/hints for a concept in this content repo.
---

# Expand questions

Adds AI-generated question variants (with hint ladders) to existing concepts,
and backfills hint ladders onto existing questions. Never touches concept
prose. One branch + PR per invocation, however many concepts.

Arguments: one or more concept ids (e.g. `arrays hash-map two-pointers`).

## Preconditions — stop with a clear message if any fail

1. Sibling app checkout exists: `../mindforge/scripts/validate-pack.ts` is
   readable. If not: "clone norwestern/mindforge as a sibling checkout first".
2. Each concept id resolves to `packs/<category>/<ns>/concepts/<id>.md` with a
   matching `questions/<id>.yaml`.

## Steps

1. **Read context**: the concept file(s), their questions yaml, `pack.json`,
   `authoring/STYLE.md`, and one other concept in the pack as a style exemplar.
2. **Generate** per concept, into `questions/<id>.yaml`:
   - ~10 new questions: difficulty spread 2×1, 3×2, 3×3, 2×4 (add a 5 only if
     the concept genuinely supports one), mixing mcq / fill-in / trace.
   - Ids `<conceptId>-ai-q<N>`, numbered from 1 (or after the highest existing
     `-ai-q` number).
   - Every new question: `pitfall` + `hints` ladder per STYLE.md.
   - Backfill `hints` (1–3) onto existing questions that lack them. Do not
     change any other field of an existing question.
3. **Verify** per `authoring/VERIFY.md`: parallel blind-solve + rubric
   subagents, fix loop max 3 rounds, drop-and-report failures.
4. **Validate**: `npx tsx ../mindforge/scripts/validate-pack.ts packs/<category>/<ns>`
   must exit 0. Fix schema errors and re-run until clean.
5. **Version bump**: bump `pack.json` minor version once per branch (content
   addition = minor). The registry build rejects re-publishing a changed pack
   at the same version.
6. **PR**: branch `content/expand-questions-<YYYY-MM-DD>`. Commit message:
   `feat(<ns>): expand <concept ids> question banks`. PR body follows the
   template at the end of `authoring/VERIFY.md`. Do not merge — the human
   review of that PR is the final quality gate.
