---
ai_generated: true
model: "openai/gpt-5.3-codex@unknown"
operator: "johnmillerATcodemag-com"
chat_id: "380dcaef-538d-40bf-9b00-5036801ca53a"
prompt: |
  create an instruction file for test driven development
started: "2026-05-20T00:00:00Z"
ended: "2026-05-20T00:18:00Z"
task_durations:
  - task: "requirements and pattern review"
    duration: "00:05:00"
  - task: "tdd instruction authoring"
    duration: "00:10:00"
  - task: "provenance and readme updates"
    duration: "00:03:00"
total_duration: "00:18:00"
ai_log: "ai-logs/2026/05/20/380dcaef-538d-40bf-9b00-5036801ca53a/conversation.md"
source: "GitHub Copilot Chat"
applyTo: "**/*.{js,mjs,cjs,ts,mts,cts,jsx,tsx,py,java,cs,go,rb,php,rs,cpp,c,h,hpp,swift,kt,kts,scala}" 
---

# Test-Driven Development Instructions

## Overview

This document defines test-driven development (TDD) expectations for this repository.

**Target Audience**: Developers and AI assistants implementing or changing behavior in programming language files
**Scope**: New features, bug fixes, and refactors that affect runtime behavior in programming language source files

**Related Documentation**:

- [AI-Assisted Output Instructions](ai-assisted-output.instructions.md)
- [Evergreen Software Development](evergreen-software-development.instructions.md)
- [Documentation Authoring Instructions](documentation.instructions.md)

## Core Rules

- Follow the TDD loop: Red -> Green -> Refactor.
- Write or update a failing automated test before the first production edit.
- Keep each cycle small: one behavior change per test when practical.
- Do not commit a behavior change without a test that proves it.
- Refactor only after tests pass.
- Existing passing tests do not satisfy the Red step for a new behavior or refactor target.
- For refactors, add at least one new characterization test for the intended seam or module boundary before moving production code.
- A change is not TDD-compliant unless the contributor can show the Red result, the minimal Green change, and the final passing validation command.
- When behavior is implemented behind a reusable function, object, or module boundary, create unit tests for that boundary instead of relying only on UI or end-to-end tests.

## Red Phase (Failing Test First)

- Start by specifying the expected behavior with a focused test.
- Ensure the test fails for the right reason.
- Use test names that describe behavior, not implementation details.
- Prefer deterministic tests with clear inputs and outputs.
- For bug fixes, create a regression test that reproduces the bug.
- Red is complete only when a newly added or modified automated test fails for the intended behavior.
- A pre-existing green suite does not count as Red.
- A failing lint, typecheck, or unrelated test does not count as Red unless it is the exact executable check that specifies the changed behavior.
- Record or report the failing test name and the command used to demonstrate the failure.

## Green Phase (Minimal Passing Change)

- Implement the smallest code change needed to pass the failing test.
- Avoid speculative abstractions during the Green phase.
- Keep the scope constrained to the behavior under test.
- Run the relevant tests immediately after the change.
- Re-run the same narrow test or test slice used in Red before widening validation scope.
- Do not batch unrelated production edits into the same Green step.
- If the change introduces a new reusable logic boundary, create the unit test file or unit test coverage in the same change.

## Refactor Phase (Design Improvement)

- Refactor only while all tests are passing.
- Remove duplication and improve naming, structure, and boundaries.
- Keep public behavior stable during refactors.
- Re-run relevant tests after each meaningful refactor step.
- For structural refactors, the first test should validate the new seam, extracted module boundary, or characterization contract that the refactor depends on.
- If the refactor introduces a reusable logic module, add or update direct module-boundary tests in addition to any UI regression tests.
- Do not stop at seam creation alone; once the reusable boundary exists, add unit tests that exercise its behavior directly.

## Test Design Guidance

- Test behavior at the module boundary whenever possible.
- Use unit tests for business rules and fast feedback.
- Add integration or end-to-end tests only where interaction risk is meaningful.
- Avoid over-mocking; mock only external boundaries.
- Prefer table-driven or data-driven tests for repeated rule validation.
- Validate edge cases explicitly: invalid input, empty state, numeric boundaries, and unsupported combinations.
- Prefer characterization tests before moving legacy behavior behind a new abstraction.
- When UI code contains domain logic, first create a failing test that proves the logic seam you intend to extract.
- Create unit tests for pure or mostly pure calculator logic such as parsing, evaluation, formatting, percentage rules, trigonometric rules, and memory state transitions.
- Prefer one unit-test file per extracted logic module when practical.
- Use browser tests to verify integration and interaction parity; use unit tests to verify rules and state transitions directly.

