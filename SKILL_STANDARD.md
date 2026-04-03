# Agent Skills Standard Format

## Purpose

This document defines the standard format for cross-platform AI agent skills in the waldronlab/ai-agent-skills repository. Skills following this standard can be used with multiple AI agents (Claude Code, GitHub Copilot, etc.) without platform-specific duplication.

## Motivation

Previously, we maintained separate `/claude` and `/copilot` directories with near-identical skill logic, differing only in:
- Trigger syntax (Claude: `/command` vs Copilot: `@workspace ...`)
- Tool invocation patterns (Claude: XML-style vs Copilot: natural language)
- Minor formatting preferences

This duplication created maintenance overhead and logic drift. The unified format provides a **single source of truth** while documenting platform-specific adaptations where necessary.

## File Structure

### Location

Unified skills live directly in domain directories:

```
ai-agent-skills/
├── r-packages/                      # R/Bioconductor domain
│   ├── analyze-r-package.md         # Unified skill
│   ├── create-package-instructions.md
│   ├── update-package-instructions.md
│   ├── templates/                   # Supporting resources
│   └── examples/
├── metagenomics/                    # Metagenomics domain
│   └── (skills will go here)
└── statistical-methods/             # Statistical methods domain
    └── (skills will go here)
```

This keeps everything for a domain together while the unified format prevents platform-specific duplication.

## Standard Format

### YAML Frontmatter

Every skill MUST begin with YAML frontmatter containing these fields:

```yaml
---
name: skill-name                     # Kebab-case identifier (REQUIRED)
description: One-line purpose        # High-level trigger description (REQUIRED)
version: 1.0.0                       # Semantic version (REQUIRED)
platforms:                           # Supported platforms (REQUIRED)
  - claude-code
  - github-copilot
triggers:                            # Platform-specific invocations (REQUIRED)
  claude:
    - /skill-name
    - "Natural language variant"
  copilot:
    - "@workspace natural language trigger"
    - "@workspace alternate trigger"
author: waldronlab                   # Optional
category: r-packages                 # Optional domain categorization
---
```

**Required Fields**:
- `name`: Unique identifier, kebab-case
- `description`: Single sentence describing the skill's purpose
- `version`: Semantic version (MAJOR.MINOR.PATCH)
- `platforms`: Array of supported AI agents
- `triggers`: Platform-specific trigger phrases

**Optional Fields**:
- `author`: Creator or maintaining organization
- `category`: Domain grouping (r-packages, metagenomics, etc.)
- `tags`: Additional metadata for discovery

### Main Content

After the frontmatter, structure the skill content as follows:

```markdown
# [Skill Name]

Brief overview of what the skill does (1-2 paragraphs).

## Usage

How users invoke this skill across platforms:
- **Claude Code**: `/command` or "natural trigger"
- **GitHub Copilot**: `@workspace trigger phrase`

## Prerequisites

List any requirements:
- Working directory location
- Required files (e.g., DESCRIPTION for R packages)
- Dependencies or prior setup

## Process

Detailed step-by-step instructions for the AI agent. Use numbered sections:

### 1. First Major Step

Description of what to do.

**Tools/Methods**:
- Platform-agnostic: "Read the DESCRIPTION file"
- Claude-specific: "Use Read tool"
- Copilot-specific: "Use file browser"

### 2. Second Major Step

Continue with clear, actionable instructions.

## Output Format

If the skill produces structured output, document the expected format using markdown code blocks or examples.

## Platform-Specific Notes

Document differences between platforms:

### Claude Code
- Use dedicated tools (Read, Grep, Glob, Edit, Write)
- Output saved to conversation context
- Can use /skill invocations

### GitHub Copilot
- Use VS Code file browser and search
- Output displayed in chat
- Trigger via @workspace

## Error Handling

Document common errors and how to handle them.

## Examples

Provide concrete examples showing:
1. How users invoke the skill
2. What the AI agent does
3. Expected output

## Notes

Additional context, caveats, or best practices.
```

## Design Principles

### 1. Platform-Agnostic Core Logic

The majority of the skill should describe **what** to do, not **how** (which tools to use):

**❌ Platform-specific**:
```markdown
Use the Read tool to read DESCRIPTION:
- Read: DESCRIPTION file
```

**✅ Platform-agnostic**:
```markdown
Read and analyze the DESCRIPTION file to extract:
- Package name
- Title and description
- Version number
```

**Platform notes** can clarify implementation:
```markdown
**Implementation**:
- Claude Code: Use `Read` tool
- Copilot: Use file browser or editor
```

### 2. Trigger Alignment

Ensure triggers capture the same **user intent** across platforms:

```yaml
triggers:
  claude:
    - /analyze-r-package
    - "Analyze this R package"
  copilot:
    - "@workspace analyze this R package"
    - "@workspace what type of R package is this?"
```

Both should handle:
- Direct command invocations
- Natural language requests with similar meaning

### 3. Template References

When skills generate content from templates, reference **shared template files** rather than embedding platform-specific templates:

