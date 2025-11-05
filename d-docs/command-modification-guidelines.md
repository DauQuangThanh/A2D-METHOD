# Agent & Workflow Customization Guidelines

**BMAD v6 - Update-Safe Customization System**

**Date**: 2025-11-05
**Version**: 6.0
**Framework**: BMAD v6 (BMad-CORE + BMad Method)

---

## Executive Summary

BMAD v6 provides an **update-safe customization system** that allows you to modify agents, workflows, and modules without touching core files. All customizations persist through updates via the `bmad/_cfg/` configuration directory.

**Key Principle**: Customize agents and workflows by editing YAML configuration files in `bmad/_cfg/`, not by modifying source files in `bmad/[module]/`. This ensures your customizations survive module updates.

**Customization Capabilities**:
- **Agent Customization**: Modify names, personas, menus, memories via `bmad/_cfg/agents/*.customize.yaml`
- **Workflow Editing**: Edit workflows using BMB workflows (`edit-agent`, `edit-workflow`, `edit-module`)
- **Module Configuration**: Configure settings via `bmad/[module]/config.yaml`
- **Custom Agents/Workflows**: Create new agents and workflows using BMB module

---

## Table of Contents

1. [BMAD v6 Architecture](#bmad-v6-architecture)
2. [Agent Customization System](#agent-customization-system)
3. [Workflow Customization](#workflow-customization)
4. [Module Configuration](#module-configuration)
5. [Step-by-Step Customization Guide](#step-by-step-customization-guide)
6. [Critical Design Rules](#critical-design-rules)
7. [Safe vs. High-Impact Changes](#safe-vs-high-impact-changes)
8. [Testing Checklist](#testing-checklist)
9. [Common Scenarios](#common-scenarios)
10. [BMB Workflows for Advanced Customization](#bmb-workflows-for-advanced-customization)

---

## BMAD v6 Architecture

### Module Structure

```
bmad/
├── core/              # Core framework (3 agents, 2 workflows, tasks, tools)
├── bmm/               # BMad Method (9 agents, 34 workflows, testing)
├── bmb/               # BMad Builder (1 agent, 11 workflows)
├── cis/               # Creative Intelligence Suite (5 agents, 5 workflows)
└── _cfg/              # 🎯 YOUR CUSTOMIZATIONS (update-safe)
    ├── agents/        # Agent customization files
    │   ├── bmm-dev.customize.yaml
    │   ├── bmm-pm.customize.yaml
    │   ├── core-bmad-master.customize.yaml
    │   └── [module]-[agent].customize.yaml
    ├── agent-manifest.csv        # All agents registry
    ├── workflow-manifest.csv     # All workflows registry
    ├── task-manifest.csv         # All tasks registry
    ├── tool-manifest.csv         # All tools registry
    └── manifest.yaml             # Global manifest config
```

### How Agents Work in BMAD v6

1. **Source Files**: Agents defined in `bmad/[module]/agents/[agent].md` (XML format)
2. **Customization Files**: Your overrides in `bmad/_cfg/agents/[module]-[agent].customize.yaml`
3. **Build Process**: Installer merges source + customization when deploying to IDE
4. **Deployment**: Final agent files deployed to `.claude/commands/bmad/[module]/agents/`
5. **Runtime**: IDE loads agent from deployment location

**Key Insight**: You never modify source files in `bmad/[module]/`. You only modify YAML files in `bmad/_cfg/`.

---

## Agent Customization System

### Customization File Location

**Pattern**: `bmad/_cfg/agents/[module]-[agent].customize.yaml`

**Examples**:
- `bmad/_cfg/agents/bmm-dev.customize.yaml` - Customize Dev agent
- `bmad/_cfg/agents/bmm-pm.customize.yaml` - Customize PM agent
- `bmad/_cfg/agents/core-bmad-master.customize.yaml` - Customize BMad Master
- `bmad/_cfg/agents/cis-brainstorming-coach.customize.yaml` - Customize Brainstorming Coach

### Customization File Structure

```yaml
# bmad/_cfg/agents/[module]-[agent].customize.yaml

# Override agent name
agent:
  metadata:
    name: ""  # Example: "Amelia" → "Amy" or "Senior Dev"

# Replace entire persona (not merged - complete replacement)
persona:
  role: ""  # Example: "Senior Implementation Engineer"
  identity: ""  # Agent's background and expertise
  communication_style: ""  # How agent communicates
  principles: []  # List of operating principles

# Add custom critical actions (appended after standard config loading)
critical_actions: []
# Example:
# critical_actions:
#   - "Always check for security vulnerabilities"
#   - "Run tests before committing code"

# Add persistent memories for the agent
memories: []
# Example:
# memories:
#   - "User prefers detailed technical explanations"
#   - "Current project uses React and TypeScript"

# Add custom menu items (appended to base menu)
# Don't include * prefix or help/exit - auto-injected
menu: []
# Example:
# menu:
#   - trigger: my-workflow
#     workflow: "{project-root}/custom/my-workflow.yaml"
#     description: My custom workflow
#   - trigger: quick-fix
#     action: "#quick-fix-prompt"
#     description: Quick bug fix helper

# Add custom prompts (for action="#id" handlers)
prompts: []
# Example:
# prompts:
# - id: quick-fix-prompt
#   content: |
#     You are a quick bug fix specialist.
#     Analyze the code and suggest minimal fix.
```

### What Can Be Customized

| Element             | Customizable             | How                           | Example                         |
| ------------------- | ------------------------ | ----------------------------- | ------------------------------- |
| Agent Name          | ✅ Yes                    | `agent.metadata.name`         | "Amelia" → "Amy"                |
| Agent Role          | ✅ Yes                    | `persona.role`                | "Developer" → "Senior Engineer" |
| Agent Identity      | ✅ Yes                    | `persona.identity`            | Change background/expertise     |
| Communication Style | ✅ Yes                    | `persona.communication_style` | "Succinct" → "Verbose"          |
| Principles          | ✅ Yes                    | `persona.principles[]`        | Add/replace principles          |
| Critical Actions    | ✅ Yes (append)           | `critical_actions[]`          | Add startup actions             |
| Memories            | ✅ Yes (append)           | `memories[]`                  | Add persistent context          |
| Menu Items          | ✅ Yes (append)           | `menu[]`                      | Add custom workflows            |
| Custom Prompts      | ✅ Yes (append)           | `prompts[]`                   | Add inline actions              |
| Base Workflows      | ❌ No (use edit-workflow) | BMB workflows                 | Edit workflow source            |

---

## Workflow Customization

### Three Approaches to Workflow Customization

#### 1. Edit Existing Workflow (BMB Module)

**Use when**: You want to modify an existing BMAD workflow

```bash
# Edit workflow using BMB
Load BMad Builder agent, then run: *edit-workflow

# Workflow guides you through editing:
# - instructions.md (workflow steps)
# - template.md (output template)
# - checklist.md (validation checklist)
# - workflow.yaml (configuration)
```

**Location**: Source files in `bmad/[module]/workflows/[workflow-name]/`

**Safe to edit**:
- `instructions.md` - Workflow instructions
- `template.md` - Output document template
- `checklist.md` - Validation checklist
- `workflow.yaml` - Configuration variables

**After editing**: Reinstall module or rebuild

#### 2. Create Custom Workflow (BMB Module)

**Use when**: You want to create a new workflow

```bash
# Create new workflow using BMB
Load BMad Builder agent, then run: *create-workflow

# Workflow guides you through:
# - Brainstorming workflow idea (optional)
# - Designing workflow structure
# - Creating workflow files
# - Validating workflow quality
```

**Output**: New workflow in your project or `bmad/[module]/workflows/`

#### 3. Add Workflow to Agent Menu (Customization File)

**Use when**: You want to add a custom workflow to an agent's menu

```yaml
# In bmad/_cfg/agents/bmm-dev.customize.yaml
menu:
  - trigger: my-workflow
    workflow: "{project-root}/custom/my-workflow.yaml"
    description: My custom development workflow
```

**After editing**: Rebuild agent with `npx bmad-method build dev`

---

## Module Configuration

### Configuration Hierarchy

```
1. Core Config (bmad/core/config.yaml)
   └─ Global settings: user_name, communication_language, output_folder

2. Module Config (bmad/[module]/config.yaml)
   └─ Module-specific + inherits core settings

3. Agent Customization (bmad/_cfg/agents/[module]-[agent].customize.yaml)
   └─ Agent-specific overrides

4. Runtime Context
   └─ Workflow variables, session state
```

### Core Configuration (bmad/core/config.yaml)

**Safe to edit**:
```yaml
user_name: "Your Name"           # Agent uses this to address you
communication_language: "English"  # Agent communication language
document_output_language: "English"  # Output document language
output_folder: "{project-root}/docs"  # Where to save artifacts
```

**Impact**: Changes affect all modules (unless overridden)

### BMM Configuration (bmad/bmm/config.yaml)

**Safe to edit**:
```yaml
project_name: "My Project"
include_game_planning: false  # Enable game dev agents
user_skill_level: "intermediate"  # beginner, intermediate, expert
tech_docs: "{project-root}/docs"
dev_story_location: "{project-root}/docs/stories"
tea_use_mcp_enhancements: false  # Enable MCP for TEA workflows

# Core values (inherited from core/config.yaml)
user_name: "Your Name"
communication_language: "English"
document_output_language: "English"
output_folder: "{project-root}/docs"
```

**Impact**: Changes affect BMM module only

### BMB Configuration (bmad/bmb/config.yaml)

**Safe to edit**:
```yaml
custom_agent_location: "{project-root}/bmad/agents"
custom_workflow_location: "{project-root}/bmad/workflows"
custom_module_location: "{project-root}/bmad"

# Core values (inherited)
user_name: "Your Name"
communication_language: "English"
document_output_language: "English"
output_folder: "{project-root}/docs"
```

**Impact**: Changes affect where BMB creates custom agents/workflows

---

## Step-by-Step Customization Guide

### Scenario 1: Customize Agent Name and Personality

**Goal**: Change Dev agent name from "Amelia" to "Alex" and make more verbose

**Steps**:

1. **Edit customization file**:
   ```bash
   # Open file
   vim bmad/_cfg/agents/bmm-dev.customize.yaml
   # Or use your preferred editor
   ```

2. **Add customizations**:
   ```yaml
   # Override agent name
   agent:
     metadata:
       name: "Alex"

   # Replace persona
   persona:
     role: "Senior Full-Stack Engineer"
     identity: "I'm Alex, a senior engineer with 10+ years experience in web development. I specialize in React, Node.js, and database design."
     communication_style: "Detailed and educational. I explain my reasoning and provide context for technical decisions."
     principles:
       - "I write clean, maintainable code with comprehensive tests"
       - "I explain technical decisions and trade-offs clearly"
       - "I prioritize security and performance in every implementation"
       - "I follow established architecture patterns and coding standards"
   ```

3. **Rebuild agent**:
   ```bash
   npx bmad-method build dev
   ```

4. **Test**:
   ```bash
   # Load Dev agent in your IDE
   # Verify:
   # - Agent introduces itself as "Alex"
   # - Communication style is more verbose
   # - Menu still shows standard workflows
   ```

**Files Modified**: 1
**Time**: 10 minutes
**Risk**: Very low (easy to revert)

---

### Scenario 2: Add Custom Workflow to Agent Menu

**Goal**: Add a custom code review workflow to Dev agent

**Steps**:

1. **Create custom workflow** (using BMB):
   ```bash
   # Load BMad Builder agent
   # Run: *create-workflow
   # Follow prompts to create: custom/quick-review.yaml
   ```

2. **Edit customization file**:
   ```yaml
   # In bmad/_cfg/agents/bmm-dev.customize.yaml
   menu:
     - trigger: quick-review
       workflow: "{project-root}/custom/quick-review.yaml"
       description: Quick code review (5 minutes)
   ```

3. **Rebuild agent**:
   ```bash
   npx bmad-method build dev
   ```

4. **Test**:
   ```bash
   # Load Dev agent
   # Menu now shows additional item:
   # 6. *quick-review - Quick code review (5 minutes)
   ```

**Files Modified**: 2 (workflow YAML + customization file)
**Time**: 30-45 minutes (including workflow creation)
**Risk**: Low

---

### Scenario 3: Add Persistent Memories to Agent

**Goal**: Make PM agent remember your product preferences

**Steps**:

1. **Edit customization file**:
   ```yaml
   # In bmad/_cfg/agents/bmm-pm.customize.yaml
   memories:
     - "User prefers minimal viable products (MVP) approach"
     - "Current product targets B2B SaaS market"
     - "User values data-driven decision making"
     - "Product follows mobile-first design philosophy"
   ```

2. **Rebuild agent**:
   ```bash
   npx bmad-method build pm
   ```

3. **Test**:
   ```bash
   # Load PM agent
   # Run: *prd
   # Agent should reference your preferences in PRD creation
   ```

**Files Modified**: 1
**Time**: 5 minutes
**Risk**: Very low

---

### Scenario 4: Change Module Configuration

**Goal**: Change output folder for all BMM artifacts to `docs/bmm/`

**Steps**:

1. **Edit module config**:
   ```yaml
   # In bmad/bmm/config.yaml
   output_folder: "{project-root}/docs/bmm"
   ```

2. **Rebuild module** (or just use - changes take effect on next workflow run):
   ```bash
   npx bmad-method build
   # Or: npx bmad-method install (reinstall)
   ```

3. **Test**:
   ```bash
   # Run any BMM workflow (e.g., *prd)
   # Verify output goes to docs/bmm/PRD.md
   ```

**Files Modified**: 1
**Time**: 2 minutes
**Risk**: Low (only affects output location)

---

### Scenario 5: Enable Game Development Agents

**Goal**: Enable game dev agents (Game Designer, Game Developer, Game Architect)

**Steps**:

1. **Edit BMM config**:
   ```yaml
   # In bmad/bmm/config.yaml
   include_game_planning: true  # Change from false to true
   ```

2. **Reinstall BMM module**:
   ```bash
   npx bmad-method@alpha install
   # Select BMM module to reinstall
   ```

3. **Test**:
   ```bash
   # Check agent-manifest.csv
   # Should now show game dev agents

   # Run: /bmad:bmm:workflows:narrative
   # Game Designer agent should be available
   ```

**Files Modified**: 1
**Time**: 5 minutes + reinstall time
**Risk**: Low

---

### Scenario 6: Multi-Language Configuration

**Goal**: Communicate in English but output documents in Spanish

**Steps**:

1. **Edit core or module config**:
   ```yaml
   # In bmad/core/config.yaml (affects all modules)
   communication_language: "English"
   document_output_language: "Spanish"
   ```

2. **Rebuild or restart**:
   ```bash
   # Changes take effect on next workflow run
   # Or rebuild: npx bmad-method build
   ```

3. **Test**:
   ```bash
   # Load any agent
   # Agent communicates in English
   # Run: *prd
   # PRD.md should be in Spanish
   ```

**Files Modified**: 1
**Time**: 2 minutes
**Risk**: Very low

---

## Critical Design Rules

### Rule 1: Never Modify Source Files Directly

**CRITICAL**: Do NOT edit files in `bmad/[module]/agents/` or `bmad/[module]/workflows/` directly unless you're contributing to BMAD itself.

✅ **Correct**:
```bash
# Edit customization file
vim bmad/_cfg/agents/bmm-dev.customize.yaml

# Rebuild agent
npx bmad-method build dev
```

❌ **Wrong**:
```bash
# DON'T edit source file
vim bmad/bmm/agents/dev.md  # ❌ Changes lost on update!
```

**Why**: Module updates overwrite source files but preserve `bmad/_cfg/`.

---

### Rule 2: Customization File Naming Convention

**Pattern**: `[module]-[agent].customize.yaml`

**Examples**:
- `bmm-dev.customize.yaml` (BMM module, dev agent)
- `core-bmad-master.customize.yaml` (Core module, bmad-master agent)
- `cis-brainstorming-coach.customize.yaml` (CIS module, brainstorming-coach agent)

**Module Prefixes**:
- `core-` - Core module agents
- `bmm-` - BMM module agents
- `bmb-` - BMB module agents
- `cis-` - CIS module agents

---

### Rule 3: Persona Replacement vs Merging

**Important**: When you customize `persona`, you REPLACE the entire persona, not merge.

```yaml
# This REPLACES entire persona
persona:
  role: "My Custom Role"
  identity: "My custom identity"
  communication_style: "My style"
  principles:
    - "My principle 1"
    - "My principle 2"
```

**Implication**: If you customize persona, you must include ALL fields you want (role, identity, communication_style, principles).

**Alternative (Partial Customization)**: If you only want to add memories or menu items without changing persona, leave `persona:` empty and use `memories:` or `menu:` only.

---

### Rule 4: Menu Item Triggers

**Format**: Use trigger name without asterisk (*) in YAML

```yaml
# Correct
menu:
  - trigger: my-workflow  # No asterisk
    workflow: "path/to/workflow.yaml"
    description: Description

# Wrong
menu:
  - trigger: *my-workflow  # ❌ Don't include asterisk
    workflow: "path/to/workflow.yaml"
```

**Why**: The asterisk (*) is added automatically when displaying the menu.

---

### Rule 5: Rebuild After Customization

**Always rebuild after editing customization files**:

```bash
# Rebuild specific agent
npx bmad-method build dev

# Rebuild all agents
npx bmad-method build

# Rebuild and reinstall (if structure changed)
npx bmad-method@alpha install
```

**Why**: Customization files are merged at build time, not runtime.

---

## Safe vs. High-Impact Changes

### Minimal Impact (Safe to Change)

These changes only affect agent behavior, not structure:

✅ **Agent name** (`agent.metadata.name`)
✅ **Agent persona** (role, identity, communication_style)
✅ **Agent principles** (operating guidelines)
✅ **Agent memories** (persistent context)
✅ **Additional menu items** (append custom workflows)
✅ **Module config values** (user_name, languages, output_folder)

**Risk Level**: Low
**Testing Required**: Load agent, verify changes
**Rollback**: Easy (revert YAML, rebuild)

---

### Medium Impact (Use Caution)

These changes affect workflow behavior:

⚠️ **Editing workflow instructions** (instructions.md)
⚠️ **Modifying workflow templates** (template.md)
⚠️ **Changing workflow config** (workflow.yaml variables)
⚠️ **Updating workflow checklists** (checklist.md)

**Risk Level**: Medium
**Testing Required**: Run workflow end-to-end
**Rollback**: Moderate (restore workflow files)

**Recommendation**: Use BMB workflows (edit-workflow) for safer editing

---

### High Impact (Dangerous - Experts Only)

These changes affect core architecture:

🚫 **Changing agent XML structure** in source files
🚫 **Modifying workflow.xml** (core workflow engine)
🚫 **Altering module structure** (folders, organization)
🚫 **Changing manifest formats** (CSV, YAML structure)
🚫 **Modifying build/install scripts**

**Risk Level**: High
**Testing Required**: Comprehensive testing + backup
**Rollback**: Difficult (may require reinstall)

**Recommendation**: Only do this if contributing to BMAD core development

---

## Testing Checklist

### After Customizing an Agent

Use this checklist to verify your changes:

#### 1. Configuration Testing

- [ ] Customization file is valid YAML (no syntax errors)
- [ ] File follows naming convention: `[module]-[agent].customize.yaml`
- [ ] All YAML fields are spelled correctly
- [ ] File is in `bmad/_cfg/agents/` directory

#### 2. Build Testing

```bash
# Rebuild agent
npx bmad-method build [agent-name]
```

- [ ] Build completes without errors
- [ ] No YAML parsing errors
- [ ] Agent file deployed to IDE (`.claude/commands/bmad/`)

#### 3. Agent Loading Testing

- [ ] Agent loads in IDE without errors
- [ ] Agent displays customized name (if changed)
- [ ] Agent uses customized persona (if changed)
- [ ] Menu shows all items (base + custom)

#### 4. Workflow Execution Testing

- [ ] Run base workflow (e.g., *dev-story)
- [ ] Workflow executes correctly
- [ ] Agent behavior reflects customizations
- [ ] Output documents use correct language

#### 5. Custom Menu Testing (if custom menu items added)

- [ ] Custom menu items appear in agent menu
- [ ] Custom workflows execute correctly
- [ ] Custom actions work as expected

#### 6. Memory Testing (if memories added)

- [ ] Agent references memories in responses
- [ ] Memories persist across workflow executions
- [ ] Memories are context-appropriate

---

## Common Scenarios

### Scenario 1: Make Agent More Concise

**Goal**: Make Architect agent more brief and less verbose

**File**: `bmad/_cfg/agents/bmm-architect.customize.yaml`

```yaml
persona:
  role: "System Architect"
  identity: "Expert in technical architecture and system design."
  communication_style: "Brief and to-the-point. Bullet points preferred. Technical jargon OK."
  principles:
    - "Communicate concisely with minimal explanation"
    - "Focus on key decisions, skip background"
    - "Use bullet points over paragraphs"
```

**Result**: Architect agent now communicates more briefly

---

### Scenario 2: Add Company-Specific Standards

**Goal**: Make all agents aware of company coding standards

**Multiple Files**: Add memories to relevant agents

```yaml
# bmad/_cfg/agents/bmm-dev.customize.yaml
memories:
  - "Company uses React 18+ with TypeScript for all frontend"
  - "Company requires 80% test coverage minimum"
  - "Company follows Airbnb JavaScript style guide"
  - "All PRs require security review for auth/payment code"

# bmad/_cfg/agents/bmm-architect.customize.yaml
memories:
  - "Company uses microservices architecture with REST APIs"
  - "Company requires PostgreSQL for primary data storage"
  - "Company uses Redis for caching and sessions"
```

**Result**: Agents automatically apply company standards

---

### Scenario 3: Change Output Location

**Goal**: Save all artifacts to `documentation/` instead of `docs/`

**File**: `bmad/core/config.yaml` (affects all modules)

```yaml
output_folder: "{project-root}/documentation"
```

**OR** per module:

```yaml
# bmad/bmm/config.yaml
output_folder: "{project-root}/documentation/bmm"

# bmad/cis/config.yaml
output_folder: "{project-root}/documentation/cis"
```

**Result**: All workflows save to new location

---

### Scenario 4: Add Quick Action to Agent

**Goal**: Add a "quick bug triage" action to Dev agent

**File**: `bmad/_cfg/agents/bmm-dev.customize.yaml`

```yaml
# Add custom menu item with inline action
menu:
  - trigger: bug-triage
    action: "#bug-triage-prompt"
    description: Quick bug triage and analysis

# Add custom prompt
prompts:
  - id: bug-triage-prompt
    content: |
      You are performing a quick bug triage.

      Ask the user for:
      1. Bug description
      2. Steps to reproduce
      3. Expected vs actual behavior

      Then provide:
      - Severity assessment (Critical/High/Medium/Low)
      - Likely root cause
      - Recommended fix approach
      - Estimated effort
```

**Rebuild**: `npx bmad-method build dev`

**Result**: Dev agent menu now has `*bug-triage` option

---

### Scenario 5: Create Team-Specific Agent Variant

**Goal**: Create a specialized "Backend Dev" variant of Dev agent

**Approach**: Use BMB to create custom agent

```bash
# Load BMad Builder agent
# Run: *create-agent

# Follow prompts:
# - Agent name: "backend-dev"
# - Based on: "bmm-dev" (hybrid agent)
# - Specialization: Backend development
# - Additional expertise: Databases, APIs, microservices
```

**Result**: New agent in `bmad/agents/backend-dev.md` with specialized focus

---

## BMB Workflows for Advanced Customization

### Using BMad Builder for Advanced Changes

BMAD v6 includes BMad Builder (BMB) module with specialized workflows for safe customization:

#### 1. Edit Agent Workflow

```bash
# Load BMad Builder agent
# Run: *edit-agent

# Workflow guides you through:
# - Select agent to edit
# - Choose what to customize (persona, menu, etc.)
# - Validate changes
# - Apply changes to customization file
# - Rebuild agent

# Safer than manual editing - validates as you go
```

**Use when**: You want guided agent customization with validation

---

#### 2. Edit Workflow Workflow

```bash
# Load BMad Builder agent
# Run: *edit-workflow

# Workflow guides you through:
# - Select workflow to edit
# - Choose what to modify (instructions, template, config)
# - Validate changes
# - Apply changes
# - Test workflow

# Ensures workflow remains valid
```

**Use when**: You want to modify workflow behavior safely

---

#### 3. Create Agent Workflow

```bash
# Load BMad Builder agent
# Run: *create-agent

# Workflow guides you through:
# - Brainstorm agent concept (optional)
# - Define agent persona
# - Design command structure
# - Create agent files
# - Validate agent structure

# Three agent types:
# - Full Module Agent (complete persona + commands)
# - Hybrid Agent (shared core + module extensions)
# - Standalone Agent (independent specialized purpose)
```

**Use when**: Creating entirely new specialized agents

---

#### 4. Create Workflow Workflow

```bash
# Load BMad Builder agent
# Run: *create-workflow

# Workflow guides you through:
# - Brainstorm workflow idea (optional)
# - Design workflow structure
# - Create workflow files (instructions, template, checklist, config)
# - Validate workflow quality
# - Deploy workflow

# Ensures best practices and structure
```

**Use when**: Creating custom workflows for your domain

---

#### 5. Audit Workflow Quality

```bash
# Load BMad Builder agent
# Run: *audit-workflow

# Workflow performs comprehensive audit:
# - Validates workflow.yaml structure
# - Checks config standards compliance
# - Detects bloat and inefficiencies
# - Validates web_bundle completeness
# - Ensures BMAD v6 standards

# Get quality report and recommendations
```

**Use when**: Ensuring workflow quality before deployment

---

## Advanced Customization Techniques

### Technique 1: Agent Inheritance Pattern

**Goal**: Create multiple variants of Dev agent for different tech stacks

**Approach**: Multiple customization files with different specializations

```yaml
# bmad/_cfg/agents/bmm-dev-frontend.customize.yaml
agent:
  metadata:
    name: "Frontend Dev"

persona:
  role: "Frontend Specialist"
  identity: "Expert in React, Vue, and modern frontend frameworks"
  communication_style: "Technical, UX-aware"
  principles:
    - "Mobile-first responsive design"
    - "Accessibility is non-negotiable"
    - "Component reusability over duplication"

memories:
  - "Project uses React 18 with TypeScript"
  - "UI library: Material-UI"
  - "State management: Redux Toolkit"
```

```yaml
# bmad/_cfg/agents/bmm-dev-backend.customize.yaml
agent:
  metadata:
    name: "Backend Dev"

persona:
  role: "Backend Specialist"
  identity: "Expert in APIs, databases, and server-side architecture"
  communication_style: "Technical, performance-focused"
  principles:
    - "API design follows REST best practices"
    - "Database normalization and optimization"
    - "Security-first approach"

memories:
  - "Project uses Node.js with Express"
  - "Database: PostgreSQL 16"
  - "Authentication: JWT with refresh tokens"
```

**Build**: Create two separate agent variants

**Result**: Two specialized agents for different purposes

---

### Technique 2: Workflow Chains via Menu

**Goal**: Create a quick-start menu that chains multiple workflows

**File**: `bmad/_cfg/agents/bmm-analyst.customize.yaml`

```yaml
menu:
  - trigger: quick-start
    action: "#quick-start-chain"
    description: Quick start new project (chains workflows)

prompts:
  - id: quick-start-chain
    content: |
      Execute the following workflows in sequence:

      1. Run workflow-init
      2. If Quick Flow: Run tech-spec
      3. If BMad Method: Run prd → create-epics-and-stories
      4. Run sprint-planning

      Ask user for confirmation before each step.
      Report progress after each workflow.
```

**Result**: One menu item that runs multiple workflows in sequence

---

### Technique 3: Domain-Specific Agent Customization

**Goal**: Customize agents for healthcare domain

```yaml
# bmad/_cfg/agents/bmm-pm.customize.yaml
memories:
  - "Healthcare domain requires HIPAA compliance"
  - "All patient data must be encrypted at rest and in transit"
  - "Audit logging required for all PHI access"
  - "User consent required before data collection"

persona:
  principles:
    - "HIPAA compliance is non-negotiable in all features"
    - "Privacy and security are top priorities"
    - "All requirements must include compliance considerations"
```

```yaml
# bmad/_cfg/agents/bmm-architect.customize.yaml
memories:
  - "Healthcare architecture requires: audit logging, encryption, access control"
  - "PHI must never be in logs or error messages"
  - "All APIs must authenticate and authorize"

persona:
  principles:
    - "Design for HIPAA compliance from day one"
    - "Security architecture is mandatory, not optional"
    - "Audit trail for all PHI access"
```

**Result**: All agents automatically apply healthcare domain knowledge

---

## Troubleshooting

### Common Issues

#### Issue 1: Customization Not Applied

**Symptom**: Agent loads but customizations don't appear

**Causes & Solutions**:
1. **Not rebuilt**: Run `npx bmad-method build [agent]`
2. **YAML syntax error**: Validate YAML syntax
3. **Wrong file location**: Must be in `bmad/_cfg/agents/`
4. **Wrong file name**: Must match pattern `[module]-[agent].customize.yaml`

---

#### Issue 2: Build Fails

**Symptom**: `npx bmad-method build` fails with error

**Causes & Solutions**:
1. **YAML syntax error**: Check YAML indentation and colons
2. **Invalid workflow path**: Verify workflow path exists
3. **Missing module**: Ensure module is installed
4. **Corrupted customization file**: Check for special characters

---

#### Issue 3: Custom Menu Item Doesn't Work

**Symptom**: Menu item appears but doesn't execute

**Causes & Solutions**:
1. **Workflow path wrong**: Verify workflow file exists at specified path
2. **Missing action prompt**: If using `action: "#id"`, ensure prompt with that ID exists
3. **Invalid workflow.yaml**: Ensure custom workflow is valid BMAD workflow

---

#### Issue 4: Persona Not Changing

**Symptom**: Agent still uses default persona despite customization

**Causes & Solutions**:
1. **Incomplete persona**: Must include all fields (role, identity, communication_style, principles)
2. **Not rebuilt**: Run `npx bmad-method build [agent]`
3. **Wrong agent loaded**: Ensure you're loading the correct agent

---

## Best Practices

### When Customizing Agents

1. **Start small**: Change one thing at a time
2. **Test immediately**: Rebuild and test after each change
3. **Keep backups**: Save working configurations before major changes
4. **Document changes**: Add comments in YAML explaining why
5. **Share patterns**: If customization works well, share with team

---

### When Using BMB Workflows

1. **Use edit-agent** for complex changes (safer than manual editing)
2. **Use create-workflow** for new workflows (ensures best practices)
3. **Use audit-workflow** before deploying custom workflows
4. **Use edit-workflow** for modifying existing workflows
5. **Use create-module** for packaging complete solutions

---

### When Configuring Modules

1. **Core config first**: Set global defaults in `bmad/core/config.yaml`
2. **Module overrides**: Override in module config if needed
3. **Test after changes**: Verify workflows use new settings
4. **Document settings**: Comment why you changed defaults
5. **Version control**: Commit config changes separately

---

## Advanced Topics

### Creating Custom Module

For creating entirely custom modules with your own agents and workflows:

```bash
# Load BMad Builder agent
# Run: *create-module

# Workflow guides you through:
# - Module brief (strategy and vision)
# - Module structure
# - Agents creation
# - Workflows creation
# - Installation infrastructure
```

**Output**: Complete module in `bmad/[your-module]/`

---

### Converting Legacy v4 to v6

If you have BMAD v4 agents or workflows:

```bash
# Load BMad Builder agent
# Run: *convert-legacy

# Workflow converts:
# - v4 agents to v6 format
# - v4 workflows to v6 structure
# - Validates v6 compliance
```

**Output**: v6-compliant agents and workflows

---

### Autonomous Documentation System

For maintaining documentation:

```bash
# Load BMad Builder agent
# Run: *redoc

# Workflow:
# - Reverse-tree approach (leaf folders first)
# - Understands BMAD conventions
# - Produces technical writer quality output
# - Maintains module, workflow, and agent docs
```

**Output**: Comprehensive documentation

---

## File Reference

### Primary Customization Files

| File                                               | Purpose                | Modification Frequency |
| -------------------------------------------------- | ---------------------- | ---------------------- |
| `bmad/_cfg/agents/[module]-[agent].customize.yaml` | Agent customization    | High                   |
| `bmad/core/config.yaml`                            | Core global settings   | Medium                 |
| `bmad/bmm/config.yaml`                             | BMM module settings    | Medium                 |
| `bmad/bmb/config.yaml`                             | BMB module settings    | Low                    |
| `bmad/cis/config.yaml`                             | CIS module settings    | Low                    |
| `bmad/_cfg/manifest.yaml`                          | Global manifest config | Low                    |

### Source Files (Read-only for users)

| Directory                    | Purpose               | Modify Via                 |
| ---------------------------- | --------------------- | -------------------------- |
| `bmad/[module]/agents/*.md`  | Agent source files    | BMB edit-agent workflow    |
| `bmad/[module]/workflows/*/` | Workflow source files | BMB edit-workflow workflow |
| `bmad/[module]/config.yaml`  | Module configuration  | Direct edit (safe)         |

### Deployed Files (Auto-generated)

| Directory                         | Purpose                | Generated By            |
| --------------------------------- | ---------------------- | ----------------------- |
| `.claude/commands/bmad/`          | IDE command files      | Installer/build process |
| `bmad/_cfg/agent-manifest.csv`    | All agents registry    | Installer               |
| `bmad/_cfg/workflow-manifest.csv` | All workflows registry | Installer               |

---

## Architecture Decision Records

### ADR-001: Update-Safe Customization

**Status**: Accepted
**Date**: 2024-2025

**Context**: Users need to customize agents without losing changes on updates.

**Decision**: All customizations go in `bmad/_cfg/` directory, which is never overwritten by updates.

**Consequences**:
- ✅ Customizations survive updates
- ✅ Users can safely update modules
- ✅ Customizations are version-controllable
- ⚠️ Requires rebuild after customization

---

### ADR-002: YAML-Based Configuration

**Status**: Accepted
**Date**: 2024-2025

**Context**: Need structured, readable customization format.

**Decision**: Use YAML for all configuration and customization files.

**Consequences**:
- ✅ Human-readable and editable
- ✅ Supports complex nested structures
- ✅ Standard format with good tooling
- ⚠️ Requires YAML syntax knowledge

---

### ADR-003: Persona Replacement (Not Merge)

**Status**: Accepted
**Date**: 2024-2025

**Context**: Need clear customization behavior.

**Decision**: Customizing `persona` replaces entire persona (not merged).

**Consequences**:
- ✅ Clear, predictable behavior
- ✅ Full control over agent personality
- ⚠️ Must specify all persona fields if customizing
- ⚠️ Can't partially override individual principles

---

## Quick Reference

### Essential Commands

```bash
# Rebuild specific agent after customization
npx bmad-method build dev

# Rebuild all agents
npx bmad-method build

# Reinstall module (after structural changes)
npx bmad-method@alpha install

# Check installed agents
cat bmad/_cfg/agent-manifest.csv

# Check installed workflows
cat bmad/_cfg/workflow-manifest.csv
```

### Essential File Paths

```bash
# Agent customization files
bmad/_cfg/agents/[module]-[agent].customize.yaml

# Module configurations
bmad/core/config.yaml
bmad/bmm/config.yaml
bmad/bmb/config.yaml
bmad/cis/config.yaml

# Agent manifests
bmad/_cfg/agent-manifest.csv
bmad/_cfg/workflow-manifest.csv

# Deployed agents (IDE)
.claude/commands/bmad/[module]/agents/[agent].md
.claude/commands/bmad/[module]/workflows/[workflow].md
```

### Essential BMB Workflows

```bash
# Edit existing agent (guided)
/bmad:bmb:workflows:edit-agent

# Edit existing workflow (guided)
/bmad:bmb:workflows:edit-workflow

# Create new agent (guided)
/bmad:bmb:workflows:create-agent

# Create new workflow (guided)
/bmad:bmb:workflows:create-workflow

# Create new module (guided)
/bmad:bmb:workflows:create-module

# Audit workflow quality
/bmad:bmb:workflows:audit-workflow

# Convert legacy v4 to v6
/bmad:bmb:workflows:convert-legacy
```

---

## Summary

BMAD v6 provides multiple levels of customization:

**Level 1: Configuration** (Easiest)
- Edit `config.yaml` files
- Change names, languages, output locations
- No rebuild required (takes effect next run)

**Level 2: Agent Customization** (Easy)
- Edit `bmad/_cfg/agents/*.customize.yaml`
- Customize names, personas, menus, memories
- Rebuild required: `npx bmad-method build [agent]`

**Level 3: Workflow Editing** (Medium)
- Use BMB `edit-workflow` workflow
- Modify instructions, templates, checklists
- Guided validation ensures quality

**Level 4: Custom Creation** (Advanced)
- Use BMB `create-agent` and `create-workflow`
- Build domain-specific solutions
- Full BMAD v6 integration

**Key Success Factors**:
1. **Never edit source files** in `bmad/[module]/` directly
2. **Always use** `bmad/_cfg/` for customizations
3. **Rebuild after changes** with `npx bmad-method build`
4. **Use BMB workflows** for complex changes (safer than manual)
5. **Test thoroughly** using the testing checklist
6. **Keep backups** of working configurations

**Update-Safe Guarantee**: All customizations in `bmad/_cfg/` survive module updates.

---

**Version**: 6.0
**Last Updated**: 2025-01-05
**Framework**: BMAD v6 (BMad-CORE + BMad Method)
