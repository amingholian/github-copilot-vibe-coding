---
ai_generated: true
model: "openai/gpt-5.4@unknown"
operator: "johnmillerATcodemag-com"
chat_id: "acaf6075-7dde-4cc7-b293-0829934f7cc3"
prompt: |
  Draft a JavaScript instructions file based on the repository structure and embedded JavaScript in calculator.html.
started: "2026-05-18T12:30:00Z"
ended: "2026-05-18T12:45:00Z"
task_durations:
  - task: "JavaScript analysis"
    duration: "00:05:00"
  - task: "Instruction drafting"
    duration: "00:10:00"
total_duration: "00:15:00"
ai_log: "ai-logs/2026/05/18/acaf6075-7dde-4cc7-b293-0829934f7cc3/conversation.md"
source: "calculator.html"
---

# JavaScript Development Instructions

## Overview

This document outlines best practices for writing and maintaining JavaScript in this repository. It emphasizes maintainability, scalability, and alignment with evergreen software development principles.

## Scope

These instructions apply to all JavaScript code, whether embedded in HTML files or written in standalone `.js` files. They aim to ensure consistent logic, reduce technical debt, and improve collaboration.

## Related Documentation

- [Evergreen Software Development Instructions](.github/instructions/evergreen-software-development.instructions.md)
- [HTML Development Instructions](.github/instructions/html.instructions.md)

## Rules for JavaScript Development

### 1. Use Modern Syntax

- Prefer `const` and `let` over `var`.
- Use arrow functions for concise callbacks.
- Example:
  ```javascript
  const add = (a, b) => a + b;
  ```

### 2. Modularize Code

- Split code into smaller, reusable modules.
- Move non-trivial business logic behind an importable or otherwise directly testable module boundary.
- Treat inline DOM scripts as UI adapters; keep calculator rules, state transitions, and validation logic in testable seams.
- Example:
  ```javascript
  export function calculateSum(a, b) {
    return a + b;
  }
  ```

### 3. Avoid Global Variables

- Use closures or modules to encapsulate variables.
- Example:
  ```javascript
  (function () {
    const privateVar = "hidden";
    console.log(privateVar);
  })();
  ```

### 4. Ensure Readability

- Use descriptive variable and function names.
- Add comments for complex logic.
- Example:
  ```javascript
  // Calculate the area of a rectangle
  function calculateArea(width, height) {
    return width * height;
  }
  ```

### 5. Handle Errors Gracefully

- Use `try-catch` blocks for error-prone code.
- Example:
  ```javascript
  try {
    const data = JSON.parse(input);
  } catch (error) {
    console.error("Invalid JSON:", error);
  }
  ```

### 6. Optimize Performance

- Debounce or throttle expensive operations.
- Example:
  ```javascript
  function debounce(func, delay) {
    let timeout;
    return function (...args) {
      clearTimeout(timeout);
      timeout = setTimeout(() => func.apply(this, args), delay);
    };
  }
  ```

### 7. Write Tests

- Add unit tests for critical functions.
- Add a failing test before the first production edit for new behavior, bug fixes, and structural refactors.
- When extracting logic from UI code, add characterization tests first and preserve them while moving the code.
- Example:
  ```javascript
  describe("calculateSum", () => {
    it("should return the sum of two numbers", () => {
      expect(calculateSum(2, 3)).toBe(5);
    });
  });
  ```

## Common Anti-Patterns

1. **Using `var`**
   - Avoid `var` in favor of `let` and `const`.

2. **Inline Event Handlers**
   - Avoid inline event handlers like `onclick`. Use `addEventListener` instead.

3. **Deeply Nested Code**
   - Refactor deeply nested code for better readability.

4. **Hardcoding Values**
   - Avoid hardcoding values. Use constants or configuration files.

5. **Ignoring Errors**
   - Always handle errors explicitly.

6. **Hiding Business Logic In UI Wiring**

- Do not leave domain logic trapped inside event listeners or page-local script state when it can be moved to a testable module seam.

## Quality Checklist

- [ ] Are `const` and `let` used instead of `var`?
- [ ] Is the code modular and reusable?
- [ ] Are variables and functions named descriptively?
- [ ] Are errors handled gracefully?
- [ ] Are there no inline event handlers?
- [ ] Is the code optimized for performance?
- [ ] Are there no hardcoded values?
- [ ] Are there unit tests for critical functions?
- [ ] Is non-trivial logic available through a direct testable seam?
- [ ] Was a failing automated test added or updated before the first production edit?

---

By following these instructions, contributors can ensure that JavaScript in this repository remains maintainable, scalable, and aligned with modern development practices.
