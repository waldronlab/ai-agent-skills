# Skill Format Standard (Technical Specification)

## Relationship to Other Documentation

- **[AGENTS.md](AGENTS.md)**: Defines WHAT agents must do (behavior, compliance, discovery)
- **SKILL_STANDARD.md** (this document): Defines HOW to format skills (structure, syntax)

This document provides detailed technical guidance for skill format. For canonical agent behavior rules, see [AGENTS.md](AGENTS.md).

## Purpose

This document defines the standard format for agent-agnostic skills in the waldronlab/ai-agent-skills repository. Skills following this standard work with multiple AI agents without platform-specific metadata or duplication.

## Core Principles

### 1. Agent Neutrality

Skills contain no platform-specific metadata (no `platforms:` or `triggers:` fields). Agents discover skills via [SKILLS.md](SKILLS.md) and match user natural language to skill descriptions.

### 2. Single Source of Truth

One skill file per skill at `skills/{skill-name}/SKILL.md`. No platform-specific variants or duplicates.

### 3. Portability

Skills work on any compliant agent platform through natural language invocation. Platform-specific shortcuts (slash commands, @workspace patterns) are optional conveniences documented in [instructions/](instructions/) adapters.

## File Structure

### Location

Skills live in flat individual directories:

```
ai-agent-skills/
├── AGENTS.md                           # Agent behavior standard
├── SKILLS.md                           # Human-readable skill index
├── SKILL_STANDARD.md                   # This file - technical format spec
│
├── skills/                             # All skills (flat structure)
│   ├── create-skill/
│   │   └── SKILL.md
│   ├── check-waldronlab-skills/
│   │   └── SKILL.md
│   ├── analyze-r-package/
│   │   └── SKILL.md
│   ├── create-package-instructions/
│   │   ├── SKILL.md
│   │   ├── templates/                 # Shared standards
│   │   └── examples/                  # Example outputs
│   └── update-package-instructions/
│       └── SKILL.md
│
└── instructions/                       # Platform adapters
    ├── README.md
    ├── claude.md
    ├── copilot.md
    └── gemini.md
```

### Naming Convention

- **Directory**: `skills/{skill-name}/` (kebab-case)
- **Skill file**: `SKILL.md` (uppercase, consistent across all skills)
- **Supporting files**: Optional templates, examples, or resources in the skill directory

## YAML Frontmatter (Required)

Every skill MUST begin with YAML frontmatter:

```yaml
---
name: skill-name                        # Unique identifier (REQUIRED)
description: One-line purpose           # Used for discovery (REQUIRED)
version: 1.0.0                          # Semantic version (REQUIRED)
category: domain                        # Primary domain (REQUIRED)
tags: [tag1, tag2, tag3]               # Searchable metadata (OPTIONAL)
author: waldronlab                      # Creator/maintainer (OPTIONAL)
---
```

### Required Fields

| Field | Type | Description | Example |
|-------|------|-------------|---------|
| `name` | string | Unique kebab-case identifier | `create-skill` |
| `description` | string | One-line purpose for discovery | `Help create a new AI agent skill through collaborative Q&A` |
| `version` | string | Semantic version (MAJOR.MINOR.PATCH) | `1.0.0` |
| `category` | string | Primary domain classification | `meta`, `r-packages`, `metagenomics` |

### Optional Fields

| Field | Type | Description | Example |
|-------|------|-------------|---------|
| `tags` | array | Cross-cutting metadata for discovery | `[meta, infrastructure, skill-creation]` |
| `author` | string | Creator or maintaining organization | `waldronlab` |

### Prohibited Fields

❌ **Do NOT include**:
- `platforms:` - Skills are agent-agnostic by design
- `triggers:` - Agents use natural language + SKILLS.md for discovery
- Agent-specific metadata

Platform-specific invocation patterns belong in [instructions/](instructions/) adapter files, not in skill YAML.

## Main Content Structure

After frontmatter, structure content as follows:

```markdown
# [Skill Name]

Brief overview of what the skill does (1-2 paragraphs).

## Usage

How to invoke this skill (natural language examples):
- "Create a new skill for [purpose]"
- "Help me with [task]"
- "[Action] this [thing]"

Platform adapters may provide optional shortcuts.

## Prerequisites

List any requirements:
- Working directory location
- Required files
- Dependencies or prior setup

## Process

Detailed step-by-step instructions using numbered sections:

### 1. First Major Step

Description of what to do (platform-agnostic).

### 2. Second Major Step

Continue with clear, actionable instructions.

## Output Format

Expected output structure or examples (if applicable).

## Examples

Concrete usage scenarios showing:
1. User invocation (natural language)
2. What the skill does
3. Expected outcome

## Notes

Additional context, caveats, or best practices.
```

### Section Guidelines

**Usage Section**:
- Use natural language invocation examples
- Avoid platform-specific syntax (no `/command` or `@workspace` patterns)
- Let platform adapters document optional shortcuts

**Process Section**:
- Describe WHAT to do, not HOW (which tools to use)
- Use platform-agnostic language: "read the file" not "use Read tool"
- Number major steps clearly
- Provide clear decision points

**Examples Section**:
- Show natural language invocation
- Demonstrate typical workflows
- Include expected outcomes

## Design Principles

### Platform-Agnostic Core Logic

The majority of the skill describes **what** to do, not **how** (which tools):

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

### Natural Language Invocation

Skills are invoked through natural language matching to descriptions, not rigid command syntax:

**❌ Rigid triggers**:
```yaml
triggers:
  claude:
    - /analyze-r-package
  copilot:
    - "@workspace analyze this R package"
```

