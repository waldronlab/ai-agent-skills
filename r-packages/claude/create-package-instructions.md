---
name: create-package-instructions
description: Create complete AI instruction documentation for an R/Bioconductor package based on its analysis
version: 1.0.0
---

# create-package-instructions

Create a complete set of AI instructions for an R/Bioconductor package. This skill orchestrates the analysis of a package and creation of appropriate instruction files based on the package type and characteristics.

## Usage

User invokes with:
- `/create-package-instructions`
- "Create instructions for this package"
- "Generate AI documentation for this R package"

## Prerequisites

This skill assumes:
- Working directory is an R package root (contains DESCRIPTION file)
- Target directory for instructions exists or will be created at `.github/instructions/`

## Process

### 1. Run Package Analysis

First, analyze the package to understand its structure:

```
Skills to use:
- /analyze-r-package
```

This provides the structured information needed to determine which instruction files to create.

### 2. Determine Required Instruction Files

Based on the analysis output, determine which instruction files are needed:

**Always create:**
- `00-overview.md` - Package overview, key functions, data sources
- `20-development.md` - Development patterns, coding conventions
- `30-testing-and-docs.md` - Testing and documentation guidelines
- `50-git-workflow.md` - Git workflow and Bioconductor submission requirements
- `INDEX.md` - Navigation and quick reference

**Conditionally create:**
- `10-data-access.md` - **If** the package has data access patterns (Type: Remote or Hybrid)
- `40-vignettes.md` - **If** the package has vignettes

### 3. Create Instruction Files

For each required file, create or update it in `.github/instructions/`:

```
Tools to use:
- Write: Create new instruction files
- Edit: Update existing instruction files
```

Use these guidelines for each file type:

#### 00-overview.md
- Package classification (Data/Analysis/Infrastructure/Utility)
- High-level purpose and goals
- Key exported functions by category
- Data sources (if applicable)
- Quick start guidance

#### 10-data-access.md (if needed)
- Data access technologies (ExperimentHub, DuckDB, etc.)
- Primary data access functions and their patterns
- Large file handling strategies
- Remote vs local data usage
- Example access patterns

#### 20-development.md
- S4 classes and methods (if applicable)
- Function naming conventions observed
- Data structure patterns
- Code organization principles
- Dependencies and their usage

#### 30-testing-and-docs.md
- Testing framework and structure
- Test data location and usage
- Remote resource handling in tests
- Documentation requirements
- Example patterns from existing tests

#### 40-vignettes.md (if needed)
- List of vignettes with purposes
- Key topics covered in each
- Recommended order for new users
- Vignette maintenance guidelines

#### 50-git-workflow.md
- Standard git workflow
- Branch naming conventions
- Bioconductor submission requirements (for data packages)
- Pre-commit checks
- Version bumping procedures

#### INDEX.md
- Quick links to all instruction files
- Package metadata summary
- Key function quick reference
- External resources

### 4. Provide Summary

After creating files, provide a summary:

```markdown
## Created Package Instructions

Created/updated the following instruction files in `.github/instructions/`:

- ✓ 00-overview.md
- ✓ 10-data-access.md (data package with remote access)
- ✓ 20-development.md
- ✓ 30-testing-and-docs.md
- ✓ 40-vignettes.md (5 vignettes)
- ✓ 50-git-workflow.md
- ✓ INDEX.md

These instructions provide comprehensive guidance for AI assistants working with [PackageName].

Next steps:
1. Review the generated instructions for accuracy
2. Commit the instructions to the repository
3. Update as the package evolves
```

## Integration with Specialized Skills

This orchestrator skill coordinates with specialized instruction-generation skills (when available):

- **create-overview-instructions** - Uses classification, key exports, and purpose
- **create-data-access-instructions** - Uses data access patterns and sources
- **create-development-instructions** - Uses coding patterns and S4 classes
- **create-testing-docs-instructions** - Uses testing framework and test data info
- **create-vignette-instructions** - Uses vignette list and purposes
- **create-git-workflow-instructions** - Uses package type for appropriate checks
- **create-index** - Uses all information for comprehensive navigation

If specialized skills are not available, this skill generates the content directly using the templates and guidelines above.

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

## Configuration

You can customize the instruction generation by:

1. **Skipping specific files**: User can specify which files to skip
   - "Create instructions but skip vignettes documentation"
   - "Just create the data access instructions"

2. **Custom instruction directory**: Default is `.github/instructions/`
   - User can specify alternate location

3. **Template customization**: Files follow waldronlab conventions
   - Can be adjusted based on organization preferences

## Error Handling

If package analysis fails:
- Propagate error from `analyze-r-package` skill
- Provide guidance on what's missing or misconfigured

If instruction directory creation fails:
- Check permissions
- Suggest alternative locations

If individual file creation fails:
- Continue with other files
- Report which files succeeded and which failed
- Provide partial output with instructions to complete

## Notes

- Always run `analyze-r-package` first to gather necessary information
- Respect existing instruction files - ask before overwriting
- For updates, prefer Edit over Write to preserve customizations
- Instructions should be concise and actionable for AI assistants
- Focus on package-specific patterns, not general R/Bioconductor knowledge
