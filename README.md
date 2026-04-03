# waldronlab AI Agent Skills

A collection of skills and instructions for AI agents (Claude Code, GitHub Copilot) working projects relevant to the Waldron Lab at CUNY SPH. This repository provides domain-specific knowledge to help AI agents understand our codebases, workflows, and standards.

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

## Cross-Platform Compatibility

Skills in this repository follow the [Agent Skills Standard Format](SKILL_STANDARD.md), making them compatible with multiple AI agents:

- **Claude Code**: Use `/skill-name` or natural language triggers
- **GitHub Copilot**: Use `@workspace` triggers
- **Future platforms**: Extensible format for new agents

This unified approach eliminates duplication and ensures consistency across platforms. See [SKILL_STANDARD.md](SKILL_STANDARD.md) for details on the format and how to create cross-platform skills.

## Available Skill Domains

### 🔧 [r-packages/](r-packages/)
**Status**: ✅ Production ready

Skills for generating `.github/instructions/` files for R/Bioconductor packages. Automatically creates comprehensive AI agent instructions tailored to your package type (data/analysis/infrastructure).

**Quick start**:
- Claude Code: `/create-package-instructions`
- GitHub Copilot: `@workspace Create .github/instructions`

**Features**:
- Automatic package type detection
- Generates modular instruction files
- Data access pattern documentation
- Bioconductor compliance guidance
- Vignette and testing standards

### 🛠️ [meta/](meta/)
**Status**: ✅ Production ready

Skills for working with the ai-agent-skills repository itself - creating, maintaining, and improving the skill framework.

**Quick start**:
- Claude Code: `/create-skill`
- GitHub Copilot: `@workspace create a new skill`

**Features**:
- Collaborative Q&A for skill creation
- Brainstorming from rough ideas
- Platform-agnostic guidance
- Iteration-friendly approach

### 🧬 [metagenomics/](metagenomics/)
**Status**: 🚧 Planned

Skills for analyzing metagenomic data following waldronlab standards.

**Planned features**:
- Standard preprocessing pipelines
- Taxonomic profiling workflows
- Functional analysis patterns
- Multi-study integration
- Reproducible analysis templates

### 📊 [statistical-methods/](statistical-methods/)
**Status**: 🚧 Planned

Skills for common statistical analysis patterns in microbiome and multi-omics research.

**Planned features**:
- Differential abundance analysis
- Dimension reduction approaches
- Batch effect correction
- Multi-omics integration
- Power analysis and study design

## Installation

### For GitHub Copilot Users

#### Option 1: Per-Repository Instructions (Recommended)

Copy the relevant instructions to your repository:

```bash
# For R packages - copy unified skills
cp ~/git/ai-agent-skills/r-packages/*.md \
   .github/copilot-instructions/
```

Copilot automatically loads instructions from `.github/copilot-instructions/`.

#### Option 2: Workspace Reference

Add to your workspace `.vscode/settings.json`:
```json
{
  "github.copilot.instructionsFile": "../ai-agent-skills/r-packages/"
}
```

Or reference specific skill files if your Copilot version supports it.

#### Option 3: Organization-Wide (Copilot Enterprise)

For organization admins:
1. Go to https://github.com/organizations/waldronlab/settings/copilot
2. Add skill files from domain directories (e.g., `r-packages/*.md`) to the knowledge base

### For Claude Code Users

#### Option 1: Global Installation (Recommended)

Clone this repository and configure Claude Code to use these skills globally:

```bash
# Clone the repository
cd ~/git
git clone https://github.com/waldronlab/ai-agent-skills.git
```

Add to your VS Code settings (`~/.config/Code/User/settings.json`):
```json
{
  "claude.globalSkills": [
    "~/git/ai-agent-skills/meta/create-skill.md",
    "~/git/ai-agent-skills/r-packages/analyze-r-package.md",
    "~/git/ai-agent-skills/r-packages/create-package-instructions.md",
    "~/git/ai-agent-skills/r-packages/update-package-instructions.md"
  ]
}
```

