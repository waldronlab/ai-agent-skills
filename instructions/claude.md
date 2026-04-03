# Claude Code Setup

Claude Code is Anthropic's CLI for Claude, available as a desktop app, web app, and IDE extension.

## Installation & Setup

### Prerequisites

- Claude Code installed (desktop app, web app at claude.ai/code, or IDE extension)
- Access to the waldronlab/ai-agent-skills repository

### Global Installation (Recommended)

Clone the repository and configure Claude Code to use these skills globally:

```bash
# Clone the repository
cd ~/git
git clone https://github.com/waldronlab/ai-agent-skills.git
```

Add to your VS Code settings (`~/.config/Code/User/settings.json` on macOS/Linux, or search for "settings.json" in VS Code):

```json
{
  "claude.globalSkills": [
    "/Users/<your-user>/git/ai-agent-skills/skills/create-skill/SKILL.md",
    "/Users/<your-user>/git/ai-agent-skills/skills/check-waldronlab-skills/SKILL.md",
    "/Users/<your-user>/git/ai-agent-skills/skills/analyze-r-package/SKILL.md",
    "/Users/<your-user>/git/ai-agent-skills/skills/create-package-instructions/SKILL.md",
    "/Users/<your-user>/git/ai-agent-skills/skills/update-package-instructions/SKILL.md"
  ]
}
```

**Important**: Replace `/Users/<your-user>` with your actual username, or use the fully-qualified path to your ai-agent-skills directory.

### Per-Workspace Installation

If you want skills available only in specific projects, add to `.vscode/settings.json` in that project:

```json
{
  "claude.skills": [
    "../ai-agent-skills/skills/create-skill/SKILL.md",
    "../ai-agent-skills/skills/analyze-r-package/SKILL.md",
    "../ai-agent-skills/skills/create-package-instructions/SKILL.md",
    "../ai-agent-skills/skills/update-package-instructions/SKILL.md"
  ]
}
```

Adjust relative paths as needed based on your project location.

## Discovering Skills

### Method 1: Natural Language (Canonical)

Simply describe what you need:

```
"Help me create a new skill for [purpose]"
"Analyze this R package"
"Create .github/instructions for this package"
"What waldronlab skills do I have?"
```

I'll automatically match your request to the appropriate skill and execute it. This works even if you don't know about slash commands.

### Method 2: Read SKILLS.md

Open the file [`SKILLS.md`](/Users/<your-user>/git/ai-agent-skills/SKILLS.md) in the repository to see all available skills and their purposes. Then describe what you need.

## Optional Slash Command Shortcuts

Claude Code supports optional slash command shortcuts for skills. These are **convenience shortcuts** — natural language invocation always works.

### Available Shortcuts

```
/create-skill          → Help create a new AI agent skill
/check-waldronlab-skills → List available waldronlab skills
/analyze-r-package     → Analyze R/Bioconductor package structure
/create-package-instructions → Generate .github/instructions for R packages
/update-package-instructions → Update existing .github/instructions
```

Usage:
```
/create-skill
/check-waldronlab-skills
/analyze-r-package
```

**Note**: These shortcuts are optional. You don't need to remember them. Natural language invocation like "Help me create a new skill" works perfectly fine.

## Usage Examples

### Example 1: Creating a New Skill

**Your request** (natural language):
```
"Help me create a new skill for validating data package structures"
```

or

**Your request** (slash command):
```
/create-skill
```

**What happens**:
1. I read `skills/create-skill/SKILL.md`
2. Follow the collaborative Q&A process
3. Help you design the skill
4. Generate a skill file
5. Suggest next steps

### Example 2: Analyzing an R Package

**Your request** (natural language):
```
"What type of package is this? Analyze the structure."
```

or

**Your request** (slash command):
```
/analyze-r-package
```

**What happens**:
1. I read `skills/analyze-r-package/SKILL.md`
2. Examine the package metadata and code
3. Provide a structured analysis
4. Suggest next steps (e.g., create instructions)

### Example 3: Generating Package Instructions

**Your request** (natural language):
```
"Create .github/instructions for this R package"
```

or

**Your request** (slash command):
```
/create-package-instructions
```

**What happens**:
1. I read `skills/create-package-instructions/SKILL.md`
2. Analyze the package (similar to example 2)
3. Generate modular instruction files in `.github/instructions/`
4. Save files to your package

### Example 4: Verifying Setup

**Your request** (natural language):
```
"Do I have the waldronlab skills installed?"
"What skills are available?"
```

or

**Your request** (slash command):
```
/check-waldronlab-skills
```

**What happens**:
1. I read `skills/check-waldronlab-skills/SKILL.md`
2. Verify you have the skills installed
3. List all available skills
4. Check your setup

## Troubleshooting

### Problem: Skills Not Loading

**Symptom**: Slash commands don't work or I can't find skills

**Solutions**:
1. **Check the path**: Make sure `/Users/<your-user>` is your actual home directory
   ```bash
   cd ~/git/ai-agent-skills/skills/create-skill/
   # If this fails, adjust your path in settings.json
   ```

2. **Reload VS Code**: Run `Developer: Reload Window` from the command palette (Cmd+Shift+P)

3. **Check file locations**: Verify files exist at the specified paths
   ```bash
   ls /Users/<your-user>/git/ai-agent-skills/skills/*/SKILL.md
   ```

4. **Check settings.json**: Make sure paths are absolute (not relative) and correct

### Problem: Skills Not Working As Expected

**Symptom**: Skill runs but output is wrong or incomplete

**Solution**:
1. Check SKILLS.md to understand what the skill should do
2. Read the actual skill file (e.g., `skills/create-skill/SKILL.md`)
3. Verify prerequisites are met (e.g., package files exist)
4. File an issue at https://github.com/waldronlab/ai-agent-skills/issues

### Problem: Natural Language Not Matching Skills

**Symptom**: I don't recognize your request as a skill

**Solutions**:
1. Be explicit: "Use the [skill-name] skill to help me with [task]"
2. Read SKILLS.md to understand descriptions
3. Try a slash command shortcut instead (if you prefer)
4. Check AGENTS.md for how discovery works

## Tips & Best Practices

### 1. Use Natural Language First

Start with natural language descriptions:
```
"I want to create a new skill"
"Analyze this package"
```

Slash commands are optional shortcuts for power users.

### 2. Provide Context

The more context you provide, the better the skill execution:
```
"Create a new skill for generating synthetic microbiome data"
vs.
"Create a new skill"
```

### 3. Check SKILLS.md

Before asking, browse SKILLS.md to see what's available and understand what each skill does.

### 4. Give Feedback

If a skill doesn't work as expected:
- Check prerequisites
- Read the skill file (e.g., `skills/create-skill/SKILL.md`)
- File an issue with details

## Platform-Agnostic Skills

Important note: These skills are **platform-agnostic** by design. The same skill works the same way on:
- Claude Code desktop
- Claude Code web (claude.ai/code)
- VS Code extension
- Any future Claude platform

Natural language invocation is canonical. Slash commands are a Claude Code convenience layer.

## Additional Resources

- **AGENTS.md** - How agent behavior and skill discovery work
- **SKILLS.md** - Index of all available skills
- **SKILL_STANDARD.md** - Technical format for skills
- **CONTRIBUTING.md** - How to contribute new skills
- **Repository**: https://github.com/waldronlab/ai-agent-skills

---

**Last Updated**: 2026-04-03
**Maintained by**: waldronlab
