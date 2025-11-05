# BMAD v6 Workflow-to-Role Matrix

**Complete Guide to Agent Roles, Workflows, and Responsibilities**

**Date**: 2025-11-05
**Version**: 6.0
**Project**: BMAD v6 (BMad-CORE + BMad Method)

---

## Executive Summary

BMAD v6 provides **19+ specialized agents** and **50+ workflows** across 4 modules (Core, BMM, BMB, CIS) that support different stages of AI-driven agile development. This document maps each workflow to specific roles (agents) and explains the purposes, timing, and use cases for each role.

**Key Principle**: Workflows are designed to support a complete scale-adaptive development lifecycle from quick bug fixes to enterprise-scale systems, with clear ownership and collaboration points.

**Three Planning Tracks**:
- **Quick Flow Track** (Levels 0-1): Tech-spec only - Bug fixes, small features
- **BMad Method Track** (Levels 2-4): PRD + Architecture + UX - Products, platforms
- **Enterprise Method Track**: Extended planning (BMad Method + Security/DevOps/Test)

---

## Table of Contents

1. [Workflow Overview](#workflow-overview)
2. [Agent Roster](#agent-roster)
3. [Role-Based Workflow Matrix](#role-based-workflow-matrix)
4. [Detailed Role Mappings](#detailed-role-mappings)
5. [Workflow Sequences](#workflow-sequences)
6. [Collaboration Patterns](#collaboration-patterns)
7. [Use Case Scenarios](#use-case-scenarios)

---

## Workflow Overview

### Available Workflows by Module

#### Core Module (2 workflows)
| Workflow                             | Purpose                                | Primary Agent | Output                  |
| ------------------------------------ | -------------------------------------- | ------------- | ----------------------- |
| `/bmad:core:workflows:party-mode`    | Multi-agent group discussions          | BMad Master   | Collaborative decisions |
| `/bmad:core:workflows:brainstorming` | Interactive brainstorming facilitation | BMad Master   | Ideas and insights      |

#### BMM Module - Phase 0: Documentation (1 workflow)
| Workflow                               | Purpose                                 | Primary Agent | Output                   |
| -------------------------------------- | --------------------------------------- | ------------- | ------------------------ |
| `/bmad:bmm:workflows:document-project` | Analyze and document existing codebases | Dev (Amelia)  | Repository documentation |

#### BMM Module - Phase 1: Analysis (4 workflows - Optional)
| Workflow                                 | Purpose                                            | Primary Agent  | Output                |
| ---------------------------------------- | -------------------------------------------------- | -------------- | --------------------- |
| `/bmad:bmm:workflows:brainstorm-project` | Project brainstorming                              | Analyst (Mary) | Brainstorming outputs |
| `/bmad:bmm:workflows:product-brief`      | Interactive product vision definition              | PM (John)      | Product brief         |
| `/bmad:bmm:workflows:research`           | Adaptive research (market, technical, competitive) | Analyst (Mary) | Research documents    |

#### BMM Module - Phase 2: Planning (6 workflows - Required)
| Workflow                                       | Purpose                                | Primary Agent       | Output                   |
| ---------------------------------------------- | -------------------------------------- | ------------------- | ------------------------ |
| `/bmad:bmm:workflows:workflow-init`            | Initialize project and determine track | Analyst (Mary)      | bmm-workflow-status.yaml |
| `/bmad:bmm:workflows:prd`                      | Product Requirements Document          | PM (John)           | PRD.md or prd/           |
| `/bmad:bmm:workflows:create-epics-and-stories` | Break PRD into epics/stories           | Analyst (Mary)      | bmm-epics.md or epics/   |
| `/bmad:bmm:workflows:tech-spec`                | Technical Specification (Quick Flow)   | Analyst (Mary)      | tech-spec.md             |
| `/bmad:bmm:workflows:narrative`                | Narrative design (games)               | Game Designer       | narrative.md             |
| `/bmad:bmm:workflows:create-ux-design`         | Collaborative UX design                | UX Designer (Sally) | UX-design.md             |

#### BMM Module - Phase 3: Solutioning (2 workflows - BMad Method Track)
| Workflow                                     | Purpose                            | Primary Agent       | Output            |
| -------------------------------------------- | ---------------------------------- | ------------------- | ----------------- |
| `/bmad:bmm:workflows:architecture`           | Architecture decision facilitation | Architect (Winston) | Architecture.md   |
| `/bmad:bmm:workflows:solutioning-gate-check` | Pre-implementation validation gate | Architect (Winston) | Validation report |

#### BMM Module - Phase 4: Implementation (10 workflows - Iterative)
| Workflow                                | Purpose                               | Primary Agent            | Output                      |
| --------------------------------------- | ------------------------------------- | ------------------------ | --------------------------- |
| `/bmad:bmm:workflows:workflow-status`   | Status checker and recommendations    | SM (Bob)                 | Status recommendations      |
| `/bmad:bmm:workflows:sprint-planning`   | Generate sprint status file           | SM (Bob)                 | bmm-workflow-status.yaml    |
| `/bmad:bmm:workflows:epic-tech-context` | Epic technical specification          | Analyst (Mary)           | Epic tech-spec              |
| `/bmad:bmm:workflows:story-context`     | Dynamic story context assembly        | Dev (Amelia)             | stories/[story].context.xml |
| `/bmad:bmm:workflows:create-story`      | Generate next user story              | SM (Bob)                 | stories/[story].md          |
| `/bmad:bmm:workflows:dev-story`         | Execute story implementation          | Dev (Amelia)             | Working code                |
| `/bmad:bmm:workflows:story-ready`       | Mark story ready (TODO → IN PROGRESS) | SM (Bob)                 | Status update               |
| `/bmad:bmm:workflows:story-done`        | Mark story done (→ DONE)              | SM (Bob)                 | Status update               |
| `/bmad:bmm:workflows:code-review`       | Senior developer code review          | Dev (Amelia) / Tech Lead | Review notes                |
| `/bmad:bmm:workflows:correct-course`    | Navigate mid-sprint changes           | SM (Bob)                 | Course correction plan      |
| `/bmad:bmm:workflows:retrospective`     | Post-epic review and lessons learned  | SM (Bob)                 | Retrospective notes         |

#### BMM Module - Testing Track (9 workflows - TEA Module)
| Workflow                                   | Purpose                                | Primary Agent | Output               |
| ------------------------------------------ | -------------------------------------- | ------------- | -------------------- |
| `/bmad:bmm:workflows:testarch:atdd`        | Acceptance Test-Driven Development     | TEA (Murat)   | ATDD tests           |
| `/bmad:bmm:workflows:testarch:test-design` | Test coverage strategy                 | TEA (Murat)   | Test design doc      |
| `/bmad:bmm:workflows:testarch:framework`   | Test framework initialization          | TEA (Murat)   | Test framework setup |
| `/bmad:bmm:workflows:testarch:automate`    | Test automation expansion              | TEA (Murat)   | Automated tests      |
| `/bmad:bmm:workflows:testarch:test-review` | Test quality review                    | TEA (Murat)   | Test review report   |
| `/bmad:bmm:workflows:testarch:trace`       | Requirements-to-tests traceability     | TEA (Murat)   | Traceability matrix  |
| `/bmad:bmm:workflows:testarch:nfr-assess`  | Non-functional requirements assessment | TEA (Murat)   | NFR assessment       |
| `/bmad:bmm:workflows:testarch:ci`          | CI/CD quality pipeline                 | TEA (Murat)   | CI/CD config         |

---

## Agent Roster

### Core Module (3 Agents)

**BMad Master** - Master orchestrator, knowledge custodian, workflow executor
- Executes: party-mode, brainstorming (Core)
- Role: Orchestration and coordination across all modules
- When to use: Strategic decisions, complex problem-solving, multi-agent coordination

### BMM Module (9 Core Agents + 3 Game Dev)

**Core Development Team:**

1. **Analyst (Mary)** - Strategic Requirements Expert, Business Analyst
   - Primary workflows: workflow-init, tech-spec, prd (support), create-epics-and-stories, epic-tech-context, brainstorm-project, product-brief (support), research
   - Role: Requirements analysis, story breakdown, project initialization
   - When to use: Starting projects, breaking down requirements, analysis

2. **PM (John)** - Product Manager, Strategic Product Leadership
   - Primary workflows: prd, product-brief
   - Secondary workflows: create-ux-design (review), brainstorm-project (support)
   - Role: Product vision, requirements definition, strategic direction
   - When to use: Defining products, strategic planning, product discovery

3. **Architect (Winston)** - System Architect, Technical Design Leader
   - Primary workflows: architecture, solutioning-gate-check
   - Secondary workflows: epic-tech-context (review), code-review (architecture compliance)
   - Role: Architecture decisions, technical design, quality gates
   - When to use: Designing systems, validating architecture, technical decisions

4. **SM (Bob)** - Scrum Master, Story Preparation Specialist
   - Primary workflows: sprint-planning, create-story, story-ready, story-done, workflow-status, correct-course, retrospective
   - Role: Sprint orchestration, story lifecycle, process facilitation
   - When to use: Sprint management, story tracking, process optimization

5. **Dev (Amelia)** - Senior Implementation Engineer
   - Primary workflows: dev-story, story-context, document-project
   - Secondary workflows: code-review (peer review)
   - Role: Implementation, code development, brownfield documentation
   - When to use: Coding, implementing stories, documenting codebases

6. **TEA (Murat)** - Master Test Architect
   - Primary workflows: All testarch/* workflows (9 workflows)
   - Role: Test strategy, quality assurance, test automation
   - When to use: Test design, quality assurance, enterprise projects

7. **UX Designer (Sally)** - UX Designer + UI Specialist
   - Primary workflows: create-ux-design
   - Secondary workflows: prd (UX sections), create-epics-and-stories (UX stories)
   - Role: User experience design, interaction design, visual design
   - When to use: Designing user interfaces, user flows, visual design

8. **Tech Writer (Paige)** - Technical Documentation Specialist
   - Primary workflows: Documentation tasks (supporting)
   - Role: Technical documentation, user guides, API documentation
   - When to use: Creating technical documentation, user guides

9. **Paige** - Documentation Guide (specialized documentation agent)
   - Primary workflows: Documentation generation
   - Role: Documentation orchestration and generation
   - When to use: Creating comprehensive documentation

**Game Development Team** (Optional via config):
- **Game Designer** - Game narrative and mechanics
- **Game Developer** - Game implementation
- **Game Architect** - Game architecture

### BMB Module (1 Agent)

**BMad Builder** - Master builder for agents, workflows, modules
- Primary workflows: create-agent, create-workflow, create-module, edit-agent, edit-workflow, edit-module, audit-workflow, redoc, convert-legacy, module-brief
- Role: Building and maintaining BMAD ecosystem
- When to use: Creating custom agents/workflows, extending BMAD, auditing quality

### CIS Module (5 Agents)

1. **Brainstorming Coach (Carson)** - Elite Brainstorming Specialist
2. **Design Thinking Coach (Maya)** - Design Thinking Maestro
3. **Creative Problem Solver (Dr. Quinn)** - Master Problem Solver
4. **Innovation Strategist (Victor)** - Disruptive Innovation Oracle
5. **Storyteller (Sophia)** - Master Storyteller

---

## Role-Based Workflow Matrix

### Quick Reference Table

| Role                    | Primary Workflows                                                                                      | Secondary Workflows                        | Read-Only Workflows                           |
| ----------------------- | ------------------------------------------------------------------------------------------------------ | ------------------------------------------ | --------------------------------------------- |
| **Product Manager**     | prd, product-brief                                                                                     | brainstorm-project, create-ux-design       | workflow-status, sprint-planning              |
| **Business Analyst**    | workflow-init, tech-spec, create-epics-and-stories, research                                           | prd, brainstorm-project, epic-tech-context | architecture, workflow-status                 |
| **Solution Architect**  | architecture, solutioning-gate-check                                                                   | epic-tech-context                          | prd, tech-spec, create-epics-and-stories      |
| **Technical Lead**      | code-review, architecture (review)                                                                     | solutioning-gate-check, epic-tech-context  | All workflows (for oversight)                 |
| **Scrum Master**        | sprint-planning, create-story, story-ready, story-done, workflow-status, correct-course, retrospective | -                                          | prd, tech-spec, architecture                  |
| **Software Engineer**   | dev-story, story-context                                                                               | code-review (peer review)                  | prd, tech-spec, architecture, sprint-planning |
| **QA Engineer / TEA**   | testarch:* (all 9 TEA workflows)                                                                       | -                                          | prd, tech-spec, architecture, stories         |
| **UX Designer**         | create-ux-design                                                                                       | prd (UX sections)                          | architecture, workflow-status                 |
| **DevOps Engineer**     | testarch:ci (CI/CD)                                                                                    | -                                          | architecture, sprint-planning                 |
| **Security Engineer**   | - (Enterprise Track - Future)                                                                          | -                                          | prd, architecture, solutioning-gate-check     |
| **Engineering Manager** | -                                                                                                      | solutioning-gate-check, retrospective      | All workflows (for oversight)                 |

---

## Detailed Role Mappings

### 1. Product Manager / Product Owner

**Primary Responsibilities**: Define what needs to be built and why

#### Workflows They Should Use

##### `/bmad:bmm:workflows:prd` ⭐ PRIMARY

**Purpose**: Create comprehensive Product Requirements Document

**When to use**:
- Starting a major feature or product (Level 2-4 projects)
- Defining epics for BMad Method Track
- Complex features requiring detailed planning
- Products and platforms

**Example scenarios**:
```bash
# New product
Load PM agent, then run: *prd
→ Creates comprehensive PRD.md with epics

# Major feature
Load PM agent, then run: *prd
→ Defines requirements for checkout flow
```

**Output**:
- `PRD.md` (or `prd/index.md` if sharded) with functional requirements
- Epic definitions with priorities
- Success criteria and metrics

**Why this role**: Product Managers understand business value and user needs better than anyone

---

##### `/bmad:bmm:workflows:product-brief` ⭐ PRIMARY

**Purpose**: Interactive product vision definition

**When to use**:
- Before creating PRD (discovery phase)
- Exploring product ideas
- Defining product vision with stakeholders
- Multiple input sources (documents, conversations)

**Example scenarios**:
```bash
# Product discovery
Load PM agent, then run: *product-brief
→ Interactive session to define product vision
→ Output: Product brief document
```

**Why this role**: Product Managers lead product vision and strategy

---

##### `/bmad:bmm:workflows:brainstorm-project` - SECONDARY

**Purpose**: Brainstorming with CIS integration (36 techniques)

**When to use**:
- Product ideation
- Feature exploration
- Strategic planning
- Complex problem-solving

**Example**:
```bash
# Product ideation
Load PM agent or Analyst agent, then run: *brainstorm-project
→ Uses CIS brainstorming workflows
→ 36 techniques across 7 categories
```

**Why this role**: Product Managers drive strategic product decisions

---

#### Workflows They Should Read (Not Execute)

- `/bmad:bmm:workflows:architecture` - Understand technical approach
- `/bmad:bmm:workflows:sprint-planning` - Review sprint setup
- `/bmad:bmm:workflows:workflow-status` - Check project status

---

### 2. Business Analyst

**Primary Responsibilities**: Requirements analysis, story breakdown, project initialization

#### Workflows They Should Use

##### `/bmad:bmm:workflows:workflow-init` ⭐ PRIMARY

**Purpose**: Initialize project and determine appropriate track

**When to use**:
- Every project start (greenfield or brownfield)
- Before any other workflow
- First workflow to run

**What it does**:
1. Analyzes project goal
2. Recommends track (Quick Flow, BMad Method, Enterprise)
3. Creates bmm-workflow-status.yaml for tracking
4. Sets up workflow path

**Example**:
```bash
# Start any project
Load Analyst agent, then run: *workflow-init
→ Recommends Quick Flow for bug fix
→ Recommends BMad Method for product feature
→ Creates tracking file
```

**Why this role**: Analysts understand project scope and requirements best

---

##### `/bmad:bmm:workflows:tech-spec` ⭐ PRIMARY (Quick Flow Track)

**Purpose**: Create technical specification for small features and bug fixes

**When to use**:
- Bug fixes
- Small features (1-3 related changes)
- Quick Flow Track (Level 0-1)
- Clear scope enhancements

**What it does**:
1. Creates implementation-focused technical specification
2. Documents approach and acceptance criteria
3. Fast-track planning (20-30 minutes)

**Example**:
```bash
# Bug fix
Load Analyst agent, then run: *tech-spec
→ Creates tech-spec.md with fix approach
→ Duration: 20-30 minutes
```

**Why this role**: Analysts translate requirements into technical specifications

---

##### `/bmad:bmm:workflows:create-epics-and-stories` ⭐ PRIMARY (BMad Method Track)

**Purpose**: Break PRD into epics and stories

**When to use**:
- After PRD is created
- BMad Method Track (Level 2-4)
- Before architecture phase

**What it does**:
1. Reads PRD.md
2. Creates epic breakdown
3. Generates story structure
4. Prioritizes epics (P1, P2, P3)

**Example**:
```bash
# After PRD
Load Analyst agent, then run: *create-epics-and-stories
→ Creates bmm-epics.md (or epics/ if sharded)
→ Breaks down into 3-10 epics with stories
→ Duration: 30-60 minutes
```

**Why this role**: Analysts excel at breaking down requirements

---

##### `/bmad:bmm:workflows:epic-tech-context` - SECONDARY

**Purpose**: Create epic-specific technical specification

**When to use**:
- After architecture is complete
- Before creating stories for an epic
- BMad Method Track

**What it does**:
1. Reads PRD epic section
2. Reads Architecture.md
3. Creates epic-specific technical spec
4. Provides just-in-time context for stories

**Example**:
```bash
# Before implementing epic
Load Analyst agent, then run: *epic-tech-context
→ Creates epic-specific tech-spec
→ Duration: 30-60 minutes per epic
```

**Why this role**: Analysts translate architecture to implementation specifications

---

##### `/bmad:bmm:workflows:research` - SECONDARY

**Purpose**: Adaptive research (market, technical, competitive)

**When to use**:
- Market research
- Technical evaluation
- Competitive intelligence
- Domain analysis

**Example**:
```bash
# Research phase
Load Analyst agent, then run: *research
→ Market research on competitors
→ Technical evaluation of libraries
→ Duration: Variable
```

**Why this role**: Analysts conduct research to inform requirements

---

#### Workflows They Should Read

- `/bmad:bmm:workflows:architecture` - Understand technical design
- `/bmad:bmm:workflows:workflow-status` - Check project status
- `/bmad:bmm:workflows:sprint-planning` - Review sprint setup

---

### 3. Solution Architect / Technical Architect

**Primary Responsibilities**: Technical design, architecture decisions, quality gates

#### Workflows They Should Use

##### `/bmad:bmm:workflows:architecture` ⭐ PRIMARY

**Purpose**: Create comprehensive architecture design document

**When to use**:
- BMad Method Track (Level 2-4 projects)
- After PRD and epics are created
- Before implementation begins
- When architectural decisions are needed

**What it does**:
1. Reads PRD.md and bmm-epics.md
2. Creates Architecture.md with:
   - Architectural views (Logical, Process, Deployment, Data)
   - Architecture decisions with rationale
   - Quality attributes (performance, security, scalability)
   - System-wide policies and patterns
   - Constraints and tradeoffs

**Example**:
```bash
# After PRD
Load Architect agent, then run: *architecture
→ Creates Architecture.md
→ Documents views, decisions, constraints
→ Duration: 2-4 hours
```

**Why this role**: Architects make technical stack and architecture decisions

---

##### `/bmad:bmm:workflows:solutioning-gate-check` ⭐ PRIMARY

**Purpose**: Pre-implementation validation gate (Quality gate before coding)

**When to use**:
- After PRD + Architecture + Epics are complete
- Before sprint planning and implementation
- BMad Method Track (Level 2-4)
- Quality gate checkpoint

**What it checks**:
- PRD-Architecture-Epics consistency
- Requirements coverage (100%)
- Missing requirements
- Contradictions and gaps
- Critical issue count

**Example**:
```bash
# Before implementation
Load Architect agent, then run: *solutioning-gate-check
→ Validates all planning artifacts
→ Reports critical issues (must be 0)
→ Reports gaps and contradictions
→ Duration: 15-30 minutes
```

**Why this role**: Architects ensure technical consistency and quality

---

#### Workflows They Should Read

- `/bmad:bmm:workflows:prd` - Understand requirements
- `/bmad:bmm:workflows:tech-spec` - Understand quick flow specs
- `/bmad:bmm:workflows:create-epics-and-stories` - See story breakdown
- `/bmad:bmm:workflows:sprint-planning` - Review sprint setup

---

### 4. Technical Lead / Engineering Lead

**Primary Responsibilities**: Code review, technical oversight, architecture review

#### Workflows They Should Use

##### `/bmad:bmm:workflows:code-review` ⭐ PRIMARY

**Purpose**: Senior developer code review with story context

**When to use**:
- After story implementation (dev-story) is complete
- Before marking story done
- For quality assurance

**What it does**:
1. Loads story file and context
2. Reviews code against:
   - Story acceptance criteria
   - Architecture.md patterns (if applicable)
   - PRD/tech-spec requirements
3. Appends structured review notes to story

**Example**:
```bash
# After dev-story
Load Dev agent or Tech Lead, then run: *code-review
→ Reviews story implementation
→ Checks acceptance criteria
→ Validates architecture compliance
→ Duration: 30-60 minutes
```

**Why this role**: Tech Leads ensure code quality and consistency

---

##### `/bmad:bmm:workflows:architecture` - SECONDARY

**Purpose**: Review or create architecture for smaller features

**When to use**:
- Review architecture created by architect
- Create architecture for smaller features (no dedicated architect)
- Validate architecture decisions

**Why this role**: Tech Leads have architectural knowledge and review responsibility

---

#### Workflows They Should Read (All for Oversight)

Tech Leads should have read access to all workflows for:
- Team oversight
- Quality assurance
- Technical guidance
- Architecture validation

---

### 5. Scrum Master / Project Manager

**Primary Responsibilities**: Sprint orchestration, story lifecycle, process facilitation

#### Workflows They Should Use

##### `/bmad:bmm:workflows:sprint-planning` ⭐ PRIMARY

**Purpose**: Generate sprint status tracking file

**When to use**:
- Before each sprint
- After epics/stories are created (BMad Method) or tech-spec is ready (Quick Flow)
- Sprint initialization

**What it does**:
1. Creates bmm-workflow-status.yaml
2. Tracks current epic, current story
3. Manages story statuses (TODO, IN PROGRESS, DONE)
4. Provides sprint progress visibility

**Example**:
```bash
# Sprint setup
Load SM agent, then run: *sprint-planning
→ Creates bmm-workflow-status.yaml
→ Sets up sprint tracking
→ Duration: 10-20 minutes
```

**Why this role**: Scrum Masters facilitate sprint planning and tracking

---

##### `/bmad:bmm:workflows:create-story` ⭐ PRIMARY

**Purpose**: Generate user story from epic

**When to use**:
- BMad Method Track
- After epic-tech-context is created
- Before story implementation

**What it does**:
1. Reads epic tech-spec, PRD, Architecture
2. Creates stories/[epic]-[story]-[name].md
3. Includes acceptance criteria
4. Templates story structure

**Example**:
```bash
# Story generation
Load SM agent, then run: *create-story
→ Creates story file from epic
→ Duration: 15-30 minutes per story
```

**Why this role**: Scrum Masters prepare stories for developers

---

##### `/bmad:bmm:workflows:story-ready` ⭐ PRIMARY

**Purpose**: Mark story ready (TODO → IN PROGRESS)

**When to use**:
- When developer starts working on story
- Moves story from TODO to IN PROGRESS
- Updates bmm-workflow-status.yaml

**Example**:
```bash
# Mark story ready
Load SM agent, then run: *story-ready
→ Updates status file
→ Duration: Instant
```

**Why this role**: Scrum Masters manage story lifecycle

---

##### `/bmad:bmm:workflows:story-done` ⭐ PRIMARY

**Purpose**: Mark story done (→ DONE)

**When to use**:
- After code review is complete
- When story is fully implemented and tested
- Moves story to DONE
- Updates bmm-workflow-status.yaml

**Example**:
```bash
# Mark story done
Load SM agent, then run: *story-done
→ Updates status file
→ Duration: Instant
```

**Why this role**: Scrum Masters complete story lifecycle

---

##### `/bmad:bmm:workflows:workflow-status` ⭐ PRIMARY

**Purpose**: Status checker and recommendations ("What should I do now?")

**When to use**:
- Daily standups
- When unsure what to do next
- Check current phase
- Get recommendations

**What it does**:
1. Reads bmm-workflow-status.yaml
2. Analyzes current phase and progress
3. Provides recommendations for next steps

**Example**:
```bash
# Check status
Load SM agent, then run: *workflow-status
→ "Current phase: Implementation"
→ "Recommendation: Run story-context for next story"
→ Duration: Instant
```

**Why this role**: Scrum Masters facilitate process and remove blockers

---

##### `/bmad:bmm:workflows:correct-course` ⭐ PRIMARY

**Purpose**: Navigate significant changes during sprint

**When to use**:
- Mid-sprint requirement changes
- Blockers affecting multiple stories
- Scope changes
- Technical pivots

**What it does**:
1. Analyzes impact of change
2. Proposes solutions (defer, adapt, pivot)
3. Routes to appropriate workflow
4. Updates plans if needed

**Example**:
```bash
# Mid-sprint change
Load SM agent, then run: *correct-course
→ Analyzes change impact
→ Proposes defer vs accept
→ Duration: 30-60 minutes
```

**Why this role**: Scrum Masters facilitate change management

---

##### `/bmad:bmm:workflows:retrospective` ⭐ PRIMARY

**Purpose**: Post-epic review and lessons learned

**When to use**:
- After epic completion
- End of sprint (if epic complete)
- Continuous improvement

**What it does**:
1. Reviews epic success
2. Extracts lessons learned
3. Explores new insights for next epic
4. Documents improvement actions

**Example**:
```bash
# After epic
Load SM agent, then run: *retrospective
→ Reviews epic completion
→ Documents lessons learned
→ Duration: 30-60 minutes
```

**Why this role**: Scrum Masters facilitate retrospectives

---

#### Workflows They Should Read

- `/bmad:bmm:workflows:prd` - Understand requirements
- `/bmad:bmm:workflows:tech-spec` - Understand quick flow specs
- `/bmad:bmm:workflows:architecture` - Understand technical design

---

### 6. Software Engineer / Developer

**Primary Responsibilities**: Implementation, code development, brownfield documentation

#### Workflows They Should Use

##### `/bmad:bmm:workflows:dev-story` ⭐ PRIMARY

**Purpose**: Execute story implementation with AI assistance

**When to use**:
- After story-context and story-ready
- Primary coding activity
- Story implementation

**What it does**:
1. Loads story file and context.xml
2. Implements story with AI assistance
3. Writes tests
4. Validates against acceptance criteria

**Example**:
```bash
# Implement story
Load Dev agent, then run: *dev-story
→ Implements story with AI
→ Writes tests
→ Duration: Variable (hours to days)
```

**Why this role**: Developers write the actual code

---

##### `/bmad:bmm:workflows:story-context` ⭐ PRIMARY

**Purpose**: Assemble dynamic context for story (just-in-time context loading)

**When to use**:
- Before dev-story
- Loads only relevant context (not entire codebase)
- Massive token savings

**What it does**:
1. Reads story file
2. Loads relevant PRD/Architecture sections
3. Loads relevant existing code
4. Creates stories/[story].context.xml

**Example**:
```bash
# Before coding
Load Dev agent, then run: *story-context
→ Creates story.context.xml
→ Just-in-time context (3k tokens vs 50k)
→ Duration: 5-10 minutes (automated)
```

**Why this role**: Developers need focused context for efficient implementation

---

##### `/bmad:bmm:workflows:document-project` - SECONDARY

**Purpose**: Analyze and document existing codebase (brownfield only)

**When to use**:
- Brownfield projects
- Before adding features to existing code
- First workflow for existing codebases

**What it does**:
1. Analyzes existing codebase
2. Documents architecture and patterns
3. Creates repository documentation

**Example**:
```bash
# Brownfield project
Load Dev agent, then run: *document-project
→ Analyzes codebase
→ Documents architecture
→ Duration: 30-60 minutes (automated)
```

**Why this role**: Developers understand existing code best

---

##### `/bmad:bmm:workflows:code-review` - SECONDARY

**Purpose**: Peer review

**When to use**:
- Peer review (not just senior review)
- When multiple developers review each other's code

**Why this role**: Developers provide peer reviews

---

#### Workflows They Should Read

- `/bmad:bmm:workflows:prd` - Understand requirements
- `/bmad:bmm:workflows:tech-spec` - Understand quick flow specs
- `/bmad:bmm:workflows:architecture` - Understand technical design
- `/bmad:bmm:workflows:sprint-planning` - Review sprint setup

---

### 7. QA Engineer / Test Engineer (TEA)

**Primary Responsibilities**: Test strategy, quality assurance, test automation

#### Workflows They Should Use (All TEA workflows)

##### `/bmad:bmm:workflows:testarch:atdd` ⭐ PRIMARY

**Purpose**: Acceptance Test-Driven Development

**When to use**:
- Before or during story implementation
- Define acceptance tests from acceptance criteria

---

##### `/bmad:bmm:workflows:testarch:test-design` ⭐ PRIMARY

**Purpose**: Test coverage strategy

**When to use**:
- Planning test approach for epic/project
- Defining test levels and coverage

---

##### `/bmad:bmm:workflows:testarch:framework` ⭐ PRIMARY

**Purpose**: Test framework initialization

**When to use**:
- Setting up test infrastructure
- Project initialization

---

##### `/bmad:bmm:workflows:testarch:automate` ⭐ PRIMARY

**Purpose**: Test automation expansion

**When to use**:
- Automating tests
- Expanding test coverage

---

##### `/bmad:bmm:workflows:testarch:test-review` ⭐ PRIMARY

**Purpose**: Test quality review

**When to use**:
- Reviewing test quality
- Quality assurance

---

##### `/bmad:bmm:workflows:testarch:trace` ⭐ PRIMARY

**Purpose**: Requirements-to-tests traceability

**When to use**:
- Ensuring test coverage
- Traceability matrix

---

##### `/bmad:bmm:workflows:testarch:nfr-assess` ⭐ PRIMARY

**Purpose**: Non-functional requirements assessment

**When to use**:
- Performance testing
- Security testing
- Scalability testing

---

##### `/bmad:bmm:workflows:testarch:ci` ⭐ PRIMARY

**Purpose**: CI/CD quality pipeline

**When to use**:
- Setting up CI/CD
- Quality gates in pipeline

---

**Why this role**: QA Engineers ensure quality through comprehensive testing

---

#### Workflows They Should Read

- `/bmad:bmm:workflows:prd` - Understand requirements
- `/bmad:bmm:workflows:tech-spec` - Understand quick flow specs
- `/bmad:bmm:workflows:architecture` - Understand technical design
- `/bmad:bmm:workflows:stories` - Understand story acceptance criteria

---

### 8. UX Designer

**Primary Responsibilities**: User experience design, interaction design

#### Workflows They Should Use

##### `/bmad:bmm:workflows:create-ux-design` ⭐ PRIMARY

**Purpose**: Collaborative UX design facilitation

**When to use**:
- BMad Method Track
- After PRD is created
- Optional but recommended for user-facing features

**What it does**:
1. Collaborative UX design session
2. Visual exploration with images
3. Creates UX-design.md

**Example**:
```bash
# UX design
Load UX Designer agent, then run: *create-ux-design
→ Collaborative design session
→ Visual exploration
→ Duration: 1-2 hours
```

**Why this role**: UX Designers create exceptional user experiences

---

#### Workflows They Should Read

- `/bmad:bmm:workflows:prd` - Understand requirements (especially UX sections)
- `/bmad:bmm:workflows:create-epics-and-stories` - See UX stories
- `/bmad:bmm:workflows:architecture` - Understand technical constraints

---

### 9. Engineering Manager

**Primary Responsibilities**: Team oversight, governance, quality assurance

#### Workflows They Should Use

##### `/bmad:bmm:workflows:solutioning-gate-check` - SECONDARY

**Purpose**: Quality gate oversight

**When to use**:
- Governance validation
- Quality oversight
- Risk assessment

---

##### `/bmad:bmm:workflows:retrospective` - SECONDARY

**Purpose**: Process improvement oversight

**When to use**:
- Team process improvement
- Strategic retrospectives

---

#### Workflows They Should Read (All for Oversight)

Engineering Managers should have read access to all workflows for:
- Team oversight
- Process improvement
- Risk identification
- Resource planning

---

## Workflow Sequences

### Typical Feature Development Flow

```
┌─────────────────────────────────────────────────────────────────────────┐
│                   QUICK FLOW TRACK (Levels 0-1)                          │
└─────────────────────────────────────────────────────────────────────────┘

Phase 0: Project Initialization
    Analyst: /bmad:bmm:workflows:workflow-init
        → Recommends Quick Flow Track

Phase 0b: Brownfield Documentation (if existing codebase)
    Dev: /bmad:bmm:workflows:document-project

Phase 2: Planning
    Analyst: /bmad:bmm:workflows:tech-spec
        → Output: tech-spec.md

Phase 4: Implementation Setup
    SM: /bmad:bmm:workflows:sprint-planning
        → Output: bmm-workflow-status.yaml

Phase 4: Implementation (Iterative per story)
    Dev: /bmad:bmm:workflows:story-context
    SM: /bmad:bmm:workflows:story-ready
    Dev: /bmad:bmm:workflows:dev-story
    Tech Lead: /bmad:bmm:workflows:code-review
    SM: /bmad:bmm:workflows:story-done

Phase 5: Retrospective (Optional)
    SM: /bmad:bmm:workflows:retrospective
```

```
┌─────────────────────────────────────────────────────────────────────────┐
│                   BMAD METHOD TRACK (Levels 2-4)                         │
└─────────────────────────────────────────────────────────────────────────┘

Phase 0: Project Initialization
    Analyst: /bmad:bmm:workflows:workflow-init
        → Recommends BMad Method Track

Phase 0b: Brownfield Documentation (if existing codebase)
    Dev: /bmad:bmm:workflows:document-project

Phase 1: Analysis (Optional)
    PM/Analyst: /bmad:bmm:workflows:brainstorm-project
    PM: /bmad:bmm:workflows:product-brief
    Analyst: /bmad:bmm:workflows:research

Phase 2: Planning
    PM: /bmad:bmm:workflows:prd
        → Output: PRD.md
    Analyst: /bmad:bmm:workflows:create-epics-and-stories
        → Output: bmm-epics.md
    UX Designer: /bmad:bmm:workflows:create-ux-design (optional)
        → Output: UX-design.md

Phase 3: Solutioning
    Architect: /bmad:bmm:workflows:architecture
        → Output: Architecture.md
    Architect: /bmad:bmm:workflows:solutioning-gate-check
        → Validates consistency

Phase 4: Implementation Setup
    SM: /bmad:bmm:workflows:sprint-planning
        → Output: bmm-workflow-status.yaml
    Analyst: /bmad:bmm:workflows:epic-tech-context (per epic)
    SM: /bmad:bmm:workflows:create-story (per story)

Phase 4: Implementation (Iterative per story)
    Dev: /bmad:bmm:workflows:story-context
    SM: /bmad:bmm:workflows:story-ready
    Dev: /bmad:bmm:workflows:dev-story
    Tech Lead: /bmad:bmm:workflows:code-review
    SM: /bmad:bmm:workflows:story-done

Phase 5: Retrospective (After each epic)
    SM: /bmad:bmm:workflows:retrospective
```

---

## Collaboration Patterns

### Pattern 1: Solo Developer (Quick Flow)

```
Developer (wearing all hats):
  /bmad:bmm:workflows:workflow-init
  /bmad:bmm:workflows:tech-spec
  /bmad:bmm:workflows:sprint-planning
  /bmad:bmm:workflows:story-context → story-ready → dev-story → story-done
```

---

### Pattern 2: Small Team (BMad Method)

```
Product Manager:  /bmad:bmm:workflows:prd
                         ↓
Business Analyst: /bmad:bmm:workflows:create-epics-and-stories
                         ↓
Solution Architect: /bmad:bmm:workflows:architecture
                    /bmad:bmm:workflows:solutioning-gate-check
                         ↓
Scrum Master:     /bmad:bmm:workflows:sprint-planning
                  /bmad:bmm:workflows:create-story
                         ↓
Developers:       /bmad:bmm:workflows:story-context → story-ready → dev-story
                         ↓
Tech Lead:        /bmad:bmm:workflows:code-review
                         ↓
Scrum Master:     /bmad:bmm:workflows:story-done
                         ↓
Scrum Master:     /bmad:bmm:workflows:retrospective
```

---

### Pattern 3: Large Team (BMad Method with TEA)

```
Product Team (PM + Analyst):
  /bmad:bmm:workflows:prd
  /bmad:bmm:workflows:create-epics-and-stories

Architecture Team (Architect + Tech Leads):
  /bmad:bmm:workflows:architecture
  /bmad:bmm:workflows:solutioning-gate-check

Scrum Masters:
  /bmad:bmm:workflows:sprint-planning
  /bmad:bmm:workflows:create-story
  /bmad:bmm:workflows:story-ready → story-done

Development Teams (3-4 teams):
  /bmad:bmm:workflows:story-context → dev-story

Quality Team (TEA):
  /bmad:bmm:workflows:testarch:* (all workflows)

Code Review Leads:
  /bmad:bmm:workflows:code-review
```

---

## Use Case Scenarios

### Scenario 1: New Product Feature (BMad Method Track)

**Project**: Add new user authentication feature
**Team**: 5 developers, 1 PM, 1 Architect, 1 SM
**Track**: BMad Method (Level 3)

```
Week 1: Planning
├─ Day 1: Analyst: workflow-init → Recommends BMad Method
├─ Day 2-3: PM: prd → Creates PRD.md
├─ Day 3: Analyst: create-epics-and-stories → Creates bmm-epics.md
├─ Day 4: Architect: architecture → Creates Architecture.md
└─ Day 5: Architect: solutioning-gate-check → Validates

Week 2-4: Implementation (3 sprints)
├─ Sprint 1: Epic 1 (4 stories)
│  └─ SM: sprint-planning → epic-tech-context → create-story
│  └─ Devs: story-context → story-ready → dev-story → story-done
│
├─ Sprint 2: Epic 2 (5 stories)
│  └─ Same workflow
│
└─ Sprint 3: Epic 3 (3 stories)
   └─ Same workflow

Week 5: Retrospective
└─ SM: retrospective → Lessons learned
```

---

### Scenario 2: Bug Fix (Quick Flow Track)

**Project**: Fix critical bug
**Team**: 1 developer
**Track**: Quick Flow (Level 0)

```
Same Day:
├─ 9:00 AM: Dev: workflow-init → Recommends Quick Flow
├─ 9:05 AM: Dev: tech-spec → Creates tech-spec.md (15 min)
├─ 9:25 AM: Dev: sprint-planning → Creates status file (5 min)
├─ 9:30 AM: Dev: story-context → Loads context (3 min)
├─ 9:35 AM: Dev: story-ready → Marks IN PROGRESS
├─ 9:40 AM: Dev: dev-story → Fixes bug (2 hours)
└─ 11:35 AM: Dev: story-done → Marks DONE

Total: 2.5 hours (25 min planning, 2 hours coding)
```

---

### Scenario 3: Brownfield Enhancement

**Project**: Add feature to existing codebase
**Team**: 3 developers, 1 Architect
**Track**: BMad Method (Level 2)

```
Week 1: Documentation & Planning
├─ Day 1: Dev: document-project → Documents existing code
├─ Day 1: Analyst: workflow-init → Recommends BMad Method
├─ Day 2-3: PM: prd → Creates PRD with integration points
├─ Day 3: Analyst: create-epics-and-stories
├─ Day 4: Architect: architecture → Includes integration patterns
└─ Day 5: Architect: solutioning-gate-check

Week 2-3: Implementation
└─ Standard story-by-story workflow with extra integration care
```

---

## Summary

BMAD v6 provides:

**19+ Specialized Agents** across 4 modules (Core, BMM, BMB, CIS)
**50+ Workflows** supporting complete development lifecycle
**Scale-Adaptive Intelligence** (Quick Flow → BMad Method → Enterprise)

**Key Success Factors**:
1. Always start with `/bmad:bmm:workflows:workflow-init`
2. Use appropriate track (Quick Flow vs BMad Method)
3. Run solutioning-gate-check before implementation (BMad Method)
4. Use story-context for efficient context loading
5. Track progress with bmm-workflow-status.yaml
6. Use correct-course for mid-sprint changes
7. Run retrospective for continuous improvement

---

**Version**: 6.0
**Last Updated**: 2025-01-05
**Framework**: BMAD v6 (BMad-CORE + BMad Method)
