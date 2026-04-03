# waldronlab AI Agent Skills

A collection of agent-agnostic skills and instructions for AI assistants (Claude Code, GitHub Copilot, and future platforms) working on projects relevant to the Waldron Lab at CUNY SPH. This repository provides domain-specific knowledge to help AI agents understand our codebases, workflows, and standards.

## What are AI Agent Skills?

Skills are structured instructions that teach AI agents about:
- Package structures and conventions
- Analysis workflows and best practices
- Data types and their handling
- Testing and documentation standards
- Organization-wide patterns

With these skills, AI agents can:
- Generate appropriate documentation
- Follow Bioconductor coding standards
- Suggest context-aware improvements
- Understand domain-specific patterns
- Provide better assistance on complex tasks

## Agent-Agnostic Design

Skills in this repository are **agent-agnostic** by design. They work across multiple AI agents through natural language invocation:

- **Canonical invocation**: Natural language matching skill descriptions
- **Optional shortcuts**: Platform adapters document conveniences (slash commands, @workspace patterns)
- **Single source**: One skill works everywhere without duplication
- **Portable**: Skills adapt to any compliant agent platform

See [AGENTS.md](AGENTS.md) for how agent behavior and skill discovery work. See [SKILL_STANDARD.md](SKILL_STANDARD.md) for technical format details.

## Quick Start

### 1. Find Skills

Browse [SKILLS.md](SKILLS.md) to see all available skills organized by category and use case.

### 2. Invoke Naturally

Describe what you need in natural language:
- "Help me create a new skill"
- "Analyze this R package"
- "Create .github/instructions for this package"

Your AI agent will match your request to the appropriate skill and execute it.

### 3. Optional Platform Shortcuts

If you prefer shortcuts:
- **Claude Code**: `/skill-name` slash commands (see [instructions/claude.md](instructions/claude.md))
- **GitHub Copilot**: `@workspace` patterns (see [instructions/copilot.md](instructions/copilot.md))

But natural language works everywhere.

## Available Skills

See [SKILLS.md](SKILLS.md) for the complete skill catalog. Quick overview:

### Meta Domain (Repository Infrastructure)

- **create-skill** - Collaborative Q&A for creating new skills
- **check-waldronlab-skills** - Verify installation and discover available skills

### R/Bioconductor Domain

- **analyze-r-package** - Analyze package structure and characteristics
- **create-package-instructions** - Generate comprehensive .github/instructions files
- **update-package-instructions** - Update existing package instructions

### Future Domains

- **metagenomics** (🚧 Planned) - Standard metagenomics workflows
- **statistical-methods** (🚧 Planned) - Statistical analysis patterns

For details on each skill, see [SKILLS.md](SKILLS.md).

## Installation

### Setup for Your Platform

Choose your AI agent platform:

- **Claude Code**: See [instructions/claude.md](instructions/claude.md) for setup
- **GitHub Copilot**: See [instructions/copilot.md](instructions/copilot.md) for setup
- **Other agents**: See [AGENTS.md](AGENTS.md) for compliance requirements

### Platform-Specific Setup

See the appropriate guide for your platform:
- **Claude Code**: [instructions/claude.md](instructions/claude.md)
- **GitHub Copilot**: [instructions/copilot.md](instructions/copilot.md)
- **Google Gemini**: [instructions/gemini.md](instructions/gemini.md)

Each guide includes complete setup instructions specific to that platform.

### Verify Installation

Ask your agent:
- "Do I have the waldronlab skills?"
- "What waldronlab skills are available?"

The agent should list the installed skills.

## Usage Examples

### Creating R Package Instructions

Natural language invocation (works everywhere):
```
"Create .github/instructions for this R package"
```

Or use optional shortcuts:
- Claude Code: `/create-package-instructions`
- GitHub Copilot: `@workspace Create .github/instructions`

### Analyzing an R Package

Natural language invocation:
```
"Analyze this R package"
"What type of R package is this?"
```

Or use optional shortcuts:
- Claude Code: `/analyze-r-package`
- GitHub Copilot: `@workspace analyze this package`

### Creating a New Skill

Natural language invocation:
```
"Help me create a new skill for [purpose]"
```

Or use optional shortcuts:
- Claude Code: `/create-skill`
- GitHub Copilot: `@workspace create a new skill`

See [SKILLS.md](SKILLS.md) for all available skills and invocation examples.

## Repository Structure