**✅ Natural language discovery**:
```yaml
description: Analyze R/Bioconductor package structure to extract key information about its purpose, exports, and characteristics
```

Agents match user intent like "analyze this package" or "what type of package is this?" to the description.

### Output Portability

Skills should produce output useful regardless of platform:
- Use markdown for structured output
- Avoid platform-specific formatting
- Keep examples self-contained

## Installation & Discovery

### For Users

Skills are discovered via [SKILLS.md](SKILLS.md):
1. Browse SKILLS.md to find relevant skills
2. Invoke using natural language matching the description
3. Optional: Use platform shortcuts documented in [instructions/](instructions/)

### For Platform Adapters

Platforms configure skill locations:

**Claude Code** (`settings.json`):
```json
{
  "claude.globalSkills": [
    "/path/to/ai-agent-skills/skills/create-skill/SKILL.md",
    "/path/to/ai-agent-skills/skills/analyze-r-package/SKILL.md"
  ]
}
```

**GitHub Copilot** (`settings.json`):
```json
{
  "chat.skillsLocations": [
    "/path/to/ai-agent-skills/skills/create-skill",
    "/path/to/ai-agent-skills/skills/analyze-r-package"
  ]
}
```

See [instructions/claude.md](instructions/claude.md) and [instructions/copilot.md](instructions/copilot.md) for complete setup.

## Version Management

Skills use semantic versioning:

- **MAJOR**: Breaking changes to skill behavior or interface
- **MINOR**: New features, non-breaking enhancements
- **PATCH**: Bug fixes, clarifications, documentation updates

When updating skills:
1. Increment version in YAML frontmatter
2. Update [SKILLS.md](SKILLS.md) if description changes
3. Document changes in commit message
4. Consider updating [CHANGELOG.md](CHANGELOG.md) for significant changes

## Validation Checklist

Use this checklist when creating or updating skills:

### Required Elements
- [ ] YAML frontmatter includes all required fields (`name`, `description`, `version`, `category`)
- [ ] `name` is unique and kebab-case
- [ ] `description` is one clear sentence suitable for discovery
- [ ] `category` matches an existing domain or is a new domain with rationale
- [ ] Core logic is platform-agnostic (describes WHAT, not HOW)
- [ ] No `platforms:` or `triggers:` fields in YAML
- [ ] Usage section shows natural language invocation examples

### Content Quality
- [ ] Process section has numbered steps with clear actions
- [ ] Examples show realistic usage scenarios
- [ ] Output format is documented (if applicable)
- [ ] Prerequisites are clear and complete
- [ ] Cross-references use correct paths

### Portability
- [ ] Tool references are generalized or in platform-specific notes
- [ ] Examples work across platforms
- [ ] No platform-specific assumptions in core logic

## Examples

### Complete Skill Example

```markdown
---
name: analyze-r-package
description: Analyze R/Bioconductor package structure to extract key information about its purpose, exports, and characteristics
version: 1.0.0
category: r-packages
tags: [r-packages, analysis, bioconductor, documentation]
author: waldronlab
---

# analyze-r-package

Analyze an R/Bioconductor package to understand its structure, purpose, and key characteristics.

## Usage

Invoke when you want to understand an R package's architecture:
- "Analyze this R package"
- "What type of R package is this?"
- "Tell me about this package structure"

## Prerequisites

- Working directory is an R package root (contains DESCRIPTION file)
- Package has standard R structure (R/, NAMESPACE, etc.)

## Process

### 1. Read Package Metadata

Read and analyze the DESCRIPTION file to extract:
- Package name from `Package` field
- Title from `Title` field
- Description from `Description` field
- Version from `Version` field

### 2. Identify Exported Functions

Parse the NAMESPACE file to extract all exports and categorize by function type.

## Output Format

Produce a structured markdown summary with classification, key exports, data access patterns, and documentation status.

## Examples

**User**: "Analyze this R package"

**Skill produces**:
```
## Package Analysis: packageName
### Classification
- **Type**: Data Package
- **Version**: 1.0.0
...
```

## Notes

- This skill produces analysis for use by other skills or for user understanding
- Manual verification recommended for complex packages
```

## Migration from v1.x

If you have skills from v1.x format:

1. **Remove platform-specific fields**:
   - Delete `platforms:` array
   - Delete `triggers:` sections

2. **Add required metadata**:
   - Add `category:` field (domain name)
   - Optionally add `tags:` array

3. **Update invocation examples**:
   - Change from `/command` syntax to natural language
   - Remove `@workspace` patterns from skill file
   - Document optional shortcuts in [instructions/](instructions/) adapters

4. **Test on both platforms**:
   - Verify natural language invocation works
   - Check optional shortcuts work (if configured)

See [MIGRATION.md](MIGRATION.md) for detailed upgrade guide.

## Questions?

- **How does skill discovery work?** → See [AGENTS.md](AGENTS.md)
- **How do I create a new skill?** → Use the `create-skill` skill or see [CONTRIBUTING.md](CONTRIBUTING.md)
- **Where are skills stored?** → `skills/{skill-name}/SKILL.md`
- **How do platform shortcuts work?** → See [instructions/claude.md](instructions/claude.md) or [instructions/copilot.md](instructions/copilot.md)
- **I found an issue** → File at https://github.com/waldronlab/ai-agent-skills/issues

---

**Version**: 2.0.0
**Last Updated**: 2026-04-03
**Authors**: waldronlab

See [AGENTS.md](AGENTS.md) for agent behavior standard, [SKILLS.md](SKILLS.md) for skill index, [CONTRIBUTING.md](CONTRIBUTING.md) for contribution guidelines.
