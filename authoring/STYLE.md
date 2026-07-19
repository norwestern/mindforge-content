# Content style guide

House voice for every concept and question in this registry. Generation skills
read this before writing anything; it wins over model defaults.

## Voice: why-first

Every concept teaches *why it was invented* before *what it is*. The
`backstory` frontmatter is the pain before the technique existed — concrete,
specific, no marketing tone. Lesson bodies follow the shape of the existing
concepts: **The problem it solves → The idea → The catch → When to reach for it.**

## Questions

- Types: `mcq` (4 options, exactly one defensibly correct), `fill-in`
  (short factual answer; list common phrasings in `acceptable`), `trace`
  (small concrete scenario, single deterministic answer).
- `id`: AI-generated questions use `<conceptId>-ai-q<N>`, numbered sequentially
  from 1 per concept. Never reuse or renumber an existing id — ids are
  provenance and attempt-history keys.
- `pitfall`: the real misconception a wrong answer reveals — never a
  restatement of the correct answer.
- `hints`: 1–3 entries, an escalating ladder:
  1. *Nudge* — point at what to focus on, no technique named.
  2. *Approach* — name the technique or property, no answer.
  3. *Near-answer* — everything but the final value.
  The last hint must still not state the answer outright.

## Difficulty (1–5)

1 recall/definition · 2 single-step application · 3 multi-step or edge case ·
4 combines prerequisite concepts · 5 adversarial edge (rare; earn it).

## Hygiene

- Terminology must match the concept file (e.g. "index", not "position/offset" interchangeably).
- No trick questions, no trivia about syntax of a specific language unless the concept is about it.
- Prompts self-contained: solvable without having the lesson open.
