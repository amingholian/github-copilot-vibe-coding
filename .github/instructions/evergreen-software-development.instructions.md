---
ai_generated: true
model: "openai/gpt-5.4@unknown"
operator: "johnmillerATcodemag-com"
chat_id: "acaf6075-7dde-4cc7-b293-0829934f7cc3"
prompt: |
  create an instruction file for evergreen software development
started: "2026-05-18T11:46:20.3574109-07:00"
ended: "2026-05-18T11:46:20.3574109-07:00"
task_durations:
  - task: "instruction design"
    duration: "00:00:00"
  - task: "instruction file creation"
    duration: "00:00:00"
  - task: "documentation update"
    duration: "00:00:00"
total_duration: "00:00:00"
ai_log: "ai-logs/2026/05/18/acaf6075-7dde-4cc7-b293-0829934f7cc3/conversation.md"
source: "GitHub Copilot Chat"
applyTo: "**/*"
---

# Evergreen Software Development

## Overview

This document defines evergreen software development practices for this repository. Use these instructions to keep code resilient to changing requirements, evolving dependencies, and normal maintenance pressure.

**Target Audience**: Developers and AI assistants making code, documentation, or architecture changes
**Scope**: Day-to-day implementation, refactoring, testing, dependency choices, and long-term maintainability decisions

**Related Documentation**:

- [AI-Assisted Output Instructions](ai-assisted-output.instructions.md)
- [Creating New Instruction Files](instruction-files.instructions.md)

## Table of Contents

- Core Principles
- Design Rules
- Implementation Guidance
- Dependency Rules
- Testing And Validation
- Documentation Expectations
- Common Failure Patterns
- Quality Checklist

## Core Principles

- Prefer explicit models over stringly typed behavior.
- Make the easiest path the maintainable path.
- Optimize for change, not just for the current requirement.
- Keep policy, logic, and presentation separate when practical.
- Encode assumptions in code, tests, or validation rather than tribal knowledge.

## Design Rules

### Model Domain Behavior Explicitly

- Represent business rules with named functions, data structures, and state transitions.
- Avoid hiding behavior inside regex chains, ad hoc string manipulation, or runtime evaluation when a parser, state machine, or typed model is more appropriate.
- Treat every shortcut that saves lines today but obscures behavior tomorrow as technical debt.

### Prefer Stable Interfaces

- Keep module boundaries narrow and purposeful.
- Expose small public APIs and keep internal helpers private.
- Do not let UI details control core logic contracts.
- When adding a feature, extend an existing abstraction only if it still describes the problem clearly.

### Keep Concerns Separated

- Separate rendering, state management, validation, and domain logic.
- Avoid large files that mix styling, control flow, persistence, and business rules unless the project is intentionally trivial.
- When a file starts serving multiple reasons to change, split it.

## Implementation Guidance

### Write For Extension

- Add new behavior in a way that does not require editing many unrelated branches.
- Prefer lookup tables, strategy maps, or dedicated objects over long condition chains when supported behaviors may grow.
- Make unsupported input fail fast with clear validation.

### Avoid Hidden Runtime Semantics

- Do not rely on language runtime parsing or evaluation when the application needs its own rules.
- Do not couple correctness to incidental language behavior such as coercion, operator precedence side effects, or formatting quirks.
- Normalize external input before processing it, then validate against an explicit contract.

### Keep State Intentional

- Use state names that explain lifecycle and meaning.
- Limit mutable shared state.
- Update related state together so UI and logic cannot drift apart.
- Remove dead flags, dead styles, and unused helpers promptly.

## Dependency Rules

- Add a dependency only when it removes meaningful maintenance burden.
- Prefer mature, well-supported libraries over niche packages for critical concerns.
- Do not add a library for trivial formatting or small utility needs that are clearer in local code.
- Reassess old dependencies periodically for support status, release activity, and security posture.
- Wrap third-party libraries behind local seams when the dependency is central to application behavior.

## Testing And Validation

- Add tests around behavior that is easy to regress and hard to inspect manually.
- Test domain rules independently from UI whenever possible.
- Cover edge cases that usually break aging code: invalid input, empty state, rounding, overflow, and unsupported combinations.
- Prefer narrow validation first: the changed behavior, then the affected typecheck, lint, or build step.
- If no automated test exists for a critical code path, add one when the change increases long-term complexity.
- Before structural refactors, add a failing characterization test at the seam you intend to introduce or preserve.
- When logic and UI are mixed, prefer introducing a testable seam before broad code movement.
- Do not treat an already-green suite as evidence that a new refactor target has completed the Red step.

## Documentation Expectations

- Document why an abstraction exists, not just what it does.
- Keep README and instruction files aligned with the current structure of the repo.
- Record architectural constraints where future contributors will encounter them.
- When introducing a non-obvious pattern, leave a concise explanation near the code or in the nearest relevant doc.

## Common Failure Patterns

- Runtime evaluation instead of explicit parsing or modeling
- One large file that mixes unrelated responsibilities
- Repeated business logic in event handlers, formatters, and validators
- Hard-coded values with no named meaning
- Features added by stacking conditionals instead of extending a stable abstraction
- Documentation that describes the intended future state rather than the current repository state

## Quality Checklist

- [ ] Domain behavior is represented explicitly
- [ ] Core logic is not tightly coupled to UI or formatting
- [ ] Validation rejects unsupported input clearly
- [ ] New code can be extended without broad edits
- [ ] Tests or executable validation cover the changed behavior
- [ ] Dependencies are justified and supportable
- [ ] Documentation reflects the current implementation
