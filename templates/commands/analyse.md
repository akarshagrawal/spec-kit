---
description: Analyse the codebase after constitution is established. Produce a structured report mapping folder structure, architecture layers, business logic, and technology stack.
handoffs: 
  - label: Create Modernisation Specs
    agent: speckit.createspecs
    prompt: Create modernisation specs based on the analysis report. I want to modernise...
---

## User Input

```text
$ARGUMENTS
```

You **MUST** consider the user input before proceeding (if not empty).

*Your input should specify the target codebase or repository to analyse, any areas of particular interest, known pain points, or specific modernisation goals. If no input is provided, analyse the current repository root.*

## Outline

You are performing a comprehensive codebase analysis to produce a structured report at `specs/<branch>/analysis-report.md`. This report will serve as the foundation for the next phase: creating modernisation specifications with user stories and acceptance criteria.

Follow this execution flow:

1. **Identify the target codebase**:
   - If the user specifies a path or repository, use that
   - Otherwise, analyse the current repository root
   - Verify the path exists and contains source code

2. **Load the constitution** at `.specify/memory/constitution.md`:
   - Understand the governing principles for this modernisation
   - Note any technology constraints, risk tolerances, or migration strategies defined

3. **Perform folder structure analysis**:
   - Recursively walk the project directory tree
   - Exclude common non-source directories: `node_modules/`, `.git/`, `__pycache__/`, `venv/`, `.venv/`, `dist/`, `build/`, `target/`, `vendor/`, `.next/`, `.nuxt/`
   - Produce a clean, annotated folder tree showing purpose of each directory
   - Note the depth and complexity of the structure

4. **Detect technology stack**:
   - Identify programming languages (by file extensions and content)
   - Detect frameworks and libraries (from package files: `package.json`, `requirements.txt`, `Gemfile`, `pom.xml`, `go.mod`, `Cargo.toml`, `*.csproj`, etc.)
   - Identify build tools, CI/CD configuration, infrastructure-as-code
   - Note versions where detectable (especially for legacy/outdated dependencies)
   - Classify as: **current**, **legacy**, or **end-of-life**

5. **Categorise architecture layers**:
   Map every significant file/directory into one or more of these categories:
   - **Frontend**: UI components, views, templates, static assets, client-side logic
   - **Backend**: API routes, controllers, services, middleware, server-side logic
   - **Data Layer**: Database models, schemas, migrations, ORM config, seed data
   - **Business Logic**: Core domain logic, algorithms, rules engines, workflows
   - **Infrastructure**: Docker, K8s, Terraform, CI/CD, deployment scripts
   - **Shared/Common**: Utilities, helpers, constants, types, interfaces
   - **Tests**: Unit, integration, e2e test files and fixtures
   - **Configuration**: Environment configs, feature flags, app settings
   - **Documentation**: READMEs, docs, API docs, changelogs

6. **Map business logic to files/modules**:
   For each significant module or file, identify:
   - **What business function it serves** (e.g., "payment processing", "user authentication", "order management", "reporting")
   - **Key classes/functions** and their responsibilities
   - **Dependencies** — what other modules it imports/calls
   - **Complexity assessment** — simple/moderate/complex based on lines of code, cyclomatic complexity indicators, and coupling

7. **Identify integration points and external dependencies**:
   - External APIs and services consumed
   - Database connections and types
   - Message queues, event buses
   - Third-party SDKs and integrations
   - Authentication/authorization providers

8. **Assess technical debt and risk areas**:
   - Outdated dependencies with known vulnerabilities
   - Deprecated APIs or patterns in use
   - Areas with no test coverage (inferred from test file mapping)
   - Tightly coupled modules that would be difficult to modernise independently
   - Configuration hardcoded vs. externalised
   - Duplicated logic across modules

9. **Produce modernisation readiness assessment**:
   - Rate each major area/module on a scale:
     - 🟢 **Ready** — Clean boundaries, well-tested, modern patterns
     - 🟡 **Moderate** — Some refactoring needed, partial test coverage
     - 🔴 **High Risk** — Tightly coupled, no tests, legacy patterns, critical business logic
   - Suggest a recommended modernisation order (lowest risk first, highest value first, or dependency-driven)
   - Identify "strangler fig" boundary candidates — natural points where new code can wrap legacy

10. **Write the analysis report**:
    - Use the template from `.specify/templates/analyse-report-template.md`
    - Fill in all sections with concrete findings (no placeholder tokens should remain)
    - Write to `specs/<branch>/analysis-report.md`

11. **Output summary to user**:
    - Report file path
    - Key statistics: number of files analysed, languages detected, modules mapped
    - Top 3 risk areas
    - Recommended next step: run `/speckit.createspecs` to generate modernisation specs

## Formatting & Style Requirements

- Use Markdown headings exactly as in the template
- Include code blocks for folder trees
- Use tables for structured comparisons (tech stack, risk assessments)
- Keep descriptions concise but specific — every finding should be actionable
- Reference specific file paths so the createspecs phase can trace back to source

## Key Rules

- Use absolute paths when referencing files
- Do NOT suggest implementation changes — this phase is analysis only
- Do NOT skip any architecture layer — even if empty, note "No files found for this layer"
- Mark uncertain categorisations with `[UNCERTAIN: reason]`
- If the codebase is very large (>1000 files), focus depth on core business logic and summarise peripheral areas
