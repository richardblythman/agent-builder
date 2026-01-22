# Init Agent Discovery

## Overview

Guide users through discovering their agent's purpose, workflow, pain points, and artifacts to design a memory structure and generate a starting CLAUDE.md. This command is for small org operators (startups, agencies, consultancies) building agents tailored to their specific workflows.

## Purpose & Value

### Workflow Being Automated

Setting up an agent requires understanding:
- **What** the agent solves (purpose, problem, success criteria)
- **How** work currently happens (workflow, stages, artifacts, completion signals)
- **What** frustrates users (pain points, inefficiencies, gaps)
- **What** gets created (artifacts, information, outputs)
- **How** to organize it (memory structure matching their mental model)
- **What** to automate (suggested commands to reduce friction)

This is discovery-based: we learn the user's specific workflow and synthesize it into a tailored memory structure and starting system prompt (CLAUDE.md).

### Time/Effort Savings

- Eliminates guesswork about what the agent should help with
- Ensures memory structure matches user's mental model and actual workflow
- Identifies automation opportunities (suggested commands)
- Creates templates matching discovered artifact types
- Produces a CLAUDE.md that accurately reflects the user's workflow

### Target Users

- Founders and operators at startups running their own agents
- Ops leads at small agencies/consultancies automating workflows
- Individual entrepreneurs building agents for their business
- Small teams wanting shared workflow agents
- Anyone bootstrapping an agent for their specific context

## Command Invocation

### Command Name
```
/init_agent_discovery
```

### Parameters

None required. This is a conversational discovery command.

### Usage Examples

```bash
# Start the agent discovery process
/init_agent_discovery
```

## Procedural Requirements

### Prerequisites

- User should have a general sense of what they want the agent to help with
- **The agent repository must already exist before running this command**
  - Assume the repository exists (use `/init_agent` first if needed)
  - Do NOT ask if they have a repository - assume they do
  - This command configures the agent's memory, not the repository itself

### Step-by-Step Workflow

---

#### Step 1: Understand Agent Purpose

**Purpose**: Establish why the agent exists and what problem it solves.

**Actions**:

1. Welcome the user and explain the process:

```
I'll help you set up your agent's memory structure and system prompt (CLAUDE.md) by discovering your actual workflow.

We'll work through:
1. Your agent's purpose and what it solves
2. How you currently do this work (the actual workflow)
3. What frustrates you about it (pain points)
4. What artifacts you create
5. How to organize memory based on that workflow
6. What commands could help automate the hard parts
7. Generate your memory structure and starting CLAUDE.md

Let's start by clarifying what this agent is for.
```

2. Ask about the agent's purpose:

```
**Tell me about the agent you're building:**

1. **What agent are you building? (What's its focus?)**
   - Examples: "A client intake agent", "A proposal writing agent", "A project tracking agent"

2. **Why does it exist?**
   - What problem does it solve for you?
   - Why do you want an agent for this?

3. **Who will use it?**
   - Who benefits? (just you? your team?)
   - What's their role?

4. **How will you know it's working?**
   - What outcomes would make this successful?
   - What changes when this agent is helping?
```

3. Wait for user response and capture their agent purpose.

**Validation**:
- User has identified a specific agent focus
- Problem is clear and solvable
- Success criteria are observable/measurable (or at least articulable)
- User has clarified primary beneficiary

**Error Handling**:
- If user is vague, ask for a concrete example: "Can you give me a specific example of when you'd use this agent?"
- If success criteria are unclear, probe: "What would be different if this agent was helping?"
- If multiple purposes, suggest focusing on the primary one first

---

#### Step 2: Workflow Discovery

**Purpose**: Map how work currently happens to understand the workflow, artifacts, and completion signals.

**Actions**:

1. Transition to workflow discovery:

```
Great! Now let's understand how you currently do this work.

I want you to walk me through a recent example - don't worry about using the "right" terminology, just describe what actually happened.
```

2. Ask about the workflow:

