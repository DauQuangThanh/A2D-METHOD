# Change Request Workflow During Feature Development

**Handling Mid-Development Changes with BMAD v6**

**Date**: 2025-11-05
**Version**: 6.0
**Context**: BMAD v6 (BMad-CORE + BMad Method)

---

## Executive Summary

**Scenario**: You're actively coding a feature when a change request comes in that affects the current feature.

**Key Question**: Should you accept the change now or defer it to later?

**BMAD v6 Solution**: Use the `/bmad:bmm:workflows:correct-course` workflow for systematic change impact analysis and decision-making.

**Decision Framework**: This guide provides structured workflows for assessing, accepting, or deferring change requests while minimizing disruption and maintaining quality in BMAD v6 projects.

---

## Table of Contents

1. [Initial Assessment: Accept or Defer?](#initial-assessment-accept-or-defer)
2. [Change Impact Analysis with BMAD v6](#change-impact-analysis-with-bmad-v6)
3. [Workflow: Minor Changes (Accept)](#workflow-minor-changes-accept)
4. [Workflow: Major Changes (Defer or Accept)](#workflow-major-changes-defer-or-accept)
5. [Workflow: Scope Changes (Usually Defer)](#workflow-scope-changes-usually-defer)
6. [Handling Partially Completed Work](#handling-partially-completed-work)
7. [Communication Patterns](#communication-patterns)
8. [Real-World Scenarios](#real-world-scenarios)
9. [Best Practices](#best-practices)
10. [Anti-Patterns to Avoid](#anti-patterns-to-avoid)

---

## Initial Assessment: Accept or Defer?

### Decision Tree

```
┌─────────────────────────────────────────────────────────────────────────┐
│               BMAD v6 CHANGE REQUEST DECISION TREE                       │
└─────────────────────────────────────────────────────────────────────────┘

Change Request Received
        │
        ▼
   Is it a bug fix?
        ├─ YES → ACCEPT IMMEDIATELY (security/critical)
        │        DEFER TO NEXT SPRINT (minor)
        │
        └─ NO → Continue assessment
                │
                ▼
   Does it change core requirements?
        ├─ YES → Does it invalidate existing work?
        │        ├─ YES (>50% rework) → RUN correct-course → LIKELY DEFER
        │        └─ NO (<50% rework) → RUN correct-course → Continue assessment
        │
        └─ NO → Continue assessment
                │
                ▼
   What is current implementation progress?
        ├─ 0-25% complete → LIKELY ACCEPT (low sunk cost)
        ├─ 25-75% complete → RUN correct-course → ASSESS CAREFULLY
        └─ 75-100% complete → LIKELY DEFER (high sunk cost)
                │
                ▼
   What is the urgency?
        ├─ CRITICAL (blocks production) → ACCEPT
        ├─ HIGH (business opportunity) → RUN correct-course → ASSESS IMPACT
        ├─ MEDIUM (nice to have) → LIKELY DEFER
        └─ LOW (future enhancement) → DEFER TO BACKLOG
                │
                ▼
   What is the change size?
        ├─ MINOR (affects 1-2 stories, <4 hours) → ACCEPT IF <75% done
        ├─ MODERATE (affects 3-5 stories, 1-2 days) → RUN correct-course
        └─ MAJOR (affects entire epic, >2 days) → RUN correct-course → LIKELY DEFER
                │
                ▼
   DECISION: Accept or Defer?
        │
        ▼
   Use BMAD v6 correct-course workflow for systematic analysis
```

---

### Quick Assessment Matrix

| Current Progress | Change Size    | Urgency       | Recommendation                                    |
| ---------------- | -------------- | ------------- | ------------------------------------------------- |
| 0-25%            | Minor          | Any           | **ACCEPT** - Low sunk cost                        |
| 0-25%            | Moderate       | Critical/High | **RUN correct-course** - Early enough to pivot    |
| 0-25%            | Major          | Critical      | **RUN correct-course** - Reassess entire approach |
| 0-25%            | Major          | Medium/Low    | **DEFER** - Too much scope change                 |
| 25-75%           | Minor          | Any           | **ACCEPT** - Manageable addition                  |
| 25-75%           | Moderate       | Critical      | **RUN correct-course** - Business need vs cost    |
| 25-75%           | Moderate       | Medium/Low    | **DEFER** - Significant disruption                |
| 25-75%           | Major          | Any           | **RUN correct-course** - Likely DEFER             |
| 75-100%          | Minor          | Critical      | **ACCEPT** - Quick addition                       |
| 75-100%          | Minor          | Medium/Low    | **DEFER** - Deliver current, then add             |
| 75-100%          | Moderate/Major | Any           | **DEFER** - Too close to completion               |

---

## Change Impact Analysis with BMAD v6

### Step 1: Use correct-course Workflow

**BMAD v6 provides a dedicated workflow for change management.**

```bash
# When change request received
Load SM agent, then run: *correct-course
→ Workflow analyzes:
   - Current sprint progress (reads bmm-workflow-status.yaml)
   - Change impact on PRD/Architecture/Epics/Stories
   - Completed vs in-progress vs pending stories
   - Effort estimates
   - Recommendations (defer, adapt, pivot)
→ Duration: 30-60 minutes
```

### Step 2: Review Current State

**The correct-course workflow automatically reviews:**

```
CURRENT STATE ANALYSIS (Automated by correct-course):
════════════════════════════════════════════════════════════════════════

Project: [Feature Name]
Track: Quick Flow / BMad Method / Enterprise
Current Epic: [Epic Number]
Current Story: [Story Number]

PROGRESS:
├─ Stories Complete: [N] DONE
├─ Stories In Progress: [N] IN PROGRESS
├─ Stories Pending: [N] TODO
├─ Overall Progress: [XX%] complete
└─ Estimated Time to Completion: [N] hours remaining

ARTIFACTS:
├─ Quick Flow Track:
│  └─ tech-spec.md
│
└─ BMad Method Track:
   ├─ PRD.md (or prd/)
   ├─ Architecture.md
   ├─ bmm-epics.md (or epics/)
   ├─ bmm-workflow-status.yaml
   └─ stories/ ([N] story files)

CHANGE REQUEST:
└─ [Brief description of change]
```

### Step 3: Impact Assessment

**The correct-course workflow calculates:**

```
CHANGE ANALYSIS (Automated by correct-course):
════════════════════════════════════════════════════════════════════════

CHANGE TYPE:
├─ [ ] Requirement Addition (new functionality)
├─ [ ] Requirement Modification (change existing)
├─ [ ] Requirement Removal (delete functionality)
├─ [ ] Non-Functional Change (performance, security, etc.)
└─ [ ] Bug Fix (fix defect in current implementation)

AFFECTED ARTIFACTS:
├─ Quick Flow:
│  └─ tech-spec.md: [Sections affected]
│
└─ BMad Method:
   ├─ PRD.md: [Epics/sections affected]
   ├─ Architecture.md: [Decisions/patterns affected]
   ├─ bmm-epics.md: [Epics affected]
   └─ stories/: [Stories affected]

IMPACT ON COMPLETED WORK:
├─ Stories to Redo: [N] stories ([X] hours)
├─ Stories to Modify: [N] stories ([X] hours)
└─ Completed Stories Unaffected: [N] stories

NEW WORK REQUIRED:
├─ New Stories: [N] stories ([X] hours)
├─ Modified Stories: [N] stories ([X] hours additional)
└─ Total Additional Effort: [X] hours

TOTAL CHANGE COST:
├─ Wasted Effort: [X] hours (completed work to redo)
├─ Additional Effort: [X] hours (new/modified work)
└─ TOTAL CHANGE COST: [X] hours

CHANGE SIZE CLASSIFICATION:
└─ [ ] MINOR: <4 hours, 1-2 stories affected
   [ ] MODERATE: 4-16 hours, 3-5 stories affected
   [ ] MAJOR: >16 hours, >5 stories affected, or >50% rework

RECOMMENDATION:
└─ [ ] ACCEPT NOW (implement immediately)
   [ ] DEFER TO NEXT SPRINT (complete current first)
   [ ] DEFER TO BACKLOG (not urgent enough)
   [ ] PIVOT (major change, restart planning)
```

---

## Workflow: Minor Changes (Accept)

**Definition**: Minor change = <4 hours, 1-2 stories, no major rework

### Scenario

```
CURRENT STATE:
├─ Feature: User Registration (Epic 1)
├─ Track: BMad Method
├─ Progress: 60% complete (3 of 5 stories DONE)
├─ Current Story: 1-4 (Email validation)

CHANGE REQUEST:
└─ "Add phone number field to registration form"
   └─ Impact: 1 story affected, 1 new story, 3 hours
```

### Workflow: Accept and Integrate

```
┌─────────────────────────────────────────────────────────────────────────┐
│           BMAD v6 MINOR CHANGE WORKFLOW (Accept Immediately)             │
└─────────────────────────────────────────────────────────────────────────┘

STEP 1: Run correct-course Workflow (10 minutes)
├─ Load SM agent, run: *correct-course
│  └─ Input: "Add phone number field to registration form"
│  └─ Analysis: Affects Story 1-1 (registration form), minimal impact
│  └─ Recommendation: ACCEPT - Minor change, early in sprint
│
└─ Decision: Accept the change

────────────────────────────────────────────────────────────────────────────

STEP 2: Update Planning Artifacts (15 minutes)

├─ QUICK FLOW TRACK:
│  └─ Manually edit tech-spec.md
│     └─ Add phone number field requirement
│
└─ BMAD METHOD TRACK:
   ├─ OPTION A (Manual - faster for minor changes):
   │  └─ Edit PRD.md or prd/epic-1.md
   │     └─ Add phone number field to Epic 1 requirements
   │
   └─ OPTION B (Re-run PRD - if major rewrite needed):
      └─ Load PM agent, run: *prd
         └─ Update PRD with new requirement

────────────────────────────────────────────────────────────────────────────

STEP 3: Update Story Files (10 minutes)

├─ Check bmm-workflow-status.yaml:
│  └─ Story 1-1: DONE (registration form UI)
│  └─ Story 1-2: DONE (registration backend)
│  └─ Story 1-3: DONE (email validation)
│  └─ Story 1-4: IN PROGRESS (password validation)
│  └─ Story 1-5: TODO (confirmation email)
│
├─ OPTION A: Create new story
│  └─ Load SM agent, run: *create-story
│     └─ Creates Story 1-6: "Add phone number field"
│     └─ Duration: 15 minutes
│
└─ OPTION B: Modify existing story
   └─ Edit Story 1-1 or Story 1-2 to include phone field
      └─ Add acceptance criteria for phone validation

────────────────────────────────────────────────────────────────────────────

STEP 4: Update Architecture (5 minutes) - BMad Method only
└─ If Architecture.md exists:
   └─ Manually edit Architecture.md
      └─ Add phone number field to User data model

────────────────────────────────────────────────────────────────────────────

STEP 5: Update Sprint Status (Instant)
└─ SM: Update bmm-workflow-status.yaml
   └─ Add Story 1-6 to TODO list (if new story created)
   └─ Or update Story 1-1/1-2 status (if existing story modified)

────────────────────────────────────────────────────────────────────────────

STEP 6: Continue Implementation (3 hours)
├─ Current story: Finish Story 1-4 (password validation)
├─ New story: Implement Story 1-6 (phone number field)
│  └─ Dev: story-context → story-ready → dev-story → code-review → story-done
└─ Continue: Rest of sprint as planned

────────────────────────────────────────────────────────────────────────────

STEP 7: Update Stakeholders (5 minutes)
└─ Communication:
   ├─ To: Product Manager, Team, Scrum Master
   ├─ Message: "Minor change accepted: Added phone number field"
   ├─ Impact: "+3 hours, delivery delayed by 0.5 days"
   ├─ Status: "Currently 55% complete (was 60%), new estimate: +0.5 days"
   └─ Update: bmm-workflow-status.yaml reflects new story

────────────────────────────────────────────────────────────────────────────

TOTAL TIME OVERHEAD: ~40 minutes for change integration
TOTAL ADDITIONAL IMPLEMENTATION: 3 hours
NET IMPACT: 3.5 hours total change cost
```

---

## Workflow: Major Changes (Defer or Accept)

**Definition**: Major change = >16 hours, >5 stories, or >50% rework

### Scenario

```
CURRENT STATE:
├─ Feature: User Registration (Epic 1)
├─ Track: BMad Method
├─ Progress: 60% complete (3 of 5 stories DONE)
├─ Current Story: 1-4 (Email validation)

CHANGE REQUEST:
└─ "Change authentication from email/password to OAuth2 only"
   └─ Impact: Completely different approach, ~70% rework
```

### Decision: Use correct-course Workflow

```
┌─────────────────────────────────────────────────────────────────────────┐
│              BMAD v6 MAJOR CHANGE DECISION PROCESS                       │
└─────────────────────────────────────────────────────────────────────────┘

STEP 1: Run correct-course Workflow (30-60 minutes)
├─ Load SM agent, run: *correct-course
│  └─ Input: "Change authentication from email/password to OAuth2"
│  └─ Workflow analyzes:
│     ├─ Reads bmm-workflow-status.yaml (3 of 5 stories DONE)
│     ├─ Reads PRD.md (email/password approach documented)
│     ├─ Reads Architecture.md (authentication design)
│     ├─ Identifies affected stories: 4 of 5 stories need rework
│     ├─ Calculates effort: 38 hours wasted, 24 hours new = 62 hours total
│     └─ Compares: 62 hours (pivot) vs 32 hours (finish current) + 50 hours (OAuth2 later)
│
├─ Workflow provides:
│  ├─ Impact analysis report
│  ├─ Options:
│  │  ├─ Option A: Accept now (pivot) - 62 hours total remaining
│  │  ├─ Option B: Defer to next sprint - 32 hours + 50 hours = 82 hours
│  │  └─ Option C: Defer to backlog - complete current, add OAuth2 later
│  │
│  └─ Recommendation: [Based on urgency, business value, technical impact]
│
└─ Output: Course correction analysis document

────────────────────────────────────────────────────────────────────────────

STEP 2: Business Justification Analysis (30 minutes)
├─ Why is this change requested?
│  ├─ Security concern? (HIGH priority)
│  ├─ Customer demand? (MEDIUM priority)
│  ├─ Competitive pressure? (MEDIUM priority)
│  └─ Nice to have? (LOW priority)
│
├─ What is the cost of deferring?
│  ├─ Blocks other features? (HIGH cost to defer)
│  ├─ Affects launch timeline? (MEDIUM cost to defer)
│  └─ Just an optimization? (LOW cost to defer)
│
└─ DECISION MATRIX:
   ├─ HIGH priority + HIGH cost to defer → ACCEPT (painful but necessary)
   ├─ HIGH priority + LOW cost to defer → ACCEPT or DEFER (evaluate deeper)
   ├─ MEDIUM priority + HIGH cost → ACCEPT carefully
   ├─ MEDIUM priority + LOW cost → DEFER (finish current, then implement)
   └─ LOW priority → DEFER TO BACKLOG

────────────────────────────────────────────────────────────────────────────

STEP 3: Make Decision with Stakeholders (30 minutes)
└─ Meeting with: Product Manager, Tech Lead, Engineering Manager

   Present correct-course Analysis showing:
   ├─ Current progress: 60% complete, 48 hours invested
   ├─ Change impact: 38 hours wasted, 62 hours total cost
   ├─ Option A (Accept): ~62 hours to implement change
   ├─ Option B (Defer): 32 hours to finish current + 50 hours for OAuth2 later = 82 hours
   └─ Recommendation: [Accept or Defer with rationale from correct-course]

   Decision: [ ] Accept Now  [ ] Defer to Next Sprint  [ ] Defer to Backlog
```

---

### If Decision = ACCEPT (Major Change - Pivot)

```
┌─────────────────────────────────────────────────────────────────────────┐
│         BMAD v6 MAJOR CHANGE WORKFLOW (Accept - Full Re-Plan)           │
└─────────────────────────────────────────────────────────────────────────┘

STEP 1: Stop Current Implementation (Immediate)
├─ Action: Commit current work to feature branch
│  └─ git add .
│  └─ git commit -m "WIP: Save progress before OAuth2 pivot"
│  └─ git push origin feature/001-user-registration
│
├─ Action: Update bmm-workflow-status.yaml
│  └─ Mark current story as PAUSED (add comment)
│  └─ Add note: "PIVOTING TO OAUTH2 - 2025-01-05"
│
└─ Action: Notify team
   └─ "Pausing current implementation for change assessment"

────────────────────────────────────────────────────────────────────────────

STEP 2: Re-Plan Requirements (2-4 hours)

├─ QUICK FLOW TRACK:
│  └─ Edit tech-spec.md
│     └─ Update authentication approach to OAuth2
│     └─ Remove email/password requirements
│     └─ Add OAuth2 requirements
│
└─ BMAD METHOD TRACK:
   ├─ OPTION A: Manually edit PRD.md
   │  └─ Update Epic 1 authentication sections
   │  └─ Remove email/password requirements
   │  └─ Add OAuth2 requirements
   │
   ├─ OPTION B: Re-run PRD workflow (if major rewrite needed)
   │  └─ Load PM agent, run: *prd
   │     └─ Creates new PRD.md with OAuth2 approach
   │
   └─ Update Epics:
      └─ Load Analyst agent, run: *create-epics-and-stories
         └─ Regenerates bmm-epics.md with OAuth2 stories

────────────────────────────────────────────────────────────────────────────

STEP 3: Update Architecture (2-4 hours) - BMad Method Track only
├─ OPTION A: Manually edit Architecture.md
│  └─ Update authentication architecture
│  └─ Add OAuth2 provider integration
│  └─ Update data model (User, OAuthToken entities)
│
└─ OPTION B: Re-run architecture workflow
   └─ Load Architect agent, run: *architecture
      └─ Creates new Architecture.md with OAuth2 design
      └─ Duration: 2-4 hours

────────────────────────────────────────────────────────────────────────────

STEP 4: Validate Consistency (15-30 minutes) - BMad Method Track only
├─ Load Architect agent, run: *solutioning-gate-check
│  └─ Validates: New PRD + Architecture + Epics consistency
│  └─ Must show: 0 critical issues before proceeding
│
└─ IF CRITICAL ISSUES FOUND:
   └─ Fix issues (update PRD/Architecture/Epics)
   └─ Re-run solutioning-gate-check until clean

────────────────────────────────────────────────────────────────────────────

STEP 5: Regenerate Stories (1-2 hours)
├─ Load SM agent, run: *sprint-planning
│  └─ Updates bmm-workflow-status.yaml with new story list
│
├─ Load SM agent, run: *create-story (for each new story)
│  └─ Creates new story files for OAuth2 approach
│  └─ Mark salvageable stories with comment: "REUSE FROM OLD"
│
└─ Review:
   └─ Identify reusable work from old stories
   └─ Example: Story 1-1 "Create registration form UI" might be partially reusable

────────────────────────────────────────────────────────────────────────────

STEP 6: Salvage Reusable Work (2-4 hours)
├─ Review old feature branch:
│  └─ git diff main...feature/001-user-registration
│
├─ Identify reusable code:
│  ├─ UI components (forms, buttons) - likely reusable
│  ├─ Database schema (User table) - needs modification for OAuth2
│  ├─ API structure - likely needs complete rewrite
│  └─ Tests - some reusable, many need rewrite
│
├─ Create new branch:
│  └─ git checkout -b feature/001-user-registration-oauth2
│
└─ Cherry-pick or port reusable work:
   └─ Copy/refactor reusable components
   └─ Update to match new architecture

────────────────────────────────────────────────────────────────────────────

STEP 7: Restart Implementation (N hours)
├─ For each new story:
│  └─ Dev: story-context → story-ready → dev-story → code-review → story-done
│
└─ Track progress: bmm-workflow-status.yaml automatically updated

────────────────────────────────────────────────────────────────────────────

STEP 8: Update Stakeholders (30 minutes)
└─ Communication:
   ├─ Email/Slack to: Product Manager, Team, Scrum Master
   ├─ Subject: "Feature 001 - Major Change Accepted: Email/Password → OAuth2"
   ├─ Content:
   │  ├─ Change summary: What changed and why
   │  ├─ Impact: Original 80 hours → New estimate 72 hours
   │  ├─ Timeline: Original delivery [date] → New delivery [date]
   │  ├─ Salvaged work: 10 hours saved from original effort
   │  └─ Next steps: Restarting implementation with new approach
   │
   └─ Update project tracking:
      ├─ JIRA: Update story estimates
      ├─ Sprint: May need to move to next sprint if too big
      └─ Roadmap: Update delivery date

────────────────────────────────────────────────────────────────────────────

TOTAL TIME OVERHEAD: 8-14 hours for re-planning
TOTAL IMPLEMENTATION TIME: ~62 hours (new approach)
SALVAGED TIME: ~10 hours (reusable work)
NET CHANGE COST: 60-66 hours (vs. 32 hours to finish original)
```

---

### If Decision = DEFER (Major Change)

```
┌─────────────────────────────────────────────────────────────────────────┐
│              BMAD v6 MAJOR CHANGE WORKFLOW (Defer)                       │
└─────────────────────────────────────────────────────────────────────────┘

STEP 1: Document Deferred Change (30 minutes)
├─ Create new epic/feature for deferred change:
│  └─ Load Analyst agent, run: *workflow-init
│     └─ Creates new project/epic for OAuth2 migration
│
├─ QUICK FLOW TRACK:
│  └─ Load Analyst agent, run: *tech-spec
│     └─ Creates tech-spec for OAuth2 migration
│     └─ Output: tech-spec-oauth2.md
│
├─ BMAD METHOD TRACK:
│  ├─ Load PM agent, run: *prd
│  │  └─ Input: "Migrate authentication from email/password to OAuth2"
│  │  └─ Output: PRD-oauth2.md (new PRD for OAuth2 feature)
│  │
│  └─ Load Analyst agent, run: *create-epics-and-stories
│     └─ Creates bmm-epics-oauth2.md
│
├─ Add to product backlog:
│  └─ JIRA: Create new epic "OAuth2 Authentication"
│  └─ Priority: [HIGH/MEDIUM/LOW]
│  └─ Sprint: [Next sprint or later]
│
└─ Link to current feature:
   └─ Add note to current PRD/tech-spec:
      "Future Enhancement: OAuth2 migration planned (see PRD-oauth2.md)"

────────────────────────────────────────────────────────────────────────────

STEP 2: Continue Current Implementation (unchanged)
├─ No changes to current workflow
├─ Complete current feature as originally planned
│  └─ Continue story-by-story: dev-story → code-review → story-done
└─ Deliver on original timeline

────────────────────────────────────────────────────────────────────────────

STEP 3: Plan Deferred Change for Future Sprint
└─ During next backlog refinement:
   ├─ BMad Method Track:
   │  ├─ Architect: /bmad:bmm:workflows:architecture (OAuth2 architecture)
   │  └─ Architect: /bmad:bmm:workflows:solutioning-gate-check
   │
   └─ Estimate separately:
      └─ OAuth2 migration: ~50 hours as separate feature

────────────────────────────────────────────────────────────────────────────

STEP 4: Update Stakeholders (15 minutes)
└─ Communication:
   ├─ To: Product Manager, Requester of change
   ├─ Message: "Change deferred to next sprint to avoid disruption"
   ├─ Rationale:
   │  ├─ Current feature 60% complete (48 hours invested)
   │  ├─ Change would require 62 hours (38 wasted + 24 new)
   │  ├─ More efficient to: Finish current (32h) + OAuth2 later (50h) = 82h total
   │  └─ Benefit: Earlier delivery of current feature, cleaner OAuth2 implementation
   │
   └─ Next steps: OAuth2 scheduled for Sprint [N+1]

────────────────────────────────────────────────────────────────────────────

TOTAL TIME OVERHEAD: 45 minutes (document and communicate)
CURRENT FEATURE: Delivers on time (32 hours remaining)
FUTURE FEATURE: OAuth2 (50 hours, next sprint)
```

---

## Workflow: Scope Changes (Usually Defer)

**Definition**: Scope change = Adding entirely new functionality beyond original spec

### Scenario

```
CURRENT STATE:
├─ Feature: User Registration (Epic 1 - email/password)
├─ Progress: 60% complete
├─ Original Scope: Register, login, password reset

CHANGE REQUEST:
└─ "Add social login (Google, Facebook, GitHub)"
   └─ This is NEW functionality, not modification of existing
```

### Recommended Approach: Defer as Separate Epic/Feature

```
┌─────────────────────────────────────────────────────────────────────────┐
│         BMAD v6 SCOPE CHANGE WORKFLOW (Defer as Separate)                │
└─────────────────────────────────────────────────────────────────────────┘

STEP 1: Run correct-course Workflow (15 minutes)
├─ Load SM agent, run: *correct-course
│  └─ Input: "Add social login (Google, Facebook, GitHub)"
│  └─ Analysis: This is scope addition, not modification
│  └─ Recommendation: Defer as separate epic/feature
│
└─ Decision: DEFER as separate epic

────────────────────────────────────────────────────────────────────────────

STEP 2: Create Separate Epic/Feature Spec (30-60 minutes)

├─ QUICK FLOW TRACK:
│  └─ Load Analyst agent, run: *tech-spec
│     └─ Creates tech-spec for social login
│     └─ Output: tech-spec-social-login.md
│
└─ BMAD METHOD TRACK:
   ├─ Add to existing PRD:
   │  └─ Edit PRD.md to add Epic 4: Social Login
   │  └─ OR create separate PRD-social-login.md
   │
   ├─ Load Analyst agent, run: *create-epics-and-stories
   │  └─ Regenerates bmm-epics.md (adds Epic 4)
   │  └─ OR creates separate epic breakdown
   │
   └─ Note relationship:
      ├─ In PRD.md: "Epic 4: Social Login (Depends on Epic 1)"
      └─ In current Epic 1: "Future Enhancement: Social login (see Epic 4)"

────────────────────────────────────────────────────────────────────────────

STEP 3: Continue Current Feature (unchanged)
└─ No disruption to current implementation
   └─ Deliver Epic 1 (email/password) on time

────────────────────────────────────────────────────────────────────────────

STEP 4: Plan Separate Epic for Future Sprint
└─ In next sprint preparation:
   ├─ BMad Method Track:
   │  ├─ Architect: /bmad:bmm:workflows:architecture (social login integration)
   │  ├─ Architect: /bmad:bmm:workflows:solutioning-gate-check
   │  ├─ SM: /bmad:bmm:workflows:epic-tech-context (Epic 4)
   │  └─ SM: /bmad:bmm:workflows:create-story (Epic 4 stories)
   │
   └─ Implement as independent epic in next sprint

────────────────────────────────────────────────────────────────────────────

STEP 5: Update Stakeholders (15 minutes)
└─ Communication:
   ├─ To: Product Manager, Team
   ├─ Message: "Social login deferred as separate epic (Epic 4)"
   ├─ Rationale: Scope addition, can be implemented independently
   ├─ Timeline: Current epic delivers [date], Social login in next sprint
   └─ Add to backlog: Epic 4 scheduled for Sprint [N+1]

────────────────────────────────────────────────────────────────────────────

TOTAL TIME OVERHEAD: 45 minutes (create new epic, communicate)
CURRENT FEATURE: No impact, delivers on time
NEW FEATURE: Planned as separate epic (independent)
```

---

## Handling Partially Completed Work

### Scenario: Change Invalidates Some Completed Stories

```
CURRENT STATE:
├─ 3 of 5 stories DONE
├─ Change affects 2 of the 3 completed stories
└─ Question: How to handle completed work that needs rework?

BMAD v6 APPROACH:
└─ Use correct-course workflow to analyze salvageable work

OPTIONS:

OPTION 1: Salvage and Refactor (if >50% reusable)
├─ Identify what's salvageable from completed stories
├─ Refactor to match new requirements
├─ Update story files with new acceptance criteria
└─ Mark stories as TODO in bmm-workflow-status.yaml if major rework
   └─ SM: Update bmm-workflow-status.yaml manually or via correct-course

OPTION 2: Discard and Rebuild (if <50% reusable)
├─ Mark affected stories as TODO in bmm-workflow-status.yaml
│  └─ Revert from DONE to TODO
├─ Update story files with new requirements
│  └─ Load SM agent, run: *create-story (regenerate stories)
└─ Reimplement from scratch with new approach

OPTION 3: Hybrid (common)
├─ Some completed work salvageable (UI components, database schema)
├─ Some completed work discarded (authentication logic)
└─ Update bmm-workflow-status.yaml:
   └─ Story 1-1: DONE (UI reusable)
   └─ Story 1-2: TODO (backend needs rework)
   └─ Story 1-3: TODO (authentication logic needs complete rewrite)
```

---

### Best Practice: Track Salvaged Work in bmm-workflow-status.yaml

```yaml
# bmm-workflow-status.yaml Example

project_info:
  name: "User Registration"
  track: "method"
  level: 3

# CHANGE REQUEST ACCEPTED: 2025-01-05
# Changed from email/password to OAuth2 authentication
# Salvaging reusable work from original implementation

sprint_status:
  current_epic: 1
  current_story: 4

  stories:
    # Original stories (salvageable)
    - id: "1-1"
      name: "Create registration form UI"
      status: done  # REUSABLE - UI structure same
      notes: "UI reusable, update OAuth2 button"

    - id: "1-2"
      name: "Create User model"
      status: done  # PARTIALLY REUSABLE - needs OAuth fields
      notes: "Needs OAuthToken relationship added"

    # Original stories (discarded)
    - id: "1-3"
      name: "Implement email/password authentication"
      status: removed  # DISCARDED - not needed for OAuth2
      notes: "Replaced by stories 1-6, 1-7, 1-8"

    # New stories for OAuth2
    - id: "1-6"
      name: "Configure OAuth2 providers"
      status: todo
      epic: 1
      acceptance_criteria: "Google, GitHub, Microsoft configured"

    - id: "1-7"
      name: "Implement OAuth2 callback handlers"
      status: todo
      epic: 1

    - id: "1-8"
      name: "Implement OAuth2 session management"
      status: todo
      epic: 1
```

---

## Communication Patterns

### Template 1: Communicating Accepted Minor Change

```
TO: Product Manager, Team, Scrum Master
SUBJECT: Change Accepted - [Feature Name] - [Brief Change Description]

Hi team,

We've accepted a change request to the current feature using BMAD v6 correct-course workflow:

FEATURE: [Feature Name]
TRACK: [Quick Flow / BMad Method / Enterprise]
CHANGE: [Brief description]

IMPACT:
├─ Stories Added: [N] stories
├─ Time Added: [X] hours
├─ Current Progress: [XX%] → [XX%] (adjusted for new stories)
├─ Original Delivery: [Date]
└─ New Delivery: [Date] (+[N] days)

RATIONALE:
[Why we accepted this change now vs. deferring - from correct-course analysis]

NEXT STEPS:
├─ Updated: PRD/tech-spec with new requirements
├─ Updated: bmm-workflow-status.yaml with new stories
└─ Continuing: Implementation with new stories integrated

STATUS:
Implementation continuing with new stories added to sprint.

Thanks,
[Your Name]
```

---

### Template 2: Communicating Deferred Major Change

```
TO: Product Manager, Change Requester, Team
SUBJECT: Change Deferred - [Feature Name] - [Brief Change Description]

Hi team,

We've assessed a change request using BMAD v6 correct-course workflow and recommend deferring to next sprint:

CURRENT FEATURE: [Feature Name]
├─ Track: [Quick Flow / BMad Method / Enterprise]
├─ Current Progress: [XX%] complete ([N] of [M] stories DONE)
├─ Hours Invested: [N] hours
└─ Est. Time to Complete: [N] hours

CHANGE REQUEST: [Brief description]
├─ Change Type: [Major/Moderate/Minor]
├─ Estimated Impact: [N] hours rework + [N] hours new work = [N] total
├─ Stories Affected: [N] stories ([N] DONE, [N] IN PROGRESS, [N] TODO)
└─ Urgency: [Critical/High/Medium/Low]

RECOMMENDATION: Defer to Next Sprint

RATIONALE (from correct-course analysis):
├─ Current investment: [N] hours (sunk cost)
├─ Change would waste: [N] hours of completed work
├─ More efficient approach:
│  ├─ Option A (Accept Now): [N] total hours
│  └─ Option B (Defer): [N] hours to finish current + [N] hours for change later = [N] total
│
├─ Change urgency: [Low/Medium] - not blocking
└─ Better outcome: Clean implementation of change as separate epic/feature

NEXT STEPS:
├─ Current feature: Continue as planned, deliver [Date]
├─ Change request: New epic/feature created (PRD/tech-spec created)
├─ New feature: Planned for Sprint [N+1]
└─ Estimation: [N] hours as separate feature

Please confirm this approach or let's discuss if urgent.

Thanks,
[Your Name]
```

---

### Template 3: Communicating Accepted Major Change (Pivot)

```
TO: Product Manager, Engineering Manager, Team, Stakeholders
SUBJECT: MAJOR CHANGE - [Feature Name] - Implementation Pivot

Hi team,

We've accepted a major change request that requires pivoting our approach:

CURRENT FEATURE: [Feature Name]
├─ Track: [Quick Flow / BMad Method / Enterprise]
├─ Original Approach: [Description]
├─ Current Progress: [XX%] complete ([N] hours invested, [N] of [M] stories DONE)
└─ Original Estimate: [N] hours

CHANGE REQUEST: [Description]
├─ Impact: [Major change to core approach]
└─ Urgency: [Critical/High] - [Reason]

DECISION: Accept Change (Pivot Implementation)

IMPACT ANALYSIS (from correct-course workflow):
├─ Wasted Effort: [N] hours (work that must be discarded)
├─ Salvageable Work: [N] hours (work we can reuse/refactor)
├─ New Work Required: [N] hours
├─ Total New Estimate: [N] hours
└─ Timeline Impact: [N] days delay

APPROACH:
├─ STEP 1: Stop current implementation ✓
├─ STEP 2: Re-specify with new requirements (ETA: [Date])
├─ STEP 3: Re-architect (BMad Method only) (ETA: [Date])
├─ STEP 4: Regenerate stories (ETA: [Date])
├─ STEP 5: Restart implementation (ETA: [Date])
└─ STEP 6: New delivery date (ETA: [Date])

RATIONALE:
[Why accepting this change now despite cost - from correct-course recommendation]

DELIVERABLES UPDATED:
├─ Quick Flow:
│  └─ tech-spec.md: Updated ✓ / In Progress / Pending
│
└─ BMad Method:
   ├─ PRD.md: Updated ✓ / In Progress / Pending
   ├─ Architecture.md: Updated ✓ / In Progress / Pending
   ├─ bmm-epics.md: Updated ✓ / In Progress / Pending
   ├─ bmm-workflow-status.yaml: Updated ✓
   ├─ New Estimate: [N] hours ([+/-X] from original)
   └─ New Delivery: [Date] ([+/-N] days from original)

STAKEHOLDER ACTION REQUIRED:
└─ Please confirm approval for this pivot and timeline change.

Current status: [Paused/Re-planning/Restarting]

Thanks,
[Your Name]
```

---

## Real-World Scenarios

### Scenario 1: UI Requirement Change (Minor - Accept)

```
SITUATION:
├─ Feature: Product Catalog
├─ Track: BMad Method
├─ Progress: 70% complete (7 of 10 stories DONE)
├─ Current Story: 3-2 (Product grid layout)
├─ Change: "Add filter by price range"
└─ Impact: 1 new story, 4 hours

WORKFLOW:

1. Run correct-course (10 min):
   └─ Load SM agent, run: *correct-course
      └─ Analysis: Minor change, late stage, but clean addition
      └─ Recommendation: ACCEPT

2. Update PRD.md (5 min):
   └─ Add "Price range filter" to Epic 3 requirements

3. Update Architecture.md (5 min) - if applicable:
   └─ No architecture change needed (uses existing filtering system)

4. Create new story (15 min):
   └─ Load SM agent, run: *create-story
      └─ Creates Story 3-11: "Add price range filter"
      └─ Updates bmm-workflow-status.yaml

5. Continue implementation (4 hours):
   └─ Finish current story → Implement new story → Rest of epic
      └─ Dev: story-context → story-ready → dev-story → code-review → story-done

OUTCOME:
├─ Overhead: 35 minutes
├─ Additional work: 4 hours
├─ Delivery delay: +0.5 days
└─ Stakeholder satisfaction: High (got requested feature)
```

---

### Scenario 2: Business Logic Change (Moderate - Defer)

```
SITUATION:
├─ Feature: E-commerce Checkout
├─ Track: BMad Method
├─ Progress: 50% complete (5 of 10 stories DONE)
├─ Current Story: 2-6 (Payment processing)
├─ Change: "Add support for payment plans (installments)"
└─ Impact: 3 stories affected, 5 new stories, 16 hours

WORKFLOW:

1. Run correct-course (30 min):
   └─ Load SM agent, run: *correct-course
      └─ Input: "Add payment plans (installments)"
      └─ Analysis:
         ├─ Moderate change
         ├─ Affects 2 completed stories (payment logic)
         ├─ Requires 5 new stories (16 hours)
         └─ Total cost: 24 hours vs 20 hours to finish current
      └─ Recommendation: DEFER to next sprint

2. Business Discussion (30 min):
   ├─ Urgency: Medium (customer request, not critical)
   ├─ Recommendation: Defer to next sprint
   └─ Decision: DEFER

3. Create New Epic/Feature (30 min):
   ├─ Add to PRD.md as Epic 5: "Payment Plans"
   │  └─ OR create separate PRD-payment-plans.md
   │
   └─ Load Analyst agent, run: *create-epics-and-stories
      └─ Updates bmm-epics.md with Epic 5

4. Continue Current Feature (unchanged):
   └─ Deliver checkout with single payments on time

5. Plan Payment Plans for Next Sprint:
   └─ Scheduled for Sprint 8 (estimated 24 hours)

OUTCOME:
├─ Current feature: Delivered on time
├─ Payment plans: Clean implementation in next sprint
├─ Total effort saved: 8 hours (avoided rework)
└─ Customer: Gets payment plans 2 weeks later (acceptable trade-off)
```

---

### Scenario 3: Security Requirement (Critical - Accept Immediately)

```
SITUATION:
├─ Feature: User Profile Management
├─ Track: BMad Method
├─ Progress: 80% complete (8 of 10 stories DONE)
├─ Current Story: 4-9 (Profile editing)
├─ Change: "Security audit found vulnerability - must encrypt all PII fields"
└─ Impact: 6 stories affected, 20 hours rework

WORKFLOW:

1. Run correct-course (15 min):
   └─ Load SM agent, run: *correct-course
      └─ Analysis: Critical security issue
      └─ Recommendation: ACCEPT IMMEDIATELY (no choice)

2. Security Assessment (1 hour):
   ├─ Critical security issue
   ├─ Must be fixed before production
   └─ Decision: ACCEPT IMMEDIATELY

3. Stop Implementation (immediate):
   └─ Halt current work, commit WIP

4. Update Planning Artifacts (2 hours):
   ├─ Update PRD.md: Add encryption requirements
   ├─ Update Architecture.md: Add encryption layer design
   └─ Update bmm-epics.md: Add encryption to affected stories

5. Regenerate/Update Stories (1 hour):
   ├─ Update affected story files with encryption requirements
   ├─ Load SM agent, run: *create-story (for new stories if needed)
   └─ Update bmm-workflow-status.yaml:
      └─ Mark affected DONE stories as TODO (need rework)

6. Implement Encryption (20 hours):
   └─ Rework stories with encryption:
      └─ Dev: story-context → story-ready → dev-story → code-review → story-done

7. Extended Testing (8 hours):
   └─ TEA: /bmad:bmm:workflows:testarch:automate
      └─ Additional security testing required

OUTCOME:
├─ Feature delayed: +1 week
├─ Rework cost: 20 hours
├─ Security: Vulnerability fixed ✓
└─ Result: Correct decision (security > schedule)
```

---

### Scenario 4: Feature Creep (Low Priority - Reject/Defer to Backlog)

```
SITUATION:
├─ Feature: Admin Dashboard
├─ Track: BMad Method
├─ Progress: 40% complete (4 of 10 stories DONE)
├─ Current Story: 2-5 (Dashboard metrics)
├─ Change: "Add real-time chat support to dashboard"
└─ Impact: Entirely new feature, 40+ hours, unrelated to current epic

WORKFLOW:

1. Run correct-course (15 min):
   └─ Load SM agent, run: *correct-course
      └─ Analysis: This is feature creep, not a change request
      └─ Recommendation: REJECT or DEFER TO BACKLOG

2. Scope Assessment (15 min):
   ├─ This is scope addition, unrelated to admin dashboard
   └─ Should be separate epic entirely

3. Discussion with Product Manager (15 min):
   ├─ Clarify: Is chat support required for admin dashboard?
   └─ Answer: No, nice-to-have for future

4. Decision: DEFER TO BACKLOG
   └─ Not in scope of current epic

5. Create Backlog Epic (30 min):
   ├─ Load PM agent, run: *prd (or add Epic to existing PRD)
   │  └─ Creates Epic: "Real-time Chat Support"
   │
   └─ Add to backlog:
      ├─ Priority: P3 (Low)
      └─ Status: Backlog (not scheduled)

6. Continue Current Feature (unchanged):
   └─ No impact to current work

OUTCOME:
├─ Current feature: No disruption
├─ Chat feature: Properly scoped as separate epic
├─ Product Manager: Understands scope boundaries
└─ Backlog: Organized with separate priorities
```

---

## Best Practices

### 1. Always Use correct-course for Change Assessment

```
❌ DON'T:
└─ Immediately accept or reject changes without analysis

✓ DO:
├─ Load SM agent, run: *correct-course
├─ Get systematic impact analysis
├─ Review recommendations (defer, adapt, pivot)
└─ Make informed decision with data
```

---

### 2. Use bmm-workflow-status.yaml as Single Source of Truth

```
❌ DON'T:
└─ Accept verbal change requests without updating artifacts

✓ DO:
├─ Always update PRD.md or tech-spec.md first
├─ Update bmm-workflow-status.yaml with new stories
├─ Keep all artifacts in sync
└─ PRD/tech-spec + bmm-workflow-status.yaml = complete picture
```

---

### 3. Communicate Impact Clearly

```
❌ DON'T:
└─ "Sure, I can add that" (without understanding impact)

✓ DO:
├─ Run correct-course first
├─ Provide concrete numbers from analysis: hours, stories affected, delivery delay
├─ Present options: accept now vs defer (from correct-course)
└─ Get explicit approval for timeline changes
```

---

### 4. Preserve Completed Work When Possible

```
❌ DON'T:
└─ Discard all completed stories when change comes

✓ DO:
├─ Use correct-course to identify salvageable work
├─ Identify reusable stories (UI, tests, infrastructure)
├─ Refactor vs rebuild decision
├─ Mark salvageable stories clearly in bmm-workflow-status.yaml
└─ Maximize reuse to reduce waste
```

---

### 5. Make Defer the Default for Non-Critical Changes

```
❌ DON'T:
└─ Accept every change request to be "helpful"

✓ DO:
├─ Default to defer unless:
│  ├─ Security/critical issue
│  ├─ Blocks other work
│  └─ Very early in implementation (<25% done)
├─ Finish current epic cleanly
└─ Implement change as separate epic
```

---

### 6. Use Party Mode for Complex Change Decisions

```
✓ DO (when appropriate):
├─ Load party mode: /bmad:core:workflows:party-mode
├─ Then run: correct-course within party mode
├─ Get perspectives from:
│  ├─ PM: Business impact
│  ├─ Architect: Technical feasibility
│  ├─ SM: Sprint impact
│  └─ Dev: Implementation complexity
└─ Collaborative decision with diverse perspectives
```

---

### 7. Track Change Request Metrics

```
✓ DO:
├─ Track: Number of change requests per epic
├─ Track: Percentage of changes accepted vs deferred
├─ Track: Average rework cost per accepted change
├─ Track: Reasons for changes (scope creep, unclear requirements, etc.)
└─ Use in retrospective workflow to improve planning quality
```

---

## Anti-Patterns to Avoid

### Anti-Pattern 1: "Yes to Everything"

```
❌ PROBLEM:
├─ Accepting every change request without running correct-course
├─ Never saying no or defer
└─ Constant rework, never finishing anything

✓ SOLUTION:
├─ Use correct-course workflow to evaluate objectively
├─ Make defer the default for non-critical changes
└─ Get stakeholder buy-in for defer decisions
```

---

### Anti-Pattern 2: "Scope Creep Acceptance"

```
❌ PROBLEM:
├─ Epic grows from 5 stories to 15 stories
├─ "Just one more thing" repeated 10 times
└─ Epic never delivers

✓ SOLUTION:
├─ Clearly define scope in PRD.md or tech-spec.md
├─ Use correct-course to distinguish changes vs new epics
├─ Move new epics to separate PRD sections or files
└─ Deliver incrementally (MVP first, enhancements later)
```

---

### Anti-Pattern 3: "Undocumented Verbal Changes"

```
❌ PROBLEM:
├─ "Can you change X to Y?" → "Sure!" → implements without updating PRD
├─ No trace of what changed or why
└─ Confusion later about what was agreed

✓ SOLUTION:
├─ ALWAYS update PRD.md or tech-spec.md for changes
├─ Use correct-course to document decisions
├─ Update bmm-workflow-status.yaml with new stories
└─ PRD/tech-spec is single source of truth
```

---

### Anti-Pattern 4: "Change Without Validation"

```
❌ PROBLEM:
├─ Accept change, update PRD.md, continue coding
├─ Skip solutioning-gate-check (BMad Method Track)
└─ Miss conflicts and inconsistencies

✓ SOLUTION:
├─ After any PRD/Architecture/Epic change (BMad Method Track)
├─ ALWAYS re-run solutioning-gate-check
├─ Fix critical issues before continuing
└─ Gate check is your safety net
```

---

### Anti-Pattern 5: "Sunk Cost Fallacy"

```
❌ PROBLEM:
├─ "We've invested 40 hours, we can't change now!"
├─ Proceed with wrong approach
└─ Deliver wrong solution

✓ SOLUTION:
├─ Sunk costs are sunk (can't recover them)
├─ Use correct-course to make forward-looking decisions
├─ Compare: cost to pivot vs. cost of wrong solution in production
└─ Sometimes pivoting late is still right decision
```

---

## Summary: Decision Framework

```
┌─────────────────────────────────────────────────────────────────────────┐
│              BMAD v6 CHANGE REQUEST DECISION SUMMARY                     │
└─────────────────────────────────────────────────────────────────────────┘

PRIMARY TOOL: /bmad:bmm:workflows:correct-course
└─ Use this workflow for ALL change requests
   └─ Provides systematic analysis and recommendations

WHEN TO ACCEPT IMMEDIATELY:
├─ Security/critical issues (no choice)
├─ Minor changes (<4 hours, early in sprint)
├─ Bug fixes (fix defects in current implementation)
└─ Blocking changes (prevents other work)

WHEN TO DEFER:
├─ Major changes (>16 hours) when >50% complete
├─ Scope additions (new epics, not modifications)
├─ Non-urgent changes (nice-to-have)
└─ Changes that invalidate >50% of completed work

WHEN TO REJECT:
├─ Feature creep (unrelated new epics)
├─ Low-priority changes with high rework cost
└─ Changes that contradict established architecture

WORKFLOW FOR ACCEPTED CHANGES:

Quick Flow Track:
1. Run correct-course workflow
2. Update tech-spec.md
3. Update bmm-workflow-status.yaml (add/modify stories)
4. Continue implementation
5. Communicate impact to stakeholders

BMad Method Track:
1. Run correct-course workflow
2. Update PRD.md (or prd/)
3. Update Architecture.md (if architectural impact)
4. Update bmm-epics.md (if epic structure changes)
5. Run solutioning-gate-check (validate consistency)
6. Update bmm-workflow-status.yaml (add/modify stories)
7. Create new story files (if new stories needed)
8. Continue/restart implementation
9. Communicate impact to stakeholders

WORKFLOW FOR DEFERRED CHANGES:

Quick Flow Track:
1. Run correct-course workflow
2. Create new tech-spec for deferred change
3. Add to backlog (future sprint)
4. Continue current feature unchanged
5. Plan deferred feature separately
6. Communicate decision and rationale

BMad Method Track:
1. Run correct-course workflow
2. Add new epic to PRD.md (or create separate PRD)
3. Run create-epics-and-stories (if needed)
4. Add to backlog (future sprint/epic)
5. Continue current epic unchanged
6. Plan deferred epic separately
7. Communicate decision and rationale

KEY METRICS TO TRACK:
├─ Change request rate per epic
├─ Accept vs defer ratio
├─ Average rework cost
├─ Reasons for changes (improve planning in retrospective)
└─ Track in bmm-workflow-status.yaml or separate change log
```

---

## Key BMAD v6 Change Management Features

### 1. correct-course Workflow
**Primary tool for change management**
- Systematic impact analysis
- Recommendation engine (defer, adapt, pivot)
- Routes to appropriate workflows
- Updates planning artifacts

### 2. bmm-workflow-status.yaml
**Single source of truth for sprint progress**
- Tracks all story statuses
- Easy to see completed vs in-progress vs pending work
- Impact analysis reads this file

### 3. Story-Centric Architecture
**Granular change tracking**
- Changes affect specific stories (not entire feature)
- Can defer some stories while continuing others
- Story independence enables partial changes

### 4. Solutioning Gate Check
**Quality gate for BMad Method Track**
- Validates consistency after changes
- Identifies gaps and contradictions
- Prevents proceeding with incomplete planning

### 5. Modular Artifacts
**Easy to update**
- PRD.md or prd/ (sharded) - easy to add epics
- Architecture.md - document new patterns
- bmm-epics.md or epics/ (sharded) - add stories
- Story files - independent, easy to add/modify

---

## Best Practice Summary

1. **Always run correct-course** for change requests
2. **Update artifacts** (PRD/tech-spec, Architecture, bmm-workflow-status.yaml)
3. **Run solutioning-gate-check** after changes (BMad Method Track)
4. **Communicate clearly** using templates above
5. **Default to defer** unless critical or minor
6. **Track changes** in retrospective for continuous improvement
7. **Use party mode** for complex change decisions

---

**Version**: 6.0
**Last Updated**: 2025-01-05
**Framework**: BMAD v6 (BMad-CORE + BMad Method)
