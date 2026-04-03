---
name: update-package-instructions
description: Update existing AI instruction documentation when an R/Bioconductor package changes
version: 1.0.0
platforms:
  - claude-code
  - github-copilot
triggers:
  claude:
    - /update-package-instructions
    - "Update the package instructions"
    - "Refresh AI documentation for this package"
  copilot:
    - "@workspace update .github/instructions based on recent package changes"
    - "@workspace refresh the package instructions"
    - "@workspace update AI documentation"
    - "@workspace sync instructions with current package state"
author: waldronlab
category: r-packages
---

# update-package-instructions

Update existing `.github/instructions/` files to reflect changes in an R/Bioconductor package. This skill intelligently detects what has changed and updates only the relevant sections while preserving manual customizations.

## Usage

**Claude Code**:
- `/update-package-instructions`
- "Update the package instructions"
- "Refresh AI documentation for this package"

**GitHub Copilot**:
- `@workspace update .github/instructions based on recent package changes`
- `@workspace refresh the package instructions`
- `@workspace update AI documentation`

## Prerequisites

- Working directory is an R package root (contains DESCRIPTION file)
- Existing instructions exist at `.github/instructions/`
- Instructions were previously generated or created

## Process

### 1. Run Package Analysis

Analyze the current package state.

**Action**: Run the `analyze-r-package` skill to produce a complete current package analysis.

This provides the current package structure and characteristics.

### 2. Read Existing Instructions

Read all existing instruction files in `.github/instructions/`:

For each `.md` file:
- Read the complete content
- Note the structure and sections
- Identify manually-added content (domain explanations, specific examples, warnings)
- Extract key documented information (version numbers, function lists, etc.)

### 3. Identify Changes

Compare current package state (from analysis) to documented state (from instruction files):

#### Package Metadata Changes

Check for differences in:
- **Version numbers**: Old version → New version
- **Package title or description**: Changes in DESCRIPTION
- **Dependencies**: New packages added to Imports/Depends
- **biocViews**: Modified classification keywords

#### Structural Changes

Check for:
- **New exported functions**: In NAMESPACE but not in instructions
- **Removed functions**: In instructions but not in NAMESPACE
- **Renamed functions**: Similar names, one removed + one added
- **New vignettes**: `.Rmd` files not documented
- **Removed vignettes**: Documented but files don't exist
- **Data access pattern changes**: New remote sources, changed technologies
- **New S4 classes**: `setClass` definitions not documented
- **Directory structure changes**: New directories or moved files

#### Documentation Changes

Check for:
- **New test files**: `test-*.R` files not mentioned
- **README updates**: Significant content changes
- **Example changes**: Different usage patterns in README or vignettes

### 4. Determine Update Scope

Based on identified changes, determine which files need updates:

#### 00-overview.md

**Update if**:
- Package version changed
- New key functions exported
- Package description changed significantly
- Major features added or removed
- Data sources changed

#### 10-data-access.md

**Update if**:
- New data access functions added
- Data sources changed (new URLs, ExperimentHub IDs, etc.)
- Access patterns modified
- New data types available
- Large file handling strategies changed

#### 20-development.md

**Update if**:
- New S4 classes defined
- Coding patterns changed
- New dependencies affect development
- Function organization changed
- Validation patterns updated

#### 30-testing-and-docs.md

**Update if**:
- New test files added
- Testing patterns changed
- Example requirements changed (new `\donttest` usage)
- Documentation structure modified
- Test data location or format changed

#### 40-vignettes.md

**Update if**:
- New vignettes added
- Vignette purposes or titles changed
- Recommended reading order should change
- Key topics in vignettes modified

#### 50-git-workflow.md

**Usually static unless**:
- Package type changed (Data ↔ Analysis)
- New workflow requirements added
- Bioconductor submission requirements changed

#### INDEX.md

**Update if**:
- Any other file changed
- New functions to reference
- Section organization changed
- External resource links changed

### 5. Update Strategy

For each file that needs updates, use these strategies:

#### Preserve Customizations

**Identify custom content**:
- Domain-specific terminology and explanations
- Detailed examples with actual package data
- Warning boxes or important notes
- Links to domain-specific resources
- Author comments or clarifications
- Biological or statistical context

**Preservation approach**:
- Extract custom sections before updating
- Apply updates only to auto-generated portions (version numbers, function lists, file counts)
- Re-insert custom sections in appropriate places
- Flag any conflicts for manual review

#### Update Systematically

**For version numbers**:
- Direct find-and-replace throughout all files
- Search for "Version", "version", and version number patterns