```
**Walk me through a recent example of this work:**

1. **What kicked it off?**
   - A request? A trigger? How does work start?

2. **What did you do to make progress?**
   - What were the concrete steps you took?
   - Are there phases or stages? (not looking for jargon, just what you actually do)

3. **What artifacts did you create?**
   - Documents? Spreadsheets? Notes? Reports? Emails? Proposals?
   - What information did you capture in each?

4. **How did you know it was done/successful?**
   - What signal or completion point told you this was finished?
   - How did you know if it went well?

5. **What was tedious, frustrating, or wasted time?**
   - What part took longest?
   - What part required the most thinking?
   - What part do you want to skip?
   - What gets lost or forgotten?
```

3. Wait for user response. Listen for:
   - **Workflow phases**: What are the concrete steps?
   - **Artifacts**: What gets created and stored?
   - **Information patterns**: What matters about each artifact?
   - **Pain points**: Where is friction?
   - **Completion signals**: How does work end?

**Validation**:
- User has described a concrete recent example (not generic description)
- Workflow has 3+ distinct phases/steps
- At least 2-3 artifacts identified
- Completion criteria are clear
- At least 1 pain point identified

**Error Handling**:
- If user gives generic answer, ask for specifics: "Can you walk me through something you did last week?"
- If workflow is ad-hoc, probe for patterns: "Even though each one is different, what do they all have in common?"
- If many artifacts, focus: "What are the 3 most important things you create?"
- If pain points are unclear, probe: "What takes the most time? What's error-prone?"

---

#### Step 3: Synthesize Workflow Understanding

**Purpose**: Verify understanding and identify the workflow structure.

**Actions**:

1. Synthesize and summarize:

```
Let me make sure I understand this correctly:

**What you told me:**
- Your work starts with: [trigger from discovery]
- The stages are: [Phase 1] → [Phase 2] → [Phase 3]
- You create these artifacts: [artifact1], [artifact2], [artifact3]
- You know it's done when: [completion signal]
- What's frustrating: [pain points]

**Am I understanding this right? What would you adjust?**
```

2. Wait for confirmation and refinement.

3. Ask clarifying questions only for gaps:

```
One more thing - help me understand the relationships:

**[Artifact A] and [Artifact B]:** Are these related? Does one lead to the other?

**[Phase 1] and [Phase 2]:** What happens between them? What triggers the move from one to the next?

**[Artifact C]:** You mentioned this gets created - does it belong in all [Phase X], or just specific ones?
```

**Validation**:
- User confirms the synthesized workflow is accurate
- Relationships between artifacts are clear
- Workflow phases are understood
- Any adjustments incorporated

---

#### Step 4: Discover Artifact Details & Hierarchy

**Purpose**: Understand what information matters in each artifact and how they relate (the natural hierarchy).

**Actions**:

1. Ask about each artifact specifically:

```
Now let's get specific about the artifacts you create.

You mentioned creating:
- [Artifact 1]
- [Artifact 2]
- [Artifact 3]

**For each one, I want to understand:**

**[Artifact Name]:**
- What information should every [artifact] include?
- Does this artifact exist on its own, or is it always part of something larger?
  - Example: "Every proposal is part of a client project"
- How often do you create these?
- Who creates/updates them? (just you? your team?)
- How long are they typically relevant?

[Repeat for each artifact]
```

2. Wait for detailed responses.

3. Ask about hierarchy and containment:

```
Now, let me understand how these fit together:

- Does [Artifact A] contain [Artifact B]? Or are they siblings?
- When you create [Artifact B], is it always within a [Artifact A]?
- Is there a top-level concept that organizes everything? (e.g., "Projects", "Clients", "Initiatives")

Draw it for me if helpful:
- Top level (what organizes everything?)
- Middle level (what sits within each top-level item?)
- Bottom level (the artifacts you create?)
```

4. Synthesize hierarchy:

```
Based on what you've described, here's the hierarchy I'm hearing:

memory/
├── {top-level-concept}/        # {Purpose from your workflow}
│   └── {mid-level-concept}/    # {Purpose from your workflow}
│       ├── {artifact}.md
│       └── {artifact}.md
└── README.md

**Does this match how you think about organizing your work?**

Would you adjust:
- The names of these levels?
- Add or remove a hierarchy level?
- The overall structure?
```

