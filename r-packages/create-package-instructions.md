---
name: create-package-instructions
description: Create complete AI instruction documentation for an R/Bioconductor package in .github/instructions/
version: 1.0.0
platforms:
  - claude-code
  - github-copilot
triggers:
  claude:
    - /create-package-instructions
    - "Create instructions for this package"
    - "Generate AI documentation for this package"
  copilot:
    - "@workspace create .github/instructions for this R package"
    - "@workspace generate AI documentation"
    - "@workspace set up instructions for this package"
    - "@workspace create instructions"
author: waldronlab
category: r-packages
---

# create-package-instructions

Create a complete set of AI instructions for an R/Bioconductor package. This skill orchestrates the analysis of a package and creation of appropriate instruction files based on the package type and characteristics.

The generated instructions help AI agents understand your package structure, coding standards, and workflows, making them more effective collaborators on your codebase.

## Usage

**Claude Code**:
- `/create-package-instructions`
- "Create instructions for this package"
- "Generate AI documentation for this package"

**GitHub Copilot**:
- `@workspace create .github/instructions for this R package`
- `@workspace generate AI documentation`
- `@workspace set up instructions for this package`

## Prerequisites

- Working directory is an R package root (contains DESCRIPTION file)
- Package has standard R structure (R/, NAMESPACE, etc.)
- Target directory `.github/instructions/` will be created if it doesn't exist

## Process

### 1. Run Package Analysis

First, analyze the package to understand its structure.

**Action**: Run the `analyze-r-package` skill to produce a complete package analysis.

This provides the structured information needed to determine which instruction files to create and what content to include.

### 2. Determine Required Instruction Files

Based on the analysis output, determine which instruction files are needed:

**Always create**:
- `00-overview.md` - Package overview, key functions, data sources
- `20-development.md` - Development patterns, coding conventions
- `30-testing-and-docs.md` - Testing and documentation guidelines
- `50-git-workflow.md` - Git workflow and Bioconductor submission requirements
- `INDEX.md` - Navigation and quick reference

**Conditionally create**:
- `10-data-access.md` - **Only if** the package has data access patterns (Type: Remote or Hybrid from analysis)
- `40-vignettes.md` - **Only if** the package has vignettes (count > 0 from analysis)

### 3. Create `.github/instructions/` Directory

If the directory doesn't exist, create it:
- Ensure `.github/` parent directory exists
- Create `instructions/` subdirectory

### 4. Create Instruction Files

For each required file, create it with appropriate content based on the package analysis:

#### 00-overview.md

**Content structure**:
```markdown
# [Package Name] Overview

## Classification
- **Type**: [Data/Analysis/Infrastructure/Utility] Package
- **Version**: [version number]

## Purpose
[2-3 paragraphs from DESCRIPTION and README explaining what the package does]

## Key Functions

### [Category Name] ([count] functions)
[List from analysis - Data Access, Processing, Utility, etc.]
- `function1()` - [Brief description]
- `function2()` - [Brief description]

## Quick Start
[Provide simple example showing typical usage - adapt from README if available]

## Key Concepts
[Important domain concepts or patterns specific to this package]

## Data Sources
[If applicable - list from analysis]
- [Source 1]: [Details]
```

**Data to populate from analysis**:
- Package type classification
- Version number
- Purpose from DESCRIPTION and README
- Categorized function lists with counts
- Data sources if applicable

#### 10-data-access.md (if needed)

**Create only if**: Package has Remote or Hybrid data access pattern

**Content structure**:
```markdown
# Data Access Patterns

## Overview
[Explain how data is accessed in this package]

## Primary Data Access Functions

### High-Level Functions
[User-facing data retrieval functions]

### Low-Level Functions
[Advanced/direct access functions]

## Data Sources
[ExperimentHub, URLs, local files, S3, HuggingFace, etc.]
- **[Source Type]**: [Details and URLs]

## Access Patterns

### Basic Retrieval
[Example of simple data access]

### Filtered Retrieval
[Example of accessing specific subsets]

### Advanced Queries
[If applicable - e.g., SQL queries for DuckDB]

## Large File Handling
[If applicable - strategies for managing large datasets]

## Testing with Data
- **Production data**: [How to access full datasets]
- **Test/example data**: [Location in inst/extdata/]
- **Running tests**: [How tests handle remote vs local data]
```

**Data to populate from analysis**:
- Data access technologies (DuckDB, ExperimentHub, etc.)
- Data access function categories
- Data source URLs and types
- Large file handling characteristics

#### 20-development.md

