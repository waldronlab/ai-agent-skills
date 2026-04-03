# Available Skills

This is the canonical index of all available AI agent skills in the waldronlab/ai-agent-skills repository. Use this to discover and understand what skills are available and when to use them.

## Quick Start

1. **Browse by category** below to find a skill that matches your need
2. **Read the skill description** to understand when to use it
3. **Invoke naturally**: Describe what you need to your AI agent
   - Example: "Help me create a new skill"
   - Agent will match this to the appropriate skill and invoke it
4. **Optional**: Use platform-specific shortcuts if available (see instructions/{agent}.md)

## Setup & Discovery

**First time?**
- See [instructions/claude.md](instructions/claude.md) (Claude Code)
- See [instructions/copilot.md](instructions/copilot.md) (GitHub Copilot)

**Understanding the design:**
- See [AGENTS.md](AGENTS.md) for how skill discovery and invocation work

## Meta Skills

Infrastructure and workflow skills for working with this repository itself.

### create-skill

**Purpose**: Help create a new AI agent skill through collaborative Q&A

**Location**: `skills/create-skill/SKILL.md`

**When to use**:
- Creating a new skill from scratch
- Converting a manual workflow into a reusable skill
- Starting from a rough idea

**Invocation**:
- Natural language: "Help me create a new skill", "Create a skill for [domain]", "I want to make a skill that..."
- Claude Code optional shortcut: `/create-skill`
- Copilot optional shortcut: `@workspace create a new skill`

**What happens**:
- Collaborative Q&A to understand your intent
- Guidance on domain and location
- Brainstorming triggers (how users naturally invoke it)
- Step-by-step process outline
- Generated skill file in markdown format

**Output**: A new skill file ready for testing and iteration

---

### check-waldronlab-skills

**Purpose**: List and verify installed waldronlab skills

**Location**: `skills/check-waldronlab-skills/SKILL.md`

**When to use**:
- Verifying skills are correctly installed
- Discovering what skills are available
- Troubleshooting skill discovery issues
- Checking setup for Claude Code or Copilot

**Invocation**:
- Natural language: "What skills are available?", "List waldronlab skills", "Are my skills installed?", "Do I have the waldronlab skills?"
- Claude Code optional shortcut: `/check-waldronlab-skills`
- Copilot optional shortcut: `@workspace What waldronlab skills are there?`

**What happens**:
- Scans the repository for available skills
- Verifies your agent can access them
- Lists skills by category with descriptions
- Suggests next steps

**Output**: List of available skills and setup status

---

### validate-skill

**Purpose**: Validate that a skill conforms to the ai-agent-skills repository standards

**Location**: `skills/validate-skill/SKILL.md`

**When to use**:
- Creating new skills (before committing)
- Reviewing PRs
- Ensuring existing skills meet current standards
- CI/CD validation in automated workflows

**Invocation**:
- Natural language: "Validate this skill", "Check if skills/[skill-name]/SKILL.md meets standards", "Does this skill conform to standards?"
- Claude Code optional shortcut: `/validate-skill`
- Copilot optional shortcut: `@workspace validate this skill`

**What happens**:
- Runs generic validation (markdownlint, yamllint) if available
- Validates waldronlab-specific requirements:
  - Checks for prohibited fields (platforms, triggers)
  - Ensures platform-agnostic language (no tool references)
  - Validates required fields (name, description, version, category)
  - Checks naming conventions and consistency
- Generates detailed report with issues, fixes, and references to AGENTS.md/SKILL_STANDARD.md

**Output**: Comprehensive validation report with pass/fail status, categorized issues (CRITICAL/WARNING/INFO), and specific fix suggestions

**Related skills**: create-skill, check-waldronlab-skills

---

## R/Bioconductor Package Skills

Skills for analyzing, documenting, and developing R/Bioconductor packages following waldronlab conventions.

### analyze-r-package

**Purpose**: Analyze R/Bioconductor package structure and characteristics

**Location**: `skills/analyze-r-package/SKILL.md`