5. Confirm the hierarchy:

```
Great! Here's what we're building:

**Memory hierarchy:**
[Show confirmed structure]

**Artifacts in each level:**
| Level | Artifact | Key Information | How Often |
|-------|----------|-----------------|-----------|
| [Level] | [Name] | [What matters] | [Frequency] |

Does this look right?
```

**Validation**:
- All artifacts are accounted for and placed in hierarchy
- Containment relationships are explicit
- User confirms hierarchy matches their mental model
- Key information fields identified for each artifact type
- Hierarchy is natural and not forced

**Error Handling**:
- If hierarchy is unclear, ask containment questions: "Does X always contain Y?"
- If too many artifacts, suggest: "Let's focus on the main ones first - we can add more later"
- If hierarchy feels wrong, validate: "Does this feel like the right way to organize?"

---

#### Step 5: Identify Pain Points & Opportunities

**Purpose**: Map pain points to workflow phases to inform suggested commands.

**Actions**:

1. Probe each pain point:

```
You mentioned several frustrations earlier. Let me dig into them so I can suggest helpful commands.

For each one, I want to understand:
- When does this happen in your workflow?
- What specifically is frustrating?
- How much time/effort does it cost?
- What would make it better?

**Pain Point 1: [From Step 2]**
- When in your workflow does this happen? [Phase/artifact]
- What would an agent help with here?

**Pain Point 2: [From Step 2]**
- [Same questions]

[Repeat for each pain point]
```

2. Wait for responses.

3. Validate automation opportunities:

```
Based on what you've described, I see several things an agent could help with:

**[Pain Point] → Possible automation:**
- You spend time on [activity]
- An agent could [guide you through / automate / organize] this
- Would that help? How?

[Repeat for each pain point]

Which of these would be most valuable?
```

**Validation**:
- Each pain point is mapped to a workflow phase/artifact
- At least 1-2 clear automation opportunities identified
- User confirms which pain points matter most

---

#### Step 6: Suggest Commands

**Purpose**: Based on discovered workflow and pain points, suggest Claude Code commands for automation.

**Actions**:

1. Propose commands:

```
Based on your workflow and pain points, here are commands that could help:

**[Command 1: verb_noun format]** - [What it guides you through]
- Addresses: [Pain point from discovery]
- Would help with: [Specific activity]
- You'd use it when: [In which phase]
- Estimated time saved: [Your estimate from pain point discussion]

**[Command 2]** - [Description]
- [Same structure]

**[Command 3]** - [Description]
- [Same structure]

[Include 3-5 suggested commands, each addressing a discovered pain point]

**Which of these would be most useful?**
- All of them?
- Just a few?
- Any you'd want to adjust or add?
```

2. Wait for user to prioritize.

3. Confirm final command list:

```
Got it! Here's what you want to focus on:

**Priority commands to create:**
1. /[command] - [Why it matters]
2. /[command] - [Why it matters]
3. /[command] - [Why it matters]

After we set up your memory structure, you can create these one at a time using `/create_agent_command`.

You don't have to create them all immediately - start with the highest impact one.
```

**Validation**:
- Commands map to discovered pain points
- Command names follow convention (verb-noun, kebab-case)
- User has confirmed which commands would be most valuable
- User understands commands are suggestions for later creation

**Error Handling**:
- If user wants too many commands, suggest: "Let's start with the 2-3 most impactful - you can add more later"
- If suggested commands don't resonate, ask: "What would actually help? What's the hardest part?"

---

#### Step 7: Confirm Memory Structure & Generate Files

**Purpose**: Create the memory directory structure, templates, and starting CLAUDE.md.

**Actions**:

1. Final confirmation before generation:

```
Before I create everything, let me confirm:

**Memory structure:** [Show the hierarchy]
**Artifact types:** [List with key fields]
**Suggested commands:** [List prioritized commands]
**CLAUDE.md purpose:** [One-liner from Step 1]

Does this all look right? Any final adjustments?
```

