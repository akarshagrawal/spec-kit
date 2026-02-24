# Modernization Plan: [LEGACY_SYSTEM]

**Branch**: `[###-modernize-system-name]` | **Date**: [DATE] | **Spec**: [link]
**Input**: Modernization specification from `/specs/[###-modernize-system-name]/spec.md`

**Note**: This template is filled in by the `/speckit.plan` command. See `.specify/templates/plan-template.md` for the modernization workflow.

## Summary

[Extract from modernization spec: current pain points + strangler-fig approach from research]

## Modernization Context

<!--
  ACTION REQUIRED: Replace the content in this section with the modernization details
  for the legacy system. The structure here guides the strangler-fig transformation process.
-->

**Legacy System**: [e.g., COBOL mainframe, Oracle 9i, .NET Framework 2.0 or NEEDS ASSESSMENT]  
**Target Architecture**: [e.g., Cloud-native microservices, React SPA + REST API, or NEEDS CLARIFICATION]  
**Migration Strategy**: [e.g., Strangler-Fig, Database-First, API-First or NEEDS CLARIFICATION]  
**Data Migration**: [e.g., ETL pipeline, Event Sourcing, Dual-Write pattern or NEEDS ASSESSMENT]  
**Testing Strategy**: [e.g., Contract tests, End-to-end regression, A/B deployment or NEEDS CLARIFICATION]  
**Rollback Plan**: [e.g., Blue-Green deployment, Feature flags, Database rollback or NEEDS CLARIFICATION]
**Risk Assessment**: [e.g., Data loss risk, Downtime tolerance, User impact or NEEDS ASSESSMENT]  
**Success Metrics**: [e.g., Performance improvement %, Reduced maintenance cost, User satisfaction or NEEDS CLARIFICATION]  
**Timeline Constraints**: [e.g., Regulatory deadline, Contract renewal, Budget cycle or NEEDS CLARIFICATION]

## Modernization Constitution Check

*GATE: Must pass before Phase 0 assessment. Re-check after Phase 1 design.*

[Gates determined based on modernization constitution file - strangler-fig compliance, risk assessment, incremental value delivery]

## Modernization Mind Map Structure

### Core Areas Analysis

```text
Legacy System Modernization
├── Current State Assessment
│   ├── Technical Debt Areas
│   ├── Performance Bottlenecks  
│   ├── Security Vulnerabilities
│   └── Integration Pain Points
├── Strangler-Fig Implementation
│   ├── Facade Layer Design
│   ├── New Component Architecture
│   ├── Legacy Interop Strategy
│   └── Gradual Retirement Plan
└── Risk Mitigation
    ├── Rollback Procedures
    ├── Data Consistency
    ├── User Impact Minimization
    └── Performance Monitoring
```

## Project Structure

### Documentation (this modernization)

```text
specs/[###-modernize-system]/
├── plan.md              # This file (/speckit.plan command output)
├── assessment.md        # Phase 0 output (/speckit.plan command)
├── architecture.md      # Phase 1 output (/speckit.plan command)
├── migration-guide.md   # Phase 1 output (/speckit.plan command)
├── contracts/           # Phase 1 output (/speckit.plan command)
└── implementation.md    # Phase 2 output (/speckit.implement command - NOT created by /speckit.plan)
```

### Source Code (repository root)
<!--
  ACTION REQUIRED: Replace the placeholder tree below with the concrete layout
  for this feature. Delete unused options and expand the chosen structure with
  real paths (e.g., apps/admin, packages/something). The delivered plan must
  not include Option labels.
-->

```text
# [REMOVE IF UNUSED] Option 1: Single project (DEFAULT)
src/
├── models/
├── services/
├── cli/
└── lib/

tests/
├── contract/
├── integration/
└── unit/

# [REMOVE IF UNUSED] Option 2: Web application (when "frontend" + "backend" detected)
backend/
├── src/
│   ├── models/
│   ├── services/
│   └── api/
└── tests/

frontend/
├── src/
│   ├── components/
│   ├── pages/
│   └── services/
└── tests/

# [REMOVE IF UNUSED] Option 3: Mobile + API (when "iOS/Android" detected)
api/
└── [same as backend above]

ios/ or android/
└── [platform-specific structure: feature modules, UI flows, platform tests]
```

**Structure Decision**: [Document the selected structure and reference the real
directories captured above]

## Strangler-Fig Complexity Tracking

> **Fill ONLY if Modernization Constitution Check has violations that must be justified**

| Violation | Why Needed | Simpler Alternative Rejected Because |
|-----------|------------|-------------------------------------|
| [e.g., Big-bang migration] | [regulatory deadline] | [why incremental approach insufficient] |
| [e.g., Dual-write complexity] | [data consistency requirement] | [why eventual consistency insufficient] |
