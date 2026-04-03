---
name: check-waldronlab-skills
description: Verify that waldronlab/ai-agent-skills are available and help users find the right skill
version: 1.0.0
platforms:
  - claude-code
  - github-copilot
triggers:
  claude:
    - /check-waldronlab-skills
    - "Do I have the waldronlab skills?"
    - "What waldronlab skills are there?"
    - "Is there a good waldronlab skill for this?"
  copilot:
    - "@workspace Do I have the waldronlab skills?"
    - "@workspace What waldronlab skills are there?"
    - "@workspace Is there a good waldronlab skill for this?"
author: waldronlab
category: meta
---

# check-waldronlab-skills

Help any user confirm that waldronlab skills are installed and visible, then provide a concise catalog of available skills with short descriptions.

This skill is intended as a quick health check and discovery entry point for the `waldronlab/ai-agent-skills` repository.

## Usage

**Claude Code**:
- `/check-waldronlab-skills`
- "Do I have the waldronlab skills?"
- "What waldronlab skills are there?"
- "Is there a good waldronlab skill for this?"

**GitHub Copilot**:
- `@workspace Do I have the waldronlab skills?`
- `@workspace What waldronlab skills are there?`
- `@workspace Is there a good waldronlab skill for this?`

## Prerequisites

- The `waldronlab/ai-agent-skills` repository is present locally.
- Skill files are accessible through configured skill locations or project-level instruction links.

## Process

### 1. Discover Available Waldronlab Skills

Collect all discoverable skill files associated with `waldronlab/ai-agent-skills`.

At minimum, include the canonical skills currently in this repository:
- `create-skill` (meta)
- `analyze-r-package` (r-packages)
- `create-package-instructions` (r-packages)
- `update-package-instructions` (r-packages)

If no waldronlab skills are found, return a clear not-found status and suggest checking skill path configuration.

### 2. Summarize Skills

For each discovered skill, provide:
- Skill name
- Domain/category
- One-sentence purpose summary
- Typical use case

Prefer concise summaries derived from each skill's frontmatter `description` and top-level overview.

### 3. Answer User Questions About Skill Fit

When the user asks task-oriented questions such as "Is there a good waldronlab skill for this?":
- Ask for brief context if the task is unclear.
- Recommend 1-2 best-fit skills with a one-line rationale each.
- If no skill is a clear match, say so directly and suggest `create-skill` to draft a new one.

### 4. Report Installation Health

Conclude with a simple status statement:
- `Installed and discoverable` when skills are found.
- `Not detected` when no skills are found.

Include a short remediation hint when not detected.

## Output Format

Return one of the following:

1. **Skill Inventory**
- Installation status
- Bullet list of available waldronlab skills with short descriptions

2. **Question Answer**
- Direct answer to the user's skill question
- Recommended skill(s) and why
- Optional fallback recommendation to create a new skill

## Platform-Specific Notes

### Claude Code

- Supports direct slash invocation with `/check-waldronlab-skills`.
- Can be used as a first diagnostic command in a new session.

### GitHub Copilot

- Works best with `@workspace` prompts.
- If skills appear duplicated, explain that multiple configured locations may expose the same skill.

## Examples

### Example 1: Installation Check

**User**: "Do I have the waldronlab skills?"

**Expected response style**:
- "Status: Installed and discoverable"
- List available skills with one-line summaries

### Example 2: Discovery

**User**: "What waldronlab skills are there?"

**Expected response style**:
- Short catalog grouped by domain (meta, r-packages)
- One-line purpose and when to use each

### Example 3: Fit Recommendation

**User**: "Is there a good waldronlab skill for creating package instructions?"

**Expected response style**:
- Recommend `create-package-instructions`
- Mention `analyze-r-package` as companion where appropriate

## Notes

- Keep responses concise and practical.
- Prioritize helping users confirm setup quickly.
- If skills are missing, provide actionable next checks rather than generic troubleshooting.