2. Create directory structure:

```bash
# Create memory directory and subdirectories based on discovered hierarchy
memory/
├── {top-level}/
│   └── {mid-level}/
│       └── .gitkeep
└── README.md (created with index and structure explanation)

# Create templates directory
templates/
├── README.md (index of templates)
└── {artifact-type}.md (one per artifact type, discovery-based templates)
```

3. Create memory/README.md:

```markdown
# Memory Structure

## Overview

This is where your agent stores artifacts related to your [workflow type] work.

## Organization

Your artifacts are organized as:

\`\`\`
memory/
├── {top-level}/              # {Purpose}
│   └── {mid-level}/          # {Purpose}
│       ├── {artifact}.md
│       └── {artifact}.md
└── README.md
\`\`\`

## How to Use

1. **Create new artifacts:** Use templates from `templates/` to create new [artifact type]
2. **Place them correctly:** Store in `memory/{top-level}/{mid-level}/`
3. **Name consistently:** Use kebab-case for file names
4. **Keep updated:** Update artifacts as work progresses

## Current Artifacts

| Name | Type | Purpose | Status |
|------|------|---------|--------|
| — | — | — | — |

_Add artifacts as you create them_

## Example Workflow

[Brief description of how to use this structure for their specific workflow]
```

4. Create artifact templates in templates/:

For each artifact type discovered, create a template file (templates/{artifact-name}.md):

```markdown
# {Artifact Name}

## Overview
{One sentence description based on user's discovery}

## Key Information

**{Field 1}**: {What matters here from discovery}

**{Field 2}**: {What matters here from discovery}

**{Field 3}**: {What matters here from discovery}

## Status

- [ ] {Stage 1 from discovered workflow}
- [ ] {Stage 2 from discovered workflow}
- [ ] {Stage 3 from discovered workflow}

## Notes

{Any additional information that matters for this artifact}
```

5. Create templates/README.md:

```markdown
# Artifact Templates

## Overview

These templates help you create consistent artifacts for your workflow.

## Available Templates

| Template | Use For | Key Fields |
|----------|---------|-----------|
| [artifact-type] | [Purpose from discovery] | [Field1, Field2, Field3] |

## How to Use

1. Copy the relevant template
2. Save to `memory/{top-level}/{mid-level}/{name}.md`
3. Fill in the fields based on your current work
4. Update status as you progress

## Creating New Artifacts

When the agent asks to create a new [artifact], it will:
1. Ask you for the required information
2. Fill in the template
3. Save to the right location in memory

You can also manually create artifacts by copying a template and filling it in yourself.
```

6. Generate CLAUDE.md with discovered information:

