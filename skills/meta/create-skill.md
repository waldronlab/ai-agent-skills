---
name: create-skill
description: Help create a new AI agent skill through collaborative Q&A
version: 1.0.0
platforms:
  - claude-code
  - github-copilot
triggers:
  claude:
    - /create-skill
    - "Help me create a new skill"
    - "Create a skill for [purpose]"
  copilot:
    - "@workspace create a new skill"
    - "@workspace help me create a skill for [purpose]"
    - "@workspace set up a new agent skill"
author: waldronlab
category: meta
---

# create-skill

Help users create new AI agent skills through collaborative brainstorming and Q&A. This skill guides users from rough ideas to structured skill files, focusing on clarifying intent rather than enforcing perfect formatting.

## Philosophy

**Collaborative, not prescriptive**: This skill helps users develop and refine ideas through conversation. Accept rough examples, incomplete thoughts, and evolving concepts. The goal is to capture the user's intent and help them articulate it clearly - not to enforce rigid standards.

**Iteration-friendly**: Generate working drafts that can be refined over time. A skill doesn't need to be perfect on first creation.

## Usage

**Claude Code**:
- `/create-skill`
- "Help me create a new skill for [domain/purpose]"
- "I want to make a skill that does [rough description]"

**GitHub Copilot**:
- `@workspace create a new skill`
- `@workspace help me create a skill for [purpose]`
- `@workspace I need a skill that [description]`

## Prerequisites

- User has a general idea of what they want the skill to do
- Working directory is the ai-agent-skills repository (or user can specify where to save)
- Existing domain directories (r-packages/, metagenomics/, meta/, etc.)

## Process

### 1. Understand the Intent

Start with open-ended questions to understand what the user wants:

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

**Ask**: "Which domain does this fit into?"

**Existing domains**:
- `r-packages/` - R/Bioconductor package development and analysis
- `metagenomics/` - Metagenomics workflows and data processing
- `statistical-methods/` - Statistical analysis and methods
- `meta/` - Repository infrastructure and skill system itself

**If uncertain**:
- Suggest the most relevant domain
- If truly novel, discuss creating a new domain directory
- Explain that domain grouping helps discoverability

**Determine filename**:
- Convert purpose to kebab-case: "analyze R package" → `analyze-r-package.md`
- Keep it descriptive but concise
- Check if similar skills exist to avoid duplication

### 3. Brainstorm Triggers

**Context**: All skills in this repository are cross-platform by design (Claude Code and GitHub Copilot). Focus on how users would naturally invoke this skill.

**Brainstorm triggers together**:

**For Claude Code**:
- Slash commands: `/skill-name`
- Natural language: "Analyze this package", "Help me with X"

**For GitHub Copilot**:
- `@workspace` patterns: "@workspace analyze this package"
- Action-oriented phrases: "@workspace set up [thing]"

**Trigger Tips**:
- Think about how users naturally describe the task
- Include common variations
- Consider both explicit commands and implicit requests
- Don't worry about perfect phrasing - these can be refined

### 4. Outline the Process

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
- Point out where platform differences might matter

### 5. Generate the Skill File

Create a well-structured skill file with:

**YAML Frontmatter**:
```yaml
---
name: [kebab-case-name]
description: [one-line purpose from user's description]
version: 1.0.0
platforms:
  - claude-code
  - github-copilot
triggers:
  claude:
    - /[name]
    - "[natural language variant]"
  copilot:
    - "@workspace [natural language]"
author: waldronlab
category: [domain]
---
```

**Main Content Sections**:

1. **Title and Overview** (1-2 paragraphs)
   - What the skill does
   - Why it's useful
   - Who should use it

2. **Usage**
   - How to invoke on each platform
   - Include examples from triggers

3. **Prerequisites** (if any)
   - Required files or setup
   - Directory location requirements
   - Dependencies

4. **Process**
   - Numbered major steps from the outline
   - Platform-agnostic descriptions
   - Clear actions and expected results
   - Decision points and branching logic

5. **Platform-Specific Notes** (if needed)
   - Claude Code tool usage
   - GitHub Copilot approaches
   - Only include if there are meaningful differences

6. **Output Format** (if applicable)
   - What the skill produces
   - Examples of expected output

7. **Error Handling** (optional for initial draft)
   - Common issues
   - How to handle them
   - Can be added later

8. **Examples** (optional for initial draft)
   - Concrete usage scenarios
   - Can be refined iteratively

9. **Notes** (optional)
   - Additional context
   - Caveats or limitations
   - Future enhancements

