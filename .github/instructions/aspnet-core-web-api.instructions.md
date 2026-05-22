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
applyTo: "{Program.cs,Controllers/**/*.cs,Services/**/*.cs,Dtos/**/*.cs,Configuration/**/*.cs}"
---

# ASP.NET Core Web API Instructions

## Overview

This file defines the ASP.NET Core Web API conventions for PostHubAPI. Follow these rules when editing startup configuration, controllers, service wiring, request DTO handling, and API response behavior.

**Target Audience**: Developers and AI assistants working on the API surface
**Scope**: Startup configuration, controllers, services, DTO validation, error mapping, and authorization behavior

**Related Documentation**:

- [C# Instructions](csharp.instructions.md)
- [Entity Framework Core Instructions](entity-framework-core.instructions.md)
- [JWT Bearer Authentication Instructions](jwt-bearer-authentication.instructions.md)
- [Swagger OpenAPI Instructions](swagger-openapi.instructions.md)

## Table of Contents

- Service Registration
- Controller Design
- Validation And Errors
- Authorization
- Environment-Aware Configuration
- Quality Checklist

## Service Registration

- Register application services with `AddScoped<IInterface, Implementation>()` before `builder.Build()`.
- Keep infrastructure registration in `Program.cs`; do not scatter service registration across unrelated files.
- Validate required configuration at startup instead of deferring missing settings to first request.

## Controller Design

- Keep controllers thin: validate input, delegate to a service, translate domain outcomes to HTTP responses.
- Return DTOs, not EF entities or Identity entities, from controller actions.
- Use async action methods throughout for database-backed work.
- Prefer explicit response semantics: `Ok`, `CreatedAtAction`, `NoContent`, `BadRequest`, `NotFound`, and `Unauthorized`.

## Validation And Errors

- Validate `ModelState` before calling service methods.
- Keep create and edit DTO validation rules aligned unless partial update semantics are intentionally different.
- Throw domain-specific exceptions such as `NotFoundException` from the service layer, then translate them consistently at the API boundary.
- Do not swallow exceptions or return ambiguous success payloads for failed operations.

## Authorization

- Apply `[Authorize]` only to endpoints that require an authenticated caller.
- Keep public endpoints such as registration and login explicitly unauthenticated.
- Put coarse-grained authorization at the controller/action level and fine-grained ownership checks in services if needed.

## Environment-Aware Configuration

- Use `builder.Environment.IsDevelopment()` to control development-only behavior such as the in-memory database or Swagger UI exposure.
- Keep startup decisions explicit and reviewable in `Program.cs`.
- Avoid development shortcuts leaking into non-development environments.

## Quality Checklist

- [ ] Services are registered centrally and before `Build()`.
- [ ] Controllers stay thin and return DTOs.
- [ ] Request validation happens before business logic.
- [ ] All database-backed flows are async end to end.
- [ ] Exceptions map to correct HTTP status codes.
- [ ] Authorization is applied only where required.
- [ ] Development-only behavior is gated by environment checks.
