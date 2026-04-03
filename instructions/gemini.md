# Google Gemini Setup

Use waldronlab skills with Gemini by manually sharing skill content.

## Setup

Unlike Claude Code or GitHub Copilot, Gemini doesn't auto-load skills. Instead, share skill content when needed:

### Quick Setup (One-Time)

1. Navigate to the skill you need: `skills/{skill-name}/SKILL.md`
2. Copy the entire skill content
3. Paste into Gemini with context:
   ```
   Follow this skill called "{skill-name}":

   [paste skill content]

   Now help me with [your task]
   ```

### For Repeated Use (Google AI Studio)

If using [Google AI Studio](https://aistudio.google.com):

1. Upload `skills/` directory
2. Reference skills by path in conversations:
   ```
   Follow the skill at skills/create-skill/SKILL.md to help me create a new skill
   ```

## Usage

Describe what you need, referencing the skill:

```
Based on the create-skill skill, help me create a new skill for [purpose]
Analyze this R package using the analyze-r-package skill
Create .github/instructions using the create-package-instructions skill
```

Share relevant skill files or content when the context resets.

## Workflow Tips

- **One-time task**: Copy-paste the specific skill content
- **Multiple tasks**: Upload entire `skills/` directory to AI Studio
- **Reference guide**: Share [SKILLS.md](../SKILLS.md) to see all available skills

## Limitations

- No auto-loading (manual copy-paste or file upload)
- No slash commands or shortcuts
- Need to re-share skills if context is lost

## Next Steps

- Browse skills: [SKILLS.md](../SKILLS.md)
- Usage examples: [README.md](../README.md#usage-examples)
- General setup: [README.md](../README.md#installation)
