# Skill Format Standard (Quick Reference)

## Purpose

This document provides a quick reference for creating skills, including version management guidelines, a validation checklist, and a complete working example.

**For the authoritative format specification**, see [AGENTS.md](AGENTS.md) sections:
- **Skill File Format** (lines 59-124) - Required/prohibited fields, content structure, platform-agnostic principles
- **Agent Responsibilities** - How agents discover and invoke skills
- **Compliance Criteria** - What makes a skill compliant

## Relationship to Other Documentation

- **[AGENTS.md](AGENTS.md)**: Canonical format requirements and agent behavior (start here)
- **SKILL_STANDARD.md** (this document): Quick reference with checklist and example
- **[SKILLS.md](SKILLS.md)**: Complete skill catalog organized by domain
- **[instructions/{agent}.md](instructions/)**: Platform-specific setup instructions

## Quick Format Summary

For complete requirements, see **[AGENTS.md § Skill File Format](AGENTS.md#skill-file-format)**.

**Required YAML fields**:
- `name` (kebab-case identifier)
- `description` (one-line purpose for discovery)
- `version` (semantic versioning)
- `category` (domain: meta, r-packages, metagenomics, etc.)

**Prohibited fields**: `platforms`, `triggers` (skills are agent-agnostic)

**Content sections**: Title, Usage (natural language), Prerequisites, Process (numbered steps), Output Format, Examples, Notes

**Key principle**: Describe WHAT to do (platform-agnostic), not HOW (tool-specific)

---

## Version Management

Skills use semantic versioning (MAJOR.MINOR.PATCH):

- **MAJOR**: Breaking changes to skill behavior or interface
- **MINOR**: New features, non-breaking enhancements
- **PATCH**: Bug fixes, clarifications, documentation updates

### When Updating Skills

1. Increment version in YAML frontmatter
2. If description changes, run `document-skill` to update SKILLS.md
3. Document changes in commit message
4. Consider updating CHANGELOG.md for significant changes

**Examples**:
- `1.0.0 → 1.0.1` - Fixed typo in Process section
- `1.0.1 → 1.1.0` - Added new optional section for error handling
- `1.1.0 → 2.0.0` - Changed required input format (breaking change)

---

## Validation Checklist

Use this checklist when creating or updating skills (or run `validate-skill` to automate):

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
- [ ] Cross-references use correct relative paths

### Portability
- [ ] Tool references are generalized or in platform-specific notes
- [ ] Examples work across platforms
- [ ] No platform-specific assumptions in core logic

---

## Complete Skill Example

Here's a well-formed skill demonstrating all key elements:

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

### 3. Detect Data Access Patterns

Check for:
- ExperimentHub metadata
- DuckDB connections
- Remote data sources

### 4. Classify Package Type

Based on the analysis, classify as:
- Data package
- Analysis package
- Infrastructure package
- Workflow package

## Output Format

Produce a structured markdown summary with:
- Package classification
- Key exports (functions, classes, methods)
- Data access patterns
- Documentation status
- Architecture notes

## Examples

**User**: "Analyze this R package"

**Skill produces**:
```
## Package Analysis: packageName
### Classification
- **Type**: Data Package
- **Version**: 1.0.0
- **Bioconductor**: Yes

### Key Exports
- Functions: `loadData()`, `queryDatabase()`
- Data objects: `metadata`

### Data Access
- DuckDB remote parquet files via URL
- ExperimentHub integration

### Architecture
- Uses DuckDB for efficient remote data access
- Lazy loading for memory efficiency
```

## Notes

- This skill produces analysis for use by other skills or for user understanding
- Manual verification recommended for complex packages
- Results can be used directly as input to `create-package-instructions`

See [SKILL_STANDARD.md](../../SKILL_STANDARD.md) for format details and [create-package-instructions](../create-package-instructions/SKILL.md) for how to use this analysis.
```

---

## Migration from v1.x

If you have skills from v1.x format (pre-agent-agnostic):

### 1. Remove Platform-Specific Fields

**Delete** from YAML frontmatter:
```yaml
platforms: [claude, copilot]  # ❌ Remove this
triggers:                      # ❌ Remove this entire section
  claude:
    - /analyze-r-package
  copilot:
    - "@workspace analyze this R package"
```

### 2. Add Required Metadata

**Add** to YAML frontmatter:
```yaml
category: r-packages           # ✅ Add domain
tags: [analysis, bioconductor] # ✅ Add tags (optional but recommended)
```

### 3. Update Invocation Examples

**Change** from platform-specific to natural language:

**Before**:
```markdown
## Usage
- Claude Code: `/analyze-r-package`
- GitHub Copilot: `@workspace analyze this R package`
```

**After**:
```markdown
## Usage
- "Analyze this R package"
- "What type of R package is this?"

Platform adapters may provide optional shortcuts.
```

### 4. Remove Tool-Specific Language

**Change** from tool-specific to platform-agnostic:

**Before**:
```markdown
Use the Read tool to read DESCRIPTION:
- Read: DESCRIPTION file
```

**After**:
```markdown
Read and analyze the DESCRIPTION file to extract package metadata.
```

### 5. Test on Both Platforms

- Verify natural language invocation works
- Check optional shortcuts work (if configured in platform adapters)
- Update SKILLS.md using `document-skill`

See [MIGRATION.md](MIGRATION.md) for detailed upgrade guide.

---

## Questions?

- **How does skill discovery work?** → See [AGENTS.md § Skill Discovery & Invocation](AGENTS.md#skill-discovery--invocation)
- **How do I create a new skill?** → Use the `create-skill` skill or see [CONTRIBUTING.md](CONTRIBUTING.md)
- **Where are skills stored?** → `skills/{skill-name}/SKILL.md` (flat structure)
- **How do platform shortcuts work?** → See [instructions/claude.md](instructions/claude.md) or [instructions/copilot.md](instructions/copilot.md)
- **How do I validate my skill?** → Run `validate-skill` or use the checklist above
- **I found an issue** → File at https://github.com/waldronlab/ai-agent-skills/issues

---

**Version**: 2.0.0
**Last Updated**: 2026-04-03
**Authors**: waldronlab

See [AGENTS.md](AGENTS.md) for canonical format specification, [SKILLS.md](SKILLS.md) for skill index, [CONTRIBUTING.md](CONTRIBUTING.md) for contribution guidelines.