**Template Approach**:
- Fill in what's clear from the conversation
- Use TODO markers or placeholder text for uncertain sections
- Add comments suggesting where user might want to expand
- Prioritize clarity over completeness

### 6. Review and Refine

After generating the draft:

**Present summary**:
- "I've created [filename] in [domain]/"
- "Here's what it does: [brief summary]"
- "Key sections: [list]"

**Invite feedback**:
- "What would you like to adjust?"
- "Are there sections that need more detail?"
- "Did I capture your intent correctly?"

**Offer next steps**:
- "You can refine this iteratively as you test it"
- "Want to add examples or error handling?"
- "Should we create a companion validation skill?"

## Output Format

Generate a markdown file following the standard structure:

```markdown
---
name: skill-name
description: Brief purpose
version: 1.0.0
platforms:
  - claude-code
  - github-copilot
triggers:
  claude: [...]
  copilot: [...]
author: waldronlab
category: domain
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

## Platform-Specific Notes
...

## Output Format
...

## Examples
...

## Notes
...
```

**Save to**: `[domain]/[skill-name].md`

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
- Insist on complete documentation before saving

### Handling Uncertainty

**If user is unsure about**:
- **Domain**: Suggest the closest match, explain it can be moved later
- **Triggers**: Propose 2-3 options based on similar skills
- **Steps**: Help them walk through a concrete example
- **Platform differences**: Start platform-agnostic, note differences as TODO
- **Output format**: Suggest "produces markdown summary" or similar generic

**Use placeholders freely**:
- `<!-- TODO: Add example -->`
- `[Details to be refined]`
- `<!-- User might want to add: X, Y, Z -->`

### Starting from Examples

If user says "like skill X but for Y":

1. Read the referenced skill
2. Identify the core pattern
3. Ask what should be different
4. Adapt structure and logic
5. Generate the variant

## Platform-Specific Notes

### Claude Code
- Can invoke with `/create-skill` directly
- Use Write tool to create the skill file
- Can read existing skills with Read tool for reference
- Output conversation is saved in context

### GitHub Copilot
- Trigger via `@workspace create a new skill`
- Create file using VS Code file operations
- Can reference existing skills in workspace
- Display generated content in chat

## Examples

### Example 1: Creating from Scratch

**User**: "I want to make a skill that helps validate R package documentation"

**Agent**: "Great idea! Let me understand what you need:
- What aspects of documentation should it validate? (roxygen, vignettes, examples?)
- When would someone use this? (before committing, during code review?)
- Should it just check or also suggest fixes?"

[Conversation continues, clarifying requirements]

**Agent**: "I've created `r-packages/validate-documentation.md` that checks roxygen completeness, example runnability, and vignette builds. Want to review it?"

### Example 2: Starting from Rough Idea

**User**: "Something that automates the boring parts of creating Bioconductor packages"

**Agent**: "I can help! That's pretty broad though. Let's narrow it down:
- Which boring parts? (directory structure, DESCRIPTION, documentation boilerplate?)
- Full new package creation or specific tasks?
- Should it be interactive or run from config?"

[Clarifies: wants to scaffold package structure from templates]

**Agent**: "Got it. I'll create `r-packages/scaffold-package.md` that sets up the standard Bioconductor structure. We can start simple and add more automation later."

### Example 3: Converting Existing Workflow

**User**: "I always do these steps manually: [lists 5-step process]. Can we make a skill?"

**Agent**: "Absolutely! Those steps map to a clear workflow. Let's turn it into a skill:
- What should we call it?
- Any variations on this process or always the same?
- What triggers would make sense?"

[Generates skill capturing the workflow]

**Agent**: "Here's `domain/skill-name.md` based on your process. Try it out and let me know what needs tweaking!"

## Integration with Other Skills

**Complements**:
- SKILL_STANDARD.md - Reference for format details
- (future) `meta/validate-skill.md` - For checking compliance after creation
- (future) `meta/migrate-skill.md` - For converting platform-specific skills

**Not a replacement for**:
- Manual refinement and testing
- Domain expertise in skill logic
- Platform-specific optimization

## Notes

- **Iteration is expected**: First draft doesn't need to be perfect
- **User testing is essential**: Encourage trying the skill and refining
- **Standards are guidelines**: Focus on clarity and usefulness over format compliance
- **Platform differences emerge**: Start platform-agnostic, add specific notes as needed
- **Domain knowledge helps**: Familiarity with r-packages/, metagenomics/, etc. improves suggestions

The goal is to **lower the barrier** to creating skills, not raise it. Make it easy for users to capture and share their workflows.

---

**Related**: See [SKILL_STANDARD.md](../SKILL_STANDARD.md) for format details (reference, not enforcement).