#### Option 2: Per-Workspace Installation

Add to your workspace `.vscode/settings.json`:
```json
{
  "claude.skills": [
    "../ai-agent-skills/meta/create-skill.md",
    "../ai-agent-skills/r-packages/analyze-r-package.md",
    "../ai-agent-skills/r-packages/create-package-instructions.md",
    "../ai-agent-skills/r-packages/update-package-instructions.md"
  ]
}
```

## Quick Start Guide

### Generating R Package Instructions

1. Open an R/Bioconductor package in VS Code
2. Ensure skills/instructions are installed (see above)
3. Open Copilot Chat or Claude Code

**With GitHub Copilot**:
```
@workspace Create .github/instructions for this R package
```

**With Claude Code**:
```
/create-package-instructions
```

4. Review generated files in `.github/instructions/`
5. Customize as needed
6. Commit and create PR

### Updating Existing Instructions

**With GitHub Copilot**:
```
@workspace Update .github/instructions based on recent package changes
```

**With Claude Code**:
```
/update-package-instructions
```

## Repository Structure

```
ai-agent-skills/
├── README.md                      # This file
├── LICENSE                        # MIT License
├── CONTRIBUTING.md                # Contribution guidelines
├── SKILL_STANDARD.md              # Standard format for cross-platform skills
│
├── r-packages/                    # R/Bioconductor package skills
│   ├── README.md                  # R packages documentation
│   ├── analyze-r-package.md       # Unified skill
│   ├── create-package-instructions.md
│   ├── update-package-instructions.md
│   ├── templates/                 # Shared templates
│   └── examples/                  # Real-world examples
│       ├── README.md
│       ├── data-package-parquet/
│       └── ...
│
├── meta/                          # Repository infrastructure skills
│   ├── README.md                  # Meta skills documentation
│   └── create-skill.md            # Collaborative skill creation
│
├── metagenomics/                  # Metagenomics skills (planned)
│   └── README.md
│
└── statistical-methods/           # Statistical analysis skills (planned)
    └── README.md
```

## Examples

See [r-packages/examples/](r-packages/examples/) for complete examples of generated instructions from real waldronlab packages:

- **data-package-parquet** (parkinsonsMetagenomicData): Remote parquet data via DuckDB
- More examples coming soon...

## Contributing

We welcome contributions! See [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines.

### Adding New Skills

**Quick start**: Use the `/create-skill` skill (or `@workspace create a new skill`) to get guided help!

Manual steps:
1. Choose or create appropriate domain directory (e.g., `r-packages/`, `metagenomics/`)
2. Follow the [Agent Skills Standard Format](SKILL_STANDARD.md)
3. Include YAML frontmatter with all required fields
4. Write platform-agnostic core logic
5. Add platform-specific notes where necessary
6. Test on both Claude Code and GitHub Copilot
7. Add examples demonstrating the skill
8. Update the domain's README file
9. Submit PR for review

### Adding New Domains

If you have a new category of skills:

1. Create new domain directory with README.md
2. Set up claude/ and copilot/ subdirectories
3. Add at least one working skill with examples
4. Update this main README
5. Submit PR for review

## Maintenance

### Ownership

Each domain has designated maintainers listed in its README:

- **r-packages/**: [Maintainer names]
- **metagenomics/**: [Maintainer names]
- **statistical-methods/**: [Maintainer names]

Domain maintainers are responsible for:
- Reviewing PRs for their domain
- Keeping skills up-to-date
- Testing on new package versions
- Responding to issues

### Version Compatibility

We aim to keep skills compatible with:
- **Claude Code**: Latest stable version
- **GitHub Copilot**: Latest VS Code extension
- **R/Bioconductor**: Current release and devel

Breaking changes are documented in [CHANGELOG.md](CHANGELOG.md).

## Support and Feedback

- **Issues**: Report bugs or request features via [GitHub Issues](https://github.com/waldronlab/ai-agent-skills/issues)
- **Discussions**: Ask questions in [GitHub Discussions](https://github.com/waldronlab/ai-agent-skills/discussions)

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
