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
applyTo: "PostHubAPI.Tests/**/*.cs"
---

# xUnit API Testing Instructions

## Overview

This file defines xUnit testing conventions for PostHubAPI. The test project mixes API integration-style checks with controller-focused tests and configuration validation, so test code must stay isolated, explicit, and async.

**Target Audience**: Developers and AI assistants editing `PostHubAPI.Tests`
**Scope**: xUnit tests, WebApplicationFactory usage, auth tests, controller tests, and configuration-driven integration tests

**Related Documentation**:

- [ASP.NET Core Web API Instructions](.github/instructions/aspnet-core-web-api.instructions.md)
- [JWT Bearer Authentication Instructions](.github/instructions/jwt-bearer-authentication.instructions.md)
- [Test-Driven Development Instructions](.github/instructions/test-driven-development.instructions.md)

## Table of Contents

- [Test Structure](#test-structure)
- [Integration Test Setup](#integration-test-setup)
- [Authentication Tests](#authentication-tests)
- [Assertions And Data](#assertions-and-data)
- [Quality Checklist](#quality-checklist)

## Test Structure

- Use clear `Method_Expected_WhenCondition` naming for test methods.
- Follow Arrange, Act, Assert structure.
- Keep each test focused on one behavior or one HTTP contract.

## Integration Test Setup

- Use `WebApplicationFactory` to exercise startup, routing, auth, and serialization behavior together.
- Override configuration in tests without relying on committed secrets.
- Keep in-memory database state isolated per test or per controlled factory instance.

## Authentication Tests

- Test both authorized and unauthorized paths for protected endpoints.
- Generate tokens through dedicated helpers so auth setup stays consistent.
- Verify semantics with `HttpStatusCode` values instead of raw integers.

## Assertions And Data

- Prefer typed response deserialization with `ReadFromJsonAsync<T>()` when validating JSON payloads.
- Keep test data explicit and local to the test or a narrowly scoped helper.
- Use async assertions such as `Assert.ThrowsAsync<T>()` for async failure paths.

## Quality Checklist

- [ ] Tests use clear names and AAA structure.
- [ ] Integration tests isolate configuration and database state.
- [ ] Protected endpoint tests cover both success and failure paths.
- [ ] Assertions use typed payloads and `HttpStatusCode` enums.
- [ ] All async paths are awaited correctly.
- [ ] Secrets are not hardcoded into committed test setup.
