# GitHub Copilot Setup

GitHub Copilot is GitHub's AI pair programmer, available as a VS Code extension and JetBrains IDE plugin.

## Installation & Setup

### Prerequisites

- GitHub Copilot extension installed in VS Code
- GitHub Copilot subscription
- Access to the waldronlab/ai-agent-skills repository

### Global Setup (Recommended)

Add to your VS Code User `settings.json`:

```json
{
  "chat.skillsLocations": [
    "/Users/<your-user>/git/ai-agent-skills/skills/create-skill",
    "/Users/<your-user>/git/ai-agent-skills/skills/check-waldronlab-skills",
    "/Users/<your-user>/git/ai-agent-skills/skills/analyze-r-package",
    "/Users/<your-user>/git/ai-agent-skills/skills/create-package-instructions",
    "/Users/<your-user>/git/ai-agent-skills/skills/update-package-instructions"
  ],
  "github.copilot.advanced.instructionsFolders": [
    "/Users/<your-user>/git/ai-agent-skills/skills"
  ]
}
```

**Important**: Replace `/Users/<your-user>` with your actual username, or use the fully-qualified path to your ai-agent-skills directory.

**Notes**:
- `chat.skillsLocations` points to individual skill directories (for agent skill discovery)
- `github.copilot.advanced.instructionsFolders` points to the parent skills directory (broader context)

### Per-Project Setup (Alternative)

If you want skills available only in specific projects:

```bash
cd ~/git/your-project
mkdir -p .github
ln -s /Users/<your-user>/git/ai-agent-skills/skills .github/copilot-instructions
```

This creates `.github/copilot-instructions` as a symlink to the shared skills repository, so updates are immediately available.

Then add to `.vscode/settings.json` in that project:

```json
{
  "chat.skillsLocations": [
    ".github/copilot-instructions/create-skill",
    ".github/copilot-instructions/analyze-r-package",
    ".github/copilot-instructions/create-package-instructions"
  ]
}
```

### Organization-Wide Setup (Copilot Enterprise)

For organization admins with Copilot Enterprise:

1. Go to https://github.com/organizations/waldronlab/settings/copilot
2. Add skill files from the repository to the knowledge base
3. Users in the organization automatically have access

## Discovering Skills

### Method 1: Natural Language (Canonical)

Open Copilot Chat and describe what you need:

```
@workspace Help me create a new skill for [purpose]
@workspace Analyze this R package
@workspace Create .github/instructions for this package
@workspace What waldronlab skills are available?
```

I'll automatically match your request to the appropriate skill. The `@workspace` trigger tells Copilot to look at your project context.

### Method 2: Read SKILLS.md

Open [`SKILLS.md`](../SKILLS.md) in this repository to see all available skills and their purposes. Then describe what you need.

## Optional @workspace Shortcuts

Copilot supports optional `@workspace` patterns for invoking skills. These are **convenience shortcuts** — natural language invocation always works.

### Available Patterns

```
@workspace create a new skill
@workspace help me create a skill for [purpose]
@workspace analyze this R package
@workspace what type of R package is this?
@workspace Create .github/instructions for this R package
@workspace Update .github/instructions based on recent changes
@workspace Do I have the waldronlab skills?
@workspace What waldronlab skills are there?
```

Usage:
```
@workspace create a new skill
@workspace analyze this package
@workspace what skills are available?
```

**Note**: These patterns are optional. You don't need to remember them. Natural language like "help me create a new skill" works perfectly fine.

## Usage Examples

### Example 1: Creating a New Skill

**Your request** (natural language with @workspace):
```
@workspace Help me create a new skill for validating data packages
```

**What happens**:
1. Copilot reads `skills/create-skill/SKILL.md`
2. Engages in collaborative Q&A
3. Helps you design the skill
4. Generates a skill file
5. Suggests next steps

### Example 2: Analyzing an R Package

**Your request** (natural language with @workspace):
```
@workspace What type of package is this? Analyze the structure.
```

**What happens**:
1. Copilot reads `skills/analyze-r-package/SKILL.md`
2. Examines your package metadata and code
3. Provides structured analysis
4. Suggests next steps

### Example 3: Generating Package Instructions

**Your request** (natural language with @workspace):
```
@workspace Create .github/instructions for this R package
```

