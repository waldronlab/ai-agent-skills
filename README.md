# waldronlab AI Agent Skills

A collection of agent-agnostic skills and instructions for AI assistants (Claude Code, GitHub Copilot, Gemini, and future platforms) working on projects relevant to the Waldron Lab at CUNY SPH. This repository provides domain-specific knowledge to help AI agents understand our codebases, workflows, and standards.

## What are AI Agent Skills?

Skills are structured instructions that teach AI agents about:
- Package structures and conventions
- Analysis workflows and best practices
- Data types and their handling
- Testing and documentation standards
- Organization-wide patterns

With these skills, AI agents can:
- Create new skills and index them in [SKILLS.md](SKILLS.md)
- Follow Bioconductor coding standards
- Analyze R code and packages and suggest improvements
- Define and follow bioinformatic workflows and statistical methods

## Design Philosophy

This repository is built on core architectural decisions tailored specifically to how Large Language Models (LLMs) operate and how we build software in the waldronlab.

### Workflow Orchestration vs. Code-Centric Snippets

Many AI skill repositories act simply as code snippet libraries—providing the AI with advanced copy-paste templates to execute a single task. While fast, this **Code-Centric approach** is brittle, lacks autonomy, and misses the "why" behind the code.

Instead, we use **Workflow/Process Orchestration**. Our skills treat the AI like a junior developer given a Standard Operating Procedure (SOP). Rather than just providing raw syntax, a skill defines the *intent*, the *multi-step workflow*, and the *domain knowledge* required. 

For example, our code coverage skill doesn't just provide the command to run `covr`; it orchestrates a workflow: run the coverage, summarize the gaps, classify testing needs (Normal Use, Edge Cases, Error Handling, Correctness), and proactively write new test cases based on those criteria. This approach enables high autonomy, ensures the AI adheres to waldronlab quality standards, and allows it to adapt to different project structures using its general reasoning capabilities.

### Centralized Registry vs. Decentralized Discovery

When an AI agent needs to discover what it can do, it can either search through a file tree (**Decentralized Discovery**) or read a single index (**Centralized Registry**).

We use a **Centralized Registry** ([`SKILLS.md`](SKILLS.md)). For an AI agent, reading a single markdown file is an O(1) operation. Modern LLMs have massive context windows; parsing a comprehensive registry takes fractions of a second and negligible tokens. If discovery were decentralized, the agent would waste time, conversational turns, and context running search tools to hunt down the right instructions across dozens of folders. 

A centralized registry also provides vital relational context, allowing the LLM to instantly understand how skills chain together through "Use Case Workflows". While scaling to hundreds of skills may eventually require auto-generating the `SKILLS.md` file via CI/CD to prevent human git merge conflicts, the discovery interface for the AI remains intentionally centralized.

## Agent-Agnostic Design

Skills in this repository are **agent-agnostic** by design. They work across multiple AI agents through natural language invocation. For example:

- "What waldronlab skills do I have?" (to confirm you have the skills installed)
- "Help me create a new skill"
- "Analyze this R package"
- "Create .github/instructions for this package"

Your AI agent will match your request to the appropriate skill and execute it.

See [AGENTS.md](AGENTS.md) for detailed requirements for this repository, to be used for agent-assisted understanding of the repository and creation of new skills. See [SKILL_STANDARD.md](SKILL_STANDARD.md) for technical format details.

## Quick Start
1. Install the skills on your platform (see [Installation](#installation))
2. Ask your agent: "What waldronlab skills do I have?" to confirm
3. Use natural language to invoke skills (see [Usage Examples](#usage-examples))

## Usage Examples

Create AI Instructions for an R Package:

```
"Create .github/instructions for this R package"
```

Analyze an R Package:

```
"Analyze this R package"
"What type of R package is this?"
```

### Creating a New Skill

Natural language invocation:
```
"Help me create a new skill for [purpose]"
```

See [SKILLS.md](SKILLS.md) for all available skills and invocation examples. Using the skill-creation skill will guide you through the process of creating a new skill, validate that it conforms with standards, [SKILL_STANDARD.md](SKILL_STANDARD.md), and update the index in [SKILLS.md](SKILLS.md).

## Repository Structure

```
ai-agent-skills/
├── README.md                      # This file
├── LICENSE                        # MIT License
├── AGENTS.md                      # Agent behavior standard (how discovery works)
├── SKILLS.md                      # Human-readable skill index (what skills exist)
├── SKILL_STANDARD.md              # Technical format spec (how to format skills)
├── CONTRIBUTING.md                # Contribution guidelines
├── CHANGELOG.md                   # Version history and release notes
│
├── skills/                        # All skills (flat structure)
│   ├── {skill-name}/              # Each skill in its own directory
│   │   ├── SKILL.md               # Skill documentation (required)
│   │   ├── templates/             # Optional supporting files
│   │   └── examples/              # Optional examples
│   └── ... (see SKILLS.md for complete list)
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
- **[CHANGELOG.md](CHANGELOG.md)** - Version history and release notes
- **[instructions/](instructions/)** - Platform-specific setup and shortcuts

## Examples

See [skills/create-package-instructions/examples/](skills/create-package-instructions/examples/) for complete examples of generated instructions from real waldronlab packages:

- **data-package-parquet** - parkinsonsMetagenomicData with remote parquet access via DuckDB
- More examples coming soon...

## Contributing

We welcome contributions! See [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines.

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

## Support and Feedback

- **Issues**: Report bugs or request features via [GitHub Issues](https://github.com/waldronlab/ai-agent-skills/issues)
- **Discussions**: Ask questions in [GitHub Discussions](https://github.com/waldronlab/ai-agent-skills/discussions)

## License

MIT License - see [LICENSE](LICENSE) for details.

## Acknowledgments

These skills are developed and maintained by the waldronlab at CUNY SPH and collaborators to make AI agents more effective collaborators.

---

**Version**: 2.0.0 (agent-agnostic)
**Last Updated**: 2026-04-08
