# OpenKit

*A plugin kit for [OpenCode](https://opencode.ai) with 24 commands, 26 skills, and 7 subagents for AI-assisted development.*

[Commands](#commands) | [Skills](#skills) | [Agents](#agents) | [Installation](#installation)

---

Drop this kit into any project and get a full suite of AI development workflows — from feature planning to implementation, verification, and archiving.

## Installation

Install the kit:

```bash
npm install -g @ndhuy05/openkit
```

Initialize OpenKit in your existing project:

```bash
openkit init
```

> [!NOTE]
> Restart OpenCode after initializing to see the new commands in the slash menu.

### Prerequisites

- [OpenCode](https://opencode.ai) installed and configured
- Node.js >= 18

### Optional tools

Some skills use these tools when available:

- **OpenSpec**: `npm i -g @fission-ai/openspec@latest` — spec-driven workflow (proposal, tasks, verify, archive)
- **GitNexus**: `npm i -g gitnexus` — blast radius analysis and dependency tracing

## Commands

All commands use the `ok!` prefix. Type `/ok!` in OpenCode to see the full list.

### Planning

| Command | What it does |
|---------|-------------|
| `/ok!feat` | Plan a new feature — explore, brainstorm, then implement |
| `/ok!fix` | Investigate and fix a bug — trace root cause, plan fix |
| `/ok!chore` | Plan maintenance work |
| `/ok!refactor` | Plan code refactoring |
| `/ok!optimize` | Plan performance optimization |

### Implementation

| Command | What it does |
|---------|-------------|
| `/ok!apply` | Implement tasks from a spec or conversation plan |
| `/ok!yolo` | Autonomous pipeline — explores, implements, verifies without stopping |
| `/ok!proposal` | Create an OpenSpec change with proposal, design, and tasks |

### Verification

| Command | What it does |
|---------|-------------|
| `/ok!verify` | Verify implementation matches spec — report only, no fixes |
| `/ok!archive` | Archive a completed change |

### Research & Analysis

| Command | What it does |
|---------|-------------|
| `/ok!research` | Search the web for technical info, best practices, docs |
| `/ok!analyze` | Trace dependencies, blast radius, call chains via GitNexus |
| `/ok!explain` | Explain how a code area works using Feynman Technique |
| `/ok!database-design` | Database schema design, ORM selection, indexing strategy |

### Tooling

| Command | What it does |
|---------|-------------|
| `/ok!git` | Git operations — commit, push, merge, rebase, changelog |
| `/ok!test` | Plan and implement tests |
| `/ok!docs` | Plan and implement documentation |
| `/ok!ci` | Plan CI/CD pipeline changes |
| `/ok!docker` | Plan Docker/containerization work |
| `/ok!browser` | Reproduce bugs or run QA flows in the browser |
| `/ok!setup` | Set up a project from boilerplate or tech stack |
| `/ok!port` | Port a feature from another codebase to this project |
| `/ok!uiux-design` | UI/UX design analysis and recommendations |
| `/ok!create-readme` | Generate a README for the project |

## Skills

Skills define the behavior behind each command. They live in `.opencode/skills/*/SKILL.md`.

Planning commands (`feat`, `fix`, `chore`, `refactor`, `optimize`) all load the shared `explore` skill, which provides:

- **Orchestrator identity gate** — planning commands never write code directly
- **Feynman-first approach** — restate requirements in simple language to find gaps
- **Stress-test protocol** — self-check questions resolved by exploring the codebase
- **Zero-fog checklist** — no "probably" or "should work" allowed before implementation
- **OpenSpec awareness** — integrates with spec-driven workflows when available

## Agents

Subagents handle specialized tasks. They run in foreground, have no conversation history, and receive all context from the invoking skill.

| Agent | Role |
|-------|------|
| `osf-apply` | Writes code, completes tasks, auto-verifies |
| `osf-proposal` | Creates OpenSpec artifacts (proposal, design, tasks) |
| `osf-verify` | Independent verification — reports issues, never fixes |
| `osf-archive` | Finalizes completed changes |
| `osf-analyze` | Structural analysis via GitNexus knowledge graph |
| `osf-researcher` | Web research with cited sources |
| `osf-uiux-designer` | UI/UX design analysis and reports |

## Project Structure

```
.opencode/
  agents/          7 subagent definitions
  commands/        24 slash commands (ok!*)
  skills/          26 skill folders with SKILL.md + resources
  package.json     depends on @opencode-ai/plugin
```

## Workflow

A typical workflow looks like:

```
/ok!feat "add user auth"     Plan the feature (explore mode)
/ok!apply                    Implement from the plan
/ok!verify                   Verify the implementation
/ok!archive                  Archive the completed change
```

Or skip straight to autonomous mode:

```
/ok!yolo "add user auth"     Explore + implement + verify, no stops
```