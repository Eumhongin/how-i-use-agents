# Common Rules (The Harness)

> Every agent MUST follow these rules, regardless of role.
> This file is the harness: the roles do the work, these rules keep them honest.

## I/O Boundary

An agent call carries only four things:

- **Scope** — what part of the system is in play
- **Goal** — what "done" means for this call
- **Constraints** — what must not change / must be respected
- **Output** — the expected deliverable and its format

Agents do not reach outside this boundary, and do not act in another role's
domain (e.g. the developer does not change the spec).

## Status Reporting

All agents report exactly one of the following four statuses on completion.

| Status                 | Meaning                          | Next Action                       |
|------------------------|----------------------------------|-----------------------------------|
| **DONE**               | Completed                        | Proceed to next step              |
| **DONE_WITH_CONCERNS** | Completed, but with reservations | Review concerns before proceeding |
| **NEEDS_CONTEXT**      | Missing information              | Provide info and restart          |
| **BLOCKED**            | Cannot proceed                   | Escalate to a human               |

### Report Format

```
- Status: DONE | DONE_WITH_CONCERNS | NEEDS_CONTEXT | BLOCKED
- Work summary: what was done
- Deliverables: files created / modified
- Concerns / Blockers: (if any)
```

## Escalation (No Guessing)

**When unsure, stop and ask. A question beats a wrong guess.**

Stop and escalate when:
- requirements are ambiguous or have multiple interpretations
- a contradiction is found with a previous stage's deliverable
- scope significantly exceeds expectations
- proceeding without confidence would affect other agents' work

How: report `NEEDS_CONTEXT` or `BLOCKED`, and state exactly what is unclear
and what information is needed.

## Collaboration

- Respect and faithfully reflect previous stages' deliverables.
- Do not encroach on other roles' domains.
- When you disagree, report `DONE_WITH_CONCERNS` and let the human decide.
