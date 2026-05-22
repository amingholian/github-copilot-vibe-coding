---
ai_generated: true
model: "openai/gpt-5.3-codex@unknown"
operator: "johnmillerATcodemag-com"
chat_id: "950941c4-4c36-4ba9-b757-4c9539968e87"
prompt: |
  create a prompt file that generates an insrtuction file for documentation
started: "2026-05-19T00:00:00Z"
ended: "2026-05-19T00:12:00Z"
task_durations:
  - task: "requirements review"
    duration: "00:03:00"
  - task: "prompt authoring"
    duration: "00:07:00"
  - task: "provenance updates"
    duration: "00:02:00"
total_duration: "00:12:00"
ai_log: "ai-logs/2026/05/19/950941c4-4c36-4ba9-b757-4c9539968e87/conversation.md"
source: "GitHub Copilot Chat"
mode: agent
tools: ["search", "read", "list", "create", "edit"]
description: Generate a complete repository instruction file for documentation standards and maintenance workflows.
prompt_metadata:
  id: documentation-instruction-file-generator
  title: Documentation Instruction File Generator
  owner: johnmillerATcodemag-com
  version: 1.0.0
  created: 2026-05-19
  updated: 2026-05-19
  output_path: .github/instructions/documentation.instructions.md
  output_format: markdown
  category: documentation
  tags: [documentation, instructions, standards, authoring, governance]
---

# Documentation Instruction File Generator

Create a new repository instruction file that defines how documentation should be authored, reviewed, and maintained.

## Objective

Produce `.github/instructions/documentation.instructions.md` with clear, enforceable rules for writing and updating documentation in this repository.

## Inputs

- Existing instruction files in `.github/instructions/`
- Current repository structure and docs
- Existing README conventions

## Required Process

1. Review existing instruction files to align style, tone, and metadata conventions.
2. Detect where documentation currently lives in the repository.
3. Define documentation standards that are specific, testable, and maintainable.
4. Include rules for structure, writing style, links, examples, and update cadence.
5. Add a quality checklist that can be used in PR reviews.
6. Ensure the generated file is optimized for AI and human consumption with concise, non-redundant wording.

## Required Output File

- Path: `.github/instructions/documentation.instructions.md`
- Format: Markdown with YAML front matter
- Include `applyTo` pattern suitable for documentation files (for example `**/*.md`), except where this would create circular conflicts with existing instruction files.

## Required Sections In Generated Instruction File

1. Overview
2. Scope
3. Documentation Principles
4. Content Structure Rules
5. Writing Style Rules
6. Linking and Reference Rules
7. Examples and Snippet Rules
8. Maintenance and Update Rules
9. Common Anti-Patterns
10. Quality Checklist

## Compliance Requirements

- Follow repository-level AI provenance policy in `.github/instructions/ai-assisted-output.instructions.md`.
- Include complete front matter metadata in the generated instruction file.
- Create required AI logs for the generation chat:
  - `ai-logs/YYYY/MM/DD/<chat-id>/conversation.md`
  - `ai-logs/YYYY/MM/DD/<chat-id>/summary.md`
- Update `README.md` with a short artifact entry linking to the generated instruction file and AI log.

## Output Rules

- Keep language concise and directive.
- Use bullet lists for actionable rules.
- Avoid vague recommendations.
- Do not duplicate large policy blocks from other instruction files; reference canonical files instead.

## Deliverable

A production-ready `.github/instructions/documentation.instructions.md` file that can be committed immediately and used by contributors and AI agents as the canonical documentation authoring standard.
