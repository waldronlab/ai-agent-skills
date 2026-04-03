# Next Steps for waldronlab AI Agent Skills

This repository has been initialized with the structure and foundation for creating AI agent skills. Here's what exists and what needs to be done next.

## ✅ What's Been Created

### Repository Structure
```
ai-agent-skills/
├── README.md                 # Main overview and installation guide
├── LICENSE                   # MIT License
├── CONTRIBUTING.md           # Contribution guidelines
├── CHANGELOG.md             # Version history
├── .gitignore               # Git ignore patterns
│
├── r-packages/              # R/Bioconductor package skills
│   ├── README.md            # Domain documentation
│   ├── claude/
│   │   ├── analyze-r-package.md           # Analysis skill
│   │   └── create-package-instructions.md # Orchestrator skill
│   ├── copilot/             # Empty, to be populated
│   ├── templates/           # Empty, to be populated
│   └── examples/
│       ├── README.md
│       └── data-package-parquet/   # parkinsonsMetagenomicData
│           ├── DESCRIPTION
│           ├── NAMESPACE
│           ├── README.md
│           └── .github/instructions/  # Complete example
│
├── metagenomics/            # Placeholder for future skills
│   └── README.md
│
└── statistical-methods/     # Placeholder for future skills
    └── README.md
```

### Documentation
- ✅ Comprehensive main README with installation instructions
- ✅ Domain-specific README for r-packages
- ✅ Contributing guidelines
- ✅ Example documentation
- ✅ Changelog structure

### Examples
- ✅ Complete parkinsonsMetagenomicData instruction set as reference

### Skills
- ✅ Two working skills (Claude Code format):
  - `analyze-r-package`: Pure package analysis
  - `create-package-instructions`: Orchestrator for creating complete instruction sets

## 📋 Immediate Next Steps

### 1. Create Remaining Claude Code Skills (Priority 1)

Based on the drafts in parkinsonsMetagenomicData/.github/instructions/, create:

**Location**: `r-packages/claude/`

- [ ] `create-overview-instructions.md`
- [ ] `create-data-access-instructions.md`
- [ ] `create-development-instructions.md`
- [ ] `create-testing-docs-instructions.md`
- [ ] `create-vignette-instructions.md`
- [ ] `create-git-workflow-instructions.md`
- [ ] `create-index.md`
- [✓] `create-package-instructions.md` (orchestrator)
- [ ] `update-package-instructions.md`

**Source**: Use parkinsonsMetagenomicData/.github/instructions/SKILL_IMPLEMENTATIONS.md as template

**Time estimate**: 4-6 hours

### 2. Create Template Files (Priority 1)

**Location**: `r-packages/templates/`

Create `.template.md` files for each instruction type:
- [ ] `00-overview.template.md`
- [ ] `10-data-access.template.md`
- [ ] `20-development.template.md`
- [ ] `30-testing-and-docs.template.md`
- [ ] `40-vignettes.template.md`
- [ ] `50-git-workflow.md`
- [ ] `INDEX.template.md`

Include `{{PLACEHOLDER}}` variables for dynamic content.

**Source**: Use parkinsonsMetagenomicData example as base

**Time estimate**: 2-3 hours

### 3. Create Copilot Instructions (Priority 2)

**Location**: `r-packages/copilot/instructions.md`

Create comprehensive instructions for GitHub Copilot that parallels the Claude skills.

**Source**: Use parkinsonsMetagenomicData/.github/instructions/SKILL_IMPLEMENTATIONS.md Copilot section

**Time estimate**: 2-3 hours

### 4. Test on Additional Packages (Priority 1)

Before public release, test skills on:

- [ ] **Another data package** (e.g., curatedMetagenomicData)
- [ ] **An analysis package** (e.g., MicrobiomeProfiler)
- [ ] **An infrastructure package** (if available)

Document any issues found and refine skills.

**Time estimate**: 1-2 days

### 5. Create Additional Examples (Priority 2)

Add 2-3 more examples to `r-packages/examples/`:

- [ ] `data-package-experimenthub/` - Different data access pattern
- [ ] `analysis-package/` - Statistical methods package
- [ ] `infrastructure-package/` - S4 classes package

**Time estimate**: 3-4 hours

### 6. Set Up Repository on GitHub (Priority 1)

- [ ] Create repository at github.com/waldronlab/ai-agent-skills
- [ ] Push initial commit
- [ ] Set up branch protection on main
- [ ] Enable Issues and Discussions
- [ ] Add repository topics: ai, skills, r, bioconductor, claude, copilot
- [ ] Add repository description
- [ ] Create initial GitHub Issues for TODOs

**Time estimate**: 1 hour

### 7. Create CI/CD Validation (Priority 3)

**Location**: `.github/workflows/`

Create workflows to:
- [ ] Validate markdown formatting
- [ ] Check YAML frontmatter in skills
- [ ] Verify cross-references in examples
- [ ] Run markdown link checker

**Time estimate**: 2-3 hours

## 🎯 Phase 1 Goals (2-3 Weeks)

**Objective**: Complete and validate r-packages skills

- [ ] All Claude Code skills implemented
- [ ] Copilot instructions complete
- [ ] All templates created
- [ ] Tested on 3+ packages of different types
- [ ] 3 complete examples
- [ ] Repository live on GitHub
- [ ] CI/CD validation in place

**Success Criteria**:
- Skills generate quality instructions in <10 minutes
- Instructions pass manual review with minimal edits
- Works for data, analysis, and infrastructure packages

## 📅 Phase 2 Goals (1-2 Months)

**Objective**: Organization adoption and refinement

- [ ] Present to waldronlab team
- [ ] Create training materials (video, cheat sheet)
- [ ] Generate instructions for 5-10 priority packages
- [ ] Collect feedback and iterate
- [ ] Document common customization patterns
- [ ] Add more examples from diverse packages

**Success Criteria**:
- 50%+ of active waldronlab packages have instructions
- Positive feedback from users
- Skills refined based on real-world usage

## 🚀 Phase 3 Goals (3-6 Months)

**Objective**: Expand to other domains

- [ ] Develop metagenomics analysis skills
- [ ] Develop statistical-methods skills
- [ ] Create examples for each domain
- [ ] Expand beyond waldronlab (if desired)

**Success Criteria**:
- Multiple skill domains active
- Community contributions
- Skills used beyond original team

## 💡 Quick Wins to Start

### Option 1: Validate Concept (Fastest)
1. Use analyze-r-package skill on another waldronlab package
2. Manually generate instructions following the example
3. Get feedback from package maintainer
4. Refine approach based on feedback

**Time**: 2-3 hours
**Risk**: Low
**Learning**: High

### Option 2: Complete One Skill (Most Valuable)
1. Implement create-package-instructions orchestrator
2. Test on parkinsonsMetagenomicData (known good)
3. Test on one other package
4. Document any issues

**Time**: 4-6 hours
**Risk**: Medium
**Learning**: Very high

### Option 3: Expand Examples (Broadest Validation)
1. Add 2 more package examples
2. Document patterns unique to each type
3. Identify common vs. package-specific content
4. Use learnings to refine skill approach

**Time**: 3-4 hours
**Risk**: Low
**Learning**: High

## 🔧 Development Workflow

### For Each New Skill

1. **Design**: Write skill specification
2. **Implement**: Create skill file with clear instructions
3. **Test**: Try on 2-3 different packages
4. **Document**: Add usage examples
5. **Review**: Get feedback from others
6. **Iterate**: Refine based on testing
7. **Commit**: Add to repository

### Testing Checklist

For each skill:
- [ ] Works on data package
- [ ] Works on analysis package
- [ ] Works on infrastructure package
- [ ] Handles edge cases gracefully
- [ ] Produces consistent output
- [ ] Documentation is clear
- [ ] Examples are helpful

## 📞 Getting Help

### Resources
- **Source material**: parkinsonsMetagenomicData/.github/instructions/SKILLS_*.md files
- **Example output**: parkinsonsMetagenomicData/.github/instructions/ directory
- **Format examples**: analyze-r-package.md skill file

### Questions to Consider
1. Should skills be strict or flexible in their output?
2. How much customization is expected vs automated?
3. What's the right balance of detail in instructions?
4. Should skills validate their output?
5. How to handle edge cases and unusual packages?

## ✅ Ready to Start?

**Recommended First Task**: Create the `create-package-instructions` orchestrator skill

This will:
- Validate the overall approach
- Provide end-to-end testing
- Show how skills compose together
- Give concrete output to evaluate

**Steps**:
1. Copy parkinsonsMetagenomicData/.github/instructions/SKILL_IMPLEMENTATIONS.md
2. Extract the create-package-instructions section
3. Convert to proper Claude Code skill format (follow analyze-r-package.md structure)
4. Test on parkinsonsMetagenomicData
5. Compare output to existing instructions
6. Iterate until quality matches

**Estimated time**: 2-3 hours for first draft, plus testing

---

**Repository Location**: `~/git/ai-agent-skills`
**Current Status**: Foundation complete, skills to be implemented
**Next Milestone**: Complete r-packages skill suite
