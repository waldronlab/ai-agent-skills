# Meta Skills

Skills for working with the ai-agent-skills repository itself - creating, maintaining, and improving the skill framework.

## Purpose

The `meta/` domain contains skills that help contributors work with the skill system. Unlike domain-specific skills (r-packages, metagenomics), these are about the repository infrastructure.

## Available Skills

### [create-skill.md](create-skill.md)
**Purpose**: Help create new AI agent skills through collaborative Q&A
**Triggers**:
- `/create-skill` (Claude Code)
- `@workspace create a new skill` (GitHub Copilot)

**Philosophy**: Collaborative brainstorming partner that guides users from rough ideas to structured skill files. Focuses on clarifying intent rather than enforcing strict formatting.

**Use when**:
- Creating a new skill from scratch
- Converting manual workflows into skills
- Unsure how to structure a skill idea

## Future Skills

Potential additions to this domain:

- **validate-skill.md** - Check skill format compliance (separate from creation)
- **migrate-skill.md** - Convert platform-specific skills to unified format
- **test-skill.md** - Test skills across platforms
- **update-templates.md** - Maintain shared template files
- **document-domain.md** - Create or update domain documentation

## Philosophy

**Meta skills prioritize**:
- Lowering contribution barriers
- Helping rather than enforcing
- Iteration over perfection
- Collaboration over prescription

**Separation of concerns**:
- **Creation** (create-skill.md): Help users develop ideas
- **Validation** (future): Check compliance after creation
- **Migration** (future): Convert existing skills
- **Testing** (future): Verify cross-platform functionality

## Related Resources

- [SKILL_STANDARD.md](../SKILL_STANDARD.md) - Format specification and design principles
- [r-packages/](../r-packages/) - Example skills following the standard
- Repository [README.md](../README.md) - Overall project structure

---

**Version**: 1.0.0
**Maintainers**: waldronlab
**Purpose**: Repository infrastructure and skill system management
