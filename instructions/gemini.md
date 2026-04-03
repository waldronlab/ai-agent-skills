# Google Gemini Setup

Google Gemini is Google's AI assistant, available through various platforms including web, mobile, and API.

## Installation & Setup

### Prerequisites

- Access to Google Gemini (gemini.google.com, Google AI Studio, or API)
- Access to the waldronlab/ai-agent-skills repository
- File system access or ability to reference local files (varies by platform)

### Setup Options

Since Gemini doesn't currently have built-in skill file loading like Claude Code or GitHub Copilot, you'll need to manually provide skill content when needed.

#### Option 1: Copy Skill Content (Most Reliable)

When you want to use a skill with Gemini:

1. Navigate to the skill file: `skills/{skill-name}/SKILL.md`
2. Copy the entire skill content
3. Paste into your Gemini conversation with context:
   ```
   I have a skill called "{skill-name}" that you should follow.
   Here's the skill content:

   [paste skill content]

   Now, [describe what you want to do]
   ```

#### Option 2: Reference Repository (If File Access Available)

If using Gemini through an environment with file system access (like Google AI Studio with file uploads):

1. Upload the entire `ai-agent-skills/` repository
2. Reference skills by path when needed:
   ```
   Follow the skill at skills/create-skill/SKILL.md to help me create a new skill
   ```

#### Option 3: Summarize from SKILLS.md

For simpler tasks, reference the skill index:

1. Share [SKILLS.md](../SKILLS.md) with Gemini
2. Ask Gemini to follow a specific skill's process:
   ```
   Based on SKILLS.md, use the "analyze-r-package" process to analyze this R package
   ```

## Discovering Skills

### Method 1: Natural Language (Always Works)

Describe what you need:

```
"Help me create a new skill for [purpose]"
"Analyze this R package"
"Create .github/instructions for this package"
"What waldronlab skills are available?"
```

If you've shared skill content with Gemini, it will recognize and follow the appropriate skill.

### Method 2: Reference SKILLS.md

Share the [SKILLS.md](../SKILLS.md) file with Gemini to get an overview of all available skills, then ask it to follow a specific one.

### Method 3: Direct Skill Reference

When you know which skill you need:

```
"Follow the create-skill process to help me design a new skill"
"Use the analyze-r-package skill to examine this package"
```

## Platform-Specific Considerations

### Gemini Web (gemini.google.com)

- **File uploads**: Supported (can upload skill files)
- **Context length**: Limited conversation context
- **Best approach**: Copy-paste skill content or upload specific skill files as needed

### Google AI Studio

- **File uploads**: Full support for file uploads
- **Context length**: Extended context available
- **Best approach**: Upload entire `skills/` directory, reference skills by path
- **Code execution**: Can run code examples from skills

### Gemini API

- **File uploads**: Supported via API
- **Context length**: Configurable
- **Best approach**: Include skill content in system instructions or as uploaded files
- **Integration**: Can build custom tools that reference skill files

## Usage Examples

### Example 1: Creating a New Skill

**Setup**:
1. Copy `skills/create-skill/SKILL.md` content
2. Share with Gemini

**Your request**:
```
I want to create a new skill for validating R package documentation.
Follow the create-skill process we discussed.
```

**What Gemini does**:
1. Follows the collaborative Q&A process from the skill
2. Asks clarifying questions about your needs
3. Helps you design and generate the skill file
4. Provides the complete skill markdown

### Example 2: Analyzing an R Package

**Setup**:
1. Navigate to your R package directory
2. Copy `skills/analyze-r-package/SKILL.md` content
3. Share with Gemini

**Your request**:
```
Analyze this R package following the analyze-r-package skill.
Here's my DESCRIPTION file:
[paste DESCRIPTION]

Here's my NAMESPACE:
[paste NAMESPACE]
```

**What Gemini does**:
1. Follows the analysis process from the skill
2. Examines package metadata and structure
3. Provides structured analysis output
4. Suggests next steps

### Example 3: Generating Package Instructions

**Setup**:
1. Share `skills/create-package-instructions/SKILL.md`
2. Share analysis from previous example

**Your request**:
```
Create .github/instructions for this package following the create-package-instructions skill.
Use the analysis output from earlier in our conversation.
```

**What Gemini does**:
1. Uses the analysis to determine required instruction files
2. Generates each instruction file following the templates
3. Provides complete markdown for all files
4. Suggests customization points

