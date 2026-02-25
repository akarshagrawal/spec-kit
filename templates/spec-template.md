# Modernisation Specification: [FEATURE NAME]

**Feature Branch**: `[###-feature-name]`  
**Created**: [DATE]  
**Status**: Draft  
**Analysis Report**: `specs/[###-feature-name]/analysis-report.md`
**Input**: User description: "$ARGUMENTS"

## Analysis Reference

<!--
  Link to the codebase analysis report that informed this specification.
  Summarise key findings relevant to this modernisation effort.
-->

**Analysis Summary**: [Brief summary of relevant findings from analysis-report.md]
**Legacy System**: [e.g., COBOL mainframe, Oracle 9i, .NET Framework 2.0 or from analysis]  
**Target Architecture**: [e.g., Cloud-native microservices, React SPA + REST API]  
**Migration Strategy**: [e.g., Strangler-Fig, Database-First, API-First]

## Modernisation Research

<!--
  Consolidated research findings from deep-dive into each area.
  Each decision should have rationale and alternatives considered.
-->

### [Research Area 1: e.g., Backend Framework Migration]

**Decision**: [what was chosen]  
**Rationale**: [why chosen]  
**Alternatives Considered**: [what else evaluated and why rejected]  
**Risk**: [identified risks and mitigations]

---

### [Research Area 2: e.g., Database Migration Strategy]

**Decision**: [what was chosen]  
**Rationale**: [why chosen]  
**Alternatives Considered**: [what else evaluated]  
**Risk**: [identified risks]

---

[Add more research areas as needed]

## User Stories & Acceptance Criteria *(mandatory)*

<!--
  IMPORTANT: User stories should be PRIORITISED by modernisation value.
  Each story MUST reference specific files/modules from the analysis report.
  Each story MUST include rollback plan and migration notes.
  
  Priorities:
  - P1: Highest risk + highest business value (modernise first)
  - P2: Medium risk or medium value
  - P3: Low risk, quality-of-life improvements
-->

### User Story 1 - [Brief Title] (Priority: P1)

[Describe this modernisation journey in plain language]

**Source Files**: `[path1]`, `[path2]` (from analysis report)  
**Current Behaviour**: [how it works today]  
**Target Behaviour**: [how it should work after modernisation]

**Why this priority**: [Explain the value and risk justification]

**Acceptance Criteria**:

1. **Given** [current state], **When** [migration action], **Then** [expected modern behaviour]
2. **Given** [current state], **When** [user action], **Then** [expected outcome]

**Migration Notes**: [how to transition without downtime]  
**Rollback Plan**: [how to revert if something goes wrong]  
**Independent Test**: [how to verify this story works on its own]

---

### User Story 2 - [Brief Title] (Priority: P2)

[Describe this modernisation journey in plain language]

**Source Files**: `[path1]`, `[path2]`  
**Current Behaviour**: [how it works today]  
**Target Behaviour**: [how it should work after modernisation]

**Why this priority**: [justification]

**Acceptance Criteria**:

1. **Given** [initial state], **When** [action], **Then** [expected outcome]

**Migration Notes**: [transition approach]  
**Rollback Plan**: [revert strategy]  
**Independent Test**: [verification approach]

---

### User Story 3 - [Brief Title] (Priority: P3)

[Describe this modernisation journey in plain language]

**Source Files**: `[path1]`, `[path2]`  
**Current Behaviour**: [how it works today]  
**Target Behaviour**: [how it should work after modernisation]

**Why this priority**: [justification]

**Acceptance Criteria**:

1. **Given** [initial state], **When** [action], **Then** [expected outcome]

**Migration Notes**: [transition approach]  
**Rollback Plan**: [revert strategy]  
**Independent Test**: [verification approach]

---

[Add more user stories as needed, each with an assigned priority]

### Edge Cases

- What happens during data migration if [boundary condition]?
- How does the system handle [partial migration state]?
- What if [legacy and modern systems are out of sync]?

## Data Model Changes

<!--
  Document schema changes needed for the modernisation.
  Show current → target for each entity.
-->

### [Entity 1]