**When to use**:
- Understanding a package's architecture and design
- Determining package type (data, analysis, infrastructure)
- Identifying key functions and data structures
- Before generating documentation for a package

**Invocation**:
- Natural language: "Analyze this R package", "What type of package is this?", "Tell me about the package structure"
- Claude Code optional shortcut: `/analyze-r-package`
- Copilot optional shortcut: `@workspace analyze this R package`

**What happens**:
- Reads package metadata (DESCRIPTION, README, code)
- Identifies package type and purpose
- Lists key functions and classes
- Detects data access patterns (ExperimentHub, DuckDB, etc.)
- Summarizes architecture and design patterns

**Output**: Structured analysis of the package

---

### create-package-instructions

**Purpose**: Generate comprehensive .github/instructions files for R/Bioconductor packages

**Location**: `skills/create-package-instructions/SKILL.md`

**When to use**:
- Creating AI agent instructions for a new R package
- Generating documentation for AI agents working on the package
- Standardizing package documentation across waldronlab
- After analyzing a package with analyze-r-package

**Invocation**:
- Natural language: "Create .github/instructions for this package", "Generate AI agent instructions", "Create instructions for this R package"
- Claude Code optional shortcut: `/create-package-instructions`
- Copilot optional shortcut: `@workspace Create .github/instructions for this R package`

**What happens**:
- Uses analyze-r-package internally to understand the package
- Reads shared standards (Bioconductor conventions, waldronlab patterns)
- Generates modular instruction files in .github/instructions/
- Creates package-specific guidance
- References reusable standards to avoid duplication

**Output**:
- `.github/instructions/00-overview.md` - Package classification and architecture
- `.github/instructions/10-data-access.md` - Data handling patterns (if applicable)
- `.github/instructions/20-development.md` - Development patterns and conventions
- `.github/instructions/30-vignettes.md` - Vignette purposes and standards (if applicable)

**Related skills**: analyze-r-package, update-package-instructions

---

### update-package-instructions

**Purpose**: Update existing .github/instructions files based on recent package changes

**Location**: `skills/update-package-instructions/SKILL.md`

**When to use**:
- Refreshing package instructions after major changes
- Updating instructions when architecture changes
- Adding new data patterns or functions
- Keeping AI agent instructions current with the package

**Invocation**:
- Natural language: "Update the package instructions", "Refresh .github/instructions", "Update instructions based on recent changes"
- Claude Code optional shortcut: `/update-package-instructions`
- Copilot optional shortcut: `@workspace Update .github/instructions for this package`

**What happens**:
- Re-analyzes the current package state
- Compares with existing instructions
- Updates changed sections
- Preserves customizations and hand-written notes
- References updated standards if needed

**Output**: Updated `.github/instructions/` files

**Related skills**: analyze-r-package, create-package-instructions

---

## Metagenomics Skills

*Planned for future release*

Skills for standard metagenomics data processing and analysis workflows.

**Coming soon**:
- Standard preprocessing pipelines
- Taxonomic profiling workflows
- Functional analysis patterns

---

## Statistical Methods Skills

*Planned for future release*

Skills for statistical analysis patterns in microbiome and multi-omics research.

**Coming soon**:
- Differential abundance analysis
- Dimension reduction approaches
- Batch effect correction
- Multi-omics integration

---

## Skill Categories & Tags

### By Category

| Category | Skills | Purpose |
|----------|--------|---------|
| **meta** | create-skill, check-waldronlab-skills, validate-skill | Repository and workflow infrastructure |
| **r-packages** | analyze-r-package, create-package-instructions, update-package-instructions | R/Bioconductor package development |
| **metagenomics** | (Planned) | Metagenomics data workflows |
| **statistical-methods** | (Planned) | Statistical analysis patterns |

### By Tag

| Tag | Skills | Use Case |
|-----|--------|----------|
| **infrastructure** | create-skill, check-waldronlab-skills, validate-skill | Repository and workflow tasks |
| **validation** | validate-skill | Quality control and standards compliance |
| **quality-control** | validate-skill | Ensuring skill quality |
| **documentation** | create-package-instructions, update-package-instructions | Generating and maintaining docs |
| **analysis** | analyze-r-package | Understanding code and architecture |
| **bioconductor** | analyze-r-package, create-package-instructions, update-package-instructions | Bioconductor-specific workflows |
| **data-access** | analyze-r-package (detects), create-package-instructions | Working with remote data |

