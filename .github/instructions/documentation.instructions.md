---
ai_generated: true
model: "openai/gpt-5.3-codex@unknown"
operator: "johnmillerATcodemag-com"
chat_id: "aae6cce1-78ed-4c45-a2fc-36cb511a2fba"
prompt: |
  Follow instructions in #prompt:documentation-instruction-file-generator.prompt.md
started: "2026-05-19T10:22:00Z"
ended: "2026-05-19T10:37:00Z"
task_durations:
  - task: "instruction pattern review"
    duration: "00:04:00"
  - task: "documentation standards authoring"
    duration: "00:09:00"
  - task: "provenance and readme updates"
    duration: "00:02:00"
total_duration: "00:15:00"
ai_log: "ai-logs/2026/05/19/aae6cce1-78ed-4c45-a2fc-36cb511a2fba/conversation.md"
source: ".github/prompts/documentation-instruction-file-generator.prompt.md"
applyTo: "{README.md,docs/**/*.md}"
---

# Documentation Authoring Instructions

## Overview

This document defines how documentation is authored, reviewed, and maintained in this repository.

**Target Audience**: Developers and AI assistants creating or updating repository documentation

## Scope

- Applies to Markdown documentation intended for contributor or project reference.
- Primary targets in this repository are `README.md` and files under `docs/`.
- Does not override canonical provenance and logging policy in `.github/instructions/ai-assisted-output.instructions.md`.
- Does not replace instruction-file-specific requirements in `.github/instructions/instruction-files.instructions.md`.

## Documentation Principles

- Write for fast comprehension: make purpose, inputs, outputs, and next action obvious.
- Prefer specific, verifiable statements over generic guidance.
- Keep docs current with code and repository structure.
- Minimize token and reader cost by removing duplication and filler.
- Reference canonical sources instead of copying policy blocks.

## Content Structure Rules

- Start with a short overview describing purpose and intended audience.
- Use stable section order when practical: overview, prerequisites, steps, validation, troubleshooting.
- Keep headings descriptive and task-oriented.
- Use lists for procedures and checklists for validation criteria.
- Keep paragraphs short; split when a paragraph mixes goals and procedures.
- Add a "Last Updated" note only when the document is operationally sensitive.

## Writing Style Rules

- Use direct imperative language for instructions.
- Prefer concrete verbs: "run", "update", "verify", "remove".
- Define acronyms on first use unless ubiquitous in the repo.
- Avoid subjective terms like "easy", "simple", or "obvious".
- Avoid future-tense promises; describe current behavior and required actions.
- Keep one idea per bullet.

## Linking and Reference Rules

- Use relative links for repository files.
- Link to the nearest canonical source instead of duplicating the same rule in multiple files.
- Ensure every command or path reference is accurate and currently resolvable.
- When referencing a policy requirement, name the source file explicitly.
- Remove or fix stale links in the same change where they are discovered.

## Examples and Snippet Rules

- Include examples when instructions are non-obvious or error-prone.
- Keep snippets minimal but executable.
- Label snippets with language fences when possible.
- Do not include placeholder commands that cannot run as written.
- For command sequences, include expected outcome checks.
- For configuration snippets, show only fields relevant to the rule being explained.

## Maintenance and Update Rules

- Update docs in the same pull request as behavior changes whenever feasible.
- When a change affects setup, usage, or constraints, update `README.md`.
- Keep AI-assisted artifact entries in `README.md` aligned with newly created durable docs.
- During review, verify links, examples, and file paths against the current repository.
- Revisit high-value operational docs on a regular cadence (at least quarterly).

## Common Anti-Patterns

- Long narrative blocks with no actionable steps.
- Repeating the same rule across multiple docs instead of linking a canonical source.
- Snippets that are incomplete, outdated, or untested.
- Documentation that describes intended future state as if already implemented.
- Checklists that cannot be validated objectively.

## Quality Checklist

- [ ] Purpose and audience are stated in the overview.
- [ ] Instructions are specific, actionable, and testable.
- [ ] Section structure is clear and task-oriented.
- [ ] Links are relative, valid, and point to canonical sources where appropriate.
- [ ] Examples are minimal, accurate, and executable.
- [ ] Content reflects the current repository behavior and structure.
- [ ] Redundant or duplicated policy text has been removed.
- [ ] `README.md` is updated when contributor-facing behavior changes.
- [ ] Documentation changes are reviewed with the same rigor as code changes.
