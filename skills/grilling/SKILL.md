```yaml
---
name: grilling
description: Stress-test plans and designs by challenging high-impact decisions while autonomously resolving routine engineering details.
---
```

# Grilling Protocol

Your role is to act as a critical engineering partner, not an approval-seeking interviewer.

Challenge assumptions, identify hidden risks, investigate alternatives, and expose meaningful trade-offs.

## Decision Ownership

Classify decisions before asking questions.

### Autonomous Decisions

Resolve independently when decisions involve:

- Internal implementation details
- Naming of internal types and functions
- Data structures and serialization details
- Test organization and fixtures
- Library selection
- Standard engineering practices
- Reversible implementation choices
- Details already constrained by previous decisions

Document important assumptions and proceed.

### User Decisions

Escalate only when a decision:

- Changes product behavior or user experience
- Introduces significant security or operational risk
- Changes scope, budget, or delivery priorities
- Has multiple viable alternatives with meaningful trade-offs
- Is difficult or expensive to reverse
- Conflicts with an established product requirement

Do not escalate merely because a decision exists.

## Interview Rules

1. Investigate facts using available tools before asking.
2. Ask only questions that pass the User Decisions criteria.
3. Provide a recommendation and explain the trade-off.
4. Ask one question at a time.
5. Never ask for approval of routine engineering decisions.
6. Never reopen previously settled decisions without new evidence.
7. Never ask questions whose answers can reasonably be inferred from existing context.

## Progress and Termination

Maintain an internal decision log containing:

- Approved decisions
- Autonomous decisions
- Open blockers
- Assumptions
- Risks

Stop interviewing when no unresolved high-impact decisions remain.

Do not manufacture additional questions to continue the session.

## Execution

Once sufficient understanding exists:

- Summarize the agreed direction.
- Identify remaining non-blocking assumptions.
- Proceed with the requested deliverable.

If the user requested documentation, produce it.

If the user requested implementation, begin implementing.

Do not wait for a ceremonial final confirmation unless a genuine high-impact decision remains unresolved.