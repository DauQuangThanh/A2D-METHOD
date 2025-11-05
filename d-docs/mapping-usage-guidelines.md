# Mapping BMAD v6 to Software Development Processes

**Comprehensive Integration Guidelines for AI-Driven Agile Development**

**Date**: 2025-11-05
**Version**: 6.0
**Project**: BMAD v6 (BMad-CORE + BMad Method)

---

## Executive Summary

BMAD v6 is an **AI-driven agile framework** that provides 19+ specialized agents and 50+ workflows across 4 modules (Core, BMM, BMB, CIS) to support the complete Software Development Life Cycle (SDLC). This document provides comprehensive guidelines for integrating BMAD v6 into various development methodologies including Agile/Scrum, Kanban, Waterfall, and hybrid approaches.

**Key Value Proposition**: BMAD v6 bridges the gap between requirements and implementation through scale-adaptive intelligence that automatically adjusts from quick bug fixes to enterprise-scale systems, providing AI-powered guidance at every stage.

**Three Planning Tracks**:
- **Quick Flow Track**: Tech-spec only (Levels 0-1) - Bug fixes, small features
- **BMad Method Track**: PRD + Architecture + UX (Levels 2-4) - Products, platforms
- **Enterprise Method Track**: Extended planning (BMad Method + Security/DevOps/Test) - Enterprise requirements

---

## Table of Contents