**For function lists**:
- Add new functions to appropriate category with placeholder description: "[Description needed]"
- Remove functions that no longer exist
- Preserve any customized descriptions for existing functions
- Maintain the categorical organization and ordering

**For new sections**:
- Add at the end of the appropriate category
- Use clear markers if helpful: `<!-- Added [date] -->`
- Preserve existing section ordering

**For structural changes**:
- Edit specific sections, not wholesale replacement
- Maintain existing headers and organization
- Add new subsections where appropriate

#### Mark Changes

When adding new content, consider marking it:
```markdown
<!-- Auto-updated [date]: Added new function -->
```

This helps users identify what was automatically changed vs. manually customized.

### 6. Apply Updates

For each file to update:

**Use targeted edits**:
- Make specific, surgical changes to update outdated information
- Preserve surrounding content and formatting
- Keep manual customizations intact
- Only replace what needs to change

**Example edit patterns**:

Updating a version number:
- Find: `Version**: 0.99.0`
- Replace: `Version**: 1.0.0`

Adding a new function to a list:
- Find the end of the appropriate category section
- Insert: `- \`newFunction()\` - [Description needed]`

Removing a deleted function:
- Find the line: `- \`oldFunction()\` - ...`
- Delete that line

Adding a new vignette:
- Find the vignette list section
- Append new entry with number, filename, title, and purpose

#### Check Cross-References

After updates:
- Verify internal links still work
- Update any cross-references to renamed functions
- Check that examples still reference existing functions

### 7. Provide Update Summary

After updating files, provide a detailed summary:

```markdown
## Updated Package Instructions

### Changes Detected

**Version**: 0.99.0 → 1.0.0

**Functions**:
- Added (3): `newFunction1()`, `newFunction2()`, `newFunction3()`
- Removed (1): `oldFunction()`
- Renamed: `getData()` → `retrieveData()`

**Documentation**:
- New vignette: advanced-usage.Rmd

**Data Access**:
- New data source: HuggingFace waldronlab/new-dataset

### Files Updated

#### 00-overview.md
Changes made:
- Updated version number to 1.0.0
- Added 3 new functions to exports list
- Removed deprecated function `oldFunction()`
- Updated function count (18 → 20 total)

#### 10-data-access.md
Changes made:
- Added new HuggingFace data source
- Updated data source list with new URLs

#### INDEX.md
Changes made:
- Updated function quick reference with new functions
- Added link to new vignette
- Updated function count

### Files Not Updated

- 30-testing-and-docs.md - No changes to testing structure
- 50-git-workflow.md - No workflow changes

### Manual Review Recommended

The following changes may need your attention:
- New function `complexFunction()` has unique patterns - consider adding detailed usage examples
- Vignette reading order changed - verify the sequence makes sense for new users

### Preserved Customizations

The following manually-added content was preserved:
- Custom domain explanations in 00-overview.md
- Detailed biological context in 10-data-access.md
- Warning about memory usage in 20-development.md

### Next Steps

1. Review the updated files for accuracy
2. Verify cross-references still work
3. Add descriptions for new functions marked "[Description needed]"
4. Test that examples in documentation still work
5. Commit changes: `git add .github/instructions/`
```

## Smart Update Strategies

### Handling Version Changes

**Patch version (0.99.0 → 0.99.1)**:
- Update version number only
- Check for "Version X.X.X" references throughout files

**Minor version (0.99.0 → 1.0.0)**:
- Update version number
- Check if "What's new" section should be added
- Look for "new in version X" markers that need updating

**Major version (1.0.0 → 2.0.0)**:
- Update version number
- Flag as significant change requiring careful review
- Recommend reviewing all instruction files for breaking changes
- Warn user about potential API changes

### Handling Function Changes

**When functions are added**:
- Append to existing list in appropriate category
- Use placeholder description: "[Description needed]"
- Preserve any existing custom descriptions
- Maintain alphabetical order if that's the pattern

**When functions are removed**:
- Remove from function lists
- Search all files for references to the removed function
- Warn user if function is referenced elsewhere
- Check examples that might use the removed function

**When functions are renamed**:
- Detect patterns: old name in existing docs but not in NAMESPACE, new similar name in NAMESPACE
- Replace throughout all instruction files
- Preserve associated documentation
- Update cross-references

### Preserving Custom Content

**Identifying customizations**:
- Detailed domain-specific explanations (biology, statistics)
- Specific examples using actual package data
- Warning boxes or caution notes
- Links to publications or external resources
- Author annotations or clarifications
- Biological/medical context

**Preservation tactics**:
1. Before updating a section, extract paragraphs that look custom (not lists, not version numbers)
2. Apply updates to structural content (lists, versions, counts)
3. Re-insert custom paragraphs in logical positions
4. Flag any conflicts where custom content contradicts new information