```markdown
# {Agent Name}

A Claude Code agent that helps you {one-sentence description from Step 1: what problem it solves}.

## Purpose

This agent helps with: {Description of the workflow from Step 2}

**Jobs to Be Done:**
When {circumstance from discovery},
you want to {workflow action from discovery},
so that {success criterion from Step 1}.

**Success Criteria:**
- [Observable outcome 1 from Step 1]
- [Observable outcome 2 from Step 1]
- [Observable outcome 3 from Step 1]

## Memory Structure

The agent maintains memory organized by your workflow:

\`\`\`
memory/
├── {top-level}/              # {Purpose from discovery}
│   └── {mid-level}/          # {Purpose from discovery}
│       ├── {artifact1}.md
│       ├── {artifact2}.md
│       └── .gitkeep
└── README.md
\`\`\`

### Directory Purposes

- **memory/{top-level}/**: {Purpose based on discovery}
- **memory/{top-level}/{mid-level}/**: {Purpose based on discovery}

### File Naming Conventions

- Use kebab-case for all file and folder names (e.g., `client-proposal.md`, `project-timeline.md`)
- Name artifacts descriptively (e.g., `acme-corp-proposal.md` not `proposal-1.md`)

## Artifacts

This agent works with the following artifact types from your workflow:

| Artifact Type | Purpose | Key Fields | Frequency |
|---------------|---------|-----------|-----------|
| {artifact1} | {Purpose from discovery} | {Field1, Field2, Field3} | {Frequency} |
| {artifact2} | {Purpose from discovery} | {Field1, Field2, Field3} | {Frequency} |

### Using Templates

When creating a new {artifact type}:
1. Use the template from `templates/{artifact-name}.md`
2. Place in `memory/{appropriate-location}/`
3. Fill in required fields based on user input
4. Update status as work progresses

## Execution Flow

Based on your discovered workflow:

**Stages:**
1. **{Stage 1 from discovery}** - {What happens in this stage}
2. **{Stage 2 from discovery}** - {What happens in this stage}
3. **{Stage 3 from discovery}** - {What happens in this stage}

### Activities by Stage

| Stage | Activity | Artifact(s) | Notes |
|-------|----------|------------|-------|
| {Stage 1} | {Activity from discovery} | {artifact} | {Pain point addressed by suggested command} |
| {Stage 2} | {Activity from discovery} | {artifact} | {Pain point addressed by suggested command} |
| {Stage 3} | {Activity from discovery} | {artifact} | {Pain point addressed by suggested command} |

### Suggested Commands

Commands that would help automate parts of this workflow:

| Command | Purpose | Helps With | When to Use |
|---------|---------|-----------|------------|
| `/[command1]` | {What it guides you through} | {Pain point from Step 5} | {When you'd use it in the workflow} |
| `/[command2]` | {What it guides you through} | {Pain point from Step 5} | {When you'd use it in the workflow} |
| `/[command3]` | {What it guides you through} | {Pain point from Step 5} | {When you'd use it in the workflow} |

You can create these commands one at a time using `/create_agent_command`.

## Agent Capabilities

### Core Functions

- **Create artifacts**: Guide through creating new {artifact types} using templates
- **Track progress**: Update artifact status and track work through the workflow
- **Navigate memory**: Help find and reference existing artifacts
- **Maintain consistency**: Ensure artifacts follow templates and stay organized

### Common Commands (from user perspective)

- "Create a new {artifact type}" - Creates artifact using template in correct location
- "Show me all {artifacts}" - Lists artifacts from memory
- "Update [artifact name]" - Opens and updates an existing artifact
- "What's the status of [artifact]?" - Summarizes artifact status

## Workflows

### Creating a New {Primary Artifact Type}

1. User requests a new {artifact type}
2. Agent asks for required information: {list key fields}
3. Agent creates file at `memory/{path}/{name}.md` using template
4. Agent confirms creation with user

### {Workflow Phase 2}: {Description}

[Describe the workflow for this phase based on discovery]

### {Workflow Phase 3}: {Description}

[Describe the workflow for this phase based on discovery]

## Conventions

- Always use templates when creating new artifacts
- Maintain the memory structure - don't create files outside defined paths
- Use kebab-case for file and folder names
- Update artifact status as work progresses
- Keep memory/README.md updated as an index

---
```

7. Report what was created:

```
Your agent's memory structure and system prompt are ready!

**Files created:**
- CLAUDE.md - Your agent's system prompt (Purpose, Memory Structure, Artifacts, Execution Flow)
- memory/README.md - Index for your memory structure
- memory/{top-level}/ - Directories for your workflow
- templates/README.md - Index of artifact templates
- templates/{artifact-name}.md - Templates for each artifact type

**What's next:**

1. **Create your first artifact:**
   Ask the agent to create a new {artifact type}

2. **Create your first command:**
   Use `/create_agent_command` to build the highest-impact suggested command

3. **Test the workflow:**
   Use your new agent and command to see how it feels

4. **Iterate:**
   Refine CLAUDE.md, add more commands, adjust structure as needed

**Your suggested commands to create (in priority order):**
1. /[command] - [Why it matters]
2. /[command] - [Why it matters]
3. /[command] - [Why it matters]

You don't have to create all of them immediately - start with one!

Would you like help with any of these next steps?
```