**Content structure**:
```markdown
# Development Patterns

## Function Organization
[How R/ directory is structured]

## Naming Conventions
[Patterns observed in the codebase]

## S4 Classes and Methods
[If applicable]

### Classes
[List with slots]

### Methods
[Key methods]

## Input Validation
[Validation patterns used]

## Error Handling
[How errors and warnings are handled]

## Key Dependencies
[Important dependencies and their usage]

## Code Style
[Package-specific style guidelines]
```

**Data to populate from analysis**:
- S4 classes if defined
- Key dependencies and why they're important
- Observed coding patterns

#### 30-testing-and-docs.md

**Content structure**:
```markdown
# Testing and Documentation

## Testing Framework
[testthat / other]

## Test Structure
[Organization from analysis]

## Test Data
- **Location**: [inst/extdata/, data/, etc.]
- **File types**: [Parquet, RDS, TSV, etc.]

## Running Tests
\`\`\`r
devtools::test()
testthat::test_file("tests/testthat/test-name.R")
\`\`\`

## Documentation Requirements

### Function Documentation (roxygen2)
Required tags for exported functions:
- `@title` and/or first line
- `@description`
- `@param` for each parameter
- `@return` describing return value
- `@examples` with working examples
- `@export` for exported functions

### Examples Guidelines
- Use `\\donttest{}` for examples requiring remote resources
- Use `\\dontrun{}` for examples that shouldn't run in R CMD check
- Ensure examples are reproducible

## Common Testing Patterns
[Package-specific patterns]
```

**Data to populate from analysis**:
- Testing framework
- Test file count and structure
- Test data location and types
- Whether tests use remote resources

#### 40-vignettes.md (if needed)

**Create only if**: Package has vignettes (count > 0)

**Content structure**:
```markdown
# Vignette Guide

## Available Vignettes

### [vignette-filename.Rmd]
**Title**: [From YAML frontmatter]
**Purpose**: [What this vignette teaches]
**Audience**: [Beginner/Intermediate/Advanced]
**Key Topics**:
- [Topic 1]
- [Topic 2]

## Recommended Reading Order

For new users:
1. [first-vignette.Rmd] - [Why start here]
2. [second-vignette.Rmd] - [What it builds on]

## Updating Vignettes

Guidelines for maintaining vignettes:
- Ensure all code chunks execute successfully
- Update examples if function signatures change
- Test: `devtools::build_vignettes()`
```

**Data to populate from analysis**:
- List of vignettes with titles and purposes
- Suggested reading order based on content

#### 50-git-workflow.md

**Content structure**:
```markdown
# Git Workflow

## Branch Naming
- `feature/description` - New features
- `bugfix/description` - Bug fixes
- `docs/description` - Documentation only

## Commit Messages
Format:
\`\`\`
type: brief description

Optional detailed explanation.
\`\`\`

Types: feat, fix, docs, test, refactor

## Pre-Commit Checks

Before committing:
1. **Tests pass**: `devtools::test()`
2. **Examples work**: `devtools::run_examples()`
3. **Documentation builds**: `devtools::document()`
4. **R CMD check passes**: `devtools::check()`

## Pull Requests

PRs should:
- Have clear title and description
- Pass all CI checks
- Include tests for new functionality
- Update documentation as needed

## Version Bumping

[For Bioconductor packages]
- Development: 0.99.x (pre-Bioconductor)
- After acceptance: Increment y in x.y.z
- Update DESCRIPTION and commit separately

## Bioconductor Submission

[If Data Package or submitting to Bioconductor]

Requirements:
- Pass `BiocCheck::BiocCheck()`
- Vignettes build successfully
- All examples run
```

**Data to populate from analysis**:
- Package type affects Bioconductor submission section

#### INDEX.md

**Content structure**:
```markdown
# Instructions Index

Quick reference for AI assistants working with [Package Name].

## Quick Links
- [Overview](00-overview.md) - Package classification and key functions
[If data package:]
- [Data Access](10-data-access.md) - Data retrieval patterns
- [Development](20-development.md) - Coding standards
- [Testing & Docs](30-testing-and-docs.md) - Testing and documentation
[If has vignettes:]
- [Vignettes](40-vignettes.md) - Vignette guide
- [Git Workflow](50-git-workflow.md) - Git and release workflow

## Package Metadata
- **Name**: [Package name]
- **Type**: [Package type]
- **Version**: [Current version]
- **Repository**: [GitHub URL if in README]

## Key Functions Quick Reference

### Data Access
[One-line descriptions]

### Analysis/Processing
[One-line descriptions]

## External Resources
- [Bioconductor page](https://bioconductor.org/packages/[PackageName]/)
- [GitHub repository]([URL])

## Quick Commands

\`\`\`r
BiocManager::install("[PackageName]")
library([PackageName])
?[keyFunction]
browseVignettes("[PackageName]")
\`\`\`
```

