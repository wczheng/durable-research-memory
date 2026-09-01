# Project Instructions

## Engineering principles

- Choose the simplest implementation that fully meets the current requirements. Avoid speculative abstractions, configuration, and indirection.
- Grow the system in layers. Start with the smallest version that works end to end, then add capabilities without replacing working behavior with unfinished complexity.
- Keep components modular and responsibilities clear.
- Prefer established, well-maintained libraries when they reduce overall complexity or improve reliability.
- Reuse existing project code and dependencies before adding new implementations or packages. Check documentation and types before assuming a capability is missing.
- Preserve backward compatibility only when requirements or public contracts demand it. Otherwise, remove obsolete paths instead of adding unrequested compatibility layers.
- Make durable architectural decisions. Avoid temporary designs that are intended to be replaced later.

## Durable project context and handoff

### Separation of concerns

- `AGENTS.md` contains stable rules, constraints, and project conventions. Do not store volatile task progress in it.
- `<project-root>/work_progress.md` is the required concise entry point for current project state and cross-session handoff.
- `<project-root>/work_progress/*.md` contains optional topic-specific progress when the root file is no longer sufficient.
- For research projects, `<project-root>/RESEARCH_PROGRESS.md` is the optional canonical record of research direction, validated milestones, lasting decisions, and open research questions.
- Canonical project documentation and ADRs contain stable architecture, interfaces, and lasting decisions.
- Skills contain reusable procedures. A skill must not contain current task state, temporary blockers, experiment results, secrets, or one-off project history.

### Start-of-task protocol

For every substantive project task:

1. Determine the project root, using the Git root when available and otherwise the current workspace root.
2. Respect the applicable root and nested `AGENTS.md` instructions.
3. Look for `<project-root>/work_progress.md`.
4. If it exists, read it before planning or changing the project.
5. Read only the linked topic files relevant to the current task. Do not load the entire `work_progress/` directory by default.
6. If `RESEARCH_PROGRESS.md` exists and the task may affect the research direction, read it before acting.
7. Validate important progress claims against the current code, configuration, Git state, artifacts, and tests. Treat progress files as maintained handoff snapshots, not unquestionable truth.
8. If `work_progress.md` is missing and the task is mutating, multi-step, experimental, long-running, or likely to require another session, initialize it from verified repository evidence. Mark unknown facts as unknown instead of guessing.
9. Do not create or update progress files for trivial questions or purely read-only work unless requested.

Creating and updating project-local progress files under this policy is part of substantive project work and does not require separate confirmation. It does not authorize staging, committing, publishing, or modifying global files.

### Progress structure

Always start with the single root `work_progress.md`. Keep it concise and include:

- Last verified time, including timezone.
- Current objective and overall status.
- Handoff summary: current state, most important finding or decision, immediate next action, and blocker if any.
- Active topics, with status, last verification time, one-line next action, and relative links to topic files.
- Recent verified milestones.
- Decisions and assumptions that still affect ongoing work.
- Blockers and open questions.
- Exact next actions in execution order.
- Verification evidence, including commands, tests, metrics, or artifacts.
- Reusable workflow candidates.

Create `<project-root>/work_progress/` and split out a topic only when at least one condition is true:

- More than two independent topics are active.
- The root file is approaching roughly 200 lines.
- A topic has substantial experiments, evidence, or decisions that are independently useful.
- Different topics have distinct lifecycles or are likely to be resumed separately.

Do not create speculative or empty topic files. Use stable kebab-case names such as `data-processing.md` or `model-changes.md`. Keep the root file as the authoritative navigation and handoff snapshot.

A topic file should contain:

- Scope and objective.
- Status and last verified time.
- Current verified state.
- Relevant files, components, datasets, and artifacts.
- Decisions and rationale.
- Completed milestones with evidence.
- Failed approaches only when remembering them prevents likely repeated work.
- Blockers and unresolved questions.
- Exact next steps.
- Reusable workflow observations.

For experiments, record enough information to reproduce and interpret the result: hypothesis, data or version, configuration, seed when relevant, command or entry point, metrics, artifact location, and conclusion.

### Update discipline

