# R/Bioconductor Package Instructions for GitHub Copilot

This file provides comprehensive instructions for GitHub Copilot to work effectively with R/Bioconductor packages in the waldronlab organization.

## Overview

You are assisting with R/Bioconductor package development. These packages typically fall into four categories:

1. **Data Packages**: Provide access to datasets (ExperimentData)
2. **Analysis Packages**: Statistical methods and workflows (Software)
3. **Infrastructure Packages**: Base classes and core functionality (Software)
4. **Utility Packages**: Helper functions and tools (Software)

## Core Tasks

### 1. Analyzing Package Structure

When asked to analyze an R package, follow this process:

**Read key files**:
- `DESCRIPTION`: Package metadata, dependencies, biocViews
- `NAMESPACE`: Exported functions and classes
- `README.md`: Package overview and key features
- `R/`: Source code for all functions
- `vignettes/`: Documentation and tutorials
- `tests/testthat/`: Test files

**Extract information**:
- Package type (from biocViews: ExperimentData, StatisticalMethod, etc.)
- Exported functions (from NAMESPACE: export, exportClasses, exportMethods)
- Data access patterns (search for: ExperimentHub, DuckDB, download.file, aws.s3, parquet)
- S4 classes (search for: setClass, setMethod, setGeneric)
- Testing structure (count test files, identify test data)
- Vignettes (list .Rmd files with their purposes)

**Produce analysis output**:
```markdown
## Package Analysis: [Package Name]

### Classification
- **Type**: [Data/Analysis/Infrastructure/Utility] Package
- **Purpose**: [1-2 sentence summary]
- **Version**: [version number]

### Key Exports ([count] total)
[List by category: Data Access, Data Processing, Utility, Visualization]

### Data Access Pattern
- **Type**: [None / Local Only / Remote / Hybrid]
- **Sources**: [If applicable]
- **Technologies**: [e.g., ExperimentHub, DuckDB, direct URLs]

### Documentation
- **Vignettes**: [count and list]
- **Testing**: [framework, test file count, test data location]

### Special Characteristics
[Notable patterns to document]
```

### 2. Creating .github/instructions/

When asked to create instructions for an R package:

**Step 1**: Analyze the package (see above)

**Step 2**: Create `.github/instructions/` directory if it doesn't exist

**Step 3**: Generate appropriate instruction files based on package type:

**Always create**:
- `00-overview.md` - Package classification, key functions, quick start
- `20-development.md` - Coding patterns, S4 classes, dependencies
- `30-testing-and-docs.md` - Testing requirements, examples, roxygen
- `50-git-workflow.md` - Branch naming, commits, pre-commit checks
- `INDEX.md` - Navigation and quick reference

**Conditionally create**:
- `10-data-access.md` - If package has data access patterns (Remote or Hybrid)
- `40-vignettes.md` - If package has vignettes

**Step 4**: Update `.gitignore` and `.Rbuildignore` if needed

**Step 5**: Provide summary of created files

### 3. Updating Existing Instructions

When asked to update existing instructions:

**Step 1**: Analyze current package state

**Step 2**: Read existing instruction files

**Step 3**: Identify changes:
- Version bumps
- New/removed functions
- New vignettes
- Changed data access patterns
- Modified testing structure

**Step 4**: Update relevant sections:
- Use targeted edits, not wholesale replacement
- Preserve manual customizations
- Update cross-references

**Step 5**: Provide change summary

## Instruction File Content Guidelines

### 00-overview.md Structure

```markdown
# Package Overview

## Classification
[Data/Analysis/Infrastructure/Utility Package]

## Purpose
[2-3 paragraphs explaining what the package does]

## Key Functions

### Data Access Functions
[If applicable - list with brief descriptions]

### Analysis Functions
[If applicable - list with brief descriptions]

### Utility Functions
[List with brief descriptions]

## Quick Start
[Simple example showing typical usage]

## Key Concepts
[Important domain concepts or patterns]
```

### 10-data-access.md Structure (if applicable)

```markdown
# Data Access Patterns

## Overview
[How data is accessed in this package]

## Primary Data Access Functions

### High-Level Functions
[User-facing data retrieval functions]

### Low-Level Functions
[Advanced/direct access functions]

## Data Sources
[List sources: ExperimentHub, URLs, local files]

## Access Patterns
[Examples of typical data queries]

## Large File Handling
[If applicable - strategies for managing large datasets]

## Testing with Data
[How to use test vs. production data]
```

### 20-development.md Structure

```markdown
# Development Patterns

## Function Organization
[How R/ directory is structured]

## Naming Conventions
[Patterns for function names, e.g., snake_case vs camelCase]

## S4 Classes and Methods
[If applicable - document classes, slots, methods]

## Input Validation
[Common validation patterns used]

## Error Handling
[How errors and warnings are handled]

## Dependencies
[Key dependencies and their usage]

## Code Style
[Any package-specific style guidelines beyond Bioconductor standards]
```

### 30-testing-and-docs.md Structure

```markdown
# Testing and Documentation

## Testing Framework
[testthat, other]

## Test Structure
[How tests/ directory is organized]

## Test Data
[Location and usage of test data files]

## Running Tests
[How to run tests locally]

## Documentation Requirements

### Function Documentation
[roxygen2 patterns, required tags]

### Examples
[Requirements for examples: \dontrun, \donttest usage]

### Vignette Code
[Requirements for vignette code chunks]

## Common Patterns
[Testing patterns specific to this package]
```

### 40-vignettes.md Structure (if applicable)

```markdown
# Vignette Guide

## Available Vignettes

### [vignette-name.Rmd]
**Purpose**: [What this vignette teaches]
**Audience**: [Beginner/Intermediate/Advanced]
**Key Topics**: [List main topics covered]

## Recommended Reading Order
[Suggested sequence for new users]

## Updating Vignettes
[Guidelines for maintaining vignettes]

## Vignette Patterns
[Common structures or approaches used]
```

