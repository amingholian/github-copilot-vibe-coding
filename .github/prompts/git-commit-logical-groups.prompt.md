---
ai_generated: true
model: "openai/gpt-4o@2024-11-20"
operator: "johnmillerATcodemag-com"
chat_id: "f484659e-32e1-441a-958c-e33d2d7925f1"
prompt: |
  create a prompt file the commits changes in the git workspace in logical groups
started: "2026-05-19T00:00:00Z"
ended: "2026-05-19T00:10:00Z"
task_durations:
  - task: "requirements review"
    duration: "00:02:00"
  - task: "prompt authoring"
    duration: "00:06:00"
  - task: "provenance updates"
    duration: "00:02:00"
total_duration: "00:10:00"
ai_log: "ai-logs/2026/05/19/f484659e-32e1-441a-958c-e33d2d7925f1/conversation.md"
source: "GitHub Copilot Chat"
mode: agent
agent: .github/agents/git-expert.agent.md
tools: ["search", "read", "edit", "list", "run", "execute"]
description: Analyze workspace changes, create logical commit groups, and commit each group with clear Conventional Commit messages.
prompt_metadata:
  id: git-commit-logical-groups
  title: Git Commit Logical Groups
  owner: johnmillerATcodemag-com
  version: 1.0.0
  created: 2026-05-19
  updated: 2026-05-19
  output_format: markdown
  category: source-control
  tags: [git, commits, conventional-commits, workflow, automation]
---

# Git Commit Logical Groups

Group and commit local workspace changes in coherent, review-friendly batches.

## Context

This prompt is for repositories where multiple unrelated edits may exist at once. The goal is to produce clean history by creating one commit per logical change unit (feature, fix, docs, refactor, test, chore).

## Target Audience

Developers and AI agents preparing local changes for pull requests.

## Requirements

1. Inspect current repository state before staging:
   - Run `git status --short` and `git diff --stat`.
   - If there are no changes, report and stop.

2. Derive logical groups from changed files:
   - Group by intent, not file extension.
   - Keep unrelated concerns in separate groups.
   - Prefer the smallest meaningful commit for each group.

3. For each group:
   - Stage only files for that group with `git add <paths>`.
   - Verify staged content via `git diff --cached --stat`.
   - Commit using Conventional Commits format:
     - `feat: ...`
     - `fix: ...`
     - `docs: ...`
     - `refactor: ...`
     - `test: ...`
     - `chore: ...`
   - Message must include scope when obvious, for example `fix(parser): handle unary minus`.

4. Safety checks:
   - Never run destructive commands such as `git reset --hard`.
   - Never amend existing commits unless explicitly requested.
   - Do not include generated or temporary files unless they are intentional artifacts.
   - If merge conflicts or staged leftovers appear, stop and explain.

5. Completion output:
   - Provide final list of created commits in order:
     - hash (short)
     - commit message
     - file count
   - Show remaining uncommitted files, if any.

## Technical Requirements

- Use non-interactive git commands only.
- Preserve existing worktree changes that do not belong to the current task.
- If a logical grouping is ambiguous, propose the grouping plan first, then execute after confirmation.

## Output Format

Return a concise Markdown report with:

1. Grouping rationale
2. Commits created
3. Remaining changes
4. Suggested next action (push, open PR, or continue grouping)

## Quality Standards

- Each commit should pass the single-purpose test.
- Commit messages should be specific and actionable.
- No unrelated file should be staged together.

## Deliverable

A clean sequence of local commits representing logical groups of workspace changes, ready for push and pull request review.
