---
name: update-package-instructions
description: Update existing AI instruction documentation when an R/Bioconductor package changes
version: 1.0.0
---

# update-package-instructions

Update existing `.github/instructions/` files to reflect changes in an R/Bioconductor package. This skill intelligently detects what has changed and updates only the relevant sections while preserving manual customizations.

## Usage

User invokes with:
- `/update-package-instructions`
- "Update the package instructions"
- "Refresh AI documentation for this package"

## Prerequisites

This skill assumes:
- Working directory is an R package root (contains DESCRIPTION file)
- Existing instructions exist at `.github/instructions/`
- Instructions were previously generated or created

## Process

### 1. Run Package Analysis

Analyze the current package state:

```
Skills to use:
- /analyze-r-package
```

This provides current package structure and characteristics.

### 2. Read Existing Instructions

Read all existing instruction files:

```
Tools to use:
- Glob: .github/instructions/*.md
- Read: Each instruction file
```

Extract key information from each file to understand what's currently documented.

### 3. Identify Changes

Compare current package state to documented state:

**Package metadata changes**:
- Version bumps
- Title or description changes
- New dependencies added
- biocViews modifications

**Structural changes**:
- New exported functions added
- Functions removed or renamed
- New vignettes added
- Data access patterns changed
- New S4 classes defined
- Directory structure changes

**Documentation changes**:
- New test files added
- README content updated
- New examples in vignettes

### 4. Determine Update Scope

Based on identified changes, determine which files need updates:

**00-overview.md** - Update if:
- Package version changed
- New key functions exported
- Package description changed
- Major features added or removed

**10-data-access.md** - Update if:
- New data access functions
- Data sources changed
- Access patterns modified
- New data types added

**20-development.md** - Update if:
- New S4 classes defined
- Coding patterns changed
- New dependencies affect development
- Function organization changed

**30-testing-and-docs.md** - Update if:
- New test files added
- Testing patterns changed
- Example requirements changed
- Documentation structure modified

**40-vignettes.md** - Update if:
- New vignettes added
- Vignette purposes changed
- Vignette order should be updated
- Key topics modified

**50-git-workflow.md** - Usually static unless:
- Package type changed (data ↔ analysis)
- New workflow requirements added
- Bioconductor submission requirements changed

**INDEX.md** - Update if:
- Any other file changed
- New functions to reference
- Section organization changed

### 5. Update Strategy

For each file that needs updates:

**Preserve customizations**:
- Read existing content carefully
- Identify sections that look manually customized (domain context, specific examples, warnings)
- Preserve these sections when possible

**Update systematically**:
- Version numbers → Direct replacement
- Function lists → Add new, remove deleted, preserve descriptions if customized
- Section additions → Append new content with clear markers
- Structural changes → Edit specific sections, not wholesale replacement

**Mark automated vs. manual sections**:
When adding new content, consider using comments to indicate auto-generated portions:
```markdown
<!-- Auto-generated function list - customize as needed -->
```

### 6. Apply Updates

For each file to update:

```
Tools to use:
- Read: Read current file completely
- Edit: Make targeted edits to specific sections
```

**Prefer Edit over Write**:
- Use Edit tool for targeted changes
- Only use Write if completely restructuring a file
- Always ask user before wholesale replacement

### 7. Provide Update Summary

After updating files, provide detailed summary:

```markdown
## Updated Package Instructions

### Changes Detected
- Package version: 0.99.0 → 1.0.0
- New functions: 3 added (function1, function2, function3)
- Removed functions: 1 (oldFunction)
- New vignette: advanced-usage.Rmd

### Files Updated

#### 00-overview.md
- Updated version number
- Added 3 new functions to exports list
- Removed deprecated function

#### 20-development.md
- Added documentation for new S4 class: NewClass

#### 40-vignettes.md
- Added new vignette: advanced-usage.Rmd
- Updated recommended reading order

#### INDEX.md
- Updated function quick reference
- Added link to new vignette

### Files Not Updated
- 10-data-access.md - No data access changes
- 30-testing-and-docs.md - No testing changes
- 50-git-workflow.md - No workflow changes

### Manual Review Recommended
The following changes may need manual attention:
- New function `complexFunction()` has unique patterns - consider adding usage examples
- Vignette order changed - verify recommended sequence makes sense

### Next Steps
1. Review the updated files
2. Test that cross-references still work
3. Add package-specific examples where needed
4. Commit changes: `git add .github/instructions/`
```

## Smart Update Strategies

### Handling Function Lists

**When functions are added**:
- Append to existing list in appropriate category
- Use placeholder description: "TODO: Add description"
- Preserve any existing custom descriptions

**When functions are removed**:
- Remove from list
- Check for references in other files
- Warn user if function is referenced elsewhere

**When functions are renamed**:
- Detect patterns (old name → new name)
- Update throughout all files
- Preserve associated documentation

### Handling Version Changes

**Patch version (0.99.0 → 0.99.1)**:
- Update version number only
- Check if any "Version X.X.X" references exist

**Minor version (0.99.0 → 1.0.0)**:
- Update version number
- Check for "new in version X" markers
- May add "What's new" section if major features added

**Major version (1.0.0 → 2.0.0)**:
- Update version number
- Flag as significant change
- Recommend review of all files

### Preserving Customizations

**Identifying custom content**:
- Domain-specific terminology
- Detailed examples with package data
- Warning boxes or notes
- Links to external resources
- Author notes or comments

**Preservation strategy**:
- Extract custom sections before updating
- Apply updates to auto-generated portions
- Re-insert custom sections
- Flag any conflicts for manual review

## Configuration Options

Users can specify update scope:

**Update all files**:
```
/update-package-instructions
```

**Update specific files**:
```
/update-package-instructions --files="00-overview,20-development"
```

**Dry run (show what would change)**:
```
/update-package-instructions --dry-run
```

**Force update (overwrite customizations)**:
```
/update-package-instructions --force
```
*Note: Always warn before forcing*

## Error Handling

**No existing instructions found**:
- Suggest running `/create-package-instructions` instead
- Offer to create instructions

**No changes detected**:
- Inform user instructions are up-to-date
- Offer to force refresh if needed

**Conflicting changes**:
- Show conflicts to user
- Offer options: keep existing, use new, manual merge
- Save backup before applying changes

**File format incompatible**:
- Warn if instruction files don't match expected format
- Suggest manual review
- Offer to regenerate from scratch

## Best Practices

**DO**:
✅ Run after significant package changes
✅ Review diffs before committing
✅ Preserve manually added domain knowledge
✅ Update cross-references between files
✅ Check that examples still work

**DON'T**:
❌ Blindly overwrite all content
❌ Remove custom examples without checking
❌ Update without running analysis first
❌ Ignore user customizations
❌ Skip verification of cross-references

## Integration with Other Skills

**Called by this skill**:
- `analyze-r-package` - To get current package state

**Calls this skill**:
- Users manually when package changes
- Potentially automated via git hooks (future)

**Works with**:
- Individual file generator skills - For targeted updates
- `create-package-instructions` - For initial creation

## Examples

### Example 1: Version Bump Only

```
User: /update-package-instructions

Claude: Analyzing package changes...

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

Claude: Analyzing package changes...

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

Claude: Analyzing package changes...

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
- Use Edit tool preferentially over Write to maintain file structure
- Check cross-references between files after updates
- Version changes alone may not require full regeneration
- When in doubt, ask the user before making destructive changes
