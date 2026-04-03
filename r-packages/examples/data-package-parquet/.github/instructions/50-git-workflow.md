---
title: Git Workflow Guidance
topics: [git, commits, branches, checks, bioconductor]
---

# Git Workflow Guidance

For complete workflow standards, see:
- [Core Bioconductor standards](https://github.com/waldronlab/ai-agent-skills/blob/main/r-packages/templates/bioconductor-standards.md) - R CMD check, BiocCheck requirements
- [Waldronlab conventions](https://github.com/waldronlab/ai-agent-skills/blob/main/r-packages/templates/waldronlab-standards.md) - Git workflow, commits, PRs, AI agent acknowledgements

## Package-Specific Checks

### Before Committing

Standard checks (see [Bioconductor standards](https://github.com/waldronlab/ai-agent-skills/blob/main/r-packages/templates/bioconductor-standards.md)) plus:
- Verify vignettes knit successfully (this package has 5 vignettes)
- Test parquet file access with local test data
- Confirm UUID validation works correctly

## Quick commands
```bash
R CMD build .
R CMD check parkinsonsMetagenomicData_*.tar.gz
R -e "BiocCheck::BiocCheck('parkinsonsMetagenomicData_*.tar.gz')"
R -e "roxygen2::roxygenize()"
R -e "rmarkdown::render('vignettes/codebook.Rmd')"
R CMD INSTALL .
```