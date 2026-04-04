---
name: create-package-instructions
description: Create complete AI instruction documentation for an R/Bioconductor package in .github/instructions/
version: 1.0.0
category: r-packages
tags: [r-packages, documentation, bioconductor]
author: waldronlab
---

# create-package-instructions

Create complete AI instruction documentation for an R/Bioconductor package in `.github/instructions/`.

## Usage

Invoke this skill when you want to generate AI-friendly documentation for an R package:
- "Create instructions for this package"
- "Generate AI documentation"
- "Create .github/instructions for this R package"
- "Set up instructions for this package"

You must be in an R package directory (contains DESCRIPTION file) for this skill to work.

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
- `10-data-access.md` - Only if package has data access patterns (Type: Remote or Hybrid from analysis)
- `40-vignettes.md` - Only if package has vignettes (count > 0 from analysis)

### 3. Create `.github/instructions/` Directory

If the directory doesn't exist, create it:
- Ensure `.github/` parent directory exists
- Create `instructions/` subdirectory

### 4. Create Instruction Files

For each required file, create it with appropriate content based on the package analysis.

#### 00-overview.md

Content structure:

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

Populate from analysis:
- Package type classification
- Version number
- Purpose from DESCRIPTION and README
- Categorized function lists with counts
- Data sources if applicable

#### 10-data-access.md (if needed)

Create only if package has Remote or Hybrid data access pattern.

Content structure:

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

Populate from analysis:
- Data access technologies
- Data access function categories
- Data source URLs and types
- Large file handling characteristics

#### 20-development.md

Content structure:

```markdown
# Development Patterns

For complete Bioconductor and waldronlab standards, see:
- [Core Bioconductor standards](../../templates/bioconductor-development.md)
- [Waldronlab conventions](../../templates/waldronlab-standards.md)

## Package-Specific Patterns

### Function Organization
[How this package's R/ directory is structured]

### Naming Conventions
[Patterns specific to this package]

## S4 Classes and Methods
[If applicable - describe package-specific classes]

## Key Dependencies
[Important dependencies and their specific usage in this package]

## Code Style Notes
[Any package-specific style patterns]
```

Populate from analysis:
- S4 classes if defined
- Key dependencies and their role
- Package-specific naming patterns
- Custom validation patterns
- Function organization approach

#### 30-testing-and-docs.md

Content structure:

```markdown
# Testing and Documentation

For complete standards, see:
- [Core Bioconductor standards](../../templates/bioconductor-development.md)
- [Waldronlab conventions](../../templates/waldronlab-standards.md)

## Package-Specific Testing

### Test Organization
[How tests are organized for this package]

### Test Data
- **Location**: [inst/extdata/, tests/testthat/fixtures/]
- **File types**: [Parquet, RDS, TSV, etc.]
- **Purpose**: [What the test data represents]

### Remote Data Testing
[If applicable - how this package handles remote resources]

### Running Tests
[Commands and examples]

## Package-Specific Documentation Patterns

### Function Categories
[Document how functions are grouped and documented]

### Common Parameters
[If functions share common parameters, document them]

## Common Testing Patterns
[Specific to this package]
```

Populate from analysis:
- Test file organization and names
- Test data location, types, and purpose
- Whether remote resources are tested
- Common parameters across functions
- Package-specific testing patterns

#### 40-vignettes.md (if needed)

Create only if package has vignettes (count > 0).

Content structure:

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

Populate from analysis:
- List of vignettes with titles and purposes
- Suggested reading order based on content

#### 50-git-workflow.md

Content structure:

```markdown
# Git Workflow

For complete workflow standards, see:
- [Core Bioconductor standards](../../templates/bioconductor-development.md)
- [Waldronlab conventions](../../templates/waldronlab-standards.md)

## Package-Specific Checks

### Pre-Commit Quick Commands

\`\`\`bash
# Build and check
R CMD build .
R CMD check [PackageName]_*.tar.gz

# Documentation
R -e "roxygen2::roxygenize()"

# Tests
R -e "devtools::test()"
\`\`\`

## Package-Specific Considerations

[List any special requirements for this package]

## Version and Release

Current version: [from DESCRIPTION]

## CI/CD

[If GitHub Actions or other CI configured]
- Automated checks: [list what's automated]
- Manual checks: [list what requires manual verification]
```

Populate from analysis:
- Package name for command examples
- Current version from DESCRIPTION
- Package type (pre-Bioc, Bioc, CRAN)
- Whether package has vignettes, S4 classes, remote data
- CI/CD configuration if detected

#### INDEX.md

Content structure:

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

[Organized by category with one-line descriptions]

## External Resources
- [Bioconductor page]
- [GitHub repository]

## Quick Commands

\`\`\`r
BiocManager::install("[PackageName]")
library([PackageName])
?[keyFunction]
browseVignettes("[PackageName]")
\`\`\`
```

Populate from analysis:
- All metadata from package analysis
- Links to all created instruction files
- Function quick reference by category

### 5. Update Package Files

#### .gitignore

Check that `.github/instructions/` is NOT ignored (instructions should be committed).

#### .Rbuildignore

Add entry to prevent instructions from being included in package build:

```
^\.github/instructions$
```

If `.Rbuildignore` doesn't exist, create it with this line.

### 6. Provide Summary

After creating all files, provide a detailed summary showing:
- Which files were created
- Number of functions documented
- Data access patterns if applicable
- Number of vignettes if applicable
- Next steps for customization
- Recommendation to commit to the repository

## Integration

**This skill uses**:
- `analyze-r-package` - To gather package information

**This skill is used by**:
- Users manually when setting up new packages
- Can be called from other orchestration workflows

**Works with**:
- `update-package-instructions` - For updating existing instructions

## Error Handling

**If package analysis fails**:
- Propagate error from analyze-r-package
- Provide guidance on what's missing or misconfigured

**If instruction directory creation fails**:
- Check permissions
- Suggest alternative locations or manual creation

**If instructions already exist**:
- Ask user: "Instructions already exist. Overwrite, merge, or cancel?"
- Suggest using `update-package-instructions` instead

## Notes

- Run package analysis first to gather necessary information
- Ask before overwriting existing instruction files
- Focus on package-specific patterns, reference shared standards rather than duplicating
- Generated content is a starting point—customization expected
- Commit instructions to repository for team use

---

**Related**: See [analyze-r-package](../analyze-r-package/SKILL.md) for package analysis skill, [update-package-instructions](../update-package-instructions/SKILL.md) for updating existing instructions.
