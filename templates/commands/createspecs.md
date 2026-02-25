---
description: Create comprehensive modernisation specifications with user stories, acceptance criteria, research findings, and task breakdown from the codebase analysis report.
handoffs: 
  - label: Implement Modernisation
    agent: speckit.implement
    prompt: Execute the modernisation plan
    send: true
scripts:
  sh: scripts/bash/create-new-feature.sh --json "{ARGS}"
  ps: scripts/powershell/create-new-feature.ps1 -Json "{ARGS}"
agent_scripts:
  sh: scripts/bash/update-agent-context.sh __AGENT__
  ps: scripts/powershell/update-agent-context.ps1 -AgentType __AGENT__
---

## User Input

```text
$ARGUMENTS
```

You **MUST** consider the user input before proceeding (if not empty).

*Describe your modernisation goals, target state, priorities, and any constraints. This builds upon the codebase analysis report to create detailed user stories, acceptance criteria, research findings, and a complete task breakdown for implementation.*

## Outline

The text the user typed after `/speckit.createspecs` in the triggering message **is** the modernisation description. Assume you always have it available in this conversation even if `{ARGS}` appears literally below. Do not ask the user to repeat it unless they provided an empty command.

Given the modernisation description and any existing analysis report, do this:

1. **Generate a concise short name** (2-4 words) for the modernisation branch:
   - Analyze the modernisation description and extract the most meaningful keywords
   - Create a 2-4 word short name that captures the essence of the modernisation
   - Use action-noun format when possible (e.g., "modernize-payment-api", "migrate-user-store")
   - Preserve technical terms and legacy system names (COBOL, mainframe, Oracle, etc.)

2. **Check for existing branches before creating new one**:

   a. First, fetch all remote branches to ensure we have the latest information:

      ```bash
      git fetch --all --prune
      ```

   b. Find the highest feature number across all sources for the short-name:
      - Remote branches: `git ls-remote --heads origin | grep -E 'refs/heads/[0-9]+-<short-name>$'`
      - Local branches: `git branch | grep -E '^[* ]*[0-9]+-<short-name>$'`
      - Specs directories: Check for directories matching `specs/[0-9]+-<short-name>`

   c. Determine the next available number:
      - Extract all numbers from all three sources
      - Find the highest number N
      - Use N+1 for the new branch number

   d. Run the script `{SCRIPT}` with the calculated number and short-name:
      - Pass `--number N+1` and `--short-name "your-short-name"` along with the feature description
      - Bash example: `{SCRIPT} --json --number 5 --short-name "user-auth" "Modernise user authentication"`
      - PowerShell example: `{SCRIPT} -Json -Number 5 -ShortName "user-auth" "Modernise user authentication"`

   **IMPORTANT**:
   - Check all three sources (remote branches, local branches, specs directories) to find the highest number
   - Only match branches/directories with the exact short-name pattern
   - If no existing branches/directories found with this short-name, start with number 1
   - You must only ever run this script once per feature
   - The JSON is provided in the terminal as output - always refer to it to get the actual content you're looking for
   - The JSON output will contain BRANCH_NAME and SPEC_FILE paths
   - For single quotes in args like "I'm Groot", use escape syntax: e.g 'I'\\''m Groot' (or double-quote if possible: "I'm Groot")

3. **Load context**:
   - Read FEATURE_SPEC and `/memory/constitution.md`
   - Load the analysis report from `specs/*/analysis-report.md` (find the most recent one, or the one specified by the user)
   - Load the spec template from `.specify/templates/spec-template.md`

4. **Phase A — Research & Deep-Dive**:

   For each business area and module identified in the analysis report:

   a. **Extract unknowns and research needs**:
      - What technologies are needed to replace legacy components?
      - What migration patterns apply? (strangler-fig, blue-green, parallel run)
      - What are the data migration requirements?
      - What integration contracts need to change?

   b. **Generate and dispatch research tasks**:

      ```text
      For each modernisation area:
        Task: "Research replacement options for {legacy_component}"
        Task: "Find best practices for migrating {tech} to {target_tech}"
        Task: "Assess risk for {high_risk_area}"
      ```

   c. **Consolidate findings** for each area:
      - Decision: [what was chosen]
      - Rationale: [why chosen]
      - Alternatives considered: [what else evaluated]
      - Risk: [identified risks and mitigations]

5. **Phase B — User Stories & Acceptance Criteria**:

   For each business area identified in the analysis report, create user stories:

   a. **Prioritise by modernisation value**:
      - P1: Highest risk + highest business value (modernise first)
      - P2: Medium risk or medium value
      - P3: Low risk, quality-of-life improvements

   b. **For each user story, create**:
      - Title and description in plain language
      - Priority level with justification
      - **Source files**: Specific files/modules from analysis report that this story touches
      - **Current behaviour**: How it works today (from analysis)
      - **Target behaviour**: How it should work after modernisation
      - **Acceptance criteria** in Given/When/Then format:
        ```
        Given [current state or precondition],
        When [migration action or user action],
        Then [expected modern behaviour]
        ```
      - **Migration notes**: How to transition from current to target without downtime
      - **Rollback plan**: How to revert if something goes wrong
      - **Independent test**: How to verify this story works on its own

   c. **Edge cases and risk scenarios per story**