**Data to populate from analysis**:
- All metadata from package analysis
- Links to all created instruction files
- Function quick reference by category

### 5. Update Package Files

#### .gitignore

Check that `.github/instructions/` is NOT ignored (instructions should be committed).

If `.gitignore` contains `.github/instructions/`, remove that line.

#### .Rbuildignore

Add entry to prevent instructions from being included in package build:

```
^\.github/instructions$
```

If `.Rbuildignore` doesn't exist, create it with this line.

### 6. Provide Summary

After creating all files, provide a detailed summary:

```markdown
## Created Package Instructions

Created the following instruction files in `.github/instructions/`:

- ✓ 00-overview.md - Package overview with [N] key functions
[If applicable:]
- ✓ 10-data-access.md - [Type] data access patterns with [N] sources
- ✓ 20-development.md - Development patterns and coding standards
- ✓ 30-testing-and-docs.md - Testing ([N] test files) and documentation
[If applicable:]
- ✓ 40-vignettes.md - Guide for [N] vignettes
- ✓ 50-git-workflow.md - Git workflow and release process
- ✓ INDEX.md - Navigation and quick reference

These instructions provide comprehensive guidance for AI assistants working with [PackageName].

### Next Steps
1. Review the generated instructions for accuracy
2. Add package-specific examples where helpful
3. Customize domain-specific terminology
4. Commit the instructions: `git add .github/instructions/`
5. Create PR for team review

### Customization Recommended
The following sections may benefit from manual enhancement:
- [Section 1] - [Why]
- [Section 2] - [Why]
```

## Example Output

For a data package like parkinsonsMetagenomicData:

```
## Created Package Instructions

Created the following instruction files in `.github/instructions/`:

- ✓ 00-overview.md - Package overview with 18 exported functions across 3 categories
- ✓ 10-data-access.md - DuckDB/parquet data access patterns with large file strategies
- ✓ 20-development.md - Development patterns for TreeSummarizedExperiment output
- ✓ 30-testing-and-docs.md - Testing with remote resources and example data
- ✓ 40-vignettes.md - Documentation for 5 vignettes from quick-start to advanced
- ✓ 50-git-workflow.md - Bioconductor submission workflow and version management
- ✓ INDEX.md - Complete navigation and quick reference

These instructions provide comprehensive guidance for AI assistants working with parkinsonsMetagenomicData.

Key highlights:
- Hybrid data access pattern (remote HuggingFace + local testing)
- DuckDB technology for efficient parquet queries
- Multiple data types: taxonomic, functional, QC
- 5 vignettes covering different use cases and skill levels
```

## Platform-Specific Notes

### Claude Code
- Use Write tool to create new instruction files
- Use Edit tool if files already exist (ask user first)
- Run `/analyze-r-package` or invoke the skill directly
- Output summary to conversation

### GitHub Copilot
- Create files using VS Code file operations
- Run analysis by following analyze-r-package instructions
- Display summary in chat

## Configuration Options

Users can customize the instruction generation:

**Skip specific files**:
- "Create instructions but skip vignettes documentation"
- "Just create the data access instructions"

**Custom directory**:
- Default is `.github/instructions/`
- User can specify alternate location

**Template customization**:
- Files follow waldronlab conventions
- Can be adjusted based on organization preferences

## Error Handling

**If package analysis fails**:
- Propagate error from analyze-r-package
- Provide guidance on what's missing or misconfigured

**If instruction directory creation fails**:
- Check permissions
- Suggest alternative locations or manual creation

**If individual file creation fails**:
- Continue with other files
- Report which files succeeded and which failed
- Provide partial output with instructions to complete

**If instructions already exist**:
- Ask user: "Instructions already exist. Overwrite, merge, or cancel?"
- Suggest using `update-package-instructions` instead

## Integration

**This skill uses**:
- `analyze-r-package` - To gather package information

**This skill is used by**:
- Users manually when setting up new packages
- Can be called from other orchestration workflows

**Works with**:
- `update-package-instructions` - For updating existing instructions
- Individual file generator skills (if they exist)

## Notes

- Always run package analysis first to gather necessary information
- Respect existing instruction files - ask before overwriting
- Instructions should be concise and actionable for AI assistants
- Focus on package-specific patterns, not general R/Bioconductor knowledge
- Generated content is a starting point - encourage customization
- Instructions should be committed to the repository for team use
