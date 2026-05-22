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
applyTo: "{Program.cs,Controllers/**/*.cs,Dtos/**/*.cs}"
---

# Swagger OpenAPI Instructions

## Overview

This file defines Swagger and OpenAPI conventions for PostHubAPI. API documentation should describe the real HTTP contract, expose authentication requirements clearly, and stay aligned with controller and DTO behavior.

**Target Audience**: Developers and AI assistants editing API surface or documentation metadata
**Scope**: Swagger registration, endpoint documentation, DTO schema clarity, and auth visibility in API docs

**Related Documentation**:

- [ASP.NET Core Web API Instructions](aspnet-core-web-api.instructions.md)
- [JWT Bearer Authentication Instructions](jwt-bearer-authentication.instructions.md)
- [Documentation Instructions](documentation.instructions.md)

## Table of Contents

- Startup Configuration
- Endpoint Documentation
- DTO Clarity
- Authentication In Docs
- Quality Checklist

## Startup Configuration

- Register Swagger generation centrally in `Program.cs`.
- Keep Swagger UI enabled only in approved environments such as development unless requirements explicitly change.
- Treat OpenAPI configuration as part of the public API contract, not an optional afterthought.

## Endpoint Documentation

- Add XML comments and explicit response metadata for public controller actions when the API surface grows.
- Document success and failure response codes that clients must handle.
- Keep documented behavior aligned with actual controller and service behavior.

## DTO Clarity

- Use DTOs with names and properties that communicate request and response intent clearly.
- Avoid exposing entity internals that should not appear in the HTTP contract.
- Keep validation rules visible through DTO annotations so the generated contract stays useful.

## Authentication In Docs

- Configure JWT bearer support in Swagger when protected endpoints exist.
- Make auth requirements visible in endpoint descriptions and generated schema metadata.
- Keep public and protected endpoint documentation unambiguous.

## Quality Checklist

- [ ] Swagger registration remains centralized.
- [ ] Swagger UI exposure is environment-aware.
- [ ] Endpoint response metadata matches real behavior.
- [ ] DTOs communicate the public contract clearly.
- [ ] Auth requirements are visible in generated docs.
- [ ] Documentation changes stay aligned with controller changes.