1. [SDLC Phase Mapping](#sdlc-phase-mapping)
2. [Agile/Scrum Integration](#agilescrum-integration)
3. [Kanban Integration](#kanban-integration)
4. [Waterfall Integration](#waterfall-integration)
5. [DevOps/CI-CD Integration](#devopsci-cd-integration)
6. [Team Size Adaptations](#team-size-adaptations)
7. [Project Type Adaptations](#project-type-adaptations)
8. [Quality Gates and Metrics](#quality-gates-and-metrics)
9. [Best Practices and Patterns](#best-practices-and-patterns)
10. [Common Pitfalls and Solutions](#common-pitfalls-and-solutions)
11. [Integration with Existing Tools](#integration-with-existing-tools)
12. [Real-World Workflows](#real-world-workflows)

---

## SDLC Phase Mapping

### Traditional SDLC Phases

```
┌─────────────────────────────────────────────────────────────────────────┐
│                    BMAD v6 SDLC PHASE MAPPING                            │
└─────────────────────────────────────────────────────────────────────────┘

Phase 0: PROJECT INITIALIZATION (Required for all projects)
├─ Activities: Determine project track, establish workflow path
├─ BMAD Workflows:
│  └─ /bmad:bmm:workflows:workflow-init (PRIMARY)
│     └─ Input: Project goal description
│     └─ Output: Recommended track (Quick Flow / BMad Method / Enterprise)
│     └─ Output: bmm-workflow-status.yaml (project tracking file)
│     └─ Duration: 5-10 minutes
│
├─ Artifacts Produced: bmm-workflow-status.yaml, workflow path determination
├─ Agent: Analyst (Mary) - Strategic Requirements Expert
├─ Exit Criteria: Track determined, workflow path established
└─ Applies to: ALL tracks (Quick Flow, BMad Method, Enterprise)

─────────────────────────────────────────────────────────────────────────

Phase 0b: BROWNFIELD DOCUMENTATION (Required for existing codebases)
├─ Activities: Document existing codebase before adding features
├─ BMAD Workflows:
│  └─ /bmad:bmm:workflows:document-project (PRIMARY)
│     └─ Input: Existing codebase
│     └─ Output: Comprehensive repo documentation
│     └─ Duration: 30-60 minutes (automated analysis)
│
├─ Artifacts Produced: Repository documentation, architecture analysis
├─ Agent: Dev (Amelia) - Senior Implementation Engineer
├─ Exit Criteria: Codebase documented, ready for new features
└─ Applies to: Brownfield projects only

─────────────────────────────────────────────────────────────────────────

Phase 1: ANALYSIS (Optional discovery phase)
├─ Activities: Brainstorming, research, product vision definition
├─ BMAD Workflows:
│  ├─ /bmad:bmm:workflows:brainstorm-project (OPTIONAL)
│  │  └─ Uses CIS brainstorming with 36 techniques
│  │  └─ Duration: 30-60 minutes
│  │
│  ├─ /bmad:bmm:workflows:product-brief (OPTIONAL)
│  │  └─ Interactive product vision definition
│  │  └─ Duration: 30-60 minutes
│  │
│  └─ /bmad:bmm:workflows:research (OPTIONAL)
│     └─ Market, technical, competitive research
│     └─ Duration: Variable
│
├─ Artifacts Produced: Brainstorming outputs, product brief, research docs
├─ Agents: Analyst (Mary), PM (John), CIS agents
├─ Exit Criteria: Vision clarified, research complete (if needed)
└─ Applies to: BMad Method Track, Enterprise Track (optional)

─────────────────────────────────────────────────────────────────────────

Phase 2: PLANNING (Required - Track-dependent depth)
├─ Activities: Requirements definition, technical specification
│
├─ BMAD Workflows (QUICK FLOW TRACK - Levels 0-1):
│  └─ /bmad:bmm:workflows:tech-spec (PRIMARY)
│     └─ Input: Feature description
│     └─ Output: tech-spec.md (implementation-focused)
│     └─ Duration: 20-30 minutes
│
├─ BMAD Workflows (BMAD METHOD TRACK - Levels 2-4):
│  ├─ /bmad:bmm:workflows:prd (PRIMARY)
│  │  └─ Input: Product requirements
│  │  └─ Output: PRD.md or prd/index.md (if sharded)
│  │  └─ Duration: 1-2 hours per product/feature
│  │
│  ├─ /bmad:bmm:workflows:create-ux-design (OPTIONAL)
│  │  └─ Collaborative UX design facilitation
│  │  └─ Duration: 1-2 hours
│  │
│  └─ /bmad:bmm:workflows:narrative (OPTIONAL - game dev)
│     └─ Narrative design for story-driven apps/games
│     └─ Duration: 1-2 hours
│
├─ Artifacts Produced:
│  └─ Quick Flow: tech-spec.md
│  └─ BMad Method: PRD.md (or prd/), UX-design.md, narrative.md
│
├─ Agents:
│  └─ PM (John), Analyst (Mary), UX Designer (Sally)
│
├─ Exit Criteria:
│  └─ Quick Flow: Tech spec approved
│  └─ BMad Method: PRD complete, UX designed (if applicable)
│
└─ Applies to: ALL tracks (different workflows per track)

─────────────────────────────────────────────────────────────────────────

Phase 2b: EPIC AND STORY CREATION (BMad Method only)
├─ Activities: Break PRD into epics and stories
├─ BMAD Workflows:
│  └─ /bmad:bmm:workflows:create-epics-and-stories (PRIMARY)
│     └─ Input: PRD.md
│     └─ Output: bmm-epics.md or epics/index.md (if sharded)
│     └─ Duration: 30-60 minutes
│
├─ Artifacts Produced: bmm-epics.md with story breakdown
├─ Agent: Analyst (Mary) - Strategic Requirements Expert
├─ Exit Criteria: Epics defined, stories drafted
└─ Applies to: BMad Method Track only (Level 2-4)

─────────────────────────────────────────────────────────────────────────

Phase 3: SOLUTIONING (BMad Method Track only)
├─ Activities: Architecture decisions, technical design
├─ BMAD Workflows:
│  ├─ /bmad:bmm:workflows:architecture (PRIMARY)
│  │  └─ Input: PRD.md or tech-spec.md
│  │  └─ Output: Architecture.md
│  │  └─ Duration: 2-4 hours
│  │
│  └─ /bmad:bmm:workflows:solutioning-gate-check (QUALITY GATE)
│     └─ Input: All planning artifacts (PRD, Architecture, Epics)
│     └─ Output: Validation report
│     └─ Duration: 15-30 minutes
│
├─ Artifacts Produced: Architecture.md, validation report
├─ Agent: Architect (Winston) - System Architect
├─ Exit Criteria: Architecture approved, gate check passed
└─ Applies to: BMad Method Track (Levels 2-4), Enterprise Track

─────────────────────────────────────────────────────────────────────────

Phase 4: IMPLEMENTATION SETUP
├─ Activities: Sprint planning, story preparation
├─ BMAD Workflows:
│  ├─ /bmad:bmm:workflows:sprint-planning (PRIMARY)
│  │  └─ Input: Epics/stories or tech-spec
│  │  └─ Output: bmm-workflow-status.yaml (sprint status file)
│  │  └─ Duration: 10-20 minutes
│  │
│  ├─ /bmad:bmm:workflows:epic-tech-context (BMad Method only)
│  │  └─ Input: Epic from bmm-epics.md
│  │  └─ Output: Epic-specific technical specification
│  │  └─ Duration: 30-60 minutes per epic
│  │
│  └─ /bmad:bmm:workflows:create-story (BMad Method only)
│     └─ Input: Epic tech-spec, PRD, Architecture
│     └─ Output: stories/[epic]-[story]-[name].md
│     └─ Duration: 15-30 minutes per story
│
├─ Artifacts Produced: Sprint status file, epic tech-specs, story files
├─ Agents: Scrum Master (Bob), Analyst (Mary)
├─ Exit Criteria: Sprint planned, stories drafted
└─ Applies to: ALL tracks (different workflows per track)

─────────────────────────────────────────────────────────────────────────

Phase 4: IMPLEMENTATION (Iterative)
├─ Activities: Story development, code review, testing
├─ BMAD Workflows (Story Lifecycle):
│  ├─ /bmad:bmm:workflows:story-context (BEFORE CODING)
│  │  └─ Input: Story file
│  │  └─ Output: stories/[story].context.xml (dynamic context)
│  │  └─ Duration: 5-10 minutes (automated)
│  │
│  ├─ /bmad:bmm:workflows:story-ready (MARK READY)
│  │  └─ Moves story from TODO → IN PROGRESS in status file
│  │  └─ Duration: Instant
│  │
│  ├─ /bmad:bmm:workflows:dev-story (PRIMARY IMPLEMENTATION)
│  │  └─ Input: Story file + context.xml
│  │  └─ Output: Working code implementation
│  │  └─ Duration: Variable (hours to days)
│  │
│  ├─ /bmad:bmm:workflows:code-review (QUALITY CHECK)
│  │  └─ Senior developer review with story context
│  │  └─ Duration: 30-60 minutes
│  │
│  └─ /bmad:bmm:workflows:story-done (MARK COMPLETE)
│     └─ Moves story from IN PROGRESS → DONE in status file
│     └─ Duration: Instant
│
├─ Artifacts Produced: Source code, tests, story context files
├─ Agents: Dev (Amelia), SM (Bob)
├─ Exit Criteria: All stories DONE, code reviewed, tests passing
└─ Applies to: ALL tracks

─────────────────────────────────────────────────────────────────────────

Phase 4: COURSE CORRECTION (As needed)
├─ Activities: Handle mid-sprint changes and blockers
├─ BMAD Workflows:
│  ├─ /bmad:bmm:workflows:correct-course (WHEN NEEDED)
│  │  └─ Navigate significant changes during sprint
│  │  └─ Duration: 30-60 minutes
│  │
│  └─ /bmad:bmm:workflows:workflow-status (STATUS CHECK)
│     └─ "What should I do now?" recommendations
│     └─ Duration: Instant
│
├─ Artifacts Produced: Course correction analysis, updated plans
├─ Agents: SM (Bob), Architect (Winston)
└─ Applies to: ALL tracks (when changes occur)

─────────────────────────────────────────────────────────────────────────

Phase 5: RETROSPECTIVE (After epic/sprint)
├─ Activities: Review, lessons learned, continuous improvement
├─ BMAD Workflows:
│  └─ /bmad:bmm:workflows:retrospective (PRIMARY)
│     └─ Run after epic completion
│     └─ Duration: 30-60 minutes
│
├─ Artifacts Produced: Retrospective notes, improvement actions
├─ Agent: SM (Bob) - Scrum Master
└─ Applies to: BMad Method Track (after each epic)

─────────────────────────────────────────────────────────────────────────

Phase 6: TESTING (Parallel with implementation)
├─ Activities: Test design, automation, quality assurance
├─ BMAD Workflows (TEA module):
│  ├─ /bmad:bmm:workflows:testarch:atdd (ATDD approach)
│  ├─ /bmad:bmm:workflows:testarch:test-design (Test coverage strategy)
│  ├─ /bmad:bmm:workflows:testarch:framework (Test framework init)
│  ├─ /bmad:bmm:workflows:testarch:automate (Test automation)
│  ├─ /bmad:bmm:workflows:testarch:test-review (Test quality review)
│  ├─ /bmad:bmm:workflows:testarch:trace (Traceability)
│  ├─ /bmad:bmm:workflows:testarch:nfr-assess (NFR assessment)
│  └─ /bmad:bmm:workflows:testarch:ci (CI/CD quality pipeline)
│
├─ Artifacts Produced: Test plans, test automation, traceability matrix
├─ Agent: TEA (Murat) - Master Test Architect
└─ Applies to: All projects (especially enterprise)
```

---

## Agile/Scrum Integration

### Scrum Ceremony Mapping

```
┌─────────────────────────────────────────────────────────────────────────┐
│                  BMAD v6 SCRUM CEREMONY INTEGRATION                      │
└─────────────────────────────────────────────────────────────────────────┘

SPRINT 0: Project Initialization
├─ Activity: Determine project track and workflow path
├─ BMAD Usage:
│  └─ Analyst: /bmad:bmm:workflows:workflow-init
│     └─ Analyzes project goal
│     └─ Recommends track: Quick Flow / BMad Method / Enterprise
│     └─ Creates: bmm-workflow-status.yaml
│
└─ Duration: 5-10 minutes

═══════════════════════════════════════════════════════════════════════════

BACKLOG REFINEMENT (Weekly) - QUICK FLOW TRACK
├─ Activity: Elaborate bug fixes and small features
├─ BMAD Usage:
│  ├─ Analyst: /bmad:bmm:workflows:tech-spec
│  │  └─ For each feature in backlog
│  │  └─ Creates: tech-spec.md per feature
│  │  └─ Duration: 20-30 minutes per feature
│  │
│  └─ SM: /bmad:bmm:workflows:sprint-planning
│     └─ Creates sprint status tracking
│     └─ Duration: 10-20 minutes
│
├─ Output: "Ready" features with tech-spec complete
└─ Duration: 1-2 hours per week

BEST PRACTICE: Refine 2-3 small features for next sprint

═══════════════════════════════════════════════════════════════════════════

BACKLOG REFINEMENT (Weekly) - BMAD METHOD TRACK
├─ Activity: Elaborate products and platforms
├─ BMAD Usage:
│  ├─ PM: /bmad:bmm:workflows:prd
│  │  └─ For each major feature/epic
│  │  └─ Creates: PRD.md or prd/index.md (sharded)
│  │  └─ Duration: 1-2 hours per feature
│  │
│  ├─ UX Designer: /bmad:bmm:workflows:create-ux-design (optional)
│  │  └─ Collaborative UX design
│  │  └─ Duration: 1-2 hours
│  │
│  ├─ Analyst: /bmad:bmm:workflows:create-epics-and-stories
│  │  └─ Breaks PRD into epics and stories
│  │  └─ Duration: 30-60 minutes
│  │
│  ├─ Architect: /bmad:bmm:workflows:architecture
│  │  └─ Creates architecture design
│  │  └─ Duration: 2-4 hours
│  │
│  └─ Architect: /bmad:bmm:workflows:solutioning-gate-check
│     └─ Validates planning completeness
│     └─ Duration: 15-30 minutes
│
├─ Output: "Ready" features with PRD, Architecture, Epics complete
└─ Duration: 2-3 hours per week

BEST PRACTICE: Refine epics 1-2 sprints ahead of implementation

═══════════════════════════════════════════════════════════════════════════

SPRINT PLANNING (Start of sprint)
├─ Activity: Select stories/features, commit to sprint goal
├─ BMAD Usage:
│  ├─ SM: /bmad:bmm:workflows:sprint-planning
│  │  └─ Generates sprint status file
│  │  └─ Tracks: current epic, current story, all story statuses
│  │  └─ Duration: 10-20 minutes
│  │
│  └─ SM: /bmad:bmm:workflows:workflow-status
│     └─ Validates: All stories ready for implementation
│     └─ Provides: "What should we do now?" recommendations
│
├─ Decision: Which stories/features to include in sprint
└─ Duration: 2-4 hours

SPRINT PLANNING PART 1 (What to build):
  - Review tech-spec.md (Quick Flow) or PRD.md (BMad Method)
  - Review bmm-epics.md for story breakdown
  - Confirm acceptance criteria
  - Verify planning artifacts complete

SPRINT PLANNING PART 2 (How to build):
  - Review Architecture.md (BMad Method only)
  - Assign stories to developers
  - Identify dependencies

═══════════════════════════════════════════════════════════════════════════

DAILY STANDUP (Every day)
├─ Activity: Synchronize team, identify blockers
├─ BMAD Usage:
│  └─ Team: Reviews bmm-workflow-status.yaml
│     ├─ "Yesterday: Completed story 1-2"
│     ├─ "Today: Working on story 1-3"
│     └─ "Blockers: Story 2-1 needs clarification"
│
├─ Blocker Resolution:
│  └─ SM: /bmad:bmm:workflows:correct-course
│     └─ Analyzes impact and proposes solutions
│     └─ Updates plans if needed
│
└─ Duration: 15 minutes

BEST PRACTICE: Use workflow-status to check current state

═══════════════════════════════════════════════════════════════════════════

SPRINT IMPLEMENTATION (Throughout sprint)
├─ Activity: Story development
├─ BMAD Usage (Story Lifecycle):
│  ├─ SM: /bmad:bmm:workflows:create-story (if not pre-created)
│  │  └─ Creates story file from epic
│  │
│  ├─ Dev: /bmad:bmm:workflows:story-context
│  │  └─ Assembles dynamic context for story
│  │  └─ Duration: 5-10 minutes (automated)
│  │
│  ├─ SM: /bmad:bmm:workflows:story-ready
│  │  └─ Marks story as IN PROGRESS
│  │
│  ├─ Dev: /bmad:bmm:workflows:dev-story
│  │  └─ Implements story with AI assistance
│  │  └─ Duration: Variable (hours to days)
│  │
│  ├─ Dev/Lead: /bmad:bmm:workflows:code-review
│  │  └─ Senior developer review
│  │
│  └─ SM: /bmad:bmm:workflows:story-done
│     └─ Marks story as DONE
│
└─ Duration: Sprint length (1-2 weeks)

RECOMMENDED WORKFLOW:
  Day 1-2: Setup and foundational stories
  Day 3-8: User story implementation (prioritized order)
  Day 9-10: Code review, testing, polish

═══════════════════════════════════════════════════════════════════════════

SPRINT REVIEW (End of sprint)
├─ Activity: Demo completed work to stakeholders
├─ BMAD Usage:
│  └─ PM: Validates against planning artifacts
│     ├─ Quick Flow: Checks tech-spec.md requirements
│     ├─ BMad Method: Checks PRD.md requirements
│     └─ Checks: Story acceptance criteria satisfied
│
├─ Acceptance:
│  ├─ PASS: Stories accepted, marked DONE
│  └─ FAIL: Identify gaps, create follow-up stories
│
└─ Duration: 1-2 hours

═══════════════════════════════════════════════════════════════════════════

SPRINT RETROSPECTIVE (End of sprint)
├─ Activity: Process improvement
├─ BMAD Usage:
│  └─ SM: /bmad:bmm:workflows:retrospective
│     └─ Review epic completion
│     └─ Extract lessons learned
│     └─ Explore new insights for next epic
│     └─ Duration: 30-60 minutes
│
├─ Discussion Points:
│  ├─ "Were specs clear enough?" → Improve PRD/tech-spec quality
│  ├─ "Did architecture help?" → Refine architecture workflow
│  ├─ "Were stories well-sized?" → Improve story creation
│  └─ "Did course corrections work?" → Refine correct-course usage
│
└─ Duration: 1-2 hours
```

---

### Sprint-Level Workflow Example

**2-Week Sprint with 3 User Stories (BMad Method Track)**

```
WEEK BEFORE SPRINT (Backlog Refinement):
┌────────────────────────────────────────────────────────────────┐
│ Monday-Wednesday: Epic Elaboration                             │
├────────────────────────────────────────────────────────────────┤
│ Epic 1: User Authentication (P1)                               │
│   PM: /bmad:bmm:workflows:prd → PRD.md                         │
│   UX: /bmad:bmm:workflows:create-ux-design → UX-design.md      │
│   Analyst: /bmad:bmm:workflows:create-epics-and-stories        │
│   Architect: /bmad:bmm:workflows:architecture → Architecture.md│
│   Architect: /bmad:bmm:workflows:solutioning-gate-check ✓      │
│   Status: ✓ Ready (3 stories planned)                          │
└────────────────────────────────────────────────────────────────┘

SPRINT PLANNING (Friday):
┌────────────────────────────────────────────────────────────────┐
│ Part 1: What (1 hour)                                          │
│   - Review PRD.md for Epic 1                                   │
│   - Review bmm-epics.md for story breakdown                    │
│   - Sprint Goal: "Complete user authentication MVP"            │
│   - SM: /bmad:bmm:workflows:sprint-planning                    │
│   - Commitment: Epic 1, Stories 1-3 (team velocity: 20 points) │
├────────────────────────────────────────────────────────────────┤
│ Part 2: How (1 hour)                                           │
│   - Review Architecture.md                                     │
│   - SM: /bmad:bmm:workflows:workflow-status                    │
│   - Assign stories:                                            │
│     • Dev A: Story 1-1 (User registration)                     │
│     • Dev B: Story 1-2 (User login)                            │
│     • Dev C: Story 1-3 (Password reset)                        │
└────────────────────────────────────────────────────────────────┘

SPRINT EXECUTION (Week 1):
┌────────────────────────────────────────────────────────────────┐
│ Monday (Day 1):                                                │
│   SM: /bmad:bmm:workflows:create-story (Stories 1-1, 1-2, 1-3) │
│   Dev A: /bmad:bmm:workflows:story-context (Story 1-1)         │
│   SM: /bmad:bmm:workflows:story-ready (Story 1-1)              │
│   Dev A: /bmad:bmm:workflows:dev-story (Story 1-1 started)     │
│   Daily Standup: No blockers                                   │
├────────────────────────────────────────────────────────────────┤
│ Tuesday (Day 2):                                               │
│   Dev A continues Story 1-1                                    │
│   Dev B: /bmad:bmm:workflows:story-context (Story 1-2)         │
│   SM: /bmad:bmm:workflows:story-ready (Story 1-2)              │
│   Dev B: /bmad:bmm:workflows:dev-story (Story 1-2 started)     │
│   Daily Standup: Dev A needs architecture clarification       │
│   - Architect reviews Architecture.md with Dev A               │
├────────────────────────────────────────────────────────────────┤
│ Wednesday (Day 3):                                             │
│   Dev A completes Story 1-1                                    │
│   Lead: /bmad:bmm:workflows:code-review (Story 1-1)            │
│   SM: /bmad:bmm:workflows:story-done (Story 1-1) ✓             │
│   Dev C starts Story 1-3                                       │
│   Daily Standup: Story 1-1 complete                            │
├────────────────────────────────────────────────────────────────┤
│ Thursday (Day 4):                                              │
│   Dev B completes Story 1-2                                    │
│   Lead: /bmad:bmm:workflows:code-review (Story 1-2)            │
│   SM: /bmad:bmm:workflows:story-done (Story 1-2) ✓             │
│   Daily Standup: 2 of 3 stories done                           │
├────────────────────────────────────────────────────────────────┤
│ Friday (Day 5):                                                │
│   Dev C completes Story 1-3                                    │
│   Lead: /bmad:bmm:workflows:code-review (Story 1-3)            │
│   SM: /bmad:bmm:workflows:story-done (Story 1-3) ✓             │
│   Daily Standup: All stories complete!                         │
└────────────────────────────────────────────────────────────────┘

SPRINT EXECUTION (Week 2):
┌────────────────────────────────────────────────────────────────┐
│ Monday (Day 6): Integration testing, bug fixes                 │
│ Tuesday (Day 7): Performance testing                           │
│ Wednesday (Day 8): Demo preparation                            │
│ Thursday (Day 9): Sprint Review                                │
│   - Review: All 3 stories accepted ✓                           │
│ Friday (Day 10): Sprint Retrospective                          │
│   - SM: /bmad:bmm:workflows:retrospective                      │
│   - Team: Epic 1 complete, velocity accurate                   │
└────────────────────────────────────────────────────────────────┘
```

---

## Kanban Integration

### Kanban Board with BMAD v6

```
┌─────────────────────────────────────────────────────────────────────────┐
│                      BMAD v6 KANBAN BOARD COLUMNS                        │
└─────────────────────────────────────────────────────────────────────────┘

Column 1: BACKLOG
├─ WIP Limit: Unlimited
├─ Entry Criteria: Raw feature request
├─ BMAD Actions: None yet
└─ Exit Criteria: Ready for planning

─────────────────────────────────────────────────────────────────────────

Column 2: PLANNING IN PROGRESS
├─ WIP Limit: 3 features
├─ Entry Criteria: Feature selected for elaboration
│
├─ BMAD Actions (QUICK FLOW TRACK):
│  └─ Analyst: /bmad:bmm:workflows:tech-spec
│
├─ BMAD Actions (BMAD METHOD TRACK):
│  ├─ PM: /bmad:bmm:workflows:prd
│  ├─ UX Designer: /bmad:bmm:workflows:create-ux-design (optional)
│  └─ Analyst: /bmad:bmm:workflows:create-epics-and-stories
│
├─ Definition of Done for column:
│  └─ Quick Flow: tech-spec.md created
│  └─ BMad Method: PRD.md + epics created
│
└─ Exit Criteria: Planning complete, ready for architecture

─────────────────────────────────────────────────────────────────────────

Column 3: ARCHITECTURE DESIGN (BMad Method Track only)
├─ WIP Limit: 2 features
├─ Entry Criteria: Planning complete
├─ BMAD Actions:
│  ├─ Architect: /bmad:bmm:workflows:architecture
│  └─ Architect: /bmad:bmm:workflows:solutioning-gate-check
│
├─ Definition of Done for column:
│  ├─ Architecture.md created
│  └─ Solutioning gate check passed
│
└─ Exit Criteria: Architecture approved, ready for implementation

─────────────────────────────────────────────────────────────────────────

Column 4: SPRINT SETUP
├─ WIP Limit: 4 features
├─ Entry Criteria: Architecture complete (or tech-spec for Quick Flow)
├─ BMAD Actions:
│  ├─ SM: /bmad:bmm:workflows:sprint-planning
│  └─ SM: /bmad:bmm:workflows:create-story (BMad Method)
│
├─ Definition of Done for column:
│  ├─ Sprint status file created
│  └─ Stories created (BMad Method) or tech-spec ready (Quick Flow)
│
└─ Exit Criteria: Ready for development

─────────────────────────────────────────────────────────────────────────

Column 5: READY FOR DEVELOPMENT
├─ WIP Limit: 6 stories (depends on team size)
├─ Entry Criteria: All planning artifacts complete
├─ BMAD Actions: None (waiting for developer availability)
├─ Definition of Done for column: N/A (queue)
└─ Exit Criteria: Developer pulls story into In Progress

─────────────────────────────────────────────────────────────────────────

Column 6: IN DEVELOPMENT
├─ WIP Limit: 1 per developer (e.g., 3 for 3 developers)
├─ Entry Criteria: Developer available, story pulled from Ready
├─ BMAD Actions:
│  ├─ Dev: /bmad:bmm:workflows:story-context
│  ├─ SM: /bmad:bmm:workflows:story-ready
│  └─ Dev: /bmad:bmm:workflows:dev-story
│
├─ Definition of Done for column:
│  ├─ Code written and committed
│  ├─ Unit tests pass
│  └─ Self-review complete
│
└─ Exit Criteria: Code ready for review

─────────────────────────────────────────────────────────────────────────

Column 7: CODE REVIEW
├─ WIP Limit: 4 stories
├─ Entry Criteria: Development complete
├─ BMAD Actions:
│  └─ Lead/Sr Dev: /bmad:bmm:workflows:code-review
│     └─ Validates against planning artifacts
│
├─ Definition of Done for column:
│  ├─ Code reviewed and approved
│  ├─ All comments addressed
│  └─ Meets coding standards
│
└─ Exit Criteria: Approved, ready for testing

─────────────────────────────────────────────────────────────────────────

Column 8: TESTING
├─ WIP Limit: 5 stories
├─ Entry Criteria: Code review approved
├─ BMAD Actions:
│  └─ QA validates against:
│     ├─ tech-spec.md (Quick Flow) or PRD.md (BMad Method)
│     └─ Story acceptance criteria
│
├─ Definition of Done for column:
│  ├─ All tests pass
│  ├─ Acceptance criteria met
│  └─ No critical bugs
│
└─ Exit Criteria: Testing passed, ready for deployment

─────────────────────────────────────────────────────────────────────────

Column 9: DONE
├─ WIP Limit: Unlimited
├─ Entry Criteria: Testing passed, deployed to production
├─ BMAD Actions:
│  └─ SM: /bmad:bmm:workflows:story-done
│
└─ Exit Criteria: N/A (final state)
```

---

## Waterfall Integration

### Waterfall Phases with BMAD v6

```
┌─────────────────────────────────────────────────────────────────────────┐
│                  BMAD v6 WATERFALL METHODOLOGY INTEGRATION               │
└─────────────────────────────────────────────────────────────────────────┘

PHASE 0: Project Initialization (Week 1)
├─ Traditional Activities:
│  ├─ Project kickoff
│  └─ Team formation
│
├─ BMAD Integration:
│  └─ Analyst: /bmad:bmm:workflows:workflow-init
│     └─ Determines track (usually BMad Method or Enterprise for waterfall)
│     └─ Duration: 5-10 minutes
│
└─ Duration: 1 week

─────────────────────────────────────────────────────────────────────────

PHASE 1: REQUIREMENTS GATHERING & ANALYSIS (Weeks 2-6)
├─ Traditional Activities:
│  ├─ Stakeholder interviews
│  ├─ Business requirements documentation
│  └─ Requirements review meetings
│
├─ BMAD Integration:
│  ├─ Week 2-3: Discovery (optional)
│  │  ├─ PM/Analyst: /bmad:bmm:workflows:brainstorm-project
│  │  ├─ PM: /bmad:bmm:workflows:product-brief
│  │  └─ Analyst: /bmad:bmm:workflows:research
│  │
│  ├─ Week 4-5: Requirements specification
│  │  ├─ PM: /bmad:bmm:workflows:prd
│  │  │  └─ Creates comprehensive PRD.md for all features
│  │  │  └─ Duration: 2-4 hours per feature
│  │  │
│  │  ├─ UX Designer: /bmad:bmm:workflows:create-ux-design
│  │  │  └─ Duration: 1-2 hours per major screen/flow
│  │  │
│  │  └─ Analyst: /bmad:bmm:workflows:create-epics-and-stories
│  │     └─ Creates complete epic/story breakdown
│  │     └─ Duration: 1-2 hours for full project
│  │
│  └─ Week 6: Requirements validation
│     └─ Stakeholders review PRD.md, bmm-epics.md, UX-design.md
│
├─ Deliverables:
│  ├─ Complete PRD.md (or prd/ if sharded)
│  ├─ UX-design.md (if applicable)
│  ├─ bmm-epics.md (or epics/ if sharded)
│  └─ Requirements Specification Document (RSD) approved
│
├─ Quality Gate:
│  └─ GATE 1: Requirements Sign-Off
│     ├─ All stakeholders approve PRD.md
│     ├─ All epics and stories defined
│     └─ UX design approved
│
└─ Duration: 5 weeks

─────────────────────────────────────────────────────────────────────────

PHASE 2: SYSTEM DESIGN (Weeks 7-10)
├─ Traditional Activities:
│  ├─ High-level design (HLD)
│  ├─ Low-level design (LLD)
│  ├─ Architecture review
│  └─ Design review meetings
│
├─ BMAD Integration:
│  ├─ Week 7-9: Architecture design
│  │  └─ Architect: /bmad:bmm:workflows:architecture
│  │     └─ Creates comprehensive Architecture.md
│  │     └─ Includes: Views, decisions, constraints, patterns
│  │     └─ Duration: 2-4 hours per major system component
│  │
│  └─ Week 10: Design validation
│     └─ Architect: /bmad:bmm:workflows:solutioning-gate-check
│        └─ Validates: PRD + Architecture + Epics alignment
│        └─ Identifies: Gaps, contradictions, missing requirements
│        └─ Duration: 30-60 minutes
│
├─ Deliverables:
│  ├─ Complete Architecture.md
│  ├─ Solutioning gate check report
│  └─ System Design Document (SDD) approved
│
├─ Quality Gate:
│  └─ GATE 2: Design Sign-Off
│     ├─ Architecture review board approval
│     ├─ All design decisions documented
│     ├─ Solutioning gate check passed (no critical issues)
│     └─ Security and performance validated
│
└─ Duration: 4 weeks

─────────────────────────────────────────────────────────────────────────

PHASE 3: IMPLEMENTATION PLANNING (Week 11)
├─ Traditional Activities:
│  ├─ Work breakdown structure (WBS)
│  ├─ Resource allocation
│  ├─ Schedule development
│  └─ Risk assessment
│
├─ BMAD Integration:
│  ├─ SM: /bmad:bmm:workflows:sprint-planning
│  │  └─ Creates sprint status file for entire project
│  │  └─ Tracks all epics and stories
│  │  └─ Duration: 20-30 minutes
│  │
│  ├─ Analyst: /bmad:bmm:workflows:epic-tech-context (for each epic)
│  │  └─ Creates epic-specific technical specifications
│  │  └─ Duration: 30-60 minutes per epic
│  │
│  └─ SM: /bmad:bmm:workflows:create-story (for all stories)
│     └─ Creates all story files upfront
│     └─ Duration: 15-30 minutes per story
│
├─ Deliverables:
│  ├─ bmm-workflow-status.yaml (complete project tracking)
│  ├─ Epic tech-specs for all epics
│  ├─ Story files for all stories
│  ├─ Project schedule (Gantt chart)
│  ├─ Resource allocation plan
│  └─ Risk mitigation plan
│
├─ Quality Gate:
│  └─ GATE 3: Implementation Planning Sign-Off
│     ├─ All stories defined
│     ├─ Epic tech-specs complete
│     ├─ Schedule approved by stakeholders
│     └─ Resources committed
│
└─ Duration: 1 week

─────────────────────────────────────────────────────────────────────────

PHASE 4: IMPLEMENTATION (Weeks 12-28)
├─ Traditional Activities:
│  ├─ Coding
│  ├─ Unit testing
│  ├─ Code reviews
│  └─ Integration
│
├─ BMAD Integration (Story-by-Story Execution):
│  └─ For each story (iteratively):
│     ├─ Dev: /bmad:bmm:workflows:story-context
│     ├─ SM: /bmad:bmm:workflows:story-ready
│     ├─ Dev: /bmad:bmm:workflows:dev-story
│     ├─ Lead: /bmad:bmm:workflows:code-review
│     └─ SM: /bmad:bmm:workflows:story-done
│
├─ Implementation Phases:
│  ├─ Weeks 12-14: Setup and foundational stories
│  ├─ Weeks 15-24: Core feature implementation (epic by epic)
│  ├─ Weeks 25-26: Integration and polish
│  └─ Weeks 27-28: Bug fixes and final integration
│
├─ Deliverables:
│  ├─ Source code
│  ├─ Story context files
│  ├─ Code review records
│  └─ Build artifacts
│
├─ Quality Gate:
│  └─ GATE 4: Implementation Complete
│     ├─ All stories marked DONE
│     ├─ All unit tests pass
│     ├─ Code review completed
│     ├─ Code coverage meets standards
│     └─ No critical bugs
│
└─ Duration: 17 weeks

─────────────────────────────────────────────────────────────────────────

PHASE 5: TESTING (Weeks 29-32)
├─ Traditional Activities:
│  ├─ Integration testing
│  ├─ System testing
│  ├─ User acceptance testing (UAT)
│  └─ Performance testing
│
├─ BMAD Integration (TEA module):
│  ├─ TEA: /bmad:bmm:workflows:testarch:test-design
│  ├─ TEA: /bmad:bmm:workflows:testarch:framework
│  ├─ TEA: /bmad:bmm:workflows:testarch:automate
│  ├─ TEA: /bmad:bmm:workflows:testarch:trace
│  └─ TEA: /bmad:bmm:workflows:testarch:test-review
│
├─ Validation against:
│  └─ QA Team validates:
│     ├─ PRD.md (all functional requirements)
│     ├─ Story acceptance criteria
│     └─ Success criteria in PRD.md
│
├─ Deliverables:
│  ├─ Test plans and test cases
│  ├─ Test execution reports
│  ├─ Defect logs
│  └─ UAT sign-off
│
├─ Quality Gate:
│  └─ GATE 5: Testing Complete
│     ├─ All test cases pass
│     ├─ All critical bugs resolved
│     ├─ Performance meets requirements
│     ├─ Security scan clean
│     └─ UAT approved
│
└─ Duration: 4 weeks

─────────────────────────────────────────────────────────────────────────

PHASE 6: DEPLOYMENT (Week 33)
├─ Traditional Activities:
│  ├─ Production deployment
│  ├─ Data migration
│  ├─ Training
│  └─ Handover to operations
│
├─ BMAD Integration:
│  └─ SM: /bmad:bmm:workflows:retrospective
│     └─ Final project retrospective
│     └─ Extract lessons learned
│     └─ Document for future projects
│
├─ Deliverables:
│  ├─ Production deployment
│  ├─ User documentation
│  ├─ Operations manual
│  └─ Retrospective report
│
└─ Duration: 1 week

─────────────────────────────────────────────────────────────────────────

PHASE 7: MAINTENANCE (Ongoing)
├─ Traditional Activities:
│  ├─ Bug fixes
│  ├─ Minor enhancements
│  └─ User support
│
├─ BMAD Integration:
│  └─ For each change request:
│     ├─ Analyst: /bmad:bmm:workflows:workflow-init
│     │  └─ Determines if Quick Flow or BMad Method
│     ├─ Follow appropriate track workflow
│     └─ SM: /bmad:bmm:workflows:correct-course (if mid-sprint change)
│
└─ Duration: Ongoing post-launch
```

---

## DevOps/CI-CD Integration

### Continuous Integration Pipeline

```
┌─────────────────────────────────────────────────────────────────────────┐
│                  BMAD v6 CI/CD PIPELINE INTEGRATION                      │
└─────────────────────────────────────────────────────────────────────────┘

STAGE 1: PLANNING VALIDATION (Pre-Pipeline)
├─ Trigger: Pull request to add/modify PRD.md or tech-spec.md
├─ Automated Checks:
│  ├─ Check 1: All mandatory sections present
│  ├─ Check 2: PRD.md or tech-spec.md exists
│  ├─ Check 3: bmm-workflow-status.yaml is valid YAML
│  └─ Check 4: Planning artifacts pass markdown linting
│
├─ Quality Gate:
│  └─ GATE: Planning Valid
│     └─ Status: ✓ PASS / ✗ FAIL (blocks merge)
│
└─ Action: Auto-comment on PR with validation results

─────────────────────────────────────────────────────────────────────────

STAGE 2: ARCHITECTURE VALIDATION (Pre-Pipeline - BMad Method only)
├─ Trigger: Pull request to add/modify Architecture.md
├─ Automated Checks:
│  ├─ Check 1: Architecture.md references valid PRD.md
│  ├─ Check 2: All mandatory architecture sections present
│  ├─ Check 3: Architecture decisions documented
│  └─ Check 4: bmm-workflow-status.yaml shows solutioning phase
│
├─ Quality Gate:
│  └─ GATE: Architecture Valid
│     └─ Status: ✓ PASS / ✗ FAIL (blocks merge)
│
└─ Action: Auto-comment on PR with validation results

─────────────────────────────────────────────────────────────────────────

STAGE 3: STORY VALIDATION (Pre-Pipeline)
├─ Trigger: Pull request to add/modify story files (stories/*.md)
├─ Automated Checks:
│  ├─ Check 1: Story file format valid (has acceptance criteria)
│  ├─ Check 2: Story references valid epic in bmm-epics.md
│  ├─ Check 3: Story context file exists (.context.xml)
│  └─ Check 4: Story status in bmm-workflow-status.yaml is valid
│
├─ Quality Gate:
│  └─ GATE: Story Valid
│     └─ Status: ✓ PASS / ✗ FAIL (blocks merge)
│
└─ Action: Auto-comment on PR with validation results

─────────────────────────────────────────────────────────────────────────

STAGE 4: SOLUTIONING GATE CHECK (Pre-Implementation Gate - BMad Method)
├─ Trigger: Manual or scheduled (before sprint starts)
├─ Action: Run /bmad:bmm:workflows:solutioning-gate-check via CLI
├─ Automated Checks:
│  ├─ PRD-Architecture-Epics consistency
│  ├─ Requirements coverage
│  ├─ Missing requirements
│  ├─ Contradictions and gaps
│  └─ Critical issue count
│
├─ Quality Gate:
│  └─ GATE: Solutioning Passed
│     ├─ Critical issues: 0
│     ├─ Requirements coverage: 100%
│     └─ Status: ✓ PASS / ✗ FAIL (blocks sprint start)
│
└─ Action: Generate gate check report, post to project management tool

─────────────────────────────────────────────────────────────────────────

STAGE 5: BUILD (Standard CI)
├─ Trigger: Push to feature branch
├─ Actions:
│  ├─ Checkout code
│  ├─ Install dependencies
│  ├─ Compile/Build
│  └─ Run linters
│
└─ Quality Gate: Build succeeds

─────────────────────────────────────────────────────────────────────────

STAGE 6: UNIT TESTS (Standard CI)
├─ Trigger: After build succeeds
├─ Actions:
│  ├─ Run unit tests
│  ├─ Generate coverage report
│  └─ Check coverage threshold
│
├─ BMAD Integration:
│  └─ Validate tests against:
│     └─ Story acceptance criteria
│
└─ Quality Gate:
│  ├─ All tests pass
│  └─ Coverage ≥ threshold (typically 80%)

─────────────────────────────────────────────────────────────────────────

STAGE 7: CODE REVIEW AUTOMATION
├─ Trigger: After unit tests pass
├─ BMAD Integration:
│  └─ Automated pre-checks before human review:
│     ├─ Story context loaded
│     ├─ Code matches Architecture.md patterns
│     └─ PRD/tech-spec requirements addressed
│
└─ Quality Gate: Automated checks pass, ready for human review

─────────────────────────────────────────────────────────────────────────

STAGE 8: INTEGRATION TESTS
├─ Trigger: After code review approved
├─ Actions:
│  ├─ Deploy to test environment
│  ├─ Run integration tests
│  └─ Run API tests
│
└─ Quality Gate: All integration tests pass

─────────────────────────────────────────────────────────────────────────

STAGE 9: SECURITY SCAN
├─ Trigger: After integration tests pass
├─ Actions:
│  ├─ SAST (Static Application Security Testing)
│  ├─ Dependency vulnerability scan
│  ├─ Secret scanning
│  └─ License compliance check
│
├─ BMAD Integration (Enterprise Track):
│  └─ Validate against security requirements in PRD
│
└─ Quality Gate:
│  ├─ No critical vulnerabilities
│  ├─ No high-severity vulnerabilities (or approved exceptions)
│  └─ No secrets in code

─────────────────────────────────────────────────────────────────────────

STAGE 10: ACCEPTANCE VALIDATION
├─ Trigger: Manual (before merge to main)
├─ Actions:
│  └─ Validate implementation against story acceptance criteria
│
├─ BMAD Integration:
│  └─ Automated script checks:
│     ├─ Story acceptance criteria met
│     ├─ All tests for story passing
│     └─ Code matches Architecture.md (if applicable)
│
└─ Quality Gate:
│  └─ GATE: Acceptance Criteria Met
│     └─ Status: ✓ PASS / ✗ FAIL (blocks merge)

─────────────────────────────────────────────────────────────────────────

STAGE 11: DEPLOYMENT (CD)
├─ Trigger: Merge to main branch
├─ Actions:
│  ├─ Deploy to staging
│  ├─ Smoke tests
│  ├─ Deploy to production (with approval)
│  └─ Monitor metrics
│
├─ BMAD Integration:
│  └─ SM: /bmad:bmm:workflows:story-done (automated)
│     └─ Updates bmm-workflow-status.yaml
│     └─ Marks story as DONE
│
└─ Quality Gate: Deployment successful, smoke tests pass
```

---

## Team Size Adaptations

### Solo Developer / Small Team (1-3 people)

```
┌─────────────────────────────────────────────────────────────────────────┐
│                  SOLO DEVELOPER / SMALL TEAM (1-3)                       │
└─────────────────────────────────────────────────────────────────────────┘

Team Size: 1-3 developers
Project Complexity: Small to medium features
Timeline: Days to weeks

SIMPLIFIED WORKFLOW (QUICK FLOW TRACK):

Developer (wearing all hats):
├─ 1. Project Initialization (5 minutes)
│  └─ /bmad:bmm:workflows:workflow-init
│     └─ Usually recommends Quick Flow Track
│
├─ 2. Technical Specification (20 minutes)
│  └─ /bmad:bmm:workflows:tech-spec
│
├─ 3. Sprint Setup (10 minutes)
│  └─ /bmad:bmm:workflows:sprint-planning
│
├─ 4. Story Context (5 minutes per story)
│  └─ /bmad:bmm:workflows:story-context
│
├─ 5. Implementation (varies)
│  ├─ /bmad:bmm:workflows:story-ready
│  ├─ /bmad:bmm:workflows:dev-story
│  └─ /bmad:bmm:workflows:story-done
│
└─ 6. Retrospective (optional, 15 minutes)
   └─ /bmad:bmm:workflows:retrospective

TOTAL OVERHEAD: ~40 minutes of planning work
BENEFIT: Clear direction, testable requirements, no scope creep

OPTIMIZATIONS:
- Use Quick Flow Track for all work
- Skip retrospective for very small features
- Use party mode sparingly (only for complex decisions)
- Focus on speed while maintaining quality

WHEN TO USE BMAD METHOD TRACK:
- Building a product (not just features)
- Complex integrations
- Unclear requirements requiring detailed PRD
- Multiple developers need coordination
```

---

### Medium Team (4-10 people)

```
┌─────────────────────────────────────────────────────────────────────────┐
│                      MEDIUM TEAM (4-10)                                  │
└─────────────────────────────────────────────────────────────────────────┘

Team Composition:
├─ 1 Product Manager (or Product Owner)
├─ 1 Tech Lead / Architect
├─ 4-8 Developers
└─ 1 QA Engineer (part-time or full-time)

ROLE DISTRIBUTION (BMAD METHOD TRACK):

Product Manager (20% time on BMAD):
├─ /bmad:bmm:workflows:workflow-init (project setup)
├─ /bmad:bmm:workflows:prd (for major features)
├─ /bmad:bmm:workflows:product-brief (optional discovery)
└─ /bmad:bmm:workflows:create-ux-design (optional UX)

Tech Lead/Architect (30% time on BMAD):
├─ /bmad:bmm:workflows:architecture (Level 2-4 projects)
├─ /bmad:bmm:workflows:solutioning-gate-check (quality gate)
├─ /bmad:bmm:workflows:epic-tech-context (per epic)
└─ /bmad:bmm:workflows:code-review (story reviews)

Scrum Master/PM (15% time on BMAD):
├─ /bmad:bmm:workflows:create-epics-and-stories (break down PRD)
├─ /bmad:bmm:workflows:sprint-planning (sprint setup)
├─ /bmad:bmm:workflows:create-story (story generation)
├─ /bmad:bmm:workflows:story-ready (mark stories ready)
├─ /bmad:bmm:workflows:story-done (mark stories complete)
├─ /bmad:bmm:workflows:workflow-status (status checks)
└─ /bmad:bmm:workflows:retrospective (after each epic)

Developers (10% time on BMAD):
├─ /bmad:bmm:workflows:story-context (before coding)
├─ /bmad:bmm:workflows:dev-story (primary activity)
└─ /bmad:bmm:workflows:correct-course (when changes needed)

QA Engineer (Optional - TEA workflows):
├─ /bmad:bmm:workflows:testarch:test-design
├─ /bmad:bmm:workflows:testarch:framework
└─ /bmad:bmm:workflows:testarch:automate

WORKFLOW:

Sprint Planning Preparation (1 week before):
├─ Monday-Tuesday: PM creates PRD
│  └─ /bmad:bmm:workflows:prd
│
├─ Wednesday: SM creates epics and stories
│  └─ /bmad:bmm:workflows:create-epics-and-stories
│
├─ Thursday: Architect designs architecture
│  └─ /bmad:bmm:workflows:architecture
│
└─ Friday: Architect validates
   └─ /bmad:bmm:workflows:solutioning-gate-check

Sprint Execution (2 weeks):
├─ Day 1: Sprint planning
│  └─ SM: /bmad:bmm:workflows:sprint-planning
│
├─ Day 2-9: Developers implement stories
│  └─ Dev: story-context → story-ready → dev-story
│
└─ Day 10: Sprint review + retrospective
   └─ SM: /bmad:bmm:workflows:retrospective

PARALLEL WORK OPPORTUNITIES:
- Multiple developers work on different stories simultaneously
- Tech Lead prepares future epics while developers implement current sprint
- QA validates completed stories while developers continue new ones
```

---

### Large Team (11-30 people)

```
┌─────────────────────────────────────────────────────────────────────────┐
│                       LARGE TEAM (11-30)                                 │
└─────────────────────────────────────────────────────────────────────────┘

Team Composition:
├─ 2-3 Product Managers (by domain)
├─ 1-2 Solution Architects
├─ 2-3 Technical Leads
├─ 15-20 Developers (3-4 scrum teams)
├─ 2-3 QA Engineers
├─ 1 Security Engineer (optional, Enterprise Track)
├─ 1 DevOps Engineer (optional, Enterprise Track)
└─ 2-3 Scrum Masters

ROLE DISTRIBUTION BY TEAM (BMAD METHOD / ENTERPRISE TRACK):

PRODUCT TEAM (PMs + Analysts):
├─ Daily: /bmad:bmm:workflows:prd (new features)
├─ Daily: /bmad:bmm:workflows:product-brief (discovery)
├─ Weekly: /bmad:bmm:workflows:research (market/technical)
└─ Weekly: /bmad:bmm:workflows:create-ux-design (UX design)

ARCHITECTURE TEAM (Architects + Tech Leads):
├─ Weekly: /bmad:bmm:workflows:architecture (all major features)
├─ Weekly: /bmad:bmm:workflows:solutioning-gate-check (quality gates)
├─ Weekly: /bmad:bmm:workflows:epic-tech-context (epic specs)
├─ Bi-weekly: Review architecture decisions across teams
└─ Maintains: Architecture library

SCRUM MASTERS (Sprint Orchestration):
├─ Weekly: /bmad:bmm:workflows:create-epics-and-stories (PRD breakdown)
├─ Weekly: /bmad:bmm:workflows:sprint-planning (sprint setup)
├─ Daily: /bmad:bmm:workflows:workflow-status (status checks)
├─ Daily: /bmad:bmm:workflows:create-story (story generation)
├─ Daily: /bmad:bmm:workflows:story-ready (mark ready)
├─ Daily: /bmad:bmm:workflows:story-done (mark complete)
├─ Weekly: /bmad:bmm:workflows:retrospective (after epics)
└─ As needed: /bmad:bmm:workflows:correct-course (course corrections)

DEVELOPMENT TEAMS (3-4 Scrum Teams):
├─ Scrum Team Alpha (5 developers)
├─ Scrum Team Beta (5 developers)
├─ Scrum Team Gamma (5 developers)
└─ Scrum Team Delta (5 developers)

Each Scrum Team:
├─ Daily: /bmad:bmm:workflows:story-context (before coding)
├─ Daily: /bmad:bmm:workflows:dev-story (implementation)
└─ As needed: /bmad:bmm:workflows:correct-course (blockers)

QUALITY TEAM (QA + TEA workflows - Enterprise Track):
├─ Weekly: /bmad:bmm:workflows:testarch:test-design
├─ Weekly: /bmad:bmm:workflows:testarch:framework
├─ Continuous: /bmad:bmm:workflows:testarch:automate
└─ Bi-weekly: /bmad:bmm:workflows:testarch:test-review

CODE REVIEW LEADS:
└─ Daily: /bmad:bmm:workflows:code-review (story reviews)

COORDINATION WORKFLOW:

Week N-2 (Two weeks ahead):
├─ Product Managers: Create PRDs for Week N
│  └─ /bmad:bmm:workflows:prd
│
└─ UX Designers: Create UX designs
   └─ /bmad:bmm:workflows:create-ux-design

Week N-1 (One week ahead):
├─ Scrum Masters: Break down PRDs
│  └─ /bmad:bmm:workflows:create-epics-and-stories
│
├─ Architecture Team: Create designs
│  └─ /bmad:bmm:workflows:architecture
│
└─ Architecture Team: Validate
   └─ /bmad:bmm:workflows:solutioning-gate-check

Week N (Current sprint):
├─ Sprint Planning: All Scrum teams select stories
├─ Daily: Teams implement independently
│  └─ story-context → story-ready → dev-story → code-review → story-done
└─ Weekly: Cross-team sync for dependencies

PARALLEL EXECUTION:
- 4 Scrum teams implement 4 independent epics simultaneously
- Product team prepares Sprint N+2 while teams execute Sprint N
- Architecture team designs Sprint N+1 while teams execute Sprint N
- Quality team validates Sprint N-1 output while teams execute Sprint N

SCALING BENEFITS:
- Clear separation of concerns (product, architecture, quality, implementation)
- 2-sprint look-ahead ensures work is always ready
- Multiple teams work independently on different epics
- Consistent quality via shared Architecture.md and solutioning gates
```

---

## Project Type Adaptations

### Greenfield Project (New Product)

```
PHASE 0: Foundation (Week 1)
├─ Analyst: /bmad:bmm:workflows:workflow-init
│  └─ Usually recommends BMad Method Track for new products
│  └─ Duration: 5-10 minutes
│
└─ Output: bmm-workflow-status.yaml (project tracking)

PHASE 1: Product Definition (Weeks 2-3)
├─ PM: /bmad:bmm:workflows:product-brief (optional discovery)
│  └─ Define product vision
│  └─ Duration: 30-60 minutes
│
├─ PM: /bmad:bmm:workflows:research (optional)
│  └─ Market, competitive, technical research
│  └─ Duration: Variable
│
└─ PM: /bmad:bmm:workflows:prd (comprehensive MVP)
   └─ Focus on core value proposition
   └─ 3-5 key epics maximum for MVP
   └─ Duration: 1-2 hours

PHASE 2: Architecture & Solutioning (Weeks 3-4)
├─ Analyst: /bmad:bmm:workflows:create-epics-and-stories
│  └─ Break PRD into epics and stories
│  └─ Duration: 30-60 minutes
│
├─ UX Designer: /bmad:bmm:workflows:create-ux-design (optional)
│  └─ Design key user flows
│  └─ Duration: 1-2 hours
│
├─ Architect: /bmad:bmm:workflows:architecture
│  └─ Make foundational technology decisions
│  └─ Document architecture views and decisions
│  └─ Duration: 2-4 hours
│
└─ Architect: /bmad:bmm:workflows:solutioning-gate-check
   └─ Validate PRD + Architecture + Epics alignment
   └─ Duration: 15-30 minutes

PHASE 3: Implementation (Weeks 5-16)
├─ SM: /bmad:bmm:workflows:sprint-planning
├─ SM: /bmad:bmm:workflows:epic-tech-context (per epic)
├─ SM: /bmad:bmm:workflows:create-story (all stories)
└─ Team: Story-by-story implementation (dev-story workflow)

BEST PRACTICES:
- Take time on PRD - it defines your product vision
- Document ALL architecture decisions in Architecture.md
- Start with minimal but complete MVP epics
- Focus on architecture that can scale
- Use solutioning-gate-check before implementation
```

---

### Brownfield Project (Adding to Existing System)

```
PHASE 0: Documentation (Week 1)
├─ Dev: /bmad:bmm:workflows:document-project
│  └─ Analyze and document existing codebase
│  └─ Duration: 30-60 minutes (automated analysis)
│
└─ Output: Repository documentation, architecture analysis

PHASE 0b: Project Initialization (Week 1)
├─ Analyst: /bmad:bmm:workflows:workflow-init
│  └─ Determine track based on change scope
│  └─ Quick Flow for small enhancements
│  └─ BMad Method for major features
│
└─ Duration: 5-10 minutes

PHASE 1: Integration Planning (Week 2) - QUICK FLOW
├─ Analyst: /bmad:bmm:workflows:tech-spec
│  └─ Include: Integration points with existing system
│  └─ Include: Migration requirements if applicable
│  └─ Duration: 20-30 minutes
│
└─ Proceed to sprint-planning and implementation

PHASE 1: Integration Planning (Week 2) - BMAD METHOD
├─ PM: /bmad:bmm:workflows:prd
│  └─ Include: Integration points with existing system
│  └─ Include: Migration requirements if applicable
│  └─ Duration: 1-2 hours
│
├─ Analyst: /bmad:bmm:workflows:create-epics-and-stories
│  └─ Duration: 30-60 minutes
│
├─ Architect: /bmad:bmm:workflows:architecture
│  └─ Focus on: How new feature integrates with existing
│  └─ Document: Existing system constraints
│  └─ Update: Architecture.md with integration patterns
│  └─ Duration: 2-4 hours
│
└─ Architect: /bmad:bmm:workflows:solutioning-gate-check
   └─ Pay special attention to integration points
   └─ Duration: 15-30 minutes

PHASE 2: Task Breakdown (Week 2-3)
├─ SM: /bmad:bmm:workflows:sprint-planning
├─ SM: /bmad:bmm:workflows:epic-tech-context (BMad Method only)
└─ SM: /bmad:bmm:workflows:create-story (BMad Method only)

PHASE 3: Implementation (Weeks 3-N)
└─ Developers: Story-by-story using dev-story workflow
   └─ Extra care with existing code integration

BEST PRACTICES:
- ALWAYS run document-project first for brownfield
- Document existing system constraints in Architecture.md
- Include integration tests in TEA workflows
- Plan for rollback strategies
- Consider data migration carefully in tech-spec/PRD
```

---

### Microservices Project

```
PATTERN: One BMAD workflow per microservice

SERVICE 1: User Service
├─ Analyst: /bmad:bmm:workflows:workflow-init
├─ PM: /bmad:bmm:workflows:prd → User management features
├─ Analyst: /bmad:bmm:workflows:create-epics-and-stories
├─ Architect: /bmad:bmm:workflows:architecture → Service-specific
├─ Architect: /bmad:bmm:workflows:solutioning-gate-check
├─ SM: /bmad:bmm:workflows:sprint-planning
└─ Team: Story-by-story implementation

SERVICE 2: Payment Service
├─ [Same workflow]
└─ CRITICAL: Architecture.md must define inter-service APIs

SERVICE 3: Notification Service
└─ [Same workflow]

CROSS-SERVICE COORDINATION:

Shared Architecture Principles:
└─ Each service has its own Architecture.md
   ├─ Defines: Service boundaries
   ├─ Defines: Communication patterns (REST/gRPC/Events)
   ├─ Defines: Data ownership
   └─ Defines: Inter-service contracts

Service-Specific Artifacts:
├─ Each service has: PRD.md (service requirements)
├─ Each service has: Architecture.md (service design)
├─ Each service has: bmm-epics.md (service epics)
├─ Each service has: bmm-workflow-status.yaml (service tracking)
└─ Each service has: stories/ (service stories)

VALIDATION STRATEGY:
└─ solutioning-gate-check MUST validate:
   ├─ Inter-service contracts are documented
   ├─ Data ownership boundaries are clear
   └─ Dependencies on other services are explicit
```

---

### API-First Project

```
CRITICAL: Architecture.md documents all API contracts

PHASE 1: API Design (Before any other work)
├─ PM: /bmad:bmm:workflows:prd (API requirements)
│  └─ Focus on: What operations API must support
│  └─ Duration: 1-2 hours
│
├─ Analyst: /bmad:bmm:workflows:create-epics-and-stories
│  └─ Duration: 30-60 minutes
│
└─ Architect: /bmad:bmm:workflows:architecture
   ├─ Document API design in Architecture.md:
   │  ├─ Complete REST/GraphQL endpoint specifications
   │  ├─ All request/response models
   │  ├─ All error responses
   │  ├─ Authentication/authorization
   │  └─ API versioning strategy
   │
   └─ Duration: 2-4 hours

PHASE 2: Contract Validation
├─ Architect: /bmad:bmm:workflows:solutioning-gate-check
│  └─ Validates:
│     ├─ All endpoints have error handling
│     ├─ All models have validation rules
│     ├─ API versioning strategy defined
│     └─ Authentication/authorization specified
│
└─ Team reviews and approves Architecture.md

PHASE 3: Parallel Development
├─ Backend Team: /bmad:bmm:workflows:dev-story
│  └─ Implements API exactly as specified in Architecture.md
│
└─ Frontend Team: Can start immediately
   └─ Uses Architecture.md to build against mock API

PHASE 4: Contract Testing (TEA workflows)
└─ TEA: /bmad:bmm:workflows:testarch:automate
   └─ Tests implementation against Architecture.md contracts
   └─ Every endpoint must match specification exactly

BEST PRACTICES:
- Architecture.md is source of truth for API contracts
- Never deviate from contracts without updating Architecture.md
- Use contract testing tools (Pact, Dredd, etc.)
- Version APIs from day one
- Document API evolution strategy
```

---

## Quality Gates and Metrics

### Quality Gates by Phase

```
┌─────────────────────────────────────────────────────────────────────────┐
│                     BMAD v6 QUALITY GATES                                │
└─────────────────────────────────────────────────────────────────────────┘

GATE 1: Planning Quality
├─ Workflows: workflow-init, prd, tech-spec
├─ Criteria:
│  ├─ Quick Flow:
│  │  └─ ✓ tech-spec.md complete and approved
│  │
│  └─ BMad Method:
│     ├─ ✓ PRD.md complete (all mandatory sections)
│     ├─ ✓ bmm-epics.md created (epic breakdown)
│     └─ ✓ UX-design.md created (if applicable)
│
├─ Metrics:
│  ├─ Planning completeness: 100%
│  ├─ Time to planning: Target ≤2 hours (Quick), ≤4 hours (BMad Method)
│  └─ Epic count: Appropriate for project level
│
└─ Decision: PASS → Proceed to architecture | FAIL → Revise planning

─────────────────────────────────────────────────────────────────────────

GATE 2: Architecture Quality (BMad Method Track only)
├─ Workflows: architecture, solutioning-gate-check
├─ Criteria:
│  ├─ ✓ Architecture.md complete (views, decisions, constraints)
│  ├─ ✓ All architecture decisions documented with rationale
│  ├─ ✓ Quality attributes defined (performance, security, scalability)
│  ├─ ✓ System patterns and policies documented
│  └─ ✓ Solutioning gate check passed (no critical issues)
│
├─ Metrics:
│  ├─ Architecture completeness: 100%
│  ├─ Decisions documented: 100%
│  ├─ Gate check critical issues: Must be 0
│  └─ Gate check high issues: Target ≤3
│
└─ Decision: PASS → Proceed to implementation | FAIL → Revise architecture

─────────────────────────────────────────────────────────────────────────

GATE 3: Sprint Readiness
├─ Workflows: sprint-planning, create-story
├─ Criteria:
│  ├─ ✓ bmm-workflow-status.yaml created
│  ├─ ✓ All stories defined (BMad Method) or tech-spec ready (Quick)
│  ├─ ✓ Epic tech-specs complete (BMad Method, per epic)
│  └─ ✓ Story files created with acceptance criteria
│
├─ Metrics:
│  ├─ Story completeness: 100%
│  ├─ Acceptance criteria clarity: 100%
│  └─ Sprint tracking setup: Complete
│
└─ Decision: PASS → Proceed to implementation | FAIL → Complete setup

─────────────────────────────────────────────────────────────────────────

GATE 4: Story Implementation Quality
├─ Workflows: dev-story, code-review
├─ Criteria:
│  ├─ ✓ Code implements story acceptance criteria
│  ├─ ✓ Unit tests written and passing
│  ├─ ✓ Code follows Architecture.md patterns (if applicable)
│  ├─ ✓ Code review approved
│  └─ ✓ Story context validated
│
├─ Metrics:
│  ├─ Acceptance criteria met: 100%
│  ├─ Test pass rate: 100%
│  ├─ Code coverage: Per project standards (typically ≥80%)
│  ├─ Code quality: No critical issues
│  └─ Architecture compliance: 100%
│
└─ Decision: PASS → Mark story DONE | FAIL → Fix implementation

─────────────────────────────────────────────────────────────────────────

GATE 5: Epic Completion
├─ Workflows: retrospective
├─ Criteria:
│  ├─ ✓ All stories in epic marked DONE
│  ├─ ✓ All acceptance criteria met
│  ├─ ✓ Integration tests passing
│  ├─ ✓ Epic retrospective completed
│  └─ ✓ Lessons learned documented
│
├─ Metrics:
│  ├─ Story completion rate: 100%
│  ├─ Acceptance criteria met: 100%
│  ├─ Retrospective insights: Documented
│  └─ Course corrections: Documented (if any)
│
└─ Decision: PASS → Epic complete | FAIL → Complete remaining work
```

---

## Best Practices and Patterns

### 1. Always Initialize with workflow-init
```
❌ DON'T: Guess which track to use
✓ DO: Run /bmad:bmm:workflows:workflow-init first
   └─ Let BMAD analyze your project and recommend the right track
   └─ Creates bmm-workflow-status.yaml for tracking
   └─ Duration: 5-10 minutes
```

### 2. Use Document Sharding for Large Projects
```
❌ DON'T: Load entire PRD.md (50k tokens) every time
✓ DO: Use document sharding for projects with >20k token documents
   └─ /bmad:core:tools:shard-doc to split documents
   └─ Workflows automatically detect and load only needed sections
   └─ 90%+ token savings in Phase 4
```

### 3. Run Solutioning Gate Check Before Implementation
```
❌ DON'T: Start coding without validation
✓ DO: Run /bmad:bmm:workflows:solutioning-gate-check
   └─ Validates PRD + Architecture + Epics consistency
   └─ Identifies gaps, contradictions, missing requirements
   └─ Duration: 15-30 minutes (prevents days of rework)
```

### 4. Use Story Context for Just-in-Time Context Loading
```
❌ DON'T: Load entire codebase for every story
✓ DO: Run /bmad:bmm:workflows:story-context before dev-story
   └─ Assembles only relevant context (PRD sections, arch patterns, existing code)
   └─ Creates stories/[story].context.xml
   └─ Massive token savings, focused development
```

### 5. Use Party Mode for Strategic Decisions
```
✓ DO: Use /bmad:core:workflows:party-mode when:
   ├─ Making architecture decisions affecting multiple teams
   ├─ Resolving complex technical challenges
   ├─ Brainstorming product direction
   └─ Need diverse perspectives from 19+ specialized agents
```

### 6. Track Progress with workflow-status
```
✓ DO: Run /bmad:bmm:workflows:workflow-status when:
   ├─ "What should I do now?"
   ├─ Check current phase and recommended next steps
   ├─ Validate sprint progress
   └─ Duration: Instant (reads bmm-workflow-status.yaml)
```

### 7. Use Course Correction for Mid-Sprint Changes
```
❌ DON'T: Panic when requirements change mid-sprint
✓ DO: Run /bmad:bmm:workflows:correct-course
   └─ Analyzes impact of changes
   └─ Proposes solutions (defer, adapt, pivot)
   └─ Routes to appropriate workflow
   └─ Duration: 30-60 minutes
```

### 8. Leverage Retrospective for Continuous Improvement
```
✓ DO: Run /bmad:bmm:workflows:retrospective after each epic
   └─ Reviews overall success
   └─ Extracts lessons learned
   └─ Explores if new information impacts next epic
   └─ Duration: 30-60 minutes (investment in quality)
```

---

## Common Pitfalls and Solutions

### Pitfall 1: Choosing Wrong Track
```
❌ PROBLEM: Using BMad Method Track for bug fixes (overkill)
✓ SOLUTION: Run workflow-init to get recommendation
   └─ Quick Flow for: Bug fixes, 1-3 related changes, clear scope
   └─ BMad Method for: Products, platforms, complex features
   └─ Let BMAD analyze and recommend
```

### Pitfall 2: Skipping Solutioning Gate Check
```
❌ PROBLEM: Starting implementation with gaps in planning
✓ SOLUTION: Always run solutioning-gate-check before sprint-planning
   └─ Catches inconsistencies between PRD and Architecture
   └─ Identifies missing requirements
   └─ Prevents costly rework during implementation
```

### Pitfall 3: Not Using Story Context
```
❌ PROBLEM: Loading entire codebase for each story (massive token usage)
✓ SOLUTION: Run story-context before dev-story
   └─ Assembles only relevant context
   └─ Creates focused .context.xml file
   └─ Enables efficient story-centric development
```

### Pitfall 4: Not Tracking Story Lifecycle
```
❌ PROBLEM: Losing track of story status across team
✓ SOLUTION: Use story-ready and story-done workflows
   └─ Updates bmm-workflow-status.yaml automatically
   └─ Provides single source of truth for progress
   └─ Enables workflow-status recommendations
```

### Pitfall 5: Ignoring Brownfield Documentation
```
❌ PROBLEM: Adding features to existing code without understanding it
✓ SOLUTION: ALWAYS run document-project first for brownfield
   └─ Analyzes existing codebase
   └─ Documents architecture and patterns
   └─ Provides context for AI-assisted development
```

### Pitfall 6: Not Using Document Sharding
```
❌ PROBLEM: Large projects with 50k+ token PRDs killing performance
✓ SOLUTION: Use document sharding early
   └─ Run /bmad:core:tools:shard-doc on large documents
   └─ Workflows automatically detect sharded format
   └─ Load only needed sections (90%+ savings)
```

---

## Integration with Existing Tools

### JIRA / Azure DevOps Integration
```
BMAD Artifact → Project Management Tool Mapping:

bmm-workflow-status.yaml → JIRA Sprint Board
├─ Story status → JIRA Status (TODO, IN PROGRESS, DONE)
├─ Epic tracking → JIRA Epics
└─ Sprint tracking → JIRA Sprint

PRD.md → JIRA Epic Description
bmm-epics.md → JIRA Epic Breakdown
Story files (stories/*.md) → JIRA Story Descriptions
Story acceptance criteria → JIRA Story Acceptance Criteria

AUTOMATION:
- Sync bmm-workflow-status.yaml to JIRA via API
- Update JIRA stories when story-done workflow completes
- Import JIRA stories into BMAD format
```

### GitHub / GitLab Integration
```
BMAD Artifact → Git Repository Mapping:

docs/ folder:
├─ PRD.md or prd/ → docs/PRD/
├─ Architecture.md → docs/Architecture.md
├─ tech-spec.md → docs/tech-spec.md
├─ bmm-epics.md or epics/ → docs/epics/
├─ bmm-workflow-status.yaml → docs/workflow-status.yaml
└─ stories/ → docs/stories/

.github/workflows/:
└─ bmad-validation.yml (CI/CD validation of BMAD artifacts)

AUTOMATION:
- PR validation checks for planning artifacts
- Automated solutioning-gate-check in CI pipeline
- Story status sync on merge to main
```

### Confluence / Notion Integration
```
BMAD Artifact → Documentation Tool Mapping:

PRD.md → Confluence Product Page
Architecture.md → Confluence Architecture Page
Story context files → Confluence Story Pages

AUTOMATION:
- Export BMAD artifacts to Confluence format
- Link BMAD stories to Confluence documentation
- Sync retrospective notes to Confluence
```

---

## Real-World Workflows

### Real-World Example 1: E-Commerce Checkout Feature

**Project**: Add new checkout flow to existing e-commerce platform
**Team**: 5 developers, 1 PM, 1 Architect, 1 SM
**Track**: BMad Method (Level 3 - Complex feature)

```
WEEK 1: Planning
├─ Day 1: Analyst: /bmad:bmm:workflows:workflow-init
│  └─ Recommends: BMad Method Track
│
├─ Day 2-3: PM: /bmad:bmm:workflows:prd
│  └─ Creates: PRD.md with checkout requirements
│  └─ Duration: 3 hours
│
├─ Day 3: Analyst: /bmad:bmm:workflows:create-epics-and-stories
│  └─ Creates: bmm-epics.md with 3 epics, 12 stories
│  └─ Duration: 45 minutes
│
├─ Day 4: Architect: /bmad:bmm:workflows:architecture
│  └─ Creates: Architecture.md with payment integration design
│  └─ Duration: 3 hours
│
└─ Day 5: Architect: /bmad:bmm:workflows:solutioning-gate-check
   └─ Validates: All planning complete, no critical issues
   └─ Duration: 20 minutes

WEEK 2-4: Implementation (3 two-week sprints)
├─ Sprint 1: Epic 1 (Cart management) - 4 stories
│  └─ SM runs: sprint-planning → epic-tech-context → create-story
│  └─ Devs run: story-context → story-ready → dev-story → story-done
│  └─ Result: 4 stories DONE
│
├─ Sprint 2: Epic 2 (Payment processing) - 5 stories
│  └─ Same workflow
│  └─ Result: 5 stories DONE
│
└─ Sprint 3: Epic 3 (Order confirmation) - 3 stories
   └─ Same workflow
   └─ Result: 3 stories DONE

WEEK 5: Retrospective
└─ SM: /bmad:bmm:workflows:retrospective
   └─ Lessons learned documented
   └─ Insights for next epic

TOTAL TIME:
- Planning: 1 week
- Implementation: 3 sprints (6 weeks)
- Retrospective: 1 day
- Total: 7 weeks (on schedule)
```

---

### Real-World Example 2: Bug Fix

**Project**: Fix critical payment processing bug
**Team**: 1 developer
**Track**: Quick Flow (Level 0 - Bug fix)

```
SAME DAY:
├─ 9:00 AM: Dev: /bmad:bmm:workflows:workflow-init
│  └─ Recommends: Quick Flow Track
│  └─ Duration: 2 minutes
│
├─ 9:05 AM: Dev: /bmad:bmm:workflows:tech-spec
│  └─ Creates: tech-spec.md with bug description and fix approach
│  └─ Duration: 15 minutes
│
├─ 9:25 AM: Dev: /bmad:bmm:workflows:sprint-planning
│  └─ Creates: bmm-workflow-status.yaml
│  └─ Duration: 5 minutes
│
├─ 9:30 AM: Dev: /bmad:bmm:workflows:story-context
│  └─ Loads relevant payment code context
│  └─ Duration: 3 minutes
│
├─ 9:35 AM: Dev: /bmad:bmm:workflows:story-ready
│  └─ Marks story IN PROGRESS
│
├─ 9:40 AM - 11:30 AM: Dev: /bmad:bmm:workflows:dev-story
│  └─ Fixes bug with AI assistance
│  └─ Writes tests, verifies fix
│  └─ Duration: 2 hours
│
└─ 11:35 AM: Dev: /bmad:bmm:workflows:story-done
   └─ Marks story DONE

TOTAL TIME: 2.5 hours (25 minutes planning, 2 hours coding)
BENEFIT: Clear documentation, testable fix, no regression
```

---

## Summary

BMAD v6 provides a comprehensive AI-driven agile framework that adapts to:

**Project Complexity**: Quick Flow → BMad Method → Enterprise
**Team Size**: Solo → Small → Medium → Large → Enterprise
**Methodology**: Agile/Scrum, Kanban, Waterfall, Hybrid
**Project Type**: Greenfield, Brownfield, Microservices, API-first, Mobile, Data Engineering

**Key Success Factors**:
1. Always start with `/bmad:bmm:workflows:workflow-init`
2. Use the recommended track (Quick Flow vs BMad Method vs Enterprise)
3. Run solutioning-gate-check before implementation (BMad Method)
4. Use story-context for efficient just-in-time context loading
5. Track progress with bmm-workflow-status.yaml
6. Use correct-course for mid-sprint changes
7. Run retrospective after each epic for continuous improvement

**19+ Agents | 50+ Workflows | Scale-Adaptive Intelligence**

---

**Version**: 6.0
**Last Updated**: 2025-01-05
**Framework**: BMAD v6 (BMad-CORE + BMad Method)
