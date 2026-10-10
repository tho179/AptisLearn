# Agent Skills (OpenCode) + Ponytail

This project uses skills installed under `.opencode/skills/` (project) and `~/.config/opencode/skills/` (global).
Each skill directory contains a `SKILL.md` with valid `name` + `description` frontmatter.
Shared checklists live in `references/`. Review/plan helpers live in `agents/` and `.opencode/commands/`.

## Core Rules

- If a task matches a skill, invoke it with the `skill` tool BEFORE acting.
- Follow the skill workflow strictly; do not partially apply it.
- Never skip required steps such as spec, plan, or test when a skill demands them.
- Ponytail (lazy senior dev) is ACTIVE EVERY RESPONSE on any coding task, default **full**. Off only on "stop ponytail" / "normal mode".

## Intent → Skill Mapping

- Vague idea / needs sharpening → `idea-refine`, then `interview-me` if still underspecified
- Underspecified ask ("build me X") → `interview-me`
- New feature / significant change, no spec → `spec-driven-development`
- Spec exists, work feels big → `planning-and-task-breakdown`
- Implementing multi-file change / next task from plan → `incremental-implementation`
- Any logic, bug fix, behavior change → `test-driven-development` (red-green-refactor)
- Bug / failure / 500 / worked-yesterday-broke → `debugging-and-error-recovery`
- Review own/other-agent/human code, PR, diff → `code-review-and-quality`
- Code works but hard to read → `code-simplification`
- Designing REST/GraphQL, module boundaries, contracts → `api-and-interface-design`
- UI/pages/components/layout/a11y → `frontend-ui-engineering`
- Anything running in browser (DOM, console, network, perf, visual) → `browser-testing-with-devtools` (needs chrome-devtools MCP)
- Input/auth/sessions/deps/PII/GDPR/OWASP → `security-and-hardening`
- Slow queries, N+1, Core Web Vitals, bottlenecks → `performance-optimization`
- Logs/metrics/traces/alerts, "can't tell what happened in prod" → `observability-and-instrumentation`
- Committing/branching/PR/release/version/changelog, messy tree → `git-workflow-and-versioning`
- Pipeline build/deploy/quality-gates → `ci-cd-and-automation`
- Removing old API/feature, schema migration, sunset decision → `deprecation-and-migration`
- ADR, design rationale, public API change → `documentation-and-adrs`
- No quality bar written down, agent silences checks/skips tests → `constraint-driven-development` (writes CONSTRAINTS.md)
- High-stakes / unfamiliar code / irreversible op → `doubt-driven-development` (adversarial review)
- Verify against official docs before implementing → `source-driven-development`
- Context files/rules setup, new session, quality degrades → `context-engineering`
- Deploy to prod, pre-launch checklist, rollout/rollback → `shipping-and-launch`
- Which skill applies? → `using-agent-skills` (meta-skill)
- ANY coding task: writing/adding/refactor/fix/review/design, lib choice → `ponytail` (ladder: YAGNI → reuse codebase → stdlib → native → installed dep → one-liner → minimum code; bug fix = root cause via grep all callers; `ponytail:` comment on deliberate ceilings; ONE runnable check for non-trivial logic)

## Execution Model

1. Determine if any skill applies (even a small chance).
2. Load it with `skill({ name: "<skill-name>" })`.
3. Follow the workflow exactly.
4. Only proceed once required steps are complete.

## Lifecycle (implicit)

DEFINE → `spec-driven-development` → PLAN → `planning-and-task-breakdown` → BUILD → `incremental-implementation` + `test-driven-development` → VERIFY → `debugging-and-error-recovery` → REVIEW → `code-review-and-quality` (+ `doubt-driven-development` when high-stakes) → SHIP → `shipping-and-launch`
