# R Package Instructions Skills

Skills for automatically generating `.github/instructions/` files for R/Bioconductor packages. These instructions help AI agents understand your package structure, coding standards, and workflows.

## What This Does

Analyzes your R/Bioconductor package and generates a complete set of modular instruction files that teach AI agents:

- **Package purpose and architecture** - What the package does and how it's organized
- **Data access patterns** - How to retrieve and work with package data (if applicable)
- **Coding standards** - Function naming, validation, S4 classes, etc.
- **Testing and documentation** - Requirements for tests, examples, and roxygen
- **Vignette guidance** - Purpose of each vignette and update guidelines
- **Git workflow** - Branch naming, commits, checks, and release process

## Quick Start

### Using GitHub Copilot

**Create instructions**:
```
@workspace Create .github/instructions for this R package
```

**Update instructions**:
```
@workspace Update .github/instructions based on recent package changes
```

### Using Claude Code

**Analyze your package**:
```
/analyze-r-package
```

**Generate complete instructions**:
```
/create-package-instructions
```

**Update existing instructions**:
```
/update-package-instructions
```

## Generated File Structure

```
.github/instructions/
├── INDEX.md                  # Navigation and quick reference
├── 00-overview.md           # Package overview and key functions
├── 10-data-access.md        # Data retrieval patterns (if data package)
├── 20-development.md        # Coding standards and patterns
├── 30-testing-and-docs.md   # Testing and documentation requirements
├── 40-vignettes.md          # Vignette purposes (if vignettes exist)
└── 50-git-workflow.md       # Git workflow and checks
```

Files are generated conditionally based on your package type:
- All packages get: 00, 20, 30, 50, INDEX
- Data packages also get: 10
- Packages with vignettes also get: 40

## Package Type Detection

The skills automatically detect and adapt to different package types:

### Data Packages
- ExperimentData with remote or local data access
- Focus on data retrieval functions and filtering patterns
- Document data sources (ExperimentHub, URLs, local files)
- Include large file handling strategies if applicable

**Example**: parkinsonsMetagenomicData (remote parquet files via DuckDB)

### Analysis Packages
- Statistical methods and workflows
- Focus on method documentation and use cases
- Document input/output formats
- Include common analysis patterns

**Example**: MicrobiomeProfiler, microbiomeMarker

### Infrastructure Packages
- Base classes and core functionality
- Focus on S4 class structures and validation
- Document extensibility patterns
- Include constructor and accessor documentation

**Example**: TreeSummarizedExperiment, MultiAssayExperiment

### Utility Packages
- Helper functions and tools
- Focus on function organization and use cases
- Group related functions
- Include error handling patterns

## Available Skills

### Core Skills

#### analyze-r-package
Analyzes package structure to extract key information.

**What it does**:
- Reads DESCRIPTION, NAMESPACE, README
- Identifies package type and key exports
- Detects data access patterns
- Lists vignettes and tests
- Produces structured summary

**Usage**: `/analyze-r-package`

#### create-package-instructions
Orchestrator that generates complete instruction set.

**What it does**:
- Runs package analysis
- Creates `.github/instructions/` directory
- Generates all applicable instruction files
- Updates .gitignore and .Rbuildignore
- Provides summary and next steps

**Usage**: `/create-package-instructions`

#### update-package-instructions
Updates existing instructions based on package changes.

**What it does**:
- Compares current package state to existing instructions
- Identifies outdated information
- Updates relevant files
- Preserves manual customizations where possible

**Usage**: `/update-package-instructions`

### Individual File Generators

These can be run individually if you only need to update specific files:

- `create-overview-instructions` → 00-overview.md
- `create-data-access-instructions` → 10-data-access.md
- `create-development-instructions` → 20-development.md
- `create-testing-docs-instructions` → 30-testing-and-docs.md
- `create-vignette-instructions` → 40-vignettes.md
- `create-git-workflow-instructions` → 50-git-workflow.md
- `create-index` → INDEX.md

## Examples

See [examples/](examples/) for complete instruction sets from real waldronlab packages:

- **[data-package-parquet](examples/data-package-parquet/)** - parkinsonsMetagenomicData
  - Remote parquet files via DuckDB
  - Large file handling strategies
  - Multiple data types and vignettes

More examples coming soon.

## Installation

### For GitHub Copilot

**Per-repository (recommended)**:
```bash
cp ~/git/ai-agent-skills/r-packages/copilot/instructions.md \
   .github/copilot-instructions.md
```

