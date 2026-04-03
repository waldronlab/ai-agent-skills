---
title: Testing and Documentation Guidance
topics: [roxygen, examples, testing, documentation]
---

# Testing and Documentation Guidance

For complete standards, see:
- [Core Bioconductor standards](https://github.com/waldronlab/ai-agent-skills/blob/main/r-packages/templates/bioconductor-development.md) - Documentation and testing requirements
- [Waldronlab conventions](https://github.com/waldronlab/ai-agent-skills/blob/main/r-packages/templates/waldronlab-standards.md) - Documentation and testing practices

## Package-Specific Testing

### Test Data
- **Location**: Small local files in `inst/extdata/`
- **File types**: Representative parquet, TSV/TXT, and RDS test files
- **Remote testing**: Tests avoid remote dependencies where possible; use local alternatives

### Testing Focus Areas
- Invalid input and error handling
- UUID validation patterns
- Parquet column structure verification
- TreeSummarizedExperiment output format

## Package-Specific Documentation

### Examples Approach
- Include at least one runnable example per exported function
- Use `\donttest{}` for examples requiring network access or that may hit rate limits
- Always provide a local alternative using test data when network examples exist
- **Never** use `\dontrun{}` - if it can't run, provide a local alternative

## Before considering a change complete
- Run `roxygen2::roxygenize()` if docs changed
- Verify examples still work
- Check that exported functions have tests
- Follow the complete checklist in [50-git-workflow.md](50-git-workflow.md#before-committing)