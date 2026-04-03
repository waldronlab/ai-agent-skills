# Contributing to waldronlab AI Agent Skills

Thank you for your interest in contributing! This repository is a collaborative effort to make AI agents more effective partners in waldronlab research and development.

## Ways to Contribute

### 1. Add New Skills

If you've developed patterns or workflows that AI agents could learn:

1. Choose the appropriate domain directory (or propose a new one)
2. Follow the skill format (see examples in `r-packages/claude/`)
3. Test on multiple real projects
4. Include examples showing the output
5. Document usage and expected behavior

### 2. Improve Existing Skills

Found a way to make a skill better?

1. Test your improvements on multiple packages/projects
2. Ensure backwards compatibility or document breaking changes
3. Update examples if output format changes
4. Add test cases if applicable

### 3. Add Examples

Good examples help everyone:

1. Choose a representative package/project
2. Ensure instructions are high quality
3. Include minimal context (DESCRIPTION, README, etc.)
4. Follow the examples directory structure
5. Document what makes the example notable

### 4. Report Issues

Found a bug or have a suggestion?

1. Check if issue already exists
2. Provide clear reproduction steps
3. Include package/project details
4. Suggest solution if you have one

### 5. Improve Documentation

Documentation improvements are always welcome:

- Fix typos or clarify instructions
- Add missing usage examples
- Update outdated information
- Improve formatting or organization

## Contribution Process

### Small Changes (typos, doc fixes)

1. Fork the repository
2. Make your changes
3. Submit a pull request
4. Address any review comments

### Larger Changes (new skills, major updates)

1. **Open an issue first** to discuss your proposal
2. Get feedback from maintainers
3. Fork and create a feature branch
4. Develop and test your changes
5. Update documentation
6. Submit a pull request
7. Respond to review feedback

## Skill Development Guidelines

### Format

Skills should be markdown files with:

**For Claude Code** (`claude/` directory):
```markdown
---
name: skill-name
description: Brief description of what the skill does
version: 1.0.0
---

# Skill Title

Clear description of purpose and usage.

## Usage
/skill-command or "trigger phrase"

## Process
Step-by-step instructions for the AI agent

## Output Format
Description of expected output
```

**For GitHub Copilot** (`copilot/` directory):
- Natural language instructions
- Pattern-based guidance
- Example interactions
- Quick reference commands

### Testing

Before submitting a skill:

1. **Test on at least 3 different packages/projects**
   - Include different package types if applicable
   - Test edge cases
   - Verify output quality

2. **Validate output**
   - Generated files should be accurate
   - Cross-references should work
   - Format should be consistent

3. **Get feedback**
   - Have others test your skill
   - Iterate based on feedback

### Documentation

Every skill should have:

- Clear description of purpose
- Usage instructions
- Example output
- Known limitations
- Maintenance notes

## Code Review Process

### What Reviewers Look For

- **Correctness**: Does it produce accurate output?
- **Completeness**: Are edge cases handled?
- **Clarity**: Are instructions clear and unambiguous?
- **Consistency**: Does it follow established patterns?
- **Testing**: Has it been adequately tested?
- **Documentation**: Is usage clear?

### Timeline

- Small PRs: Usually reviewed within 2-3 days
- Large PRs: May take up to a week
- Complex changes: May require discussion and iteration

## Style Guidelines

### Markdown Formatting

- Use ATX-style headers (`#` not underlines)
- Use fenced code blocks with language tags
- Use lists for steps or items
- Keep lines under 120 characters when possible
- Include blank lines between sections

### Naming Conventions

**Skills**:
- Lowercase with hyphens: `analyze-r-package`
- Verb-noun format when possible: `create-instructions`

**Files**:
- READMEs in title case: `README.md`
- Templates: `{number}-{name}.template.md`
- Examples: `{type}-{pattern}/`

**Directories**:
- Lowercase, hyphens for multi-word: `r-packages`, `statistical-methods`

### Writing Style

- **Clear and concise**: Get to the point quickly
- **Active voice**: "Generate instructions" not "Instructions are generated"
- **Examples**: Show, don't just tell
- **Specific**: "Read DESCRIPTION file" not "Read package metadata"

## Commit Messages

Follow conventional commit format:

```
type: brief description

- Detailed point 1
- Detailed point 2

Co-Authored-By: [Your Name] <your@email.com>
```

**Types**:
- `feat`: New skill or major feature
- `fix`: Bug fix in existing skill
- `docs`: Documentation updates
- `test`: Adding or updating tests
- `refactor`: Code restructuring
- `chore`: Maintenance tasks

## Issue Labels

We use these labels:

- `bug`: Something isn't working
- `enhancement`: New feature or improvement
- `documentation`: Documentation updates needed
- `good first issue`: Good for newcomers
- `help wanted`: Extra attention needed
- `question`: Further information requested
- `wontfix`: Will not be worked on

## Community Guidelines

### Be Respectful

- Be kind and patient
- Welcome newcomers
- Respect different perspectives
- Assume good intentions

### Be Collaborative

- Share knowledge openly
- Give constructive feedback
- Credit others' contributions
- Help others learn

### Be Professional

- Keep discussions on-topic
- Use inclusive language
- Respect privacy
- Follow code of conduct

## Getting Help

Stuck? Need clarification?

- **GitHub Discussions**: General questions and ideas
- **GitHub Issues**: Specific problems or bugs
- **Maintainers**: Tag domain maintainers in issues/PRs

## Domain Maintainers

Each domain has designated maintainers (listed in domain README):

- **r-packages/**: [Maintainer names]
- **metagenomics/**: [Maintainer names]
- **statistical-methods/**: [Maintainer names]

Maintainers are responsible for:
- Reviewing domain-specific PRs
- Maintaining skill quality
- Updating documentation
- Responding to issues

## License

By contributing, you agree that your contributions will be licensed under the MIT License.

## Questions?

If anything is unclear, please ask! We're here to help and appreciate your contributions.

Thank you for helping make AI agents better collaborators! 🤖✨
