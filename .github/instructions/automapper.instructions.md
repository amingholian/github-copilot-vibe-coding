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
applyTo: "{Profiles/**/*.cs,Dtos/**/*.cs,Services/**/*.cs,Program.cs}"
---

# AutoMapper Instructions

## Overview

This file defines AutoMapper usage for PostHubAPI. Mapping should remain centralized, predictable, and aligned with the repository's create, edit, and read DTO split.

**Target Audience**: Developers and AI assistants editing DTOs, profiles, and service-layer mapping logic
**Scope**: Mapping profiles, DTO design, service-layer mapping calls, and profile registration

**Related Documentation**:

- [ASP.NET Core Web API Instructions](aspnet-core-web-api.instructions.md)
- [Entity Framework Core Instructions](entity-framework-core.instructions.md)
- [C# Instructions](csharp.instructions.md)

## Table of Contents

- DTO Intent
- Where Mapping Happens
- Profile Design
- Update Mapping
- Quality Checklist

## DTO Intent

- Keep create, edit, and read DTOs separate.
- Do not reuse read DTOs as write DTOs or vice versa.
- Keep DTO shapes aligned with API contracts rather than entity internals.

## Where Mapping Happens

- Controllers should accept and return DTOs but should not perform `mapper.Map()` calls.
- Services own DTO-to-entity and entity-to-DTO mapping.
- Avoid hand-written object copying when an established profile already covers the conversion.

## Profile Design

- Keep one profile per aggregate or closely related mapping area.
- Name profile files consistently, such as `PostProfile` and `CommentProfile`.
- Register profiles centrally via `AddAutoMapper(AppDomain.CurrentDomain.GetAssemblies())`.

## Update Mapping

- For updates, load the existing tracked entity first, then map the edit DTO onto that entity.
- Prefer `mapper.Map(source, destination)` when mutating an existing entity.
- Avoid replacing tracked entities wholesale when a partial field update is intended.

## Quality Checklist

- [ ] Create, edit, and read DTOs remain distinct.
- [ ] Mapping is performed in services, not controllers.
- [ ] Profiles are grouped by aggregate and named clearly.
- [ ] Profile registration remains centralized.
- [ ] Update flows map onto tracked entities.
- [ ] Manual copy code is removed when a profile already exists.
