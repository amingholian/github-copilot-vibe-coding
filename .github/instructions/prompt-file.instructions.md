---
ai_generated: true
model: "anthropic/claude-3.5-sonnet@2024-10-22"
operator: "johnmillerATcodemag-com"
chat_id: "optimize-instructions-20251023"
prompt: |
  Create AI-optimized version of prompt-file.instructions.md with minimal tokens
started: "2025-10-23T04:39:00Z"
ended: "2025-10-23T04:39:00Z"
task_durations:
  - task: "optimization"
    duration: "00:01:00"
total_duration: "00:01:00"
ai_log: "ai-logs/2025/10/23/optimize-instructions-20251023/conversation.md"
source: "optimization-task"
applyTo: "**/*.prompt.md"
relatedTo: "**/*.instructions.md"
---

# AI Instructions: Prompt File Creation

Generate repository prompts following standard structure and requirements.

## Prompt File Structure

```yaml
---
mode: agent|chat
model: "<provider>/<model-name>@<version>"
tools: ["create", "edit", "search"]
description: Clear description of prompt purpose
prompt_metadata:
  id: unique-identifier
  title: Human-Readable Title
  owner: author-name
  version: 1.0.0
  created: YYYY-MM-DD
  updated: YYYY-MM-DD
  output_path: path/to/output
  output_format: markdown|code|json|yaml
  category: category-name
  tags: [tag1, tag2, tag3]
---
# Prompt Title
[Prompt content]
```

## Field Requirements: Required vs. Optional

**Required Top-Level Fields**:

- `mode` - REQUIRED
- `model` - REQUIRED
- `tools` - REQUIRED
- `description` - REQUIRED
- `prompt_metadata` - REQUIRED

**Required Metadata Fields**:

- `id` - REQUIRED (unique identifier)
- `title` - REQUIRED (human-readable name)
- `output_format` - REQUIRED (expected output type)
- `category` - REQUIRED (functional category)
- `tags` - REQUIRED (3-7 tags minimum)

**Optional Metadata Fields**:

- `owner` - Optional (author or responsible team)
- `version` - Optional (semantic versioning; default "1.0.0")
- `created` - Optional (YYYY-MM-DD; auto-populated if AI-generated)
- `updated` - Optional (YYYY-MM-DD; updated on modifications)
- `output_path` - Optional (specific output location; only if fixed)

## Field Definitions and Guidance

### owner

Format: GitHub username or team identifier

- Single user: `github-username`
- Team: `@org/team-name`
- Examples: `johnmillerATcodemag-com`, `@microsoft/azure-team`

**Rule**: Use for accountability; omit if ownership is unclear or shared.

### version

Use semantic versioning: `MAJOR.MINOR.PATCH`

- `1.0.0` - Initial release
- `1.1.0` - Feature additions
- `1.1.1` - Bug fixes or minor tweaks
- `2.0.0` - Breaking changes or major redesign

**Rule**: Increment on significant changes; reset to `1.0.0` if repurposing.

### id Uniqueness Scope

**Globally unique**: Yes, across entire `.github/prompts/` directory

- Use pattern: `{domain}-{action}-{target}`
- Verify against existing IDs before creation
- Examples:
  - `api-documentation-generator`
  - `db-schema-migration-helper`
  - `ui-component-factory`

### mode

- `agent`: Autonomous file operations, code generation
- `chat`: Interactive guidance, Q&A

### model

**REQUIRED**: Use explicit format `"<provider>/<model-name>@<version>"`

- Default: `"anthropic/claude-3.5-sonnet@2024-10-22"`
- Examples:
  - `"openai/gpt-4o@2024-11-20"`
  - `"anthropic/claude-3.5-sonnet@2024-10-22"`
  - `"openai/o1-preview@2024-09-12"`

**Prohibited**: `"Auto (copilot)"` (loses provenance)

### tools

Array of required tools:

- `create` - Create files
- `edit` - Modify files
- `search` - Search codebase
- `read` - Read files
- `run` - Execute commands
- `list` - List directories

**Rule**: Include only necessary tools

### description

**Location**: Top-level (NOT in prompt_metadata)

