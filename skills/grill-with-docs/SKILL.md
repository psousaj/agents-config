```yaml
---
name: grill-with-docs
description: Refine a technical design through high-impact questions while continuously producing executable specifications, ADRs, and implementation tasks.
disable-model-invocation: true
---
```

# Grill With Docs

Use the `/grilling` and `/domain-modeling` skills to refine the design and produce implementation-ready documentation.

## Objective

Turn an ambiguous idea into an executable engineering plan with minimal user interruption.

Documentation is the deliverable. Interviewing is only a means to improve it.

## Workflow

### 1. Discover

- Inspect the existing repository, code, documentation, and issues.
- Identify already established requirements and decisions.
- Do not repeat questions previously answered.
- Identify only material gaps that prevent implementation.

### 2. Model

Use `/domain-modeling` to identify:

- Domain entities and relationships
- Invariants
- State transitions
- External boundaries
- Failure modes
- Security constraints

Resolve routine modeling decisions autonomously.

### 3. Challenge

Use `/grilling` selectively.

Ask about high-impact product and architectural decisions only.

For each question:

- Explain why the decision matters.
- Recommend a default.
- Describe meaningful alternatives.
- State what would happen if the recommendation were adopted.

Do not ask for approval of internal implementation details.

### 4. Document Incrementally

Produce or update:

- Feature specifications
- Architecture Decision Records (ADRs)
- Domain glossary
- Implementation tasks
- Acceptance criteria
- Test requirements

Create ADRs only for consequential, cross-cutting decisions.

Do not create an ADR for every enum, struct, function, or internal design choice.

### 5. Deliver

When no high-impact blockers remain:

- Finalize the specifications.
- Break implementation into independently testable tasks.
- Record dependencies.
- Identify release and safety gates.
- Update existing issues or create new ones when requested.

Do not continue interviewing after the design is sufficiently actionable.

## Definition of Done

The session is complete when:

1. Major product and architectural decisions are resolved.
2. Domain invariants and boundaries are documented.
3. Specs contain observable acceptance criteria.
4. Tasks can be implemented independently where practical.
5. Tests and validation requirements are explicit.
6. Non-blocking details are delegated to the implementing agent.

Prefer implementation-ready specifications over exhaustive theoretical modeling.

## Operating Principle

Ask less. Investigate more. Decide responsibly. Deliver artifacts.