### 50-git-workflow.md Structure

```markdown
# Git Workflow

## Branch Naming
[Convention: feature/*, bugfix/*, etc.]

## Commit Messages
[Format and style]

## Pre-Commit Checks
[What to verify before committing]

## Pull Requests
[PR requirements and review process]

## Version Bumping
[When and how to increment version numbers]

## Bioconductor Submission
[If applicable - submission process and requirements]

## Release Process
[Steps for creating releases]
```

### INDEX.md Structure

```markdown
# Instructions Index

## Quick Links
- [Overview](00-overview.md) - Package classification and key functions
- [Data Access](10-data-access.md) - [If applicable] Data retrieval patterns
- [Development](20-development.md) - Coding standards and patterns
- [Testing & Docs](30-testing-and-docs.md) - Testing and documentation requirements
- [Vignettes](40-vignettes.md) - [If applicable] Vignette guide
- [Git Workflow](50-git-workflow.md) - Git and release workflow

## Package Metadata
- **Name**: [Package name]
- **Type**: [Package type]
- **Version**: [Current version]

## Key Functions Quick Reference
[Bulleted list of most important functions with one-line descriptions]

## External Resources
[Links to Bioconductor page, GitHub repo, documentation sites, etc.]
```

## Bioconductor Standards

### Package Structure
- `DESCRIPTION` must include: Package, Title, Version, Authors@R, Description, License, biocViews
- `NAMESPACE` should be auto-generated by roxygen2
- `R/` contains all source code (.R files)
- `man/` contains documentation (.Rd files, auto-generated)
- `vignettes/` contains .Rmd vignette files
- `tests/testthat/` contains test files (test-*.R)
- `inst/extdata/` for external data files
- `data/` for .rda data objects

### Documentation Standards
- All exported functions must have roxygen2 documentation
- Include `@param`, `@return`, `@examples` tags
- Use `\donttest{}` for examples requiring remote resources
- Use `\dontrun{}` for examples that shouldn't run in R CMD check
- Vignettes should be compilable and reproducible

### Coding Standards
- Use `<-` for assignment, not `=`
- Line length: 80 characters max (flexible to 100)
- Indentation: 4 spaces (not tabs)
- Use snake_case for function names
- Use camelCase for S4 class names
- Include space after commas: `c(1, 2, 3)`

### Testing Standards
- Use testthat framework
- Test file names: `test-<topic>.R`
- Aim for high code coverage
- Mock or skip tests requiring remote resources
- Use `inst/extdata/` for test fixtures

### Version Numbering
- Development: 0.99.x (pre-Bioconductor release)
- Released: x.y.z format
- Bioconductor devel: even y (e.g., 1.0.z)
- Bioconductor release: odd y (e.g., 1.1.z)

## Data Package Specifics

### ExperimentHub Integration
```r
# Typical pattern
hub <- ExperimentHub()
hub_data <- query(hub, "PackageName")
resource <- hub[[resource_id]]
```

### DuckDB/Parquet Pattern
```r
# Remote parquet access
con <- dbConnect(duckdb::duckdb())
data <- dbGetQuery(con, "SELECT * FROM read_parquet('url')")
```

### Data Access Function Patterns
- High-level: `getData()`, `returnSamples()`
- Low-level: `accessData()`, `loadData()`
- Discovery: `listAvailable()`, `getMetadata()`
- Validation: `validateInput()`, `checkAvailability()`

## Analysis Package Specifics

### Method Functions
- Clear input/output format documentation
- Parameter validation
- Progress reporting for long-running operations
- Sensible defaults

### Statistical Methods
- Document assumptions
- Provide diagnostic outputs
- Include examples with interpretation
- Reference publications

## Common Patterns

### Error Messages
```r
if (!valid) {
  stop("Clear error message with suggestion", call. = FALSE)
}
```

### Progress Reporting
```r
# For long operations
message("Processing sample ", i, " of ", n)
```

### Conditional Dependencies
```r
if (!requireNamespace("optionalPkg", quietly = TRUE)) {
  stop("Package optionalPkg required. Install with: BiocManager::install('optionalPkg')")
}
```

## Examples and References

See the examples/ directory in this repository for complete instruction sets from real waldronlab packages:
- `data-package-parquet/` - parkinsonsMetagenomicData example

## When to Ask for Clarification

Ask the user for clarification when:
- Package type is ambiguous (no clear biocViews)
- Data access patterns are unclear
- Vignette purposes are not obvious from titles
- Custom patterns that don't match standard Bioconductor conventions
- Breaking changes that affect instructions

## Useful Commands

### Analyzing package
```r
# Load package
devtools::load_all()

# Check package
devtools::check()

# Build documentation
devtools::document()

# Run tests
devtools::test()

# Build vignettes
devtools::build_vignettes()
```

### Package info
```r
# List exports
ls("package:packageName")

# Get help
?functionName

# View vignette
vignette("vignette-name", package = "packageName")
```

## Additional Context

- Lab follows Bioconductor standards and conventions
- Emphasis on reproducibility and documentation
- Data packages often use remote storage (HuggingFace, S3, ExperimentHub)
- TreeSummarizedExperiment is common return format for microbiome data
- Testing should work with local example data, not require full downloads

## Response Guidelines

When generating or updating instructions:
1. Be specific to the package - don't just repeat general Bioconductor docs
2. Focus on patterns actually used in the package code
3. Include examples with actual function names from the package
4. Preserve any manually added domain knowledge or warnings
5. Keep it concise - instructions should be scannable
6. Use markdown effectively (headers, lists, code blocks)
7. Cross-reference between instruction files when relevant