**What happens**:
1. Copilot reads `skills/create-package-instructions/SKILL.md`
2. Analyzes the package
3. Generates modular instruction files
4. Saves to `.github/instructions/`

### Example 4: Verifying Setup

**Your request** (natural language with @workspace):
```
@workspace Do I have the waldronlab skills installed?
@workspace What waldronlab skills are there?
```

**What happens**:
1. Copilot reads `skills/check-waldronlab-skills/SKILL.md`
2. Verifies skills are accessible
3. Lists all available skills
4. Checks your setup

## Troubleshooting

### Problem: Skills Not Discovered

**Symptom**: `@workspace` patterns don't work or skills aren't found

**Solutions**:
1. **Check the path**: Make sure `/Users/<your-user>` is your actual home directory
   ```bash
   ls -la /Users/<your-user>/git/ai-agent-skills/skills/*/SKILL.md
   # If this fails, adjust settings.json
   ```

2. **Reload VS Code**: Run `Developer: Reload Window` from the command palette (Cmd+Shift+P)

3. **Check settings.json**: Verify paths are correct and directories exist

4. **Verify Copilot Chat**: Open Copilot Chat (Cmd+I or click the chat icon)

### Problem: @workspace Not Triggering Skills

**Symptom**: `@workspace` works but doesn't match skills

**Solutions**:
1. Try a more specific pattern from the list above
2. Use natural language without a specific pattern first
3. Read SKILLS.md to understand what each skill does
4. File an issue at https://github.com/waldronlab/ai-agent-skills/issues

### Problem: Skills Not Updating

**Symptom**: You updated a skill but Copilot still uses old version

**Solution**:
1. Run `Developer: Reload Window` to refresh
2. If using symlinks, verify the symlink is current:
   ```bash
   ls -la .github/copilot-instructions
   # Should point to ai-agent-skills/skills
   ```

### Problem: Permission Issues

**Symptom**: Can't access skill files

**Solutions**:
1. Check file permissions:
   ```bash
   ls -la /Users/<your-user>/git/ai-agent-skills/skills/*/SKILL.md
   # Should be readable (at least 644)
   ```

2. Check path exists:
   ```bash
   cd /Users/<your-user>/git/ai-agent-skills/skills/
   # If this fails, clone the repository
   ```

## Tips & Best Practices

### 1. Use @workspace for Project Context

When you want Copilot to consider your project:
```
@workspace Analyze this R package
```

Copilot will look at files in your project directory.

### 2. Natural Language is Powerful

Don't memorize patterns. Describe what you need:
```
@workspace I want to create a new skill for doing X
@workspace What skills do you have available?
```

### 3. Provide Context

The more context, the better:
```
@workspace Create instructions for this R package (it's a data package with remote access)
vs.
@workspace Create instructions
```

### 4. Check SKILLS.md

Browse the skill index to understand:
- What skills exist
- When to use each one
- How to invoke them

### 5. File Issues

If something doesn't work:
- Check AGENTS.md (how skill discovery works)
- Read the skill file (e.g., `skills/create-skill/SKILL.md`)
- File an issue at https://github.com/waldronlab/ai-agent-skills/issues

## Platform-Agnostic Skills

Important note: These skills are **platform-agnostic** by design. The same skill works the same way on:
- VS Code with Copilot extension
- JetBrains IDEs (when Copilot support is available)
- GitHub.com (web editor with Copilot)
- Any future Copilot platform

Natural language invocation is canonical. `@workspace` patterns are a Copilot convenience layer.

## Skill Discovery Mechanism

Copilot discovers skills by:
1. Reading the `chat.skillsLocations` setting
2. Looking for `SKILL.md` files in those directories
3. Parsing YAML frontmatter (name, description, version, category, tags)
4. Matching user natural language intent to skill descriptions
5. Invoking the skill when there's a match

See [AGENTS.md](../AGENTS.md) for canonical skill discovery behavior.

## Additional Resources

- **AGENTS.md** - How agent behavior and skill discovery work
- **SKILLS.md** - Index of all available skills
- **SKILL_STANDARD.md** - Technical format for skills
- **CONTRIBUTING.md** - How to contribute new skills
- **Repository**: https://github.com/waldronlab/ai-agent-skills

---

**Last Updated**: 2026-04-03
**Maintained by**: waldronlab