6. **Phase C — Data Model & Contract Changes**:

   - **Extract entities from analysis report** → document data model changes:
     - Current schema → Target schema
     - Migration scripts needed
     - Backward compatibility approach
   
   - **Define interface contract changes** (if applicable):
     - Current API contracts vs. target contracts
     - Breaking changes and versioning strategy
     - Consumer notification plan

7. **Phase D — Task Breakdown**:

   For each user story, generate an ordered task list:

   - **Setup tasks**: Infrastructure, configuration, scaffolding
   - **Migration tasks**: Data migration, schema changes
   - **Implementation tasks**: New code for modern replacement
   - **Integration tasks**: Wire new code behind feature flags / strangler-fig facade
   - **Testing tasks**: Contract tests, integration tests, regression tests
   - **Cutover tasks**: Switch traffic, deprecate legacy, cleanup

   Mark parallel-safe tasks with `[P]` and specify dependencies.

8. **Phase E — Agent Context Update**:
   - Run `{AGENT_SCRIPT}`
   - Update the appropriate agent-specific context file
   - Add only new technology from current specs
   - Preserve manual additions between markers

9. **Constitution compliance check**:
   - Verify all user stories align with constitution principles
   - Check strangler-fig compliance
   - Verify risk assessment meets constitution thresholds
   - Flag any violations with justification

10. **Write the modernisation spec**:
    - Use the template structure from `.specify/templates/spec-template.md`
    - Fill in all sections with concrete findings
    - Write to SPEC_FILE path from the script output
    - No placeholder tokens should remain (except `[NEEDS CLARIFICATION]` markers, max 3)

11. **Specification Quality Validation**:
    
    a. **Create Spec Quality Checklist** at `FEATURE_DIR/checklists/requirements.md`:
    
       ```markdown
       # Modernisation Spec Quality Checklist: [FEATURE NAME]
       
       ## Content Quality
       - [ ] All business areas from analysis report are covered
       - [ ] Each user story traces back to specific files/modules
       - [ ] Acceptance criteria are in Given/When/Then format
       - [ ] Migration strategy is defined per area
       - [ ] Rollback plans exist for each story
       
       ## Research Completeness
       - [ ] Technology choices have documented rationale
       - [ ] Alternatives were evaluated
       - [ ] Risk assessment completed per area
       
       ## Task Readiness
       - [ ] All user stories have task breakdowns
       - [ ] Dependencies between tasks are mapped
       - [ ] Parallel-safe tasks are marked [P]
       - [ ] No [NEEDS CLARIFICATION] markers remain
       ```

    b. Run validation and handle results (same process as standard checklist validation — max 3 iterations, max 3 NEEDS CLARIFICATION markers)

12. **Report completion** with branch name, spec file path, checklist results, and readiness for the next phase (`/speckit.implement`).

## General Guidelines

### Quick Rules

- Build upon the analysis report — don't re-analyse what's already documented
- Every user story must reference specific files/modules from the analysis
- Acceptance criteria describe **observable behaviour**, not implementation details
- Research findings inform technology choices but don't prescribe exact code
- Task breakdown should be concrete enough for implementation but not pseudo-code
- Maximum 3 `[NEEDS CLARIFICATION]` markers — make informed decisions for the rest

### For AI Generation

When creating this spec:

1. **Use the analysis report as ground truth** for current state
2. **Make informed decisions** about migration approaches based on research
3. **Document assumptions** clearly
4. **Think like a tester**: Every acceptance criterion must be verifiable
5. **Think like an operator**: Every story needs a rollback plan
6. **Think like a product owner**: Prioritise by business value × risk reduction

### Success Criteria Guidelines

Success criteria must be:

1. **Measurable**: Include specific metrics (response time, error rate, uptime)
2. **Technology-agnostic**: Describe outcomes, not implementations
3. **Comparable**: "Before modernisation: X, After modernisation: Y"
4. **Verifiable**: Can be tested without knowing implementation details

**Good examples**:
- "Users can complete checkout in under 3 minutes (currently 5+ minutes)"
- "System handles 10,000 concurrent users without degradation (currently fails at 2,000)"
- "Deployment frequency improves from monthly to daily"
- "Mean time to recovery reduces from 4 hours to 15 minutes"

**Bad examples** (implementation-focused):
- "API response time is under 200ms" (too technical)
- "Database queries use indexes" (implementation detail)
- "Kubernetes pods autoscale" (technology-specific)

**NOTE:** The script creates and checks out the new branch and initialises the spec file before writing.
