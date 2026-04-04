---
name: check-waldronlab-skills
description: Verify that waldronlab/ai-agent-skills are available and help users find the right skill
version: 1.0.0
category: meta
tags: [meta, infrastructure, discovery]
author: waldronlab
---

# check-waldronlab-skills

Help any user confirm that waldronlab skills are installed and visible, then provide a concise catalog of available skills with short descriptions.

This skill is intended as a quick health check and discovery entry point for the `waldronlab/ai-agent-skills` repository.

## Usage

Invoke this skill to check your setup or discover available skills:
- "Do I have the waldronlab skills?"
- "What waldronlab skills are there?"
- "Is there a good waldronlab skill for [task]?"
- "List available waldronlab skills"

## Prerequisites

- The `waldronlab/ai-agent-skills` repository is present locally
- Skill files are accessible through your configured skill locations or project-level instruction links

## Process

### 1. Discover Available Waldronlab Skills

Read SKILLS.md from the repository to discover all available skills dynamically.

**Process**:
- Locate and read `SKILLS.md` in the repository root
- Parse the skill entries by category (Meta Skills, R/Bioconductor Package Skills, etc.)
- Extract for each skill:
  - Skill name
  - Category/domain
  - Purpose (from the skill description)
  - Location path

If SKILLS.md is not accessible or no skills are found, return a clear not-found status and suggest checking skill path configuration.

### 2. Summarize Skills

For each discovered skill, provide:
- Skill name
- Domain/category
- One-sentence purpose summary
- Typical use case or when to use it

Prefer concise summaries derived from each skill's frontmatter `description` and overview section.

### 3. Answer User Questions About Skill Fit

When the user asks task-oriented questions like "Is there a good waldronlab skill for [task]?":
- Ask for brief context if the task is unclear
- Recommend 1-2 best-fit skills with a one-line rationale each
- If no skill is a clear match, say so and suggest `create-skill` to draft a new one
- Reference SKILLS.md for detailed information

### 4. Report Installation Health

Conclude with a simple status statement:
- "🏃 Levi says let's go!" when skills are found
- "❌ Not detected" when no skills are found

Include a short remediation hint when not detected.

## Output Format

Return one of the following:

### 1. Skill Inventory

```
Status: 🏃 Levi says let's go!

**[Category Name]**
- [skill-name]: [Brief description from SKILLS.md]
- [skill-name]: [Brief description from SKILLS.md]

**[Category Name]**
- [skill-name]: [Brief description from SKILLS.md]
- [skill-name]: [Brief description from SKILLS.md]

[Additional categories as found in SKILLS.md]
```

**Note**: Skill list is generated dynamically from SKILLS.md, not hard-coded.

### 2. Question Answer

```
For [task description], I recommend:

**Primary**: [skill-name]
[Rationale]

**Companion**: [skill-name] (optional)
[Use case]
```

### 3. Discovery Help

For broader discovery, reference SKILLS.md:
"See SKILLS.md in the repository for the complete index organized by category and use case."

## Examples

### Example 1: Installation Check

**User**: "Do I have the waldronlab skills?"

**Process**:
1. Read SKILLS.md from repository root
2. Parse skill entries by category
3. Extract names and descriptions
4. Format and present

**Response** (dynamically generated from SKILLS.md):
```
🏃 Levi says let's go!

Available waldronlab skills:

Meta
  • [skills from Meta Skills section in SKILLS.md]

R/Bioconductor
  • [skills from R/Bioconductor Package Skills section in SKILLS.md]

[Additional categories as defined in SKILLS.md]

For detailed information, see SKILLS.md in the repository.
```

### Example 2: Discovery

**User**: "What waldronlab skills are there?"

**Response** (same as Example 1 - concise catalog)

### Example 3: Fit Recommendation

**User**: "Is there a good waldronlab skill for creating package instructions?"

**Process**:
1. Read SKILLS.md to find relevant skills
2. Match user need to skill descriptions
3. Identify primary and companion skills

**Response** (based on current SKILLS.md content):
```
Yes! I recommend:

**Primary**: [skill-name from SKILLS.md that best matches]
[Description and rationale from SKILLS.md]

**Companion**: [related skill-name from SKILLS.md]
[How it complements the primary skill]
```

### Example 4: No Skill Match

**User**: "Do you have a skill for testing Shiny apps?"

**Process**:
1. Read SKILLS.md to search for matching skills
2. If no match found, identify available domains
3. Suggest create-skill or filing an issue

**Response** (domains listed are from current SKILLS.md):
```
Not currently. Based on SKILLS.md, the waldronlab skills focus on:
  • [List current categories from SKILLS.md]

For creating a new skill, try describing your need in natural language
(e.g., "Help me create a new skill for testing Shiny apps")

Or open an issue at:
https://github.com/waldronlab/ai-agent-skills/issues
```

## Platform-Specific Notes

### Claude Code

- Supports direct slash invocation: `/check-waldronlab-skills`
- Good as a first diagnostic command in a new session
- Results are saved in conversation context

### GitHub Copilot

- Works best with `@workspace` prompts like `@workspace What waldronlab skills are there?`
- If skills appear duplicated, explain that multiple configured locations may expose the same skill
- Results appear in chat window

## Troubleshooting

### Skills Not Detected

If no skills are found:

1. **Check configuration**: Verify skill paths in your editor settings
2. **Check repository**: Clone/pull waldronlab/ai-agent-skills repository
3. **Check permissions**: Ensure you can read files in the skills directory
4. **Reload**: Run "Developer: Reload Window" in VS Code

See the appropriate platform adapter:
- Claude Code: `instructions/claude.md`
- GitHub Copilot: `instructions/copilot.md`

### Duplicate Skills

If you see duplicate skill listings, it's likely because your configuration points to multiple locations that include the same skills. This is normal if using both global and per-workspace settings.

## Notes

- **Dynamic discovery**: This skill reads SKILLS.md at runtime to discover available skills, ensuring it never goes out of sync
- **Single source of truth**: SKILLS.md is the authoritative skill catalog; this skill queries it rather than duplicating content
- Keep responses concise and actionable
- Prioritize helping users confirm setup quickly
- If skills are missing, provide actionable next steps
- This skill complements SKILLS.md as the quick-check discovery tool

See [AGENTS.md](../../AGENTS.md) for how skill discovery works and [SKILLS.md](../../SKILLS.md) for the complete index.

---

**Related**: SKILLS.md (complete skill index), instructions/claude.md, instructions/copilot.md
