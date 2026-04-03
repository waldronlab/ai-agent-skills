# Example: Complete Claude Code Skill Implementation

This shows a fully implemented skill as it would appear in the waldronlab/r-package-instructions-skills repository.

---

## File: claude/analyze-r-package.md

```markdown
---
name: analyze-r-package
description: Analyze R/Bioconductor package structure to extract key information for creating AI instructions
version: 1.0.0
---

# analyze-r-package

Analyze an R/Bioconductor package to understand its structure, purpose, and key characteristics. This skill provides structured output that other instruction-generation skills depend on.

## Usage

User invokes with:
- `/analyze-r-package`
- "Analyze this R package"
- "What type of R package is this?"

## Process

### 1. Read Package Metadata

Read and analyze the DESCRIPTION file:

\`\`\`
Tools to use:
- Read: DESCRIPTION file
\`\`\`

Extract:
- **Package name**: Package field
- **Title**: Title field (one-line summary)
- **Description**: Description field (detailed explanation)
- **Version**: Version field
- **Type classification**: Look at biocViews field for keywords:
  - "ExperimentData", "ExpressionData", etc. → Data Package
  - "StatisticalMethod", "Workflow" → Analysis Package
  - "Infrastructure", "DataRepresentation" → Infrastructure Package
  - Otherwise → Utility Package
- **Key dependencies**: Parse Imports and Depends fields, especially note:
  - SummarizedExperiment / TreeSummarizedExperiment
  - ExperimentHub / AnnotationHub
  - Database packages (DBI, DuckDB, RSQLite)
  - Remote data packages (httr2, aws.s3)

### 2. Identify Exported Functions

Read and parse the NAMESPACE file:

\`\`\`
Tools to use:
- Read: NAMESPACE
\`\`\`

Extract all lines starting with:
- `export(` - Regular function exports
- `exportClasses(` - S4 class exports
- `exportMethods(` - S4 method exports

Count and categorize:
- Data access functions (names containing: get, load, retrieve, fetch, access, return)
- Data processing functions (filter, subset, aggregate, transform)
- Utility functions (validate, check, confirm)
- Visualization functions (plot, draw, show)

### 3. Examine Directory Structure

Check which directories exist:

\`\`\`
Tools to use:
- Bash: ls -la to check directory structure
- Glob: */**.R to find R files
- Glob: vignettes/*.Rmd to find vignettes
\`\`\`

Note presence of:
- **data/** - R data objects (RDA files)
- **inst/extdata/** - Raw data files
- **vignettes/** - Count .Rmd files
- **tests/testthat/** - Testing framework
- **src/** - Compiled code (C/C++)

### 4. Detect Data Access Patterns

Search R source files for data access indicators:

\`\`\`
Tools to use:
- Grep: Search for patterns in R/ directory
\`\`\`

Search for these patterns (case insensitive):
- "ExperimentHub" → ExperimentHub integration
- "AnnotationHub" → AnnotationHub integration
- "dbConnect" OR "DuckDB" → Database access
- "download.file" OR "curl" → Direct URL downloads
- "aws.s3" OR "bucket" → AWS S3 access
- "huggingface" → HuggingFace datasets
- "parquet" → Parquet file handling
- "hdf5" OR "h5" → HDF5 file handling

If any matches found, classify as having **remote data access**.

### 5. Identify S4 Classes

Search for S4 class definitions:

\`\`\`
Tools to use:
- Grep: Search R/ for S4 patterns
\`\`\`

Search for:
- `setClass(`
- `methods::setClass(`
- `setMethod(`
- `setGeneric(`

List any S4 classes defined in the package.

### 6. Read README

Read the README file for package overview:

\`\`\`
Tools to use:
- Read: README.md (first 500 lines)
\`\`\`

Extract:
- High-level purpose (usually first few paragraphs)
- Key features listed
- Links to data sources or external resources
- Example usage patterns

### 7. Analyze Testing

Check test structure:

\`\`\`
Tools to use:
- Glob: tests/testthat/test-*.R
- Bash: ls inst/extdata/ | head -20
\`\`\`

Note:
- Number of test files
- Test data location and file types
- Whether tests use remote resources

### 8. List Vignettes

If vignettes exist:

\`\`\`
Tools to use:
- Glob: vignettes/*.Rmd
- Read: First 50 lines of each vignette to get title/purpose
\`\`\`

Create list with vignette names and purposes.

## Output Format

Produce a structured summary in this format:

\`\`\`markdown
## Package Analysis: [Package Name]

### Classification
- **Type**: [Data/Analysis/Infrastructure/Utility] Package
- **Purpose**: [1-2 sentence summary from DESCRIPTION and README]
- **Version**: [version number]

### Key Exports ([count] total)
**Data Access Functions** ([count]):
- `function1()` - [brief description if available]
- `function2()` - [brief description if available]

**Data Processing Functions** ([count]):
- `function3()` - [brief description if available]

**Utility Functions** ([count]):
- `function4()` - [brief description if available]

[Other categories as needed]

### Data Access Pattern
- **Type**: [None / Local Only / Remote / Hybrid]
- **Sources**: [List if applicable]
  - [Source 1]: [URL or location]
  - [Source 2]: [URL or location]
- **Technologies**: [e.g., ExperimentHub, DuckDB, direct URLs]

### S4 Classes
[If none: "No S4 classes defined"]
[If present:]
- `ClassName1` - [description if available]
- `ClassName2` - [description if available]

### Documentation
**Vignettes** ([count]):
1. [vignette-name.Rmd] - [Purpose/Title]
2. [vignette-name.Rmd] - [Purpose/Title]

**Testing**:
- Framework: [testthat / other / none]
- Test files: [count]
- Test data: [location and types]

### Special Characteristics
[List notable patterns that should be documented:]
- [Pattern 1]
- [Pattern 2]
- [Pattern 3]

### Dependencies of Note
[List key Bioconductor or specialized packages:]
- [Package1] - [why it's significant]
- [Package2] - [why it's significant]

## Recommendations for Instructions

Based on this analysis, create:
- [Always] 00-overview.md
- [If data access] 10-data-access.md
- [Always] 20-development.md
- [Always] 30-testing-docs.md
- [If vignettes exist] 40-vignettes.md
- [Always] 50-git-workflow.md
- [Always] INDEX.md
\`\`\`

## Example Output

Here's what the output looks like for parkinsonsMetagenomicData:

\`\`\`markdown
## Package Analysis: parkinsonsMetagenomicData

### Classification
- **Type**: Data Package
- **Purpose**: Provides uniformly processed gut microbiome data from Parkinson's Disease studies via remote parquet files accessed through DuckDB.
- **Version**: 0.99.0

### Key Exports (18 total)
**Data Access Functions** (5):
- `returnSamples()` - Main high-level data retrieval function
- `accessParquetData()` - Setup DuckDB connection to remote parquet files
- `loadParquetData()` - Load filtered data from DuckDB connection
- `load_ref()` - Load reference lookup tables
- `db_connect()` - Create DuckDB database connection

**Discovery Functions** (5):
- `parquet_colinfo()` - Inspect column structure of data types
- `get_hf_parquet_urls()` - Get HuggingFace parquet file URLs
- `get_repo_info()` - List available HuggingFace repositories
- `get_ref_info()` - List available reference tables
- `biobakery_files()` - List available data types with descriptions

**Utility Functions** (3):
- `data_dict()` - Sample metadata field definitions
- `output_file_types()` - Map data types to tool/file info
- Internal validation functions (confirm_*)

### Data Access Pattern
- **Type**: Hybrid (Remote primary, Local for testing)
- **Sources**:
  - HuggingFace: waldronlab/metagenomics_mac (full dataset)
  - HuggingFace: waldronlab/metagenomics_mac_examples (example subset)
  - Local: inst/extdata/ (test fixtures)
- **Technologies**: DuckDB for remote parquet access, TreeSummarizedExperiment output format

### S4 Classes
No S4 classes defined (returns TreeSummarizedExperiment from TreeSummarizedExperiment package)

### Documentation
**Vignettes** (5):
1. codebook.Rmd - Data Codebook: reference for all variables and data structures
2. first-15-minutes.Rmd - First 15 Minutes: quick start guide for new users
3. full-workflow.Rmd - Full Workflow: comprehensive tutorial with multiple data types
4. piecewise-workflow.Rmd - Piecewise Workflow: advanced direct database control patterns
5. working-with-large-parquet-files.Rmd - Working with Large Parquet Files: performance optimization strategies

**Testing**:
- Framework: testthat
- Test files: 3 (test-readParquet.R, test-utils.R, test-data.R)
- Test data: inst/extdata/ (parquet, TSV, RDS files - ~20KB each)

### Special Characteristics
- Uses DuckDB for efficient remote parquet file querying without full download
- Large file handling requires sorted column filtering strategies
- Multiple data types: taxonomic (MetaPhlAn), functional (HUMAnN), QC (FastQC, KneadData)
- Sample metadata included as package data object (sampleMetadata)
- Normalized and stratified variants of functional data
- Reference tables for feature name mappings

### Dependencies of Note
- TreeSummarizedExperiment - Return format for all data retrieval functions
- DuckDB - Core technology for remote parquet access
- dplyr - Data manipulation and filtering
- arrow - Parquet file support

## Recommendations for Instructions

Based on this analysis, create:
- [✓] 00-overview.md - Package overview, key functions, data sources
- [✓] 10-data-access.md - Critical: document returnSamples vs accessParquetData patterns, large file strategies
- [✓] 20-development.md - Parquet column structure, validation patterns
- [✓] 30-testing-docs.md - Test data usage, example requirements (\donttest for remote access)
- [✓] 40-vignettes.md - Document the 5 vignettes and their distinct purposes
- [✓] 50-git-workflow.md - Bioconductor submission requirements, git workflow
- [✓] INDEX.md - Navigation and quick reference
\`\`\`

## Notes

- This skill should be run first before other instruction-generation skills
- Output should be saved to conversation context for use by subsequent skills
- Manual verification recommended for complex packages
- If ambiguities exist, ask user for clarification rather than guessing

## Error Handling

If required files don't exist:
- DESCRIPTION missing → Error: "Not an R package directory"
- NAMESPACE missing → Warning: "No NAMESPACE found - may not be built yet"
- No R/ directory → Error: "No R source files found"

If directory structure is unclear:
- Ask user: "Is this a data package, analysis package, or infrastructure package?"
- Explain what you found and why classification is ambiguous
```

---

## Usage Example in VS Code

### Scenario: User Opens New R Package

1. User opens a waldronlab R package in VS Code
2. User opens Claude Code panel
3. User types: `/analyze-r-package`

### Claude's Response:

```
I'll analyze the package structure to understand its characteristics.

[Reads DESCRIPTION file...]
[Reads NAMESPACE...]
[Checks directory structure...]
[Searches for data access patterns...]
[Reads README...]

## Package Analysis: curatedMetagenomicData

[Complete structured output as shown above]

---

This package appears to be a Data Package with remote data access via ExperimentHub.

Would you like me to:
1. Create complete instructions with `/create-package-instructions`
2. Create specific instruction files (e.g., just data access guidance)
3. Explain any of these findings in more detail
```

### Follow-up Command:

User: `/create-package-instructions`

Claude generates all appropriate instruction files based on the analysis.

---

## Integration with Other Skills

The `analyze-r-package` skill output is consumed by:

1. **create-overview-instructions** - Uses classification, key exports, and purpose
2. **create-data-access-instructions** - Uses data access patterns and sources
3. **create-development-instructions** - Uses coding patterns and S4 classes
4. **create-testing-docs-instructions** - Uses testing framework and test data info
5. **create-vignette-instructions** - Uses vignette list and purposes
6. **create-git-workflow-instructions** - Uses package type for appropriate checks
7. **create-index** - Uses all information for comprehensive navigation

This modular design allows:
- Running full suite with one command
- Running individual skills for targeted updates
- Easy maintenance and improvement of individual skills
- Consistent data flow between skills