## Quality Gates

- New behavior includes tests that fail before implementation and pass after.
- Bug fixes include a regression test.
- Existing tests remain passing.
- Test names and assertions are specific and readable.
- Refactors do not change externally observable behavior unless explicitly intended.
- Refactor work includes evidence that a new or updated failing test existed before the first production edit.
- The final validation includes the narrow changed-slice check and `npm test` unless the user explicitly requests a narrower stop point.
- Reusable logic introduced or modified by the change has direct unit-test coverage.

## Evidence Requirements

- Every behavior change or refactor must identify the specific test added or updated for Red.
- Every behavior change or refactor must report the command that produced the initial failure.
- Every behavior change or refactor must report the minimal production files changed for Green.
- Every behavior change or refactor must report the final passing command.
- If strict TDD could not be followed, state the exact blocker and why no equivalent executable Red step was possible.
- If unit tests were required by the change, identify the unit test file that was created or updated.

## Pull Request Expectations

- Describe the Red-Green-Refactor sequence in the PR notes.
- Identify which tests were added or updated and why.
- Call out any behavior that could not be covered by automated tests, with rationale.
- Avoid mixing unrelated refactors with behavior changes in the same PR.

## Common Anti-Patterns

- Writing production code before writing a failing test.
- Adding large batches of production code for one test case.
- Treating passing tests as optional for refactor work.
- Testing private implementation details instead of observable behavior.
- Keeping flaky tests instead of fixing determinism.
- Starting a refactor with existing green tests and calling that Red.
- Adding a test only after the production change and calling it TDD.
- Using one new test to justify multiple unrelated behavior changes.
- Widening from a narrow failing test straight to broad refactors before the first Green pass.
- Extracting reusable logic into a module but leaving it covered only by UI tests.
- Claiming module-boundary coverage without any direct unit tests for the extracted logic.

## Repository Workflow

- Use `npm test` as the default validation command for this repository.
- Use the narrowest executable test command first, then run `npm test` before completion.
- When changing calculator UI behavior, update or add browser-facing tests in `tests/calculator.spec.js`.
- When extracting or adding reusable calculator logic, create direct unit tests alongside UI regression tests.
- Place direct calculator logic tests in a dedicated unit-test file such as `tests/calculator-engine.spec.js` when a reusable engine or helper module exists.
- Keep behavior contracts in tests aligned with user-visible calculator outcomes and any explicit module seam introduced by the change.

## Required Sequence

1. Add or update one focused automated test.
2. Run the narrowest relevant test command and confirm it fails.
3. Make the smallest production change needed to pass that test.
4. Re-run the same narrow test command and confirm it passes.
5. Add or update direct unit tests if the change introduced or modified reusable logic.
6. Perform refactor-only cleanup while tests remain green.
7. Run `npm test`.

## Repository Example

- If extracting calculator logic from `calculator.html` into a new module, first add a failing test that proves the new engine seam exists or is importable.
- After that seam test fails, implement the minimal extraction needed to make it pass, add direct unit tests for the extracted engine behavior, then re-run `npm test` before continuing.

## Quality Checklist

- [ ] A failing test was written before behavior implementation.
- [ ] The failing test was newly added or updated for this exact change.
- [ ] The failing test result was observed before the first production edit.
- [ ] The minimal production change was made to make the test pass.
- [ ] The same narrow test used for Red was re-run for Green.
- [ ] Refactor work was done only after tests passed.
- [ ] Edge cases for changed behavior are covered.
- [ ] Regression tests exist for bug fixes.
- [ ] Refactors introduced or preserved testable seams where domain logic changed structure.
- [ ] Reusable logic introduced or modified by the change has direct unit tests.
- [ ] `npm test` passes after the change.
- [ ] Notes explain the Red-Green-Refactor sequence, test coverage, and any known gaps.