## Configuration Options

Users can specify scope:

**Update all files (default)**:
- `/update-package-instructions`
- `@workspace update .github/instructions`

**Update specific files**:
- "Update just the overview and data access instructions"
- "Refresh 00-overview.md and 10-data-access.md"

**Show changes without applying (dry run)**:
- "What would change if we updated the instructions?"
- Review changes, then apply if approved

**Force update (overwrite customizations)**:
- "Force refresh all instructions"
- Always warn before forcing

## Platform-Specific Notes

### Claude Code
- Use Read tool to read existing instruction files
- Use Edit tool to make targeted updates (preferred)
- Use Write tool only for complete rewrites (ask user first)
- Run `/analyze-r-package` for current state

### GitHub Copilot
- Read files using VS Code editor
- Make edits through file operations
- Run analysis following analyze-r-package instructions

## Error Handling

### No Existing Instructions Found

If `.github/instructions/` doesn't exist or is empty:

```
Error: No existing instructions found in .github/instructions/

These instructions can only update existing files. To create instructions from scratch, use:
- Claude: /create-package-instructions
- Copilot: @workspace create .github/instructions for this R package
```

### No Changes Detected

If package state matches documented state:

```
✓ Instructions are up-to-date

No changes detected between current package state and documented state.

If you'd like to force refresh specific sections, let me know which files to update.
```

### Conflicting Changes

If custom content conflicts with new information:

```
⚠️  Conflict Detected in 10-data-access.md

The instructions document data source X at URL A, but current package uses URL B.

Options:
1. Keep existing (URL A) - assumes custom override
2. Use new (URL B) - assumes code is source of truth
3. Manual merge - I'll show you both for review

Which would you prefer?
```

### File Format Incompatible

If instruction files don't match expected format:

```
⚠️  Unexpected Format in 00-overview.md

This file doesn't match the expected instruction structure. It may have been manually created or heavily customized.

Options:
1. Skip this file (recommended - preserve customizations)
2. Attempt update anyway (may break formatting)
3. Regenerate from scratch (loses customizations)

What would you like to do?
```

## Best Practices

### DO
✅ Run package analysis first to understand current state
✅ Read all existing files before making changes
✅ Preserve manually added domain knowledge
✅ Use targeted edits rather than wholesale replacement
✅ Update cross-references between files
✅ Verify examples still work after updates
✅ Provide detailed change summary
✅ Flag content that needs manual review

### DON'T
❌ Blindly overwrite all content
❌ Remove custom examples without checking
❌ Update without running fresh analysis
❌ Ignore user customizations
❌ Skip verification of cross-references
❌ Make assumptions about ambiguous changes
❌ Update files that weren't modified

## Integration

**This skill uses**:
- `analyze-r-package` - To get current package state

**This skill is used by**:
- Users manually when package changes
- Potentially automated via git hooks (future)

**Works with**:
- `create-package-instructions` - For initial creation
- Individual file generator skills - For targeted updates

## Examples

### Example 1: Version Bump Only

```
User: /update-package-instructions

Agent: Analyzing package changes...

## Changes Detected
- Package version: 1.0.0 → 1.0.1
- No structural changes

## Files Updated
- 00-overview.md: Updated version number

All other files are up-to-date.
```

### Example 2: New Functions Added

```
User: /update-package-instructions

Agent: Analyzing package changes...

## Changes Detected
- 2 new exported functions:
  - `getData()` - data access
  - `validateInput()` - utility

## Files Updated

00-overview.md:
+ Added `getData()` to data access functions
+ Added `validateInput()` to utility functions

20-development.md:
+ Added documentation for input validation pattern

INDEX.md:
+ Updated function quick reference

Manual review recommended for `getData()` -
consider adding usage examples showing filtering patterns.
```

### Example 3: Breaking Change

```
User: /update-package-instructions

Agent: Analyzing package changes...

## ⚠️ Significant Changes Detected
- Major version: 1.5.0 → 2.0.0
- 1 function removed: `oldAccessMethod()`
- 1 function added: `newAccessMethod()`
- README indicates API redesign

This looks like a breaking change. I recommend:
1. Review all instruction files for mentions of removed functions
2. Consider adding migration guide
3. Update examples to use new API

Proceed with update? [y/N]
```

## Notes

- Always preserve user customizations unless explicitly asked to overwrite
- Use targeted edits preferentially over wholesale replacement
- Check cross-references between files after updates
- Version changes alone may not require full regeneration
- When in doubt, ask the user before making destructive changes
- Provide clear diffs or summaries so users can review changes
