---
name: create-skill
description: Use this skill when the user wants to create a new Claude Code skill that automates a workflow — scaffolding a feature directory, codifying a multi-step procedure, wrapping a CLI integration, etc. Triggers on phrases like "create a skill", "create a command", "scaffold a workflow", "automate this task", "I keep doing the same thing every time", or "/create-skill". Guides discovery, requirements gathering, and writes the new skill file at .claude/skills/<name>/SKILL.md.
---

# Create Skill

You are tasked with discovering, defining, and creating comprehensive Claude Code skills through collaborative conversation and iterative requirements gathering. Your role is to guide the user through workflow ideation, understanding procedural requirements, and producing a complete skill file.

## Initial Response

When this skill is invoked:

1. **Check if parameters were provided** (via the Skill tool's `args` field or inline context):
   - If a skill idea, workflow description, context, or rough outline was provided, begin the discovery process with that context
   - If files are referenced, read them FULLY first to understand existing context
   - If no parameters provided, respond with the default prompt below

2. **If no parameters provided**, respond with:
```
I'll help you discover, define, and specify a new Claude Code skill through collaborative conversation. Let's start by understanding what workflow you want to automate.

What skill or workflow are you considering? This could be:
- A repetitive task you want to automate ("initialize new projects with...")
- A multi-step workflow that's error-prone ("scaffold feature directories...")
- A complex process that needs consistency ("deploy agents to...")
- An integration between tools ("sync data with...")

Don't worry about having all the details - we'll explore, refine, and create the skill together!

Tip: You can also invoke this skill with context, e.g. `/create-skill scaffold feature workflow` or `/create-skill based on docs/workflows/deploy_process.md`.
```

Then wait for the user's input.

## Process Overview

This skill combines workflow discovery and skill creation into a unified workflow:

1. **Discovery Phase**: Collaborative exploration to understand the workflow and define the skill
2. **Requirements Phase**: Detailed skill creation with step-by-step procedures and validation
3. **Skill Creation**: Create the skill file directly in `.claude/skills/<skill-name>/SKILL.md`

## Phase 1: Discovery & Workflow Understanding

### Step 1: Context Gathering

1. **Read all referenced files immediately and FULLY**:
   - Related workflow documents or process descriptions
   - Existing skills for similar workflows
   - Technical documentation about tools or systems involved
   - Use the Read tool WITHOUT limit/offset parameters to read entire files
   - **CRITICAL**: DO NOT spawn sub-tasks before reading these files yourself
   - **NEVER** read files partially - if a file is mentioned, read it completely

2. **Review existing skills** (if relevant):
   - Check `.claude/skills/` for similar patterns and existing skills
   - Identify reusable procedural patterns
   - Note naming conventions and style

### Step 2: Workflow Exploration

1. **Understand the core workflow**:
   - What manual process needs automation?
   - Who will invoke this skill?
   - What triggers the need for this workflow?
   - Any time/effort savings expected?

2. **Deep dive into the process**:
   - What are the current pain points?
   - How is this done manually today?
   - What makes the current approach error-prone or inefficient?
   - What prerequisites or setup are required?

3. **Acknowledge and probe deeper**:
   ```
   I understand you're thinking about automating [summarize their workflow].

   Let me ask some clarifying questions:
   - Walk me through the exact steps you currently take manually
   - What typically goes wrong or requires extra attention?
   - Are there variations of this workflow for different scenarios?
   - What inputs or decisions are needed along the way?
   ```

### Step 3: Solution Design & Scope Definition

1. **Explore automation approach**:
   - What steps can be fully automated vs. need user input?
   - Are there decision points that require clarification?
   - What validation or error checking is critical?
   - How should the skill handle failures?

2. **Define the skill behavior**:
   - What's the minimum viable skill?
   - What parameters or inputs are needed?
   - How will users discover and invoke this?
   - What feedback should the skill provide?

3. **Consider implementation details**:
   - What tools or CLIs are required (gh, git, etc.)?
   - What file system operations are needed?
   - What absolute paths vs relative paths?
   - What platform-specific considerations?

### Step 4: Skill Naming, Description & Invocation

1. **Choose skill name** (kebab-case):
   - Use verb-noun format (e.g., `init-agent`, `scaffold-feature`, `deploy-agent`)
   - Keep it concise but descriptive
   - Check for conflicts with existing skills under `.claude/skills/`
   - Ensure it clearly describes the action

2. **Craft the `description` field** — this is the most important part of a skill. Claude reads it proactively to decide when to auto-invoke this skill, so it must:
   - Lead with "Use this skill when…" and state the trigger conditions clearly
   - List concrete example phrases the user might say
   - State what the skill does in one sentence
   - Note when NOT to use it (if there are similar skills that could be confused)
   - Keep it under ~500 characters but specific enough to disambiguate

   Bad description: `"Creates things."`
   Good description: `"Use this skill when the user wants to scaffold a new feature directory with standard subfolders (components, tests, types) and boilerplate files. Triggers on 'scaffold a feature', 'new feature folder', or '/scaffold-feature'. Do not use for whole-project init — use /init-project instead."`

3. **Define invocation patterns**:
   ```
   How should users invoke this skill?
   - Slash invocation: `/skill-name` (Claude Code recognizes this)
   - Natural language: phrases that match the description triggers
   - Programmatic: the Skill tool with optional `args`

   Most skills support all three by default. Confirm any extra arg parsing the user wants.
   ```

## Phase 2: Requirements Definition

### Step 1: Procedural Steps

1. **Break down the workflow**:
   - List each discrete step in order
   - Identify dependencies between steps
   - Note validation points
   - Highlight critical operations

2. **Define each step precisely**:
   ```
   For each step, we need to specify:
   - What exact operation to perform
   - What tools or commands to use
   - What paths (absolute vs relative)
   - What validation or error checking
   - What output to provide to the user
   ```

### Step 2: Parameters & Inputs

1. **Define what inputs are needed**:
   - Required arguments
   - Optional arguments with defaults
   - Interactive prompts for user decisions
   - File paths or external resources

2. **Specify input validation**:
   - What constitutes valid input?
   - What error messages for invalid input?
   - Any constraints or limitations?

### Step 3: Error Handling & Edge Cases

1. **Identify failure scenarios**:
   - What could go wrong at each step?
   - How to detect failures?
   - How to recover or rollback?
   - What error messages to show?

2. **Define validation checkpoints**:
   - Pre-conditions before starting
   - Validation after each critical step
   - Final verification of success
   - Cleanup on failure

## Phase 3: Skill File Creation

### Step 1: Gather Metadata

1. **Collect skill metadata**:
   - Skill name (kebab-case) and purpose
   - Description (trigger signal, see Phase 1 Step 4)
   - Related skills or workflows
   - Version or status information (if relevant)

### Step 2: Create Skill File

Write the skill file directly using this template at `.claude/skills/<skill-name>/SKILL.md`:

```markdown
---
name: <skill-name>
description: Use this skill when [trigger conditions]. Triggers on phrases like "[example 1]", "[example 2]", or "/<skill-name>". [One-sentence summary of what it does.] [Optional: when NOT to use it.]
---

# [Skill Title]

## Overview
[2-3 sentence description of what this skill automates and why it's valuable]

## Purpose & Value

### Workflow Being Automated
[Detailed description of the manual process this skill replaces]

### Time/Effort Savings
- [How this improves efficiency]
- [Error reduction benefits]
- [Consistency improvements]

### Target Users
- [Who will use this skill]
- [When they'll need it]
- [How often it's invoked]

## Skill Invocation

This skill is invoked by name via the Skill tool, or by the user typing `/<skill-name>`.

### Arguments
- `arg1`: [Description, required/optional, default value]
- `arg2`: [Description, required/optional, default value]

(If the skill takes no arguments, say so explicitly: "Takes no arguments — conversational discovery flow.")

### Usage Examples
```
# Basic invocation
/<skill-name>

# With inline context
/<skill-name> some context here

# Natural-language invocation (relies on the description field)
"Can you help me <triggering phrase>?"
```

## Procedural Requirements

### Prerequisites
[What must be in place before this skill can run:]
- [Required tools (e.g., gh CLI, git, etc.)]
- [Required permissions or authentication]
- [Required directory structure or files]
- [Environment variables or configuration]

### Step-by-Step Workflow

#### Step 1: [Step Name]
**Purpose**: [What this step accomplishes]

**Actions**:
1. [Specific operation to perform]
2. [Command or tool to use with exact syntax]
3. [Parameters and paths (specify absolute vs relative)]

**Validation**:
- [How to verify this step succeeded]
- [What to check before proceeding]

**Error Handling**:
- [What could go wrong]
- [How to detect failure]
- [What error message to show]
- [Whether to continue or abort]

**Important Notes**:
- **IMPORTANT:** [Any critical warnings or gotchas]
- [Platform-specific considerations]
- [Path handling requirements]

---

#### Step 2: [Step Name]
[Repeat structure for each step]

---

#### Step N: Confirmation & Output
**Purpose**: Confirm success and provide feedback to user

**Actions**:
1. Display completion message
2. Show output information (paths, URLs, etc.)
3. Remind user of next steps or related skills

**Output Format**:
```
[Example of what the user should see on success]
```

## File Structure & Paths

### Files Created
```
[Show the directory structure this skill creates or modifies:]

example-structure/
├── folder1/
│   ├── file1.ext
│   └── file2.ext
└── folder2/
    └── file3.ext
```

### Path Conventions
- **Absolute paths**: [When to use and examples]
- **Relative paths**: [When to use and examples]
- **User home directory**: [How to reference]
- **Project root**: [How to determine and use]

## Validation & Testing

### Success Criteria
- [ ] [Specific outcome that indicates success]
- [ ] [Files/directories created in correct locations]
- [ ] [Tools/services properly configured]
- [ ] [User receives clear confirmation]

## Integration Notes

### Related Skills
- `/related-skill-1`: [How it relates and when to use]
- `/related-skill-2`: [How it relates and when to use]
```

### Step 3: Save Skill & Review

1. **Save skill file to**:
   - `.claude/skills/<skill-name>/SKILL.md`
   - Create the directory if needed
   - The skill becomes invokable as `/<skill-name>` and auto-discoverable via its `description` field

2. **Ask for focused feedback**:
   ```
   Skill created at: .claude/skills/<skill-name>/SKILL.md

   This skill includes:
   - Frontmatter with trigger description (so Claude can auto-invoke it)
   - Complete workflow automation instructions
   - Step-by-step procedural guidance
   - Error handling and validation requirements
   - Testing and integration guidance

   Quick check:
   - Does the description accurately describe when to trigger this skill?
   - Does this accurately capture the workflow you want to automate?
   - Any missing steps or edge cases?
   - Are the error scenarios covered?
   - Ready to test the skill or need adjustments?
   ```

3. **Next steps guidance**:
   ```
   Your skill is ready to use! Next steps:

   1. Test the skill:
      - Try invoking `/<skill-name>` directly
      - Try a natural-language phrase that should trigger the description
      - Verify each test case works as expected
      - Confirm error handling works as designed
      - Check output matches expectations

   2. Document in CLAUDE.md (optional):
      - Add the skill to your agent's Suggested Skills section
      - Include usage examples and description

   Would you like me to help test the skill or update CLAUDE.md?
   ```

## Conversation Guidelines

### Be Conversational & Collaborative
- Ask open-ended questions to understand the workflow
- Build on the user's process knowledge
- Use "How do you currently..." framing to understand existing workflows
- Acknowledge complexity and explore edge cases together
- Ask for user feedback often! Process design is iterative

### Probe for Procedural Detail
- Ask "What happens next?" to map the complete workflow
- Explore failure scenarios: "What if this step fails?"
- Identify decision points: "When do you choose between options?"
- Uncover implicit knowledge: "What do you just know to do?"

### Stay Automation-Focused
- Always bring conversation back to what can be automated
- Distinguish between steps requiring user input vs. fully automated
- Question overly complex workflows: "Could we simplify this?"
- Explore how users would discover and trust the automation

### Consider Skill Design
- How does this fit with existing skills?
- Does this follow skill naming conventions (kebab-case, verb-noun)?
- Is the `description` field specific enough that Claude will trigger it at the right time and only the right time?
- What's the right level of abstraction?
- Should this be one skill or multiple?

## Quality Checklist

Before finalizing the skill:

- [ ] Frontmatter has `name` (kebab-case) and `description` (trigger-focused, specific)
- [ ] `description` includes example trigger phrases and disambiguates from similar skills
- [ ] Clear workflow description that explains the automation value
- [ ] Complete step-by-step procedural requirements
- [ ] All arguments and inputs defined with validation rules
- [ ] Error scenarios identified with handling strategies
- [ ] Success criteria and test cases specified
- [ ] File paths and tool requirements documented
- [ ] Platform-specific considerations noted
- [ ] Integration with related skills described
- [ ] Document follows template structure with proper metadata

## Common Patterns for Agent Skills

### Repository Initialization
- Use `gh repo create` with appropriate flags
- Always specify `--add-readme` to establish HEAD
- Clone to specific directory locations
- Initialize additional tools (git-butler, etc.)

### File Structure Creation
- Use absolute paths for cross-directory operations
- Add `.gitkeep` files to track empty directories
- Commit and push structural changes
- Validate directory creation before proceeding

### Tool Integration
- Verify tool availability before use
- Provide clear error messages for missing tools
- Document required tool versions
- Handle authentication requirements

### User Interaction
- Offer choices before making decisions
- Confirm destructive operations
- Provide clear success/failure feedback
- Suggest next steps after completion

## Guidelines for Success

### Focus on Reliability
- Cover normal workflow and common error cases
- Include validation after critical steps
- Provide rollback or recovery mechanisms
- Give clear error messages with actionable guidance

### Be Precise
- Specify exact commands with full syntax
- Include all required flags and parameters
- Document absolute vs relative path requirements
- Reference actual file paths and tool names

### Document Thoroughly
- Explain the "why" behind each step
- Note platform-specific behaviors
- Identify prerequisites clearly
- Provide usage examples

### Plan for Implementation
- Structure the skill clearly and logically
- Group related operations together
- Make decision points explicit
- Include testing guidance