**Current Schema**: [what it looks like today]  
**Target Schema**: [what it should become]  
**Migration Approach**: [how to transition data]  
**Backward Compatibility**: [how to maintain during migration]

### [Entity 2]

**Current Schema**: [current]  
**Target Schema**: [target]  
**Migration Approach**: [approach]  
**Backward Compatibility**: [compatibility plan]

## Contract Changes *(if applicable)*

<!--
  Document API or interface contract changes.
  Show breaking changes and versioning strategy.
-->

| Endpoint/Interface | Current Contract | Target Contract | Breaking Change? |
|-------------------|-----------------|----------------|-----------------|
| [endpoint] | [current spec] | [target spec] | [Yes/No] |

**Versioning Strategy**: [how API versions will be managed]  
**Consumer Notification Plan**: [how consumers will be informed of changes]

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: System MUST [specific modernised capability]
- **FR-002**: System MUST maintain backward compatibility with [legacy component] during migration
- **FR-003**: System MUST support [parallel run / feature flag / strangler-fig] during transition
- **FR-004**: System MUST [data migration requirement]
- **FR-005**: System MUST [rollback capability]

### Non-Functional Requirements

- **NFR-001**: [Performance target: e.g., "Response time must not increase during migration"]
- **NFR-002**: [Availability: e.g., "Zero downtime migration"]
- **NFR-003**: [Data integrity: e.g., "No data loss during schema migration"]

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: [Before/After metric, e.g., "User task completion: 2min → 30sec"]
- **SC-002**: [Performance metric, e.g., "System handles 10,000 concurrent users (was 2,000)"]
- **SC-003**: [Reliability metric, e.g., "Mean time to recovery: 4hrs → 15min"]
- **SC-004**: [Developer metric, e.g., "Deployment frequency: monthly → daily"]

## Task Breakdown

<!--
  Ordered task list derived from user stories.
  [P] = can run in parallel (different files, no dependencies)
  [US#] = which user story this task belongs to
-->

### Phase 1: Setup (Shared Infrastructure)

- [ ] T001 [Setup project structure for modernised components]
- [ ] T002 [Configure feature flags / strangler-fig facade]
- [ ] T003 [P] [Set up CI/CD for new components]

### Phase 2: Data Migration Preparation

- [ ] T004 [Create migration scripts for schema changes]
- [ ] T005 [P] [Set up dual-write / event sourcing if needed]
- [ ] T006 [P] [Create data validation scripts]

### Phase 3: User Story 1 — [Title] (P1) 🎯 MVP

- [ ] T007 [P] [US1] [Implementation task with specific file path]
- [ ] T008 [US1] [Implementation task]
- [ ] T009 [US1] [Contract / integration test]
- [ ] T010 [US1] [Wire behind feature flag]

**Checkpoint**: User Story 1 functional behind feature flag

### Phase 4: User Story 2 — [Title] (P2)

- [ ] T011 [P] [US2] [Implementation task]
- [ ] T012 [US2] [Implementation task]
- [ ] T013 [US2] [Integration with US1 if needed]

### Phase N: Cutover & Cleanup

- [ ] TXXX [Switch traffic to modernised components]
- [ ] TXXX [Deprecation notices for legacy APIs]
- [ ] TXXX [Remove feature flags]
- [ ] TXXX [Decommission legacy code]
- [ ] TXXX [Documentation updates]

## Constitution Compliance Check

*GATE: Must pass before implementation begins.*

[Gates determined from constitution file — strangler-fig compliance, risk assessment, incremental value delivery]

| Principle | Status | Notes |
|-----------|--------|-------|
| [Principle 1] | ✅ PASS / ❌ FAIL | [details] |
| [Principle 2] | ✅ PASS / ❌ FAIL | [details] |

## Risk Assessment

| Risk | Likelihood | Impact | Mitigation |
|------|-----------|--------|------------|
| [Data loss during migration] | [High/Med/Low] | [High/Med/Low] | [mitigation plan] |
| [Extended downtime] | [likelihood] | [impact] | [mitigation] |
| [Performance regression] | [likelihood] | [impact] | [mitigation] |
