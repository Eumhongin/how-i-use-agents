# The Harness, Explained

The roles (planner, architect, designer, developer, reviewer) are the visible part.
The harness is what makes them reliable. It's four rules plus a gate.

## 1. Typed I/O — Scope · Goal · Constraints · Output

A call to any agent carries only those four fields. Sounds trivial; it's the thing
that stops an agent from quietly redesigning your system while "fixing a bug." If
it isn't in Scope, it isn't theirs to touch. If it isn't in the Output contract,
they don't return it.

## 2. Status Protocol — four states, fixed format

Every agent ends with exactly one of `DONE`, `DONE_WITH_CONCERNS`,
`NEEDS_CONTEXT`, `BLOCKED`. Two payoffs:

- **Traceability.** A fixed end-format means you can always see what an agent did,
  what it produced, and what it was unsure about — without re-reading everything.
- **Honest endings.** `DONE_WITH_CONCERNS` lets an agent finish *and* flag doubt,
  instead of silently papering over a conflict to look successful.

## 3. No Guessing — stop and ask

Ambiguous? Contradictory? Out of scope? The agent does not proceed on a guess; it
reports `NEEDS_CONTEXT` / `BLOCKED` and says what it needs. Most "the AI
hallucinated" failures are really "the AI guessed because nothing told it to stop."
This rule removes the incentive to guess.

## 4. Human in the Loop — gates, not autopilot

A person confirms at each stage (spec, design, …). The agents propose; the human
decides. Disagreement is surfaced as `DONE_WITH_CONCERNS`, not resolved unilaterally.

## The Review Gate

The reviewer returns pass / fail. On fail, the developer reworks against `file:line`
notes, and it loops. Output is "done" only after it passes. This is the difference
between a pipeline and just calling an agent repeatedly and hoping.

## Why split roles at all?

A single agent told to "do everything" optimizes for *looking finished*. Splitting
the work and putting an independent reviewer at the end changes the optimization
target to *passing verification*. The harness is what keeps each role inside its
lane while that happens.

## This is an early skeleton

Worth saying plainly: this is a starting point, not a finished method. The status
protocol and the review gate are the parts I'd keep first; everything else is still
moving. I expect each role to get sharper, and the roster to split into more
specialized roles over time. If you fork it, treat it the same way — a frame to
adapt, not a spec to follow.