```markdown
## Creating 00-overview.md

Use the template from `r-packages/templates/00-overview.template.md` and populate with:
- Package classification from analysis
- Key exports by category
- Data sources (if applicable)
```

### 4. Output Portability

Skills should produce output that is useful regardless of platform:

- Use markdown for structured output
- Avoid platform-specific formatting
- Keep examples self-contained

## Migration Guide

### Converting Platform-Specific Skills to Unified Format

1. **Extract Common Logic**

   Compare Claude and Copilot versions side-by-side:
   - Identify identical sections (usually 90%+)
   - Extract to platform-agnostic language
   - Document only true differences

2. **Create YAML Frontmatter**

   ```yaml
   ---
   name: existing-skill-name
   description: [from existing header]
   version: [current version]
   platforms: ["claude-code", "github-copilot"]
   triggers:
     claude: [from Claude version]
     copilot: [from Copilot version]
   ---
   ```

3. **Generalize Tool References**

   Replace:
   ```markdown
   Tools to use:
   - Read: DESCRIPTION
   - Grep: R/ for patterns
   ```

   With:
   ```markdown
   Read the DESCRIPTION file to extract metadata.
   Search R source files for patterns (e.g., setClass, ExperimentHub).
   ```

4. **Add Platform Notes Section**

   ```markdown
   ## Platform-Specific Notes

   ### Claude Code
   - Use Read, Grep, Glob tools directly
   - Can invoke with `/skill-name`

   ### GitHub Copilot
   - Use VS Code file operations
   - Trigger with `@workspace ...`
   ```

5. **Test Both Platforms**

   Verify the unified skill works correctly:
   - Claude Code: Install as global skill or workspace skill
   - GitHub Copilot: Reference from `.github/copilot-instructions.md`
   - Test all trigger variations
   - Verify output is consistent

## Installation

### For Claude Code

Reference unified skills in VS Code settings:

```json
{
  "claude.globalSkills": [
    "~/git/ai-agent-skills/r-packages/analyze-r-package.md",
    "~/git/ai-agent-skills/r-packages/create-package-instructions.md"
  ]
}
```

### For GitHub Copilot

Copy or reference unified skills:

**Option 1: Direct reference** (if supported):
```json
{
  "github.copilot.instructionsFile": "../ai-agent-skills/r-packages/"
}
```

**Option 2: Copy to repository**:
```bash
cp ~/git/ai-agent-skills/r-packages/*.md \
   .github/copilot-instructions/
```

## Validation Checklist

Use this checklist when creating or migrating skills:

- [ ] YAML frontmatter includes all required fields
- [ ] `name` is unique and kebab-case
- [ ] `platforms` lists all supported agents
- [ ] `triggers` defined for each platform
- [ ] Core logic is platform-agnostic
- [ ] Tool references are generalized or in platform notes
- [ ] Output format is documented
- [ ] Examples show usage for both platforms
- [ ] Error handling is documented
- [ ] Tested on at least two platforms

## Bioconductor-Specific Considerations

For waldronlab R package skills:

### Template Integration

Reference shared templates in `r-packages/templates/`:

```markdown
Populate `00-overview.md` using the structure:
- [Link to template if exists, or describe inline]
```

### Standards References

Link to Bioconductor standards rather than duplicating:

```markdown
Follow Bioconductor coding standards:
- Function documentation: https://bioconductor.org/developers/package-guidelines/#rcode
- Testing requirements: https://bioconductor.org/developers/package-guidelines/#tests
```

### Domain Knowledge

Waldron lab domain knowledge (metagenomics, multi-omics) should be:
- Documented in the `/templates` directory
- Referenced by skills, not embedded
- Versioned alongside skills

## Future Extensions

### MCP (Model Context Protocol) Integration

When defining tools or capabilities:

```yaml
capabilities:
  - read_files
  - search_files
  - execute_commands
mcp_servers:
  - filesystem
  - git
```

### Multi-Agent Workflows

For skills that coordinate multiple agents:

```yaml
workflow:
  - step: analyze
    agent: explore
  - step: generate
    agent: main
```

## Examples

See [r-packages/](r-packages/) for complete examples of unified skills:
- [analyze-r-package.md](r-packages/analyze-r-package.md)
- [create-package-instructions.md](r-packages/create-package-instructions.md)
- [update-package-instructions.md](r-packages/update-package-instructions.md)

## Maintaining Parity

To ensure skills remain in sync across platforms:

1. **Single Source of Truth**: Always edit the unified skill in `/skills`
2. **Platform Testing**: Test changes on both Claude Code and Copilot
3. **Version Bumping**: Increment version in frontmatter when updating
4. **Changelog**: Document changes in skill-level comments or repo CHANGELOG

## Questions?

For questions about this standard:
- Open an issue: https://github.com/waldronlab/ai-agent-skills/issues
- Discuss: https://github.com/waldronlab/ai-agent-skills/discussions

---

**Version**: 1.0.0
**Last Updated**: 2026-04-03
**Authors**: waldronlab
