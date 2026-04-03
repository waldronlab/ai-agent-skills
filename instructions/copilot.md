# GitHub Copilot Setup

Add waldronlab skills to GitHub Copilot.

## Setup

1. Clone the repository (if needed):
   ```bash
   git clone https://github.com/waldronlab/ai-agent-skills.git
   ```

2. Add to VS Code User `settings.json` (Cmd+, → search "settings.json"):
   ```json
   {
     "chat.skillsLocations": [
       "/path/to/ai-agent-skills/skills/create-skill",
       "/path/to/ai-agent-skills/skills/check-waldronlab-skills",
       "/path/to/ai-agent-skills/skills/validate-skill",
       "/path/to/ai-agent-skills/skills/analyze-r-package",
       "/path/to/ai-agent-skills/skills/create-package-instructions",
       "/path/to/ai-agent-skills/skills/update-package-instructions"
     ]
   }
   ```

   Replace `/path/to/ai-agent-skills` with the actual path (use `pwd`).

3. Reload VS Code (Cmd+Shift+P → Developer: Reload Window).

## Per-Project Setup (Optional)

Create `.github/copilot-instructions` symlink in your project:
```bash
ln -s /path/to/ai-agent-skills/skills .github/copilot-instructions
```

Then add to `.vscode/settings.json` in that project:
```json
{
  "chat.skillsLocations": [
    ".github/copilot-instructions/create-skill",
    ".github/copilot-instructions/check-waldronlab-skills",
    ".github/copilot-instructions/validate-skill",
    ".github/copilot-instructions/analyze-r-package",
    ".github/copilot-instructions/create-package-instructions",
    ".github/copilot-instructions/update-package-instructions"
  ]
}
```

## Usage

Open Copilot Chat and describe what you need:
```
@workspace Analyze this R package
@workspace Create .github/instructions for this package
@workspace Help me create a new skill
```

Natural language always works without memorizing patterns.

## Troubleshooting

- **Skills not found**: Verify path in `settings.json` is absolute and correct
- **Skills not updating**: Reload VS Code (Cmd+Shift+P → Developer: Reload Window)
- **Symlink broken**: Check: `ls -la .github/copilot-instructions`

## Next Steps

- Browse skills: [SKILLS.md](../SKILLS.md)
- Usage examples: [README.md](../README.md#usage-examples)
- General setup: [README.md](../README.md#installation)
