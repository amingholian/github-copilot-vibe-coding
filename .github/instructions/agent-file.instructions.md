---
ai_generated: true
model: "openai/gpt-5.3-codex@unknown"
operator: "johnmillerATcodemag-com"
chat_id: "6e12419b-016a-4376-ac02-08f264cfc1a5"
prompt: |
  create an agents instruction file
started: "2026-05-20T00:00:00Z"
ended: "2026-05-20T00:10:00Z"
task_durations:
  - task: "instruction pattern review"
    duration: "00:03:00"
  - task: "agent instruction authoring"
    duration: "00:05:00"
  - task: "provenance and readme updates"
    duration: "00:02:00"
total_duration: "00:10:00"
ai_log: "ai-logs/2026/05/20/6e12419b-016a-4376-ac02-08f264cfc1a5/conversation.md"
source: "GitHub Copilot Chat"
applyTo: "**/*.agent.md"
---

# AI Instructions: Agent File Creation

## Overview

This file defines repository standards for creating custom agent definition files.

**Target Audience**: Developers and AI assistants creating or updating custom agent files

## Scope

- Applies to all files matching `**/*.agent.md`.
- Covers naming, structure, operational constraints, and validation.
- Complements repository-wide provenance requirements in `.github/instructions/ai-assisted-output.instructions.md`.

## File Structure

### Naming And Location

- Use kebab-case filenames: `<agent-name>.agent.md`.
- Keep one agent definition per file.
- Prefer `.github/agents/` as the default location unless the project already uses another location.

### Required Sections

Each agent file should include the following sections in this order:

1. Purpose
2. Activation Criteria
3. Capabilities
4. Limits And Safety Rules
5. Workflow
6. Response Contract
7. Validation Checklist

## Authoring Rules

### Purpose

- Define the primary job in one short paragraph.
- Make the value and domain explicit.
- Avoid broad claims such as "handles everything."

### Activation Criteria

- Describe when to use the agent and when not to use it.
- Include concrete trigger phrases or intent examples.
- Include at least one out-of-scope example.

### Capabilities

- List only actions the agent can reliably perform.
- Group capabilities by outcome, not by internal implementation details.
- Keep capability descriptions short and testable.

### Limits And Safety Rules

- State hard boundaries clearly.
- Define what the agent must refuse or escalate.
- Require preserving existing repository constraints and policies.

### Workflow

- Define a deterministic sequence for handling tasks.
- Include context gathering, implementation, validation, and final reporting.
- Require explicit handling for blockers and missing requirements.

### Response Contract

- Specify expected output shape for successful runs.
- Specify output shape for blocked or partial results.
- Require concise references to files changed and checks performed.

## Quality Checklist

- [ ] Filename is kebab-case and ends with `.agent.md`
- [ ] Purpose and scope are explicit and non-overlapping
- [ ] Activation criteria include both in-scope and out-of-scope cases
- [ ] Capabilities are concrete and testable
- [ ] Safety constraints are explicit and enforceable
- [ ] Workflow includes validation and blocker handling
- [ ] Response contract defines success and failure output
- [ ] Content is concise and avoids duplicated policy text

## Common Anti-Patterns

- Vague purpose that overlaps multiple unrelated domains
- No out-of-scope guidance, causing unnecessary agent invocation
- Capability lists that describe tools instead of outcomes
- Missing safety limits for destructive operations
- Response formats that omit validation or changed-file references
