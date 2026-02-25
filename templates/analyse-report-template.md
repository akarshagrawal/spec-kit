# Codebase Analysis Report: [PROJECT_NAME]

**Branch**: `[BRANCH_NAME]` | **Date**: [DATE] | **Analysed by**: speckit.analyse
**Repository**: [REPO_PATH]

## Executive Summary

[2-3 paragraph overview: what this codebase does, its current state, key findings, and overall modernisation readiness]

## Technology Stack

| Category | Technology | Version | Status |
|----------|-----------|---------|--------|
| Language | [e.g., Python] | [e.g., 3.8] | [🟢 Current / 🟡 Ageing / 🔴 EOL] |
| Framework | [e.g., Django] | [e.g., 2.2] | [Status] |
| Database | [e.g., PostgreSQL] | [e.g., 12] | [Status] |
| Frontend | [e.g., jQuery] | [e.g., 2.x] | [Status] |
| Build Tool | [e.g., Webpack] | [e.g., 4.x] | [Status] |
| CI/CD | [e.g., Jenkins] | [Version] | [Status] |

## Folder Structure

```text
[PROJECT_ROOT]/
├── [dir1]/          # [Purpose annotation]
│   ├── [subdir]/    # [Purpose annotation]
│   └── [file]       # [Purpose annotation]
├── [dir2]/          # [Purpose annotation]
└── [config files]   # [Purpose annotation]
```

**Statistics**: [X] directories, [Y] source files, [Z] total files

## Architecture Layers

### Frontend
<!-- UI components, views, templates, static assets, client-side logic -->

| Path | Purpose | Complexity | Notes |
|------|---------|-----------|-------|
| [path] | [purpose] | [Simple/Moderate/Complex] | [notes] |

### Backend
<!-- API routes, controllers, services, middleware, server-side logic -->

| Path | Purpose | Complexity | Notes |
|------|---------|-----------|-------|
| [path] | [purpose] | [Simple/Moderate/Complex] | [notes] |

### Data Layer
<!-- Database models, schemas, migrations, ORM configuration -->

| Path | Purpose | Complexity | Notes |
|------|---------|-----------|-------|
| [path] | [purpose] | [Simple/Moderate/Complex] | [notes] |

### Infrastructure
<!-- Docker, Kubernetes, Terraform, CI/CD, deployment scripts -->

| Path | Purpose | Complexity | Notes |
|------|---------|-----------|-------|
| [path] | [purpose] | [Simple/Moderate/Complex] | [notes] |

### Shared / Common
<!-- Utilities, helpers, constants, types, interfaces -->

| Path | Purpose | Complexity | Notes |
|------|---------|-----------|-------|
| [path] | [purpose] | [Simple/Moderate/Complex] | [notes] |

### Tests

| Path | Type | Coverage Area | Notes |
|------|------|--------------|-------|
| [path] | [Unit/Integration/E2E] | [What it covers] | [notes] |

### Configuration

| Path | Purpose | Notes |
|------|---------|-------|
| [path] | [purpose] | [notes] |

## Business Logic Mapping

### [Business Area 1: e.g., User Management]

**Files**: `[path1]`, `[path2]`
**Key Functions/Classes**: [list]
**Dependencies**: [what this area depends on]
**Complexity**: [Simple/Moderate/Complex]
**Description**: [what this business area does and how it works]

---

### [Business Area 2: e.g., Payment Processing]

**Files**: `[path1]`, `[path2]`
**Key Functions/Classes**: [list]
**Dependencies**: [what this area depends on]
**Complexity**: [Simple/Moderate/Complex]
**Description**: [what this business area does and how it works]

---

[Add more business areas as discovered]

## Dependencies & External Integrations

### External APIs & Services

| Service | Purpose | Integration Point | Notes |
|---------|---------|-------------------|-------|
| [service] | [why used] | [which files/modules] | [notes] |

### Database Connections

| Database | Type | Used By | Notes |
|----------|------|---------|-------|
| [db name] | [SQL/NoSQL/etc.] | [which modules] | [notes] |

### Third-Party Libraries (Notable)

| Library | Version | Purpose | Risk |
|---------|---------|---------|------|
| [library] | [version] | [why used] | [🟢/🟡/🔴] |

## Technical Debt & Risk Areas

| Area | Risk Level | Description | Impact |
|------|-----------|-------------|--------|
| [area/module] | 🔴 High | [what the issue is] | [what it affects] |
| [area/module] | 🟡 Moderate | [what the issue is] | [what it affects] |
| [area/module] | 🟢 Low | [what the issue is] | [what it affects] |

## Modernisation Readiness Assessment

| Module/Area | Readiness | Test Coverage | Coupling | Recommended Priority |
|------------|-----------|--------------|----------|---------------------|
| [module] | 🟢 Ready | [High/Medium/Low/None] | [Loose/Moderate/Tight] | [P1/P2/P3] |
| [module] | 🟡 Moderate | [coverage] | [coupling] | [priority] |
| [module] | 🔴 High Risk | [coverage] | [coupling] | [priority] |

### Recommended Modernisation Order

1. **[First area]** — [why this should go first]
2. **[Second area]** — [why this follows]
3. **[Third area]** — [rationale]

### Strangler Fig Boundary Candidates

- **[Boundary 1]**: [where new code can wrap legacy — e.g., "API gateway in front of monolith"]
- **[Boundary 2]**: [natural seam in the codebase]
- **[Boundary 3]**: [another candidate]

## Next Steps

Run `/speckit.createspecs` to generate modernisation specifications with:
- User stories for each identified business area
- Acceptance criteria based on current behaviour
- Migration strategy per module
- Task breakdown for implementation