```
ai-agent-skills/
├── README.md                      # This file
├── LICENSE                        # MIT License
├── AGENTS.md                      # Agent behavior standard (how discovery works)
├── SKILLS.md                      # Human-readable skill index (what skills exist)
├── SKILL_STANDARD.md              # Technical format spec (how to format skills)
├── CONTRIBUTING.md                # Contribution guidelines
├── MIGRATION.md                   # Upgrade guide from v1.x to v2.0
│
├── skills/                        # All skills (flat structure)
│   ├── create-skill/
│   │   └── SKILL.md               # Collaborative skill creation
│   ├── check-waldronlab-skills/
│   │   └── SKILL.md               # Skill discovery and verification
│   ├── analyze-r-package/
│   │   └── SKILL.md               # R package analysis
│   ├── create-package-instructions/
│   │   ├── SKILL.md               # Generate package instructions
│   │   ├── templates/             # Shared Bioconductor and waldronlab standards
│   │   └── examples/              # Example generated instructions
│   └── update-package-instructions/
│       └── SKILL.md               # Update existing instructions
│
└── instructions/                  # Platform adapters (thin wrappers)
    ├── README.md                  # Adapter purpose and requirements
    ├── claude.md                  # Claude Code setup and shortcuts
    ├── copilot.md                 # GitHub Copilot setup and shortcuts
    └── gemini.md                  # Google Gemini (placeholder)
```

## Key Documentation

- **[AGENTS.md](AGENTS.md)** - How agents discover and invoke skills (mandatory behavior)
- **[SKILLS.md](SKILLS.md)** - Complete skill catalog organized by domain
- **[SKILL_STANDARD.md](SKILL_STANDARD.md)** - Technical format for creating skills
- **[CONTRIBUTING.md](CONTRIBUTING.md)** - How to contribute new skills or improvements
- **[MIGRATION.md](MIGRATION.md)** - Upgrade guide for v1.x users
- **[instructions/](instructions/)** - Platform-specific setup and shortcuts

## Examples

See [skills/create-package-instructions/examples/](skills/create-package-instructions/examples/) for complete examples of generated instructions from real waldronlab packages:

- **data-package-parquet** - parkinsonsMetagenomicData with remote parquet access via DuckDB
- More examples coming soon...

## Contributing

We welcome contributions! See [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines.

### Adding New Skills

**Quick start**: Use the `create-skill` skill to get guided help!

Natural language: "Help me create a new skill for [purpose]"

Or manually:
1. Create directory: `skills/{skill-name}/`
2. Create file: `skills/{skill-name}/SKILL.md`
3. Follow the [Agent Skills Standard Format](SKILL_STANDARD.md)
4. Include YAML frontmatter with required fields (no `platforms:` or `triggers:`)
5. Write platform-agnostic core logic
6. Add to [SKILLS.md](SKILLS.md) index
7. Test on multiple platforms
8. Submit PR for review

### Adding New Domains

If you have a new category of skills:

1. Create skills with the new `category:` value
2. Add domain description to [SKILLS.md](SKILLS.md)
3. Include at least one working skill with examples
4. Submit PR for review

## Maintenance

### Ownership

Domain maintainers are responsible for:
- Reviewing PRs for their skills
- Keeping skills up-to-date
- Testing on supported platforms
- Responding to issues

### Version Compatibility

We aim to keep skills compatible with:
- **Claude Code**: Latest stable version
- **GitHub Copilot**: Latest VS Code extension
- **R/Bioconductor**: Current release and devel

Breaking changes are documented in [CHANGELOG.md](CHANGELOG.md) and [MIGRATION.md](MIGRATION.md).

## Support and Feedback

- **Issues**: Report bugs or request features via [GitHub Issues](https://github.com/waldronlab/ai-agent-skills/issues)
- **Discussions**: Ask questions in [GitHub Discussions](https://github.com/waldronlab/ai-agent-skills/discussions)
- **Skills Check**: Use `check-waldronlab-skills` to verify your setup

## License

MIT License - see [LICENSE](LICENSE) for details.

## Acknowledgments

These skills are developed and maintained by the waldronlab at CUNY SPH and collaborators to make AI agents more effective collaborators.

---

**Status Legend**:
- ✅ Production ready
- 🚧 Under development
- 📋 Planned
- ⚠️  Deprecated

**Version**: 2.0.0 (agent-agnostic)
**Last Updated**: 2026-04-03