- Update progress at meaningful state transitions, not after every command or tool call.
- Meaningful transitions include a completed milestone, an accepted decision, a reproducible experiment result, a blocker, a changed plan, or a handoff.
- Before the final response of a task that changed project state, synchronize the relevant topic file and root handoff summary.
- Read the latest progress file immediately before editing it and merge concurrent changes; do not overwrite unrelated progress.
- Never mark work complete without evidence. Record `not run` or `not verified` explicitly when verification was not performed.
- Summarize command output; do not paste large raw logs.
- Include precise relative file paths and artifact locations when they make handoff easier.
- Never record credentials, tokens, private keys, sensitive personal data, or unnecessary confidential content.
- Replace or delete stale statements instead of accumulating contradictions. Progress files are curated state, not append-only diaries.
- Move stable architecture or operational knowledge into canonical project documentation, then leave only a concise link and current implication in progress files.
- When a topic is complete, retain a short verified outcome, migrate lasting knowledge, and remove detail that has no future handoff value. Archive only when the history is materially useful.
- If progress documentation conflicts with current user instructions or verified repository evidence, follow the higher-authority or current evidence and repair the progress documentation in the same task.

## Optional research continuity

Use `RESEARCH_PROGRESS.md` only when the project has an ongoing research direction that must survive across tasks or sessions.

- Treat it as a curated map of the research idea, not an experiment ledger or engineering handoff.
- Keep only the research question, falsifiable hypotheses, non-negotiable design principles, key validated milestones, lasting decisions and rationale, roadmap, and unresolved research questions.
- Update it only when evidence changes what the project believes or does next.
- Do not store per-run metrics, seeds, commands, file-level changes, debugging history, artifact inventories, branch names, or chronological task summaries in it.
- Keep detailed exploratory evidence in the relevant `work_progress/<topic>.md` file and project artifacts.
- Describe a completed stage by its durable conclusion and limitation, then remove obsolete intermediate history.
- Keep the file compact by compressing old milestones before adding new detail.
- Keep `work_progress.md` as the operational index and cross-session handoff. Synchronize `RESEARCH_PROGRESS.md` only when the research direction changes.

## Optional Feishu group-meeting document

Apply this section only when the project maintains a Feishu group-meeting document and the user requests a read, review, or update, or when an upcoming meeting requires a material refresh.

### Prerequisite

- The official [Lark CLI](https://github.com/larksuite/cli) must be installed, configured, and authenticated before an agent attempts remote document access.
- Verify both `command -v lark-cli` and `lark-cli auth status`. If either check fails, state that Feishu synchronization is unavailable and do not claim a remote read or write succeeded.
- Never store app credentials, access tokens, authorization URLs, or secrets in project files or progress documents.

### Document maintenance

- Record the exact document name or link in project-specific documentation. Never guess the target document.
- Treat the Feishu document as a concise communication artifact, not a progress log, engineering handoff, experiment ledger, or mirror of local files.
- Lead with the research question, core hypothesis, current approach, most important verified progress, and next research decision.
- Report progress at milestone level with only decision-relevant evidence and the main limitation.
- Clearly distinguish hypotheses, verified findings, planned work, and work not yet run.
- Omit routine code details, file paths, commands, dependency versions, debugging history, raw logs, and exhaustive result tables unless essential to the discussion.
- Use `RESEARCH_PROGRESS.md`, `work_progress.md`, relevant topic files, and artifacts as evidence sources; summarize rather than copy them wholesale.
- Before writing, fetch the latest Feishu version and diagnose the smallest necessary change. Prefer targeted edits unless a full rewrite is requested or the overall narrative has materially changed.
- Preserve user edits and deletions as editorial intent unless the user asks to restore content or new evidence makes an update necessary.
- Use a dry run before a write when the selected Lark CLI command supports it.
- After writing, fetch the affected content again and verify its structure, factual status, key metrics, and absence of accidentally reintroduced detail.

## Skill incubation and promotion

Record reusable workflow candidates in `work_progress.md`. Promote a workflow to a skill only when all of the following are true:

- It has succeeded in at least two separate tasks or sessions, not merely two retries in one task.
- Its trigger, inputs, outputs, steps, and validation criteria are stable.
- It is likely to recur and would materially reduce repeated reasoning or manual work.
- It does not encode temporary project state, secrets, current task IDs, or transient paths.
- Any deterministic operation is backed by a maintained project command or script when that is simpler and more reliable.

When these criteria are met:

- For a project-specific workflow, create or update a repository skill under `<project-root>/.agents/skills/<skill-name>/`, unless project instructions prohibit automatic promotion.
- Use the available skill-creation workflow when present.
- Define clear trigger boundaries, required inputs, outputs, steps, failure handling, and validation.
- Record the promoted skill path in `work_progress.md` and remove duplicated procedural instructions from progress files.
- Require explicit approval before creating a user-wide skill.
- Update or delete obsolete skills instead of preserving obsolete behavior through compatibility wrappers or fallback procedures.
