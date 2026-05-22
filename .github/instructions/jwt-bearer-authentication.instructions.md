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
applyTo: "{Program.cs,Configuration/**/*.cs,Controllers/**/*.cs,Services/**/*.cs}"
---

# JWT Bearer Authentication Instructions

## Overview

This file defines JWT bearer authentication rules for PostHubAPI. The repository validates JWT configuration at startup and expects secrets to come from secure local or deployed configuration sources, not from tracked files.

**Target Audience**: Developers and AI assistants editing authentication, startup, or authorization logic
**Scope**: JWT configuration resolution, bearer middleware, secret handling, endpoint authorization, and environment-specific auth behavior

**Related Documentation**:

- [ASP.NET Core Web API Instructions](.github/instructions/aspnet-core-web-api.instructions.md)
- [Swagger OpenAPI Instructions](.github/instructions/swagger-openapi.instructions.md)
- [README.md](README.md)

## Table of Contents

- [Configuration Keys](#configuration-keys)
- [Secret Handling](#secret-handling)
- [Middleware Configuration](#middleware-configuration)
- [Authorization Usage](#authorization-usage)
- [Quality Checklist](#quality-checklist)

## Configuration Keys

- Use one consistent JWT configuration shape across generation and validation code.
- Keep issuer, audience, and secret keys aligned between token creation and token validation.
- Validate missing or malformed JWT settings at startup instead of allowing runtime drift.

## Secret Handling

- Do not commit live JWT secrets to source control.
- Use user secrets for local development and environment variables for deployed environments.
- Keep documented environment-variable fallback behavior aligned with the configuration resolver.

## Middleware Configuration

- Keep JWT middleware configuration in `Program.cs` explicit and reviewable.
- Validate issuer and audience during token validation.
- Keep `RequireHttpsMetadata` disabled only in development and enabled outside development.
- Use a deterministic encoding path for the signing key so token validation remains stable.

## Authorization Usage

- Mark protected endpoints with `[Authorize]`.
- Keep login and registration endpoints public unless requirements change deliberately.
- Put token issuance behavior in a single well-defined service path rather than duplicating it across controllers.

## Quality Checklist

- [ ] JWT config keys are consistent across generation and validation.
- [ ] Live secrets are not stored in tracked config files.
- [ ] Startup fails clearly when required auth settings are missing.
- [ ] Issuer and audience are validated.
- [ ] `RequireHttpsMetadata` is environment-aware.
- [ ] Protected endpoints are explicitly marked with `[Authorize]`.
