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

Collect all discoverable skill files associated with `waldronlab/ai-agent-skills`.

At minimum, include these canonical skills:
- `create-skill` (meta domain)
- `validate-skill` (meta domain)
- `check-waldronlab-skills` (meta domain)
- `analyze-r-package` (r-packages domain)
- `create-package-instructions` (r-packages domain)
- `update-package-instructions` (r-packages domain)

If no waldronlab skills are found, return a clear not-found status and suggest checking skill path configuration.

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
- Reference SKILLS.md (`/skills/SKILLS.md`) for detailed information

### 4. Report Installation Health

Conclude with a simple status statement:
- "✅ Installed and discoverable" when skills are found
- "❌ Not detected" when no skills are found

Include a short remediation hint when not detected.

## Output Format

Return one of the following:

### 1. Skill Inventory

```
Status: ✅ Installed and discoverable

**Meta Domain**
- create-skill: Help create a new AI agent skill through collaborative Q&A
- validate-skill: Validate that a skill conforms to repository standards
- check-waldronlab-skills: Verify waldronlab skills and find the right one

**R/Bioconductor Domain**
- analyze-r-package: Analyze package structure and characteristics
- create-package-instructions: Generate .github/instructions files
- update-package-instructions: Update existing package instructions
```

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

**Response**:
```
✅ Status: Installed and discoverable

Available waldronlab skills:

Meta
  • create-skill - Help create a new skill
  • validate-skill - Validate skill standards compliance
  • check-waldronlab-skills - List and verify skills (you are here)

R/Bioconductor
  • analyze-r-package - Understand package structure
  • create-package-instructions - Generate AI agent instructions
  • update-package-instructions - Refresh existing instructions

For detailed information, see SKILLS.md in the repository.
```

### Example 2: Discovery

**User**: "What waldronlab skills are there?"

**Response** (same as Example 1 - concise catalog)

### Example 3: Fit Recommendation

**User**: "Is there a good waldronlab skill for creating package instructions?"

**Response**:
```
Yes! I recommend:

**Primary**: create-package-instructions
Generates comprehensive .github/instructions files for R packages, including
overview, data access patterns, development standards, and vignette docs.

**Companion**: analyze-r-package
Run this first to understand your package structure, then use its output
to guide create-package-instructions.
```

### Example 4: No Skill Match

**User**: "Do you have a skill for testing Shiny apps?"

**Response**:
```
Not currently. The waldronlab skills focus on:
  • R/Bioconductor package development
  • Package documentation
  • Repository infrastructure

For creating a new skill, try:
  /create-skill (Claude)
  @workspace create a new skill (Copilot)

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

- Keep responses concise and actionable
- Prioritize helping users confirm setup quickly
- If skills are missing, provide actionable next steps
- Reference SKILLS.md for detailed skill information
- This skill complements SKILLS.md as the quick-check discovery tool

See [AGENTS.md](../../AGENTS.md) for how skill discovery works and [SKILLS.md](../../SKILLS.md) for the complete index.

---

**Related**: SKILLS.md (complete skill index), instructions/claude.md, instructions/copilot.md