**Validation**:
- All directories created successfully
- All template files created with correct content
- CLAUDE.md created with all discovered information
- memory/README.md created with structure explanation
- Suggested commands documented for future creation
- User understands next steps

**Error Handling**:
- If files already exist, ask: "I see these files already exist. Should I overwrite them or merge?"
- If directory creation fails, report error and suggest manual creation
- If user wants to skip templates, note: "You can always create them later using `/create_agent_command`"

---

#### Step 8: Confirmation & Next Steps

**Purpose**: Confirm success and guide user on next steps.

**Actions**:

```
Your agent's memory structure and system prompt are set up!

**Summary of what was created:**

Memory Structure:
\`\`\`
memory/
├── {your-hierarchy}
└── README.md
\`\`\`

CLAUDE.md:
- **Purpose**: {One-liner from Step 1}
- **Constitution**: Why the agent exists, core principles, boundaries
- **Specification**: Memory structure, artifacts, execution flow, suggested commands

Templates:
- {artifact-name}.md templates for consistency
- Available in `templates/`

**Next Steps (in order):**

1. **Test artifact creation**: Ask the agent to create a new {artifact type}
   - It will guide you through the template

2. **Create your first command**: Use `/create_agent_command` to build the highest-impact command
   - Start with: `/[top-priority-command]`
   - This is where the agent does most of the heavy lifting

3. **Populate memory**: Add your existing {artifacts} to the memory structure
   - Use templates for consistency

4. **Iterate**: As you use the agent, you'll refine CLAUDE.md and add more commands
   - CLAUDE.md Specification section will evolve
   - Constitution (Purpose, Principles) rarely changes

**Would you like to:**
- Create your first artifact now?
- Create your first command using `/create_agent_command`?
- Refine anything in CLAUDE.md?

The structure is ready - now it's about populating and refining it as you work!
```

---

## File Structure & Paths

### Files Created

```
{repo-root}/
├── CLAUDE.md                    # Agent system prompt (updated or created)
├── memory/
│   ├── README.md               # Memory index with structure explanation
│   └── {discovered-dirs}/      # Per discovered hierarchy
│       └── .gitkeep
└── templates/
    ├── README.md               # Template index
    └── {artifact-name}.md      # Template per artifact type
```

### Path Conventions

- **Repository root**: Command runs from repo root; all paths relative to there
- **Memory directory**: Always `memory/` at repo root
- **Templates directory**: Always `templates/` at repo root
- **File names**: kebab-case throughout (e.g., `client-proposal.md`, `project-summary.md`)
- **Directory names**: kebab-case and descriptive (e.g., `client-projects/`, `active-initiatives/`)

---

## Validation & Testing

### Success Criteria

- [ ] User has clarified agent purpose and success criteria
- [ ] User has described a concrete recent workflow example
- [ ] Workflow stages identified (3+ steps)
- [ ] Artifacts discovered and named (3+ types)
- [ ] Artifact hierarchy is natural and confirmed by user
- [ ] Pain points mapped to workflow phases
- [ ] Automation opportunities identified (3+ suggested commands)
- [ ] Memory directory structure created and matches discovered hierarchy
- [ ] Artifact templates created and in `templates/` directory
- [ ] CLAUDE.md generated with Constitution and Specification sections
- [ ] User understands next steps (create first artifact, create first command)

### Test Cases

1. **Simple workflow** (freelancer): Should produce flat or 2-level structure
2. **Agency workflow** (clients + projects): Should produce 2-3 level hierarchy
3. **Complex workflow** (multiple artifact types): Should synthesize natural hierarchy
4. **Ad-hoc work**: Should identify patterns and suggest structure
5. **With many pain points**: Should suggest 5+ commands for user to prioritize
6. **User uncertainty**: Should guide to specificity with concrete examples

---

## Conversation Guidelines

### Do:

