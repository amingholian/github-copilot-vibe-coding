---
ai_generated: true
model: "openai/gpt-5.4@unknown"
operator: "johnmillerATcodemag-com"
chat_id: "f62cf86f-6857-4562-8b9d-46319d02acd9"
prompt: |
  create a prompt from the test-driven-development instruction file that will allow me to regenerate the instruction file using the prompt
started: "2026-05-20T08:46:59.5352106-07:00"
ended: "2026-05-20T08:46:59.5352106-07:00"
task_durations:
  - task: "prompt requirements review"
    duration: "00:02:00"
  - task: "prompt authoring"
    duration: "00:06:00"
  - task: "provenance updates"
    duration: "00:02:00"
total_duration: "00:10:00"
ai_log: "ai-logs/2026/05/20/f62cf86f-6857-4562-8b9d-46319d02acd9/conversation.md"
source: "GitHub Copilot Chat"
mode: agent
tools: ["search", "read", "list", "create", "edit"]
description: Generate a repository instruction file that enforces strict test-driven development for programming language source files.
prompt_metadata:
  id: test-driven-development-instruction-file-generator
  title: Test-Driven Development Instruction File Generator
  owner: johnmillerATcodemag-com
  version: 1.0.0
  created: 2026-05-20
  updated: 2026-05-20
  output_path: .github/instructions/test-driven-development.instructions.md
  output_format: markdown
  category: documentation
  tags: [testing, tdd, instructions, unit-tests, workflow]
---

# Test-Driven Development Instruction File Generator

Create a repository instruction file that defines strict test-driven development rules for programming language source files.

## Objective

Produce `.github/instructions/test-driven-development.instructions.md` with clear, enforceable guidance for Red -> Green -> Refactor, including direct unit-test requirements for reusable logic.

## Inputs

- Existing instruction files in `.github/instructions/`
- Current repository test workflow and validation commands
- Existing calculator behavior and test layout
- Current README artifact conventions

## Required Process

1. Review the existing instruction files so the new file matches repository style, tone, and metadata conventions.
2. Scope the instruction file to programming language source files only.
3. Define strict TDD rules that require a failing automated test before the first production edit.
4. Make explicit what counts as Red, Green, and Refactor, including required evidence.
5. Require direct unit tests whenever behavior is implemented behind a reusable function, object, helper, or module boundary.
6. Keep browser or end-to-end tests for interaction parity, but do not allow them to be the only coverage for extracted reusable logic.
7. Include repository-specific workflow guidance for calculator UI tests and direct logic unit tests.
8. Add a quality checklist that can be used during review.
9. Optimize the generated file for both AI and human use with concise, directive wording.

## Required Output File

- Path: `.github/instructions/test-driven-development.instructions.md`
- Format: Markdown with YAML front matter
- Include `applyTo` for programming language file extensions only, not `**/*`

## Required Sections In Generated Instruction File

1. Overview
2. Core Rules
3. Red Phase (Failing Test First)
4. Green Phase (Minimal Passing Change)
5. Refactor Phase (Design Improvement)
6. Test Design Guidance
7. Quality Gates
8. Evidence Requirements
9. Pull Request Expectations
10. Common Anti-Patterns
11. Repository Workflow
12. Required Sequence
13. Repository Example
14. Quality Checklist

## Required Rules

The generated instruction file must include rules that:

- require a newly added or updated failing automated test before the first production edit
- state that an already-green suite does not satisfy Red for a new behavior or refactor target
- require the narrowest relevant test command first, then `npm test`
- require direct unit tests for reusable logic boundaries
- require characterization tests before extracting legacy logic into a new seam
- require reporting of the failing test, failure command, minimal production change, and final passing command
- prohibit adding tests only after code changes and calling that TDD
- distinguish direct unit tests from browser-facing regression tests
- keep the instruction file scoped to programming language files only

## Repository-Specific Expectations

The generated instruction file should explicitly mention:

- browser-facing calculator behavior tests in `tests/calculator.spec.js`
- direct unit tests for reusable calculator logic in a file such as `tests/calculator-engine.spec.js`
- an extraction example where logic moves from `calculator.html` into a reusable module and must gain direct unit tests

## Compliance Requirements

- Follow repository-level AI provenance policy in `.github/instructions/ai-assisted-output.instructions.md`.
- Include complete front matter metadata in the generated instruction file.
- Create required AI logs for the generation chat:
  - `ai-logs/YYYY/MM/DD/<chat-id>/conversation.md`
  - `ai-logs/YYYY/MM/DD/<chat-id>/summary.md`
- Update `README.md` with a short artifact entry linking to the generated instruction file and AI log.

## Output Rules

- Keep language concise, directive, and enforceable.
- Prefer MUST, DO NOT, and explicit validation statements over soft guidance.
- Use bullet lists for actionable rules.
- Avoid vague recommendations and duplicated policy blocks.
- Reference canonical files instead of copying large policy sections.

## Deliverable

A production-ready `.github/instructions/test-driven-development.instructions.md` file that can be committed immediately and used as the canonical TDD standard for programming language files in this repository.