- Active voice, present tense
- Specific about purpose
- 1-2 sentences max
- Focus on outcomes

### prompt_metadata.id

kebab-case, descriptive, unique
Pattern: `{domain}-{action}-{target}`
Example: `api-documentation-generator`

### prompt_metadata.output_path

Relative path from repo root
Examples:

- `.github/instructions/feature.instructions.md`
- `docs/generated/api-docs.md`

### prompt_metadata.tags

3-7 relevant tags
Categories: technology, function, domain, type
Example: `[python, testing, unit-tests, pytest]`

## AI Provenance Compliance

**Requirement**: All prompt files must include AI provenance metadata per [ai-assisted-output.instructions.md](ai-assisted-output.instructions.md#required-provenance-metadata-for-every-ai-assisted-artifact).

For **AI-generated prompt files**, add to front matter (alongside top-level fields):

```yaml
ai_generated: true
model: "<provider>/<model-name>@<version>"
operator: "<github-username>"
chat_id: "<unique-chat-id>"
prompt: |
  Original prompt that generated this file
started: "<ISO8601-timestamp>"
ended: "<ISO8601-timestamp>"
task_durations:
  - task: "task-name"
    duration: "HH:MM:SS"
total_duration: "HH:MM:SS"
ai_log: "ai-logs/YYYY/MM/DD/<chat-id>/conversation.md"
source: "<operator-name-or-prompt-path>"
```

**Post-Creation Steps** (MANDATORY for all AI-generated prompts):

1. Create conversation log: `ai-logs/YYYY/MM/DD/<chat-id>/conversation.md`
2. Create summary: `ai-logs/YYYY/MM/DD/<chat-id>/summary.md`
3. Update README.md with entry linking to new prompt and AI log
4. Verify all internal links work

See [Post-Creation Requirements (CANONICAL)](ai-assisted-output.instructions.md#post-creation-requirements-canonical) for full requirements.

## When to Create Prompt Files vs. Instruction Files

**Create a Prompt File (.prompt.md) when**:

- You need a reusable template for invoking an AI to perform a specific task
- The prompt will be executed multiple times with different inputs/contexts
- You want to document the exact prompting strategy for a recurring workflow
- Example: "api-documentation-generator.prompt.md" for generating API docs

**Create an Instruction File (.instructions.md) when**:

- You need guidance for **humans** (or AI) on how to perform a category of work
- The content is procedural, prescriptive, or explanatory
- Example: "api-documentation.instructions.md" for standards on writing API docs

**Relationship**:

- A prompt file may **reference** an instruction file (e.g., "Follow the guidelines in api-documentation.instructions.md")
- An instruction file should rarely reference prompt files (unidirectional dependency)

## Directory Organization within .github/prompts/

**Flat structure** (recommended for small repos):

```
.github/prompts/
  ├── api-documentation-generator.prompt.md
  ├── database-migration-helper.prompt.md
  ├── ui-component-factory.prompt.md
  └── code-review-analyzer.prompt.md
```

**Organized by domain** (recommended for large repos):

```
.github/prompts/
  ├── api/
  │   ├── api-documentation-generator.prompt.md
  │   └── openapi-converter.prompt.md
  ├── database/
  │   ├── database-migration-helper.prompt.md
  │   └── schema-analyzer.prompt.md
  ├── ui/
  │   └── ui-component-factory.prompt.md
  └── code-review/
      └── code-review-analyzer.prompt.md
```

**Rule**: Choose one structure and document it in your README.md.

## Common Templates

### Code Generator

```yaml
mode: agent
tools: ["search", "read", "create"]
description: [What code and where]
prompt_metadata:
  output_format: [language]
  category: code-generation
  tags: [language, framework, code-generation]
```

### Documentation Generator

```yaml
mode: agent
tools: ["search", "read", "create"]
description: [What docs from what source]
prompt_metadata:
  output_format: markdown
  category: documentation
  tags: [documentation, ...]
```

### Interactive Assistant

```yaml
mode: chat
tools: ["search", "read"]
description: [What guidance provided]
prompt_metadata:
  id: guidance-assistant-domain
  title: [Domain] Guidance Assistant
  output_format: markdown
  category: guidance
  tags: [interactive, guidance, domain]
```

## Content Structure

```markdown
# Prompt Title

[Brief introduction]

## Context

[Background, repo structure, conventions]

## Target Audience

[Who uses output, requirements]

## Requirements

[Detailed requirements by category]

## Technical Requirements

[Specifications, constraints, dependencies]

## Output Format

[Detailed format specs]

## Quality Standards

[Acceptance criteria, metrics]

## Deliverable

[Clear statement of what to produce]
```

## Validation Checklist

**Front Matter (YAML)**:

- [ ] All required top-level fields present (mode, model, tools, description)
- [ ] description at top-level (NOT in prompt_metadata)
- [ ] model uses explicit format: `"<provider>/<model-name>@<version>"`
- [ ] tools array is complete and minimal (only necessary tools)
- [ ] YAML syntax is valid (no indentation errors)

**Metadata**:

- [ ] All required prompt_metadata fields present (id, title, output_format, category, tags)
- [ ] `id` follows naming convention (kebab-case, `{domain}-{action}-{target}`)
- [ ] `id` is globally unique within `.github/prompts/`
- [ ] `tags` array has 3-7 items
- [ ] Optional fields (owner, version, output_path) are accurate if present
- [ ] If `output_path` specified, uses forward slashes

**AI Provenance** (if AI-generated):

- [ ] `ai_generated: true` present
- [ ] All AI provenance fields populated (operator, chat_id, started, ended, etc.)
- [ ] `ai_log` path exists: `ai-logs/YYYY/MM/DD/<chat-id>/conversation.md`
- [ ] Conversation log and summary files created

**Content**:

- [ ] File naming follows pattern: `{domain}-{action}-{target}.prompt.md`
- [ ] File located in `.github/prompts/` (or subdomain folder)
- [ ] Prompt content follows Content Structure template
- [ ] All internal links use relative paths
- [ ] No sensitive data (credentials, tokens, API keys) exposed

**Post-Creation**:

- [ ] README.md updated with entry linking to prompt and AI log (if AI-generated)
- [ ] All internal links validated
- [ ] Repository structure matches documented directory organization

## Anti-Patterns to Avoid

❌ Description in `prompt_metadata` (should be at top-level)
❌ Incomplete `tools` array (missing essential tools)
❌ Vague descriptions ("creates things" instead of "generates REST API documentation")
❌ Wrong `mode` selection (using `agent` for interactive guidance)
❌ Non-unique or overly generic `id` values (`helper`, `generator`, `utils`)
❌ Generic model names like `"Auto (copilot)"` (loses provenance)
❌ AI-generated files without complete provenance metadata
❌ Output paths not matching actual file structure
❌ Tags fewer than 3 or more than 7 items
❌ Prompt files without conversation logs (if AI-generated)

## File Naming

Pattern: `{domain}-{action}-{target}.prompt.md`

**Rules**:

- kebab-case (lowercase, hyphens between words)
- Include `.prompt.md` extension
- Descriptive and specific
- No abbreviations or acronyms
- Maximum 50 characters (excluding .prompt.md extension)

**Examples**:

- ✅ `api-documentation-generator.prompt.md`
- ✅ `database-migration-helper.prompt.md`
- ✅ `code-review-analyzer.prompt.md`
- ❌ `api-doc-gen.prompt.md` (abbreviations)
- ❌ `APIDocumentationGenerator.prompt.md` (not kebab-case)
- ❌ `api_documentation_generator.prompt.md` (underscores, not hyphens)

## Directory Structure

- Prompts: `.github/prompts/`
- Output: `.github/instructions/` or domain-specific
- Use subdirectories for organization

## Post-Creation

After creating prompt:

1. Follow [Post-Creation Requirements (CANONICAL)](ai-assisted-output.instructions.md#post-creation-requirements-canonical)
2. Verify all links use correct relative paths

## Reference

- `.github/instructions/ai-assisted-output.instructions.md` - Provenance requirements
- `.github/instructions/copilot-instructions.md` - Copilot-specific guidance
