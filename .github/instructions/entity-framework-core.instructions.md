---
ai_generated: true
model: "openai/gpt-5.4@unknown"
operator: "johnmillerATcodemag-com"
chat_id: "2f48c0bf-aac1-4cdf-8bbd-837e77db4f57"
prompt: |
  Create instructions files for the core technologies. use subagents for each technology.
started: "2026-05-22T00:00:00Z"
ended: "2026-05-22T00:25:00Z"
task_durations:
  - task: "technology exploration"
    duration: "00:12:00"
  - task: "instruction authoring"
    duration: "00:10:00"
  - task: "readme update"
    duration: "00:03:00"
total_duration: "00:25:00"
ai_log: "ai-logs/2026/05/22/2f48c0bf-aac1-4cdf-8bbd-837e77db4f57/conversation.md"
source: "GitHub Copilot Chat"
applyTo: "{Data/**/*.cs,Models/**/*.cs,Services/**/*.cs,Program.cs}"
---

# Entity Framework Core Instructions

## Overview

This file defines Entity Framework Core usage for PostHubAPI. The project uses EF Core with an environment-driven provider choice: in-memory for development and SQLite outside development.

**Target Audience**: Developers and AI assistants editing persistence code
**Scope**: `ApplicationDbContext`, models, query logic, persistence flows, provider selection, and test/development database behavior

**Related Documentation**:

- [ASP.NET Core Web API Instructions](.github/instructions/aspnet-core-web-api.instructions.md)
- [C# Instructions](.github/instructions/csharp.instructions.md)
- [Test-Driven Development Instructions](.github/instructions/test-driven-development.instructions.md)

## Table of Contents

- [Provider Selection](#provider-selection)
- [Async Data Access](#async-data-access)
- [Relationship Loading](#relationship-loading)
- [Mutations](#mutations)
- [Configuration And Secrets](#configuration-and-secrets)
- [Quality Checklist](#quality-checklist)

## Provider Selection

- Use `UseInMemoryDatabase()` only for development and test-oriented scenarios.
- Use `UseSqlite()` outside development with a connection string from configuration.
- Keep provider selection in startup code; do not hardcode provider choices deep in services.

## Async Data Access

- Use EF Core async APIs throughout: `ToListAsync`, `FirstOrDefaultAsync`, `FindAsync`, and `SaveChangesAsync`.
- Do not block on async calls with `.Result` or `.Wait()`.
- Keep service contracts async when they touch persistence.

## Relationship Loading

- Use `Include` when related data is required for a response DTO.
- Avoid N+1 query behavior by shaping the query before materialization.
- Keep navigation-loading decisions near the query that needs them.

## Mutations

- Query the entity before update or delete operations and fail clearly when it does not exist.
- Map edits onto tracked entities, then persist with a single `SaveChangesAsync()` call.
- Keep mutation logic in services rather than controllers.

## Configuration And Secrets

- Retrieve connection strings from configuration instead of hardcoding them.
- Keep production credentials and secrets outside source control.
- Preserve Identity integration through `ApplicationDbContext`; use `UserManager` for identity-specific workflows instead of bypassing it with manual context manipulation.

## Quality Checklist

- [ ] Provider selection is environment-aware.
- [ ] All EF operations use async APIs.
- [ ] Related data is eagerly loaded when required.
- [ ] Updates and deletes verify entity existence first.
- [ ] Persistence logic stays in services.
- [ ] Connection strings come from configuration.
- [ ] Identity persistence flows use the correct abstractions.