**Or reference via settings**:
```json
// .vscode/settings.json
{
  "github.copilot.instructionsFile": "../ai-agent-skills/r-packages/copilot/instructions.md"
}
```

### For Claude Code

**Global (recommended)**:
```json
// ~/.config/Code/User/settings.json
{
  "claude.globalSkills": [
    "~/git/ai-agent-skills/r-packages/claude/analyze-r-package.md",
    "~/git/ai-agent-skills/r-packages/claude/create-package-instructions.md",
    "~/git/ai-agent-skills/r-packages/claude/update-package-instructions.md"
  ]
}
```

**Per-workspace**:
```json
// .vscode/settings.json
{
  "claude.skills": [
    "../ai-agent-skills/r-packages/claude/analyze-r-package.md",
    "../ai-agent-skills/r-packages/claude/create-package-instructions.md",
    "../ai-agent-skills/r-packages/claude/update-package-instructions.md"
  ]
}
```

## Customization

After generating instructions:

1. **Review for accuracy** - Verify package-specific details
2. **Add domain context** - Include biological/statistical concepts
3. **Document gotchas** - Add warnings about common mistakes
4. **Add examples** - Include package-specific code examples
5. **Update cross-references** - Ensure links between files are correct

The generated instructions are a starting point - feel free to customize!

## Templates

The [templates/](templates/) directory contains the base templates used to generate instructions. These show the structure and can be customized if you want to change the format organization-wide.

## Testing Your Generated Instructions

After generating instructions:

1. **Test with AI agent**: Ask it questions about your package and see if responses align with instructions
2. **Check cross-references**: Verify all markdown links work
3. **Review for completeness**: Ensure package-specific patterns are documented
4. **Get feedback**: Have package maintainers review
5. **Iterate**: Update and refine based on usage

## Workflow

### Initial Creation

1. Navigate to R package root
2. Create instructions:
   - **Copilot**: `@workspace Create .github/instructions for this R package`
   - **Claude**: `/create-package-instructions`
3. Review generated files
4. Customize for package-specific patterns
5. Commit: `git add .github/instructions/`
6. Create PR for team review

### Updating Existing

1. Make changes to package (new functions, vignettes, etc.)
2. Update instructions:
   - **Copilot**: `@workspace Update .github/instructions based on recent changes`
   - **Claude**: `/update-package-instructions`
3. Review changes and diffs
4. Adjust any sections that need manual attention
5. Commit updates

### Maintenance

- **When to update**: After major feature additions, API changes, or structural changes
- **Frequency**: Review quarterly or when package structure changes
- **Responsibility**: Package maintainer or designated documentation lead

## Best Practices

### DO:
✅ Generate instructions early in package development
✅ Update instructions when package structure changes
✅ Customize generated content for your specific package
✅ Include domain-specific terminology and concepts
✅ Get feedback from other contributors
✅ Use as onboarding material for new contributors

### DON'T:
❌ Generate once and never update
❌ Include sensitive information (API keys, credentials)
❌ Copy verbatim without reviewing
❌ Remove package-specific customizations when updating
❌ Document implementation details that change frequently

## Troubleshooting

### Skills not showing up
- Verify skills are in correct location
- Check VS Code settings path is correct
- Reload VS Code window
- Check Claude Code / Copilot extension is updated

### Generated instructions seem generic
- Run `/analyze-r-package` first to ensure proper analysis
- Check DESCRIPTION has accurate biocViews
- Manually customize after generation
- Add package-specific examples

### Updates overwrite customizations
- Use individual file generators instead of full update
- Keep customizations clearly marked
- Review diffs before accepting changes
- Consider templating commonly customized sections

## Contributing

See main repository [CONTRIBUTING.md](../CONTRIBUTING.md) for general guidelines.

### For R Package Skills Specifically:

1. **Test on multiple package types** before submitting
2. **Include examples** showing the output
3. **Update templates** if changing instruction format
4. **Document** any new package patterns discovered
5. **Maintain backwards compatibility** when possible

## Support

- **Issues**: Report bugs at https://github.com/waldronlab/ai-agent-skills/issues
- **Questions**: Use GitHub Discussions

## Version History

See [CHANGELOG.md](../CHANGELOG.md) for version history and changes.

---

**Maintainers**: [Add names]
**Last Updated**: 2026-04-03
**Status**: ✅ Production ready
