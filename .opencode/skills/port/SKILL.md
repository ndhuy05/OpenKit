---
name: port
description: Port a feature from another codebase. Analyze source, extract feature graph, port to current project.
---

You are porting a feature from another codebase to the current project. This command helps you analyze the source feature, extract its dependency graph, and plan the port.

BEFORE PROCEEDING: You MUST use the Skill tool to invoke "explore". This loads the shared explore mode behavior (stance, continuous verification, fluid workflow, subagent protocols, OpenSpec awareness, guardrails) that this command depends on. Do not proceed without loading it first.

---

## What You Need From User

To migrate, you need:
1. **Source repo location** — path to the cloned repo or directory containing the feature
2. **Feature to migrate** — feature name, file(s), component(s), or module(s)
3. **Target project** — the current workspace is the target

If any of these are missing, ask with concrete options before proceeding.

---

## What You Might Do

**Explore the source feature**
- Feynman Echo — restate the migration request in the simplest possible language, then ask user to confirm or correct
- Read the source feature's entry point(s) and trace the full execution flow
- Map all files that participate in the feature (components, utils, types, tests, styles, config)
- Identify external dependencies (npm packages, APIs, services)
- Find integration points (routes, exports, config, env vars, database schemas)

**Extract the feature graph**
- Build a complete file manifest: every file the feature touches
- Classify each file: core (must copy), shared (already exists or needs merging), external (third-party dep)
- Trace import chains to catch hidden dependencies
- Identify circular dependencies or tight coupling that complicates extraction

**Analyze the target project**
- Understand current architecture, patterns, and conventions
- Map where the feature fits structurally (directory, module, route)
- Identify naming conventions, state management patterns, styling approach
- Find conflicts: same-named files, overlapping utilities, version mismatches

**Compare adaptation approaches**
- Brainstorm multiple integration strategies
- Build comparison tables for conflicting patterns
- Sketch tradeoffs between drop-in vs rewrite

**Visualize**
```
┌─────────────────────────────────────────┐
│     Use ASCII diagrams liberally        │
├─────────────────────────────────────────┤
│   Feature dependency graphs,            │
│   source → target mapping diagrams,     │
│   before/after architecture sketches,   │
│   file manifest tables                  │
└─────────────────────────────────────────┘
```

**Research external knowledge**
- When the source uses unfamiliar libraries or patterns → delegate to osf-researcher
- When version compatibility is unclear → delegate to osf-researcher

**Surface risks and unknowns**
- Identify what could break in the target after migration
- Find gaps: missing env vars, database tables, API endpoints
- Flag features that depend on infrastructure not present in target

---

## Stress-test Questions

Resolve these before ending discovery. Self-answer by exploring both codebases. Only surface items to the user that are genuinely ambiguous or require a personal/team style choice:

1. Backend dependencies:
   "Does the feature depend on backend services?
    A. No — pure frontend, self-contained
    B. Yes — API calls that exist in target already
    C. Yes — API calls that need migrating too
    D. ★ Need to verify by tracing network calls in source
    E. Khác/Other: ___"

2. Dependency conflicts:
   "How do source dependencies relate to target?
    A. All deps are new — add them
    B. Some overlap — reuse target versions
    C. ★ Version conflicts exist — need resolution strategy
    D. Khác/Other: ___"

3. Adaptation scope:
   "How much adaptation does the feature need?
    A. Drop-in — works as-is with no changes
    B. Light adaptation — rename imports, adjust paths
    C. ★ Moderate — adapt to target patterns (state mgmt, styling, etc.)
    D. Major rewrite — only the logic transfers, UI/structure rebuilt
    E. Khác/Other: ___"

4. Test strategy:
   "Test approach for migrated feature:
    A. Copy source tests and adapt
    B. Write new tests from scratch
    C. ★ Copy + adapt existing tests, add integration tests for target
    D. Khác/Other: ___"

5. Shared code:
   "Source feature uses utilities/components that also exist in target:
    A. No shared code — everything is unique
    B. Some overlap — merge carefully
    C. ★ Significant overlap — map source → target equivalents before copying
    D. Khác/Other: ___"

---

## Zero-Fog Checklist (additions)

- [ ] Feature scope is specific (exact files/components listed, not "the auth module")
- [ ] Complete file manifest created (core, shared, external classified)
- [ ] All external dependencies identified with version compatibility checked
- [ ] Integration points mapped (routes, config, env vars, DB schemas)
- [ ] Adaptation needs documented per file (not "adapt as needed" — what specifically?)
- [ ] Naming/pattern conflicts between source and target resolved
- [ ] Test migration strategy decided

---

## Extra Subagents

| Subagent | When to Use |
|----------|-------------|
| osf-analyze | Trace dependency graphs in source or target, assess blast radius of integration points |
| osf-researcher | Source uses unfamiliar tech, need version compatibility info, or migration best practices |

The following is the user's request: