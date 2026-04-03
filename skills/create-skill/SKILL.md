---
name: create-skill
description: Help create a new AI agent skill through collaborative Q&A
version: 1.0.0
category: meta
tags: [meta, infrastructure, skill-creation]
author: waldronlab
---

# create-skill

Help users create new AI agent skills through collaborative brainstorming and Q&A. This skill guides users from rough ideas to structured skill files, focusing on clarifying intent rather than enforcing perfect formatting.

## Philosophy

**Collaborative, not prescriptive**: This skill helps users develop and refine ideas through conversation. Accept rough examples, incomplete thoughts, and evolving concepts. The goal is to capture the user's intent and help them articulate it clearly - not to enforce rigid standards.

**Iteration-friendly**: Generate working drafts that can be refined over time. A skill doesn't need to be perfect on first creation.

## Usage

Invoke this skill when you want to create a new skill. Describe what you need:
- "Help me create a new skill for [domain/purpose]"
- "I want to make a skill that does [rough description]"
- "Create a skill for [workflow description]"

The skill guides you through the creation process interactively.

## Prerequisites

- You have a general idea of what you want the skill to do
- Working directory is the ai-agent-skills repository (or you can specify where to save)
- Existing domain directories (skills/*, or you're creating a new domain)

## Process

### 1. Understand the Intent

Start with open-ended questions to understand what you want:

**Core Questions**:
- "What problem are you trying to solve?"
- "Who would use this skill?" (developers, data analysts, etc.)
- "Can you give me an example of when you'd use this?"
- "What would be the typical input/output?"

**Listen for**:
- Domain context (R packages, metagenomics, repository maintenance)
- User type (package developers, data analysts, contributors)
- Workflow integration (when in their process would they invoke this?)
- Dependencies on other tools or files

**Accept rough descriptions**:
- "I want something that helps with X"
- "Like skill Y but for Z instead"
- "Automate this annoying manual process"
- "I want to create a skill for X data analysis"

### 2. Determine Domain and Location

**Existing domains**:
- `meta` - Repository infrastructure and skill system itself
- `r-packages` - R/Bioconductor package development and analysis
- `metagenomics` - Metagenomics workflows and data processing
- `statistical-methods` - Statistical analysis and methods

**If uncertain**:
- Suggest the most relevant domain
- If truly novel, discuss creating a new domain
- Explain that domain grouping helps discoverability and organization

**Determine filename**:
- Convert purpose to kebab-case: "analyze R package" → `analyze-r-package`
- Keep it descriptive but concise
- Check if similar skills exist to avoid duplication

### 3. Outline the Process

**Ask**: "Walk me through the steps - what should happen when someone uses this skill?"

**Capture**:
- Major steps in order
- Key decisions or branching points
- Required inputs at each stage
- Expected outputs

**Accept**:
- High-level descriptions: "first it reads some files, then analyzes them"
- References to existing patterns: "like how analyze-r-package does it"
- Uncertain details: "probably need to check X, not sure exactly how"
- Platform-agnostic language: "read the config" not "use the Read tool"

**Help clarify**:
- Break down complex steps
- Identify implicit dependencies
- Suggest standard approaches for common tasks

### 4. Generate the Skill File

Create a well-structured skill file with:

**YAML Frontmatter** (minimal, agent-agnostic):
```yaml
---
name: [kebab-case-name]
description: [one-line purpose from your description]
version: 1.0.0
category: [domain]
tags: [tag1, tag2]
author: waldronlab
---
```

**Main Content Sections**:

1. **Title and Overview** (1-2 paragraphs)
   - What the skill does
   - Why it's useful
   - Who should use it

2. **Usage**
   - How to invoke the skill (natural language examples)
   - Platform adapters may provide optional shortcuts

3. **Prerequisites** (if any)
   - Required files or setup
   - Directory location requirements
   - Dependencies

4. **Process**
   - Numbered major steps from the outline
   - Platform-agnostic descriptions
   - Clear actions and expected results
   - Decision points and branching logic

5. **Output Format** (if applicable)
   - What the skill produces
   - Examples of expected output

6. **Examples** (optional for initial draft)
   - Concrete usage scenarios
   - Can be refined iteratively

7. **Notes** (optional)
   - Additional context
   - Caveats or limitations
   - Future enhancements

**Template Approach**:
- Fill in what's clear from the conversation
- Use TODO markers or placeholder text for uncertain sections
- Prioritize clarity over completeness
- Skills are meant to be iterated on

### 5. Review and Refine

After generating the draft:

**Present summary**:
- "I've created `skills/[name]/SKILL.md`"
- "Here's what it does: [brief summary]"
- "Key sections: [list]"

**Invite feedback**:
- "What would you like to adjust?"
- "Are there sections that need more detail?"
- "Did I capture your intent correctly?"

**Offer next steps**:
- "You can refine this iteratively as you test it"
- "Want to add examples or error handling?"
- "Ready to commit and test this skill?"

## Output Format

Generate a markdown file with YAML frontmatter and markdown sections:

```markdown
---
name: skill-name
description: Brief purpose
version: 1.0.0
category: domain
tags: [tag1, tag2]
author: waldronlab
---

# skill-name

Overview paragraph(s).

## Usage
...

## Prerequisites
...

## Process

### 1. First Step
...

### 2. Second Step
...

## Output Format
...

## Examples
...

## Notes
...
```

**Save to**: `skills/[skill-name]/SKILL.md`

## Key Principles

- **Skills are agent-agnostic**: No platform-specific metadata in the file
- **Natural language is canonical**: Agents match user intent to the description field
- **Platform shortcuts are optional**: Platform adapters may provide conveniences (slash commands, @workspace patterns) but aren't required
- **Describe what, not how**: Use "read the file" not "use Read tool"
- **Iterate, don't perfect**: First draft can be incomplete

## Platform-Specific Notes

Skills themselves contain no platform-specific code. Platform adapters (instructions/claude.md, instructions/copilot.md) document optional shortcuts and how to invoke skills on each platform, but the skill file remains universal.

## Guidance for AI Agents

### Being a Good Collaborator

**DO**:
- Ask clarifying questions
- Suggest similar existing skills as reference
- Help break down complex workflows into steps
- Offer options when uncertain
- Accept incomplete or rough ideas
- Use conversational language
- Iterate based on feedback

**DON'T**:
- Demand perfect specifications upfront
- Reject ideas for being too vague
- Enforce strict formatting during brainstorming
- Overwhelm with too many questions at once
- Create the file without understanding intent

### Handling Uncertainty

**If unclear about**:
- **Domain**: Suggest the closest match, explain it can be moved later
- **Steps**: Help walk through a concrete example
- **Output format**: Suggest "produces markdown summary" or similar
- **Completeness**: Use placeholders (`<!-- TODO: ... -->`) and iterate

### Starting from Examples

If user says "like skill X but for Y":

1. Read the referenced skill
2. Identify the core pattern
3. Ask what should be different
4. Adapt structure and logic
5. Generate the variant

## Integration with Other Skills

**Complements**:
- SKILL_STANDARD.md - Reference for format details
- AGENTS.md - Understanding agent behavior and discovery
- check-waldronlab-skills - For discovering existing skills before creating duplicates

**Not a replacement for**:
- Manual refinement and testing
- Domain expertise in skill logic
- Reading SKILLS.md to understand what already exists

## Examples

### Example 1: Creating from Scratch

**User**: "I want to make a skill that helps validate R package documentation"

**Agent**: Engages in Q&A to understand:
- What documentation aspects to validate (roxygen, vignettes, examples)
- When to use it (before committing, code review)
- Whether to check or suggest fixes

Result: `skills/validate-r-documentation/SKILL.md`

### Example 2: Starting from Rough Idea

**User**: "Something that automates the boring parts of creating Bioconductor packages"

**Agent**: Clarifies:
- Which specific parts (directory structure, DESCRIPTION, boilerplate)
- Full new package vs specific tasks
- Interactive or config-driven

Result: `skills/scaffold-bioconductor-package/SKILL.md` (simplified version)

### Example 3: Converting Existing Workflow

**User**: "I always do these 5 steps manually: [list]. Can we make a skill?"

**Agent**: Helps structure the workflow and generate:

Result: `skills/[domain]/[workflow-name]/SKILL.md` capturing your process

## Notes

- **Iteration is expected**: First draft doesn't need to be perfect
- **User testing is essential**: Try the skill and refine based on feedback
- **Standards are guidelines**: Focus on clarity and usefulness
- **Metadata tags help discovery**: Use relevant tags (r-packages, bioconductor, data-access, etc.)
- **Domain knowledge helps**: Familiarity with existing skills improves suggestions

The goal is to **lower the barrier** to creating skills, not raise it. Make it easy to capture and share workflows.

---

**Related**: See [SKILL_STANDARD.md](../../SKILL_STANDARD.md) for technical format details. See [AGENTS.md](../../AGENTS.md) for how agent discovery and invocation work.
