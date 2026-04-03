# Platform Adapter Instructions

This directory contains setup and usage instructions for specific AI agents working with waldronlab's skill repository.

## What Are Platform Adapters?

Platform adapters are **thin wrapper documents** that explain how to use the repository on a specific platform. They:

- ✅ Provide platform-specific setup and installation steps
- ✅ Document optional platform-specific shortcuts (slash commands, @workspace patterns)
- ✅ Reference the canonical sources (AGENTS.md, SKILLS.md)
- ✅ Offer platform-specific troubleshooting tips
- ✅ Explain how that platform differs from the canonical standard

They do **NOT**:

- ❌ Duplicate skill logic
- ❌ Create platform-specific requirements for skills
- ❌ Define new invocation patterns (natural language via SKILLS.md is canonical)
- ❌ Lock skills to a specific platform

## Available Adapters

- **[claude.md](claude.md)** - Claude Code setup and usage
- **[copilot.md](copilot.md)** - GitHub Copilot setup and usage
- **[gemini.md](gemini.md)** - Google Gemini (placeholder for future support)

## Core Principles

### 1. Skills are Platform-Agnostic

Skills are stored once in `skills/{skill-name}/SKILL.md`. They contain no platform-specific metadata or logic.

### 2. Natural Language is Canonical

All agents discover and invoke skills through natural language matching to descriptions in SKILLS.md. Examples:
- "Help me create a new skill"
- "Analyze this R package"
- "Create .github/instructions"

### 3. Platform Shortcuts are Optional

Platform-specific invocation patterns (slash commands, @workspace triggers) are optional conveniences for users who know about them. Agents that don't support these shortcuts still work perfectly fine with natural language invocation.

### 4. Adapters Reference, Don't Duplicate

Every adapter should reference:
- **AGENTS.md** - For canonical agent behavior
- **SKILLS.md** - For skill discovery
- **skills/{name}/SKILL.md** - For the actual skill documentation

## Creating a New Adapter

If you want to add support for a new AI agent platform:

1. **Create a new file**: `instructions/{agent-name}.md`
2. **Follow the structure**:
   - Setup/Installation section
   - Discovering skills section (reference SKILLS.md)
   - Optional shortcuts section (if applicable)
   - Examples section
   - Troubleshooting section
   - Links to AGENTS.md and SKILLS.md
3. **Test**: Verify a few skills work on the new platform
4. **Document**: Explain what's unique about that platform
5. **Submit PR**: Include clear instructions for users

Example template:

```markdown
# [Agent Name] Setup

## Installation

[Platform-specific setup steps]

## Discovering Skills

1. Read [SKILLS.md](../SKILLS.md) for available skills
2. Describe what you need to me in natural language
3. I'll match your request to a skill and execute it

## Optional [Platform] Shortcuts

[Platform-specific command syntax examples, if any]

**Note**: These are optional. Natural language always works.

## Usage Examples

[Concrete examples specific to this platform]

## Troubleshooting

[Common issues and solutions for this platform]

See [AGENTS.md](../AGENTS.md) for canonical behavior.
```

## Adapter Maintenance

Adapters should be updated when:
- Setup instructions change
- New platforms shortcuts are added
- Troubleshooting common issues discovered
- Links to AGENTS.md or SKILLS.md are broken

Adapters should **NOT** be updated when:
- Individual skill logic changes (update the skill, not the adapter)
- YAML frontmatter format changes (update SKILL_STANDARD.md)
- New skills are added (update SKILLS.md)

## Relationship to Other Documentation

- **AGENTS.md** - Canonical agent behavior rules (what ALL agents must do)
- **SKILLS.md** - Human-readable skill index and discovery (how users find skills)
- **instructions/{agent}.md** - Platform-specific setup (how to use on this platform)
- **SKILL_STANDARD.md** - Technical format specification (how to structure skills)

---

**Maintained by**: waldronlab
**Last Updated**: 2026-04-03