---

## Finding Skills by Use Case

### "I want to work on an R package..."

1. **Understand the package** → `analyze-r-package`
2. **Create AI instructions** → `create-package-instructions`
3. **Keep instructions updated** → `update-package-instructions`

### "I want to create a new skill..."

1. **Get guided help** → `create-skill`
2. **Validate it meets standards** → `validate-skill`
3. **Verify it's accessible** → `check-waldronlab-skills`

### "I want to verify my setup..."

1. **Check installed skills** → `check-waldronlab-skills`
2. See [instructions/](instructions/) for platform-specific setup

### "I want to analyze a workflow and automate it..."

1. **Create a skill for it** → `create-skill`

### "I want to ensure my skill meets standards..."

1. **Validate the skill** → `validate-skill`
2. **Fix any issues** based on the validation report
3. **Re-validate** until it passes

---

## How Skills Are Discovered and Invoked

### For Users

1. **Browse this file** (SKILLS.md) to understand what's available
2. **Describe your need** to your AI agent in natural language
3. **Agent handles the rest**:
   - Matches your description to a skill
   - Reads the skill file
   - Executes the skill process
   - Provides output

### For AI Agents

1. **Read SKILLS.md** (this file) as the primary discovery mechanism
2. **Match user intent** to skill descriptions and purposes
3. **Locate the skill file** at the specified location
4. **Read and follow** the skill documentation
5. **Execute** using your platform's available tools
6. **Deliver output** as documented in the skill

See [AGENTS.md](AGENTS.md) for the complete agent behavior standard.

---

## Contributing New Skills

Want to add a new skill?

1. **Brainstorm**: Use `create-skill` to develop your idea
2. **Create**: Follow the guidance and create the skill file
3. **Test**: Verify it works on your platform
4. **Document**: Add an entry to this file (SKILLS.md)
5. **Submit**: Create a PR for review

See [CONTRIBUTING.md](CONTRIBUTING.md) for detailed guidelines.

---

## Platform-Specific Information

### Claude Code

See [instructions/claude.md](instructions/claude.md) for:
- Setup and installation
- Optional `/skill-name` shortcuts
- Troubleshooting

### GitHub Copilot

See [instructions/copilot.md](instructions/copilot.md) for:
- Setup and installation
- Optional `@workspace` shortcuts
- Troubleshooting

### Other Agents

We're working on support for additional agents. See [instructions/](instructions/) for available adapters.

---

## Skill File Structure

Each skill is a markdown file with:
- **YAML frontmatter**: Metadata (name, description, version, category, tags)
- **Usage section**: How to invoke the skill
- **Prerequisites section**: What's needed before running
- **Process section**: Step-by-step instructions
- **Output section**: What the skill produces
- **Examples section**: Concrete usage scenarios
- **Optional sections**: Platform notes, error handling, etc.

For technical details on skill format, see [SKILL_STANDARD.md](SKILL_STANDARD.md).

---

## Questions?

- **How does skill invocation work?** → See [AGENTS.md](AGENTS.md)
- **How do I create a new skill?** → Use `create-skill` or see [CONTRIBUTING.md](CONTRIBUTING.md)
- **Where are the actual skill files?** → `skills/{skill-name}/SKILL.md`
- **Can I use skills on multiple platforms?** → Yes! Skills are platform-agnostic
- **How do I verify my setup?** → Use `check-waldronlab-skills` or see instructions/{agent}.md
- **I found an issue with a skill** → File an issue at https://github.com/waldronlab/ai-agent-skills/issues
- **I want to suggest a new skill** → Open a discussion at https://github.com/waldronlab/ai-agent-skills/discussions

---

**Last Updated**: 2026-04-03
**Version**: 2.0.0
**Maintained by**: waldronlab
