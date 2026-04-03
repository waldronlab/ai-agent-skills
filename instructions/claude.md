# Claude Code Setup

Add waldronlab skills to your global Claude instructions.

## Setup

1. Clone the repository (if needed):
   ```bash
   git clone https://github.com/waldronlab/ai-agent-skills.git
   ```

2. Update `~/.claude/CLAUDE.md`:
   ```markdown
   # waldronlab AI Agent Skills

   See: `/path/to/ai-agent-skills/SKILLS.md`

   Describe what you need, and I'll match it to the appropriate skill.
   ```

   Replace `/path/to/ai-agent-skills` with the actual path (use `pwd`).

3. Restart Claude Code or reload the workspace.

## Optional: Slash Commands

Claude Code supports shortcuts (e.g., `/create-skill`, `/analyze-r-package`). Natural language always works without them.

## Troubleshooting

- **Skills not found**: Verify path in `~/.claude/CLAUDE.md` is absolute and correct
- **Slash commands not working**: Reload Claude Code (desktop: restart, web/IDE: Cmd+Shift+P → Developer: Reload Window)

## Next Steps

- Browse skills: [SKILLS.md](../SKILLS.md)
- Usage examples: [README.md](../README.md#usage-examples)
- General setup: [README.md](../README.md#installation)
