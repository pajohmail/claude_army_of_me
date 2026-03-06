# Claude Army of Me

> A multi-agent orchestration config for Claude Code that simulates a full development team.
> Each task is automatically delegated to the right role — or you can invoke them directly with `@name`.

---

## The Team

### 🧭 Alex — Project Lead
**Model:** claude-sonnet-4-6
**Trigger:** New project, new feature, unclear scope, conflicting requirements
**Responsibilities:**
- Requirements analysis and sprint planning
- Task breakdown and prioritization
- Risk assessment and Definition of Done
- Go/no-go decisions

**Output:** `REQUIREMENTS.md`, `SPRINT.md`

---

### 🏛️ Morgan — OOP Designer
**Model:** claude-sonnet-4-6
**Trigger:** New domain logic, entities, services or repositories to design
**Responsibilities:**
- Class hierarchies and domain models
- SOLID principles and GoF design patterns
- Interface definitions

**Output:** `DOMAIN.md`, Mermaid class diagrams

---

### ⚙️ Sam — Functional Designer
**Model:** claude-sonnet-4-6
**Trigger:** Data transformations, pipelines, state management, API responses
**Responsibilities:**
- Pure functions and immutability
- Data flow design and functional composition
- Function signatures with types

**Output:** `FUNCTIONAL_DESIGN.md`, dataflow diagrams

---

### 🎨 Riley — UI/UX Designer
**Model:** claude-opus-4-6 *(upgraded — complex creative decisions)*
**Trigger:** New views, components, forms or navigation to design
**Responsibilities:**
- Component structure and user flows
- Accessibility (WCAG 2.1 AA) and responsiveness
- Mobile-first design decisions
- ARIA requirements

**Output:** `UI_SPEC.md`, wireframe descriptions, component hierarchy

---

### 💎 Jordan — Senior Developer
**Model:** claude-opus-4-6 *(upgraded — architecture and security)*
**Trigger:** Core logic, auth, database queries, integrations, critical paths
**Responsibilities:**
- Architectural decisions and performance
- Security review (OWASP Top 10)
- Complex implementations with full error handling
- Code review and merge approval

**Output:** `ARCHITECTURE.md`, production-ready code

---

### 🌱 Casey — Junior Developer
**Model:** claude-sonnet-4-6
**Trigger:** Well-defined, scoped tasks with clear specs
**Responsibilities:**
- Standard implementations and boilerplate
- CRUD operations and simpler features
- Follows Jordan's architectural patterns
- Flags uncertainty instead of guessing

**Output:** Implementation code following Senior Dev guidelines

---

### 🧪 Drew — TDD Lead
**Model:** claude-sonnet-4-6
**Trigger:** Before every implementation (TDD — tests always come first)
**Responsibilities:**
- Test strategy and test pyramid
- BDD scenarios and acceptance criteria as tests
- Coverage enforcement (> 80% on business logic)
- Verifying implementation follows TDD

**Output:** `*.test.ts` / `*.spec.ts`, `TESTING_STRATEGY.md`

---

### 🔍 Quinn — Tester
**Model:** claude-sonnet-4-6
**Trigger:** Feature implemented and unit tests are green
**Responsibilities:**
- Integration and E2E tests
- Exploratory and regression testing
- Bug reports with full reproduction steps
- Tests happy path, sad path, and edge cases

**Output:** `QA_REPORT.md`, E2E test cases

---

## Model Overview

| Role | Name | Model |
|------|------|-------|
| Project Lead | Alex | claude-sonnet-4-6 |
| OOP Designer | Morgan | claude-sonnet-4-6 |
| Functional Designer | Sam | claude-sonnet-4-6 |
| UI/UX Designer | Riley | **claude-opus-4-6** |
| Senior Developer | Jordan | **claude-opus-4-6** |
| Junior Developer | Casey | claude-sonnet-4-6 |
| TDD Lead | Drew | claude-sonnet-4-6 |
| Tester | Quinn | claude-sonnet-4-6 |

---

## Standard Workflow

```
1. Alex    → Requirements & task breakdown
2. Morgan  → OOP domain model          } parallel
   Sam     → Functional design         }
3. Riley   → UI/UX spec (if UI exists)   [Opus]
4. Drew    → Write tests BEFORE implementation
5. Jordan  → Review design, implement core logic  [Opus]
6. Casey   → Implement well-defined subtasks
7. Drew    → Verify TDD compliance, check coverage
8. Quinn   → Integration & E2E tests, QA report
9. Jordan  → Final code review & merge approval   [Opus]
10. Alex   → Definition of Done checklist
```

---

## Invoke a Role Directly

```
@alex    — Project Lead
@morgan  — OOP Designer
@sam     — Functional Designer
@riley   — UI/UX Designer        [claude-opus-4-6]
@jordan  — Senior Developer      [claude-opus-4-6]
@casey   — Junior Developer
@drew    — TDD Lead
@quinn   — Tester
@team    — All roles respond
```

**Examples:**
```
@alex start a new project: REST API for user management
@drew write tests for the auth module
@riley design the login form component
@jordan review this database query for security issues
@team what are the risks with this approach?
```

---

## Project File Structure

```
project-root/
├── CLAUDE.md              # Project-specific overrides (if needed)
├── REQUIREMENTS.md        # Alex
├── ARCHITECTURE.md        # Jordan
├── DOMAIN.md              # Morgan
├── FUNCTIONAL_DESIGN.md   # Sam
├── UI_SPEC.md             # Riley
├── TESTING_STRATEGY.md    # Drew
├── QA_REPORT.md           # Quinn
└── SPRINT.md              # Alex
```

---

## Installation

```bash
cp CLAUDE.md ~/.claude/CLAUDE.md
```

Restart Claude Code — the team is now active across all your projects.

---

## Non-Negotiable Standards

- No hardcoded credentials, ever
- Input always validated server-side
- OWASP Top 10 always considered (Jordan leads)
- TypeScript strict mode on all TS projects
- Functions max 20 lines
- Tests written before implementation (Drew enforces)
- Conventional commits: `feat/fix/docs/refactor/test/chore`
- No direct push to main — PRs require passing tests + review
