---
ai_generated: true
model: "openai/gpt-5.4@unknown"
operator: "johnmillerATcodemag-com"
chat_id: "acaf6075-7dde-4cc7-b293-0829934f7cc3"
prompt: |
  Draft a CSS3 instructions file based on the repository structure and embedded CSS in calculator.html.
started: "2026-05-18T12:00:00Z"
ended: "2026-05-18T12:15:00Z"
task_durations:
  - task: "CSS analysis"
    duration: "00:05:00"
  - task: "Instruction drafting"
    duration: "00:10:00"
total_duration: "00:15:00"
ai_log: "ai-logs/2026/05/18/acaf6075-7dde-4cc7-b293-0829934f7cc3/conversation.md"
source: "calculator.html"
applyTo: "**/*.css"
---

# CSS3 Development Instructions

## Overview

This document outlines best practices for writing and maintaining CSS3 in this repository. It emphasizes maintainability, scalability, and alignment with evergreen software development principles.

## Scope

These instructions apply to all CSS3 code, whether embedded in HTML files or written in standalone `.css` files. They aim to ensure consistent styling, reduce technical debt, and improve collaboration.

## Related Documentation

- [Evergreen Software Development Instructions](.github/instructions/evergreen-software-development.instructions.md)
- [HTML Development Instructions](.github/instructions/html.instructions.md)

## Rules for CSS Development

### 1. Use Variables for Consistency

- Define reusable CSS variables (`--variable-name`) for colors, spacing, and other design tokens.
- Example:
  ```css
  :root {
    --primary-color: #6ee7ff;
    --font-size-base: 1rem;
  }
  ```

### 2. Follow a Mobile-First Approach

- Use `min-width` media queries to progressively enhance styles for larger screens.
- Example:
  ```css
  @media (min-width: 768px) {
    .container {
      padding: 24px;
    }
  }
  ```

### 3. Modularize Styles

- Group related styles into reusable classes and avoid inline styles.
- Example:
  ```css
  .button {
    padding: 12px 24px;
    border-radius: 8px;
  }
  ```

### 4. Optimize for Performance

- Minimize the use of complex selectors (e.g., `div > p > span`) to improve rendering performance.
- Avoid `!important` unless absolutely necessary.

### 5. Use Semantic Class Names

- Name classes based on their purpose, not their appearance.
- Example:
  ```css
  .alert-success {
    background-color: var(--success-color);
  }
  ```

### 6. Ensure Accessibility

- Use high-contrast colors and focus styles for interactive elements.
- Example:
  ```css
  button:focus-visible {
    outline: 2px solid var(--accent);
  }
  ```

### 7. Document Complex Styles

- Add comments to explain non-obvious styles or design decisions.
- Example:
  ```css
  /* Gradient background for branding */
  background: linear-gradient(135deg, #0b1f4d, #123a8c);
  ```

## Common Anti-Patterns

1. **Hardcoding Values**
   - Avoid hardcoding colors, fonts, or spacing. Use variables instead.
   - Bad:
     ```css
     color: #123456;
     ```
   - Good:
     ```css
     color: var(--text-color);
     ```

2. **Overusing IDs**
   - Avoid using IDs for styling. Use classes for better reusability.

3. **Deep Nesting**
   - Avoid deeply nested selectors, which are hard to maintain.
   - Bad:
     ```css
     .container .header .title span {
       color: red;
     }
     ```

4. **Inline Styles**
   - Avoid inline styles as they are harder to maintain and override.

5. **Global Styles**
   - Avoid applying styles directly to global elements like `div` or `span`.

## Quality Checklist

- [ ] Are CSS variables used for reusable values?
- [ ] Are styles modular and reusable?
- [ ] Are media queries mobile-first?
- [ ] Are class names semantic and meaningful?
- [ ] Are styles optimized for performance?
- [ ] Are accessibility standards met (e.g., focus styles, contrast)?
- [ ] Are there no hardcoded values or inline styles?
- [ ] Is the CSS well-documented with comments for complex rules?

---

By following these instructions, contributors can ensure that CSS in this repository remains maintainable, scalable, and aligned with modern development practices.
