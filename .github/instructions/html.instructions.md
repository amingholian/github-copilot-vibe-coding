---
ai_generated: true
model: "openai/gpt-5.4@unknown"
operator: "johnmillerATcodemag-com"
chat_id: "acaf6075-7dde-4cc7-b293-0829934f7cc3"
prompt: |
  Draft a complete .instructions.md file for HTML authoring, aligned with evergreen software development rules.
started: "2026-05-18T12:45:00Z"
ended: "2026-05-18T12:50:00Z"
task_durations:
  - task: "HTML instruction drafting"
    duration: "00:05:00"
total_duration: "00:05:00"
ai_log: "ai-logs/2026/05/18/acaf6075-7dde-4cc7-b293-0829934f7cc3/conversation.md"
source: "GitHub Copilot Chat"
applyTo: "**/*.html"
---

# HTML Authoring Instructions

## Overview

This document defines HTML authoring rules for this repository. Use these instructions to ensure semantic, accessible, and maintainable markup that integrates seamlessly with JavaScript and CSS.

**Target Audience**: Developers and AI assistants editing HTML in the repository
**Scope**: Semantic structure, accessibility, data attributes, and markup patterns for interactive browser UI

**Related Documentation**:

- [AI-Assisted Output Instructions](.github/instructions/ai-assisted-output.instructions.md)
- [Evergreen Software Development](.github/instructions/evergreen-software-development.instructions.md)

## Table of Contents

- [Semantic Structure](#semantic-structure)
- [JavaScript Hooks](#javascript-hooks)
- [Accessibility Requirements](#accessibility-requirements)
- [Interactive Markup Patterns](#interactive-markup-patterns)
- [State and Content Rules](#state-and-content-rules)
- [Common Anti-Patterns](#common-anti-patterns)
- [Quality Checklist](#quality-checklist)

## Semantic Structure

- Use semantic elements (`main`, `section`, `header`, `footer`, `article`, `nav`, `button`) instead of generic `div` or `span` containers.
- Avoid nesting elements unnecessarily; keep the DOM tree shallow for better performance and readability.
- Use `div` and `span` only when no semantic element matches the purpose.
- Ensure headings (`h1``h6`) follow a logical hierarchy and are not skipped.

## JavaScript Hooks

- Use `data-*` attributes for JavaScript hooks instead of relying on `id` or `class` selectors.
- Avoid inline JavaScript (`onclick`, `onchange`); use event listeners in external scripts.
- Ensure hooks are descriptive and unique, e.g., `data-action="submit-form"`.

## Accessibility Requirements

- All interactive elements must be keyboard-navigable.
- Use `aria-*` attributes to enhance accessibility where native semantics are insufficient.
- Ensure sufficient color contrast for text and interactive elements.
- Provide alternative text (`alt`) for images and labels for form controls.

## Interactive Markup Patterns

- Use `<button>` for clickable actions, not `<div>` or `<span>`.
- Ensure forms have proper `label` elements associated with inputs via `for` or `aria-labelledby`.
- Use `<ul>` or `<ol>` for lists, not `<div>` or `<p>`.

## State and Content Rules

- Dynamically updated content must use `aria-live` regions where appropriate.
- Avoid hardcoding styles in HTML; use CSS classes instead.
- Ensure all visible text is selectable and not embedded in images unless necessary.

## Common Anti-Patterns

- Using `div` or `span` for buttons or links.
- Inline styles or JavaScript.
- Skipping heading levels (e.g., `h1` directly followed by `h3`).
- Over-reliance on `id` for styling or scripting.
- Empty or redundant `alt` attributes on images.

## Quality Checklist

- [ ] Semantic elements are used appropriately.
- [ ] All interactive elements are accessible via keyboard and screen readers.
- [ ] JavaScript hooks use `data-*` attributes.
- [ ] No inline styles or JavaScript.
- [ ] Headings follow a logical hierarchy.
- [ ] Forms have associated labels.
- [ ] Images have meaningful `alt` attributes.
- [ ] No unnecessary nesting of elements.
- [ ] All changes are tested for accessibility compliance.

---

This file ensures that HTML in the repository adheres to best practices for maintainability, accessibility, and semantic correctness.