- Ask for **concrete recent examples** when user is vague
- **Validate understanding** frequently: "So if I understand correctly..."
- Make it **concrete**: "For example, a proposal might be called..."
- Use **explicit examples** from their workflow in suggestions
- Ask **containment questions**: "Does X contain Y?"
- Ask **why** for pain points: "Why is that frustrating?"
- **Confirm before generating**: Show structure before creating files
- **Make it collaborative**: "Does this match how you think about it?"

### Don't:

- Prescribe structure (discover it)
- Apply pre-built frameworks
- Create files without confirmation
- Overwhelm with options (focus on what they described)
- Skip validation steps
- Suggest too many commands (prioritize high-impact)
- Create commands yet (just suggest them)
- Use jargon (stick to their language)

---

## Integration Notes

### Related Commands

- `/init_agent` - Use first if the agent repository doesn't exist
- `/create_agent_command` - Create suggested commands after setup
- `/create_claude_md` - Deep dive on CLAUDE.md if you want to refine further
- `/init_org_os` - If building a product framework agent (different purpose)

### Differences from init_org_os

- **init_org_os**: Discovers product frameworks (Lean, OKRs, EOS) - prescriptive frameworks
- **init_agent_discovery**: Discovers actual workflow - discovery-based, artifact-focused
- **init_org_os**: For teams operationalizing frameworks
- **init_agent_discovery**: For small org operators automating specific workflows

---

## Troubleshooting

### User Doesn't Know Their Workflow

**Problem**: User is unsure how to describe their work.

**Solution**: Ask for a concrete example:
```
"Can you walk me through something you did recently? What did you do first, then what, then what?"
```

### Workflow Is Very Ad-Hoc

**Problem**: Work seems completely different each time.

**Solution**: Identify patterns in variation:
```
"Even though each project is different, what do they all have in common?
What do you always do, regardless of the specifics?"
```

### Too Many Artifacts

**Problem**: User lists many different artifact types.

**Solution**: Prioritize top-level ones:
```
"Of all the things you create, which are the 3 most important? Let's start there."
```

### Hierarchy Is Unclear

**Problem**: Not sure whether artifacts are nested or siblings.

**Solution**: Use containment language:
```
"Does [Artifact A] contain [Artifact B], or are they at the same level?
Is [B] something you create per [A]?"
```

### No Clear Pain Points

**Problem**: User says work is fine and there's nothing frustrating.

**Solution**: Probe for efficiency:
```
"What takes the longest? What requires the most thinking?
What part would you most like to skip or automate?"
```

### User Wants to Skip Steps

**Problem**: User wants to jump to CLAUDE.md or skip discovery.

**Solution**: Explain why discovery matters:
```
"The discovery helps ensure the memory structure and CLAUDE.md match your actual workflow,
not just what we assume. It takes 10 minutes but saves weeks of misalignment."
```

---

## Key Implementation Notes

### Always Capture These

1. **Workflow trigger** - How work starts
2. **Workflow phases** - The stages work moves through
3. **Artifacts** - What gets created and stored
4. **Completion signals** - How do you know it's done?
5. **Pain points** - Where is the friction?

### Synthesis Is Critical

- Proposed structure should be based on discovered workflow, not templates
- Hierarchy should feel natural to user (not forced)
- Commands should address identified pain points (not generic)
- CLAUDE.md should reflect their specific context (not placeholder)

### User Confirmation Required

- [ ] Confirmed workflow understanding
- [ ] Confirmed artifact hierarchy
- [ ] Confirmed memory structure before file creation
- [ ] Confirmed which suggested commands matter most
- [ ] Confirmed CLAUDE.md captures their purpose

---

## Next Steps Documentation

After this command completes, the user should know:

1. **Memory structure is ready** - They can start creating artifacts
2. **Templates are available** - For consistency and guidance
3. **CLAUDE.md is their system prompt** - How the agent operates
4. **Suggested commands are notes** - They can create with `/create_agent_command`
5. **They should iterate** - Structure and CLAUDE.md evolve with use

Recommended workflow after initialization:

1. Create first artifact (test the templates)
2. Create one high-impact command (test the automation)
3. Use together (test the workflow)
4. Refine based on actual usage
5. Add more commands as needed
