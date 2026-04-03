# waldronlab AI Agent Skills

A collection of skills and instructions for AI agents (Claude Code, GitHub Copilot) working with waldronlab projects. This repository provides domain-specific knowledge to help AI agents understand our codebases, workflows, and standards.

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

## Available Skill Domains

### 🔧 [r-packages/](r-packages/)
**Status**: ✅ Production ready

Skills for generating `.github/instructions/` files for R/Bioconductor packages. Automatically creates comprehensive AI agent instructions tailored to your package type (data/analysis/infrastructure).

**Quick start**: `/create-package-instructions` in any R package

**Features**:
- Automatic package type detection
- Generates modular instruction files
- Data access pattern documentation
- Bioconductor compliance guidance
- Vignette and testing standards

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

### For Claude Code Users

#### Option 1: Global Installation (Recommended)

Clone this repository and configure Claude Code to use these skills globally:

```bash
# Clone the repository
cd ~/git
git clone https://github.com/waldronlab/ai-agent-skills.git

# Add to VS Code user settings
code ~/.config/Code/User/settings.json
```

Add to your settings:
```json
{
  "claude.globalSkills": [
    "~/git/ai-agent-skills/r-packages/claude/analyze-r-package.md",
    "~/git/ai-agent-skills/r-packages/claude/create-package-instructions.md",
    "~/git/ai-agent-skills/r-packages/claude/update-package-instructions.md"
  ]
}
```

#### Option 2: Per-Workspace Installation

Add to your workspace `.vscode/settings.json`:
```json
{
  "claude.skills": [
    "../ai-agent-skills/r-packages/claude/analyze-r-package.md",
    "../ai-agent-skills/r-packages/claude/create-package-instructions.md"
  ]
}
```

### For GitHub Copilot Users

#### Option 1: Per-Repository Instructions

Copy the relevant instructions to your repository:

```bash
# For R packages
cp ~/git/ai-agent-skills/r-packages/copilot/instructions.md \
   .github/copilot-instructions.md
```

Copilot automatically loads `.github/copilot-instructions.md`.

#### Option 2: Workspace Reference

Add to your workspace `.vscode/settings.json`:
```json
{
  "github.copilot.instructionsFile": "../ai-agent-skills/r-packages/copilot/instructions.md"
}
```

#### Option 3: Organization-Wide (Copilot Enterprise)

For organization admins:
1. Go to https://github.com/organizations/waldronlab/settings/copilot
2. Add instructions from this repository to the knowledge base

## Quick Start Guide

### Generating R Package Instructions

1. Open an R/Bioconductor package in VS Code
2. Ensure skills are installed (see above)
3. Open Claude Code or Copilot Chat

**With Claude Code**:
```
/create-package-instructions
```

**With GitHub Copilot**:
```
@workspace Create .github/instructions for this R package
```

4. Review generated files in `.github/instructions/`
5. Customize as needed
6. Commit and create PR

### Updating Existing Instructions

**With Claude Code**:
```
/update-package-instructions
```

**With GitHub Copilot**:
```
@workspace Update .github/instructions based on recent package changes
```

## Repository Structure

```
ai-agent-skills/
├── README.md                      # This file
├── LICENSE                        # MIT License
├── CONTRIBUTING.md                # Contribution guidelines
│
├── r-packages/                    # R/Bioconductor package skills
│   ├── README.md                  # R packages documentation
│   ├── claude/                    # Claude Code skills
│   │   ├── analyze-r-package.md
│   │   ├── create-package-instructions.md
│   │   └── ...
│   ├── copilot/                   # GitHub Copilot instructions
│   │   └── instructions.md
│   ├── templates/                 # Instruction file templates
│   │   ├── 00-overview.template.md
│   │   └── ...
│   └── examples/                  # Real-world examples
│       ├── README.md
│       ├── data-package-parquet/
│       └── ...
│
├── metagenomics/                  # Metagenomics analysis skills
│   └── README.md
│
└── statistical-methods/           # Statistical analysis skills
    └── README.md
```

## Examples

See [r-packages/examples/](r-packages/examples/) for complete examples of generated instructions from real waldronlab packages:

- **data-package-parquet** (parkinsonsMetagenomicData): Remote parquet data via DuckDB
- More examples coming soon...

## Contributing

We welcome contributions! See [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines.

### Adding New Skills

1. Choose or create appropriate domain directory
2. Follow the existing skill format (see examples)
3. Test on multiple real packages/projects
4. Add examples demonstrating the skill
5. Update relevant README files
6. Submit PR for review

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
- **Internal**: waldronlab members can ask in Slack #ai-tools channel

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
