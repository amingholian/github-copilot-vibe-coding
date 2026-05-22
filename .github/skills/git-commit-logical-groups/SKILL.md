---
ai_generated: true
model: "openai/gpt-5.3-codex@unknown"
operator: "johnmillerATcodemag-com"
chat_id: "8948d9b2-5146-4fb5-8a9e-aece30d7ac17"
prompt: |
  create a skill that commit changes in logical groups
started: "2026-05-20T00:00:00Z"
ended: "2026-05-20T00:10:00Z"
task_durations:
  - task: "requirements review"
    duration: "00:02:00"
  - task: "skill authoring"
    duration: "00:06:00"
  - task: "provenance updates"
    duration: "00:02:00"
total_duration: "00:10:00"
ai_log: "ai-logs/2026/05/20/8948d9b2-5146-4fb5-8a9e-aece30d7ac17/conversation.md"
source: "GitHub Copilot Chat"
---

# git-commit-logical-groups

## Description

Create clean, review-friendly Git history by grouping local changes by intent and committing each group separately with Conventional Commits.

Use this skill when the user asks to:

- Group pending workspace edits into logical commits
- Clean up commit history before push or pull request
- Stage and commit only related files together
- Produce final commit report with remaining changes

Do not use this skill when:

- There are no local changes
- The user asks to squash, rebase, or rewrite published history
- The user asks to amend an existing commit (unless explicitly requested)

## Inputs

- Current repository working tree state
- User intent (feature/fix/docs/refactor/test/chore split)
- Branch context and any scope hints from changed files

## Workflow

1. Inspect state before staging:

- Run `git status --short`
- Run `git diff --stat`
- If no changes exist, report and stop

2. Detect safety blockers:

- Stop on merge conflicts (`UU`, `AA`, `DD` in status)
- Stop if staged leftovers exist from unrelated work unless user confirms inclusion
- Exclude generated or temporary artifacts unless intentional

3. Build logical groups:

- Group by purpose, not by extension
- Keep each commit single-purpose
- If grouping is ambiguous, present the grouping plan and wait for confirmation

4. Commit each group with verification:

- Stage only that group with `git add <paths>`
- Verify staged set via `git diff --cached --stat`
- Commit with Conventional Commits and scope when clear:
  - `feat(scope): ...`
  - `fix(scope): ...`
  - `docs(scope): ...`
  - `refactor(scope): ...`
  - `test(scope): ...`
  - `chore(scope): ...`

5. Completion report:

- List commits in creation order with short hash, message, file count
- Show remaining uncommitted files
- Suggest next action: push, open PR, or continue grouping

## Guardrails

- Use non-interactive Git commands only
- Never run destructive commands such as `git reset --hard`
- Never amend commits unless explicitly requested
- Preserve unrelated local work
- Do not include unrelated files in the same commit

## Command Template

```bash
git status --short
git diff --stat

# Group 1
git add <group-1-paths>
git diff --cached --stat
git commit -m "<type(scope): message>"

# Group 2
git add <group-2-paths>
git diff --cached --stat
git commit -m "<type(scope): message>"

# Final checks
git log --oneline -n <number-of-created-commits>
git status --short
```

## Output Contract

Return concise Markdown with these sections:

1. Grouping rationale
2. Commits created
3. Remaining changes
4. Suggested next action