### Example 4: Checking Available Skills

**Your request**:
```
Here's SKILLS.md from waldronlab/ai-agent-skills:
[paste SKILLS.md content]

What skills are available and which would help with [your task]?
```

**What Gemini does**:
1. Reviews available skills
2. Recommends relevant ones for your task
3. Explains what each skill does

## Workflow Tips

### For One-Time Tasks

Copy-paste the specific skill content you need. This works well for:
- Creating a single skill
- Analyzing one package
- One-off instruction generation

### For Multiple Tasks

Upload the entire repository to Gemini (if using AI Studio):
1. Upload `skills/` directory
2. Upload `AGENTS.md` and `SKILLS.md`
3. Reference skills by path throughout your session

### For Ongoing Work

Create a custom GPT or saved conversation with:
- SKILLS.md pre-loaded
- Common skills pre-loaded
- AGENTS.md for understanding behavior

## Troubleshooting

### Problem: Gemini Doesn't Follow Skill Process

**Symptom**: Gemini provides generic answers instead of following skill steps

**Solutions**:
1. Be explicit: "Follow the exact process outlined in the skill file"
2. Reference specific sections: "Start with step 1 of the skill: 'Understand the Intent'"
3. Share the skill content again if context was lost
4. Break the skill into smaller steps if the full process is too long

### Problem: Context Length Exceeded

**Symptom**: Gemini can't process the full skill + your content

**Solutions**:
1. Summarize the skill process in your own words
2. Share only relevant sections of the skill
3. Use Google AI Studio for longer context
4. Break the task into multiple conversations

### Problem: File Upload Not Available

**Symptom**: Can't upload skill files to Gemini

**Solutions**:
1. Copy-paste skill content directly into the conversation
2. Share skills incrementally as needed
3. Summarize skill processes for simpler tasks
4. Use Google AI Studio which supports file uploads

## Limitations vs. Built-In Skill Support

Unlike Claude Code and GitHub Copilot, Gemini doesn't have built-in skill file loading, which means:

**What's Different**:
- You manually share skill content (no auto-loading)
- No slash commands or @workspace shortcuts
- Need to re-share skills if context is lost

**What's The Same**:
- Skills work through natural language
- Same skill logic and processes
- Platform-agnostic design means full compatibility
- Same output quality and thoroughness

## Best Practices

### 1. Start With SKILLS.md

Before diving into a specific skill:
1. Share SKILLS.md with Gemini
2. Ask which skill fits your need
3. Then share that specific skill

### 2. Provide Full Context

When sharing skills, include:
- The complete skill file content
- Relevant project files (DESCRIPTION, README, etc.)
- Clear description of what you want to accomplish

### 3. Reference Shared Standards

When using r-packages skills, also share the standards:
- `skills/create-package-instructions/templates/bioconductor-development.md`
- `skills/create-package-instructions/templates/waldronlab-standards.md`

This ensures generated instructions follow conventions.

### 4. Save Generated Content

Gemini doesn't have direct file write access, so:
1. Copy generated skill files or instructions
2. Save to appropriate locations in your project
3. Verify content before committing

### 5. Verify Against AGENTS.md

Share [AGENTS.md](../AGENTS.md) to help Gemini understand:
- How skill discovery should work
- What agent-neutral means
- How to invoke skills properly

## Platform-Agnostic Skills

Important: These skills are **platform-agnostic** by design. They work with Gemini the same way they work with Claude Code or GitHub Copilot - through natural language and following the documented process.

The skills don't require any special Gemini features or integration. They're just markdown documentation that any AI agent can read and follow.

## Additional Resources

- **AGENTS.md** - How agent behavior and skill discovery work
- **SKILLS.md** - Index of all available skills
- **SKILL_STANDARD.md** - Technical format for skills
- **CONTRIBUTING.md** - How to contribute new skills
- **Repository**: https://github.com/waldronlab/ai-agent-skills

## Future Integration

If Google adds native skill file support to Gemini (similar to Claude Code's `claude.globalSkills` or Copilot's `chat.skillsLocations`), this document will be updated with:
- Configuration instructions
- Automatic skill loading
- Platform-specific shortcuts (if available)

Until then, the manual sharing approach documented here works reliably.

---

**Last Updated**: 2026-04-03
**Maintained by**: waldronlab
