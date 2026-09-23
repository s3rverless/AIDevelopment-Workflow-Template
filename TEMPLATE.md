# Set up this project's coding workflow

Version 1.0 · Designed for an approved architecture and a fresh setup session.

**Instruction to the agent:** Execute this document. Inspect the project, then
create and populate the files below. The human has already discussed the product
and approved an architecture. Your job in this session is to prepare execution.
Stop after setup unless the human also explicitly requested implementation.

This file is self-contained. It requires no plugin, other template, or installer.
If you only have chat/file-output tools, produce each populated file with its
intended path and state that installation and runtime checks remain unverified.

## 1. Discover before writing

1. Establish the project root. Read applicable repository instructions and inspect
   existing workflow files. Inspect Git status when Git exists; preserve existing
   edits. Do not initialize Git, create commits, or change branches during setup.
2. Use the architecture path supplied by the human. Otherwise look for
   `architecture.md`, `architecture/architecture.md`, then other clearly relevant
   architecture documents. If competing documents disagree and no approved one
   is identifiable, ask one focused question and continue unaffected inventory.
3. Read the approved architecture in full. Extract required outcomes, constraints,
   interfaces, exclusions, acceptance criteria, and unresolved decisions. Read
   referenced product requirements when available. Missing references are gaps,
   not permission to invent requirements.
4. Inspect manifests, lockfiles, scripts, test configuration, CI, and enough code
   to understand the current starting point. In an empty repository, distinguish
   the planned stack from installed tools. Do not copy a stack from this template.
5. Inventory actual capabilities: terminal, file editing, native subagents,
   browser, Git/worktrees, and relevant integrations. Record unknowns honestly.
   Do not assume named plugins, slash commands, or a particular model are present.
6. Establish commands from repository evidence. Inspect their side effects and
   environment requirements. Do not install dependencies, call paid services, or
   mutate remote data merely to fill in the setup document. Mark unrun checks as
   unrun. Record environment variable names and purposes, never secret values.

Default preferences, unless the human has specified otherwise:

- Main session: the user's selected current Opus model. Worker: inherit it.
  Reviewer: `opus`. Model aliases are preferences, not proof of the active model.
  Record the resolved model only if the runtime exposes it. Do not change global
  configuration. A cheaper worker model is an explicit optional adjustment.
- One orchestrator and at most two concurrent implementation workers; fewer when
  dependencies make parallel work unhelpful. These are starting defaults, not
  claims about an optimal team size.
- Main session owns task state, shared interfaces, integration, and user updates.
  Use focused workers when the task is independent and delegation saves time or
  protects context. Direct implementation is appropriate for small/coupled work.
- Keep existing permissions. Local edits and checks within requested scope proceed
  autonomously. Commits, pushes, deployment, and external writes follow the human's
  existing authorization. Setup does not grant additional permissions.

## 2. Turn the architecture into executable work

- Give required outcomes stable IDs (`R001`, etc.) and cite architecture sections.
  Map every required outcome to at least one task. Separate optional ideas.
- Preserve existing phase names/numbers if they exist. Otherwise create a short
  sequence: establish a runnable baseline, prove one complete user flow, expand
  required behavior, then finish release/documentation checks. Adapt to the project;
  do not force a web-app sequence onto a library or another kind of software.
- Create stable task IDs (`T001`, etc.), explicit dependencies, and one accountable
  owner per task. Make tasks small enough to implement and verify in one focused
  session. Avoid both one-task-per-file and one-task-for-the-entire-product.
- For the first step, specify concrete file/directory ownership, behavior-based
  acceptance criteria, and checks. Define later outcomes and dependencies now;
  refine later implementation details when their prerequisites are known.
- Include tests and integration in each feature's completion criteria. Identify
  an early check that exercises real boundaries. Unit mocks alone cannot establish
  that authentication, storage, a browser, or a third-party integration works.
- Record shared contracts before parallel implementation: types, request/response
  shapes, data transitions, and failure behavior. Reference the architecture or
  actual interface file rather than duplicating its contents across documents.
- Missing information that changes product scope, architecture, or authorization
  blocks only the affected task. Make routine, reversible implementation choices
  yourself. List each blocker with the exact information needed to unblock it.

## 3. Create populated project files

Use the blueprints below as starting content. Replace every `{{...}}` slot using
project evidence. Remove instructional filler and unused rows. If something is
unknown, write `UNKNOWN`, its impact, and a concrete discovery task; never fake it.

Create these files, adapting paths when the repository already has equivalents:

| File | Its single responsibility |
| --- | --- |
| `CLAUDE.md` | Stable operating instructions and pointers |
| `workflow/PROJECT.md` | Project facts, commands, capabilities, preferences |
| `workflow/TRACKER.md` | Requirements, tasks, ownership, task status, evidence |
| `workflow/HANDOFF.md` | Short pointer to where the next session should resume |
| `workflow/DECISIONS.md` | Dated changes to decisions after the approved baseline |
| `.claude/agents/workflow-implementer.md` | Scoped coding worker definition |
| `.claude/agents/workflow-reviewer.md` | Independent reviewer definition |

Keep an existing `.claude/CLAUDE.md` in its current location instead of creating a
second competing instruction file. Paths in generated prose are project-root
relative. Merge existing useful instructions. If old active files duplicate the
new ones, preserve historical content in an explicitly historical location and
replace active references with the canonical paths. Do not leave conflicting
instructions/imports active. Preserve unrelated human-written material.

On a repeated setup, update only what changed: preserve task IDs, evidence,
accepted decisions, work in progress, and ownership. Never reset completed work
because a blueprint uses initial defaults. When evidence is stale, flag exactly
what needs rechecking rather than erasing history or claiming it is current.

For an existing project, code establishes observed behavior; approved architecture
establishes intended behavior. A disagreement is a reconciliation task. Do not
silently rewrite the architecture to justify the code. During setup, leave the
architecture intact and document unresolved disagreements.

### File: CLAUDE.md

```markdown
# Project operating instructions

{{One sentence describing the project's purpose.}}

## Read and resume

All paths below are relative to the project root. At session start, read
`workflow/PROJECT.md`, `workflow/HANDOFF.md`, and the relevant portion of
`workflow/TRACKER.md`. Read only relevant sections of `{{architecture_path}}`
after initial setup. Check repository status before editing.

The main conversation is the orchestrator. A delegated worker follows its assigned
brief and role; it does not become another orchestrator. The orchestrator alone
writes the tracker, handoff, and decision log and integrates worker output.
Only one orchestrator owns a shared checkout at a time.

## Sources of truth

- Architecture: approved intended behavior and constraints.
- PROJECT: commands, capabilities, and operating preferences.
- TRACKER: task status, acceptance criteria, ownership, and verification evidence.
- HANDOFF: resume pointers and temporary session context; not another status list.
- DECISIONS: rationale/history of accepted changes; update the affected architecture
  section in the same change so the current design remains unambiguous.

Apply the human's latest explicit decisions. Flag contradictions that need a
product/architecture decision; continue work unaffected by them. Update superseded
current statements in place. Do not accumulate contradictory correction notes.

## Execution loop

1. Read the requested task/step and its acceptance checks. Honor the requested
   scope: "Step 2" means its tasks, not the whole roadmap. "Continue" means resume
   the handoff. Inspect stale ACTIVE ownership before reassigning it.
2. Check dependencies, relevant code, and baseline failures. Claim ownership before
   editing. Refine the immediate task's plan only as needed; do not replan the
   whole project each session. Preserve unrelated work.
3. Implement the smallest coherent change. Cover behavior and significant failure
   paths with appropriate checks. Keep targeted verification close to each change.
4. Inspect worker diffs, integrate, and run acceptance checks against the combined
   result. Follow the review policy in PROJECT. Fix substantiated findings and
   recheck affected behavior. A worker's success report is not integration proof.
   Give the reviewer a stable diff/scope that includes relevant new, staged, and
   unstaged files against the recorded baseline, excluding unrelated changes and
   secrets. If the reviewed code changes, recheck the affected scope.
5. Record commands, outcomes, revision/scope, and review dispositions in TRACKER
   or a linked evidence file. Set DONE only when its completion conditions hold.
6. Continue eligible tasks within the authorized step. Before ending, checkpoint
   partial work, active workers, unresolved checks, and the next action. Summarize
   the result and evidence to the human without requiring another confirmation.

## Delegation and integration

Use actual available subagents. Default concurrency/model preferences are in
PROJECT. Delegate independent tasks with meaningful boundaries; do small or tightly
coupled work directly. Workers may investigate broadly but edit only owned paths.

Every brief includes: task ID/outcome; relevant architecture and code references;
dependencies/contracts; allowed and excluded paths; baseline/worktree; acceptance
checks; authorization limits; and the required return format. Workers return
changed files, what works, checks actually run, remaining gaps, and integration
notes. They do not mark tasks DONE, spawn workers, or change shared contracts.

Never assign overlapping file edits concurrently. Give shared types, manifests,
lockfiles, migrations, and workflow documents one writer. For isolated worktrees,
verify the starting revision and required uncommitted/untracked inputs; record
each worktree and integration base. A worktree does not inherit uncommitted work.
Integrate deliberately and rerun affected checks on the final combined result.
Use sequential work when isolation or clean ownership cannot be established.

## Verification and review

Preserve acceptance criteria. Do not remove requirements, weaken assertions, or
hide errors to obtain passing checks. A justified scope change needs the human's
decision and a recorded rationale. Do not invent test results or reviewer runs.

Distinguish checks that passed, failed, were skipped, or could not run. Link proof
to the relevant task. Mocked checks, live-service checks, and browser/user-flow
checks establish different things. Any required missing check keeps the task open.

Review concrete changes and acceptance criteria, including correctness and
security. Fix blocking findings, then recheck the affected changes. Defer only
nonblocking findings with a reason and follow-up. If independent review is
required but unavailable, record that gap; self-review does not fulfill it.

After two attempts fail with the same evidence, change the investigation approach
or isolate the problem before another patch. Report an external blocker precisely.
Do not keep rewriting code without a new hypothesis or invent a tool capability.

## Maintain useful context

Keep this file concise; put commands and facts in PROJECT, state in TRACKER, and
long logs in `workflow/evidence/`. Keep HANDOFF short. Do not import the full
architecture, tracker, history, or this setup template into every conversation.
Update durable files at meaningful transitions and before compaction/session end.
Quiesce workers or record their exact live state before handing work to a new lead.

{{At most five project-specific invariants that prevent costly mistakes.}}
```

### File: workflow/PROJECT.md

```markdown
# Project facts and execution settings

- Purpose: {{purpose}}
- Approved architecture: {{path and relevant approval/baseline reference}}
- Required result and exclusions: {{brief scope or precise section references}}
- Current stack/toolchain: {{observed versions and manifest/lockfile sources}}
- Planned but not installed: {{tools or none}}
- Important code locations/contracts: {{short pointers; no copied specifications}}

## Commands

Paths/cwd are project-root relative. "Present, not run" is not a passing result.
Task-specific outcomes belong in TRACKER/evidence, not in this command catalog.

| Purpose | Exact command and cwd | Source | Prerequisites/side effects | Setup check |
| --- | --- | --- | --- | --- |
| Setup | {{command or UNKNOWN}} | {{source}} | {{requirements}} | {{observed/unrun}} |
| Run | {{command or UNKNOWN}} | {{source}} | {{requirements}} | {{observed/unrun}} |
| Targeted tests | {{command pattern or UNKNOWN}} | {{source}} | {{requirements}} | {{observed/unrun}} |
| Static checks | {{actual lint/type commands or none}} | {{source}} | {{requirements}} | {{observed/unrun}} |
| Build | {{command or not applicable}} | {{source}} | {{requirements}} | {{observed/unrun}} |
| Integration/user flow | {{procedure or missing-check task}} | {{source}} | {{test environment}} | {{observed/unrun}} |

Environment: {{variable names, purpose, and setup reference; never values}}
Known baseline limitations: {{links to discovery/blocker tasks, not duplicate status}}

## Agent/runtime settings

- Requested lead model: Opus; actual runtime selection: {{observed or UNKNOWN}}.
- Implementer: inherit the lead. Reviewer: opus. Change only per human preference.
- Maximum concurrent implementation workers: 2; use fewer when work is dependent.
- Execution: native subagents when available; otherwise sequential implementation.
- Workspace: explicit disjoint file ownership by default; worktrees only with a
  verified base and an explicit integration plan. Never assume a clean repository.
- Capabilities: {{available/unavailable/unknown for tools relevant to this project}}.
- Custom agents: {{created paths and whether loading has actually been verified}}.
- Agent teams/plugins/hooks: not required. Preserve any existing configuration.
- Authorization: {{existing human instructions for commits/pushes/external writes}}.

## Completion and review policy

Every task: acceptance criteria satisfied; relevant checks passed; required
documentation updated; no unresolved blocking finding; evidence tied to the
current implementation. An unmet condition keeps the task open.

Every substantive code batch/step: a fresh reviewer checks the integrated diff,
related code, correctness, and security. For auth, permissions, sensitive data,
payments, destructive migrations, or similar high-impact changes, also request a
focused security review in a separate fresh invocation. These are reviews, not
requests for human approval. Small documentation/cosmetic changes use proportionate
self-checks. If fresh review tools are unavailable, record the gap and prepare a
review brief for a separate session; continue independent work.

Step/release completion additionally requires: {{project-specific integration,
browser/manual acceptance, operational, and delivery checks from architecture}}.
Required checks cannot be silently waived. Document an explicit human-approved
change to the gate when applicable.
```

### File: workflow/TRACKER.md

```markdown
# Work tracker

This is the sole task-status authority. Only the orchestrator updates it.
Use task IDs when communicating. Do not duplicate task state in other files.

## Requirements and steps

| Requirement | Architecture reference | Observable outcome | Task IDs |
| --- | --- | --- | --- |
| {{R001}} | {{section}} | {{behavior}} | {{T001}} |

| Step | Outcome | Task IDs | Dependencies |
| --- | --- | --- | --- |
| {{Step 1}} | {{outcome}} | {{T001}} | {{none or IDs}} |

Step completion is derived from required tasks and its integration gate. No
separate manually maintained "phase complete" claim. Optional ideas stay separate.

## State and evidence rules

- BACKLOG: defined work not yet selected/refined for execution.
- READY: bounded task; prerequisites met; acceptance checks and ownership scope set.
- ACTIVE: claimed; implementation or investigation in progress.
- REVIEW: integrated implementation awaits required verification/review.
- BLOCKED: cannot satisfy the next required condition; name blocker and unblock action.
- DONE: all acceptance, verification, review, and documentation conditions met.

A task dependency is satisfied when it is DONE. Batch independent tasks for review;
review a prerequisite early if dependent work needs it. Do not wait for a phase-end
review when doing so would prevent the remaining tasks from starting.

Normal flow: BACKLOG -> READY -> ACTIVE -> REVIEW -> DONE. Any unfinished task may
be BLOCKED and return to its previous unfinished state after resolution. Failed
review returns to ACTIVE. Reopen DONE when changed code or new evidence invalidates
its result, preserving the prior evidence. Never use DONE for "code written".

## Tasks

### {{T001}} — {{specific outcome}}

- Step / requirements: {{step; requirement IDs}}
- State: {{initial state based on actual evidence}}
- Dependencies: {{task IDs or none}}
- Owner / active session: {{unassigned or actual owner/session}}
- Workspace / integration base: {{path/revision or assign before work}}
- Allowed write paths: {{concrete files/directories; refine before READY}}
- Shared contract / excluded paths: {{references and boundaries}}
- Risk / required review: {{normal or high-impact; reason and review scope}}
- Acceptance criteria: {{observable success and important failure behaviors}}
- Verification: {{exact checks/commands or linked procedure, including cwd}}
- Evidence: {{none yet, or dated commands/results and revision/scope}}
- Review: {{not run, or reviewer/scope/findings/dispositions/recheck evidence}}
- Blocker / next action: {{none or precise action}}

Repeat one card per task. Keep actual state only in its card. Before delegation,
the orchestrator records the owner, scope, and workspace, then sends the brief.
Dependencies must exist and form an acyclic graph. No two ACTIVE writers may own
the same files; serialize shared-file work.

For lengthy verification, link `workflow/evidence/Txxx.md` with date, revision or
uncommitted diff scope, environment (local/mocked/live), commands and cwd, outcome,
relevant output/artifact, reviewer findings and dispositions, and remaining limits.
If evidence is invalidated by later edits, rerun affected checks. Archive old task
cards only when needed, retaining a stable ID/link so dependencies still resolve.

## Optional backlog

{{Clearly optional improvements, separated from required delivery.}}
```

### File: workflow/HANDOFF.md

```markdown
# Resume here

- Updated: {{timestamp and session identifier if available}}
- Resume task(s): {{IDs and links to TRACKER; no copied status summaries}}
- Immediate next action: {{one concrete action}}
- Working tree/workspaces: {{uncommitted scope, branch/base if relevant}}
- Worker continuation: {{none, or live/stopped worker IDs, owned paths, worktrees}}
- Read next: {{specific architecture/code/evidence pointers}}
- Temporary context: {{non-obvious session fact or none}}
- Open question: {{exact missing decision or none; link to task}}

TRACKER holds completion claims and test results. Check it and the actual files
before resuming. This document is a short resume pointer, not a history log.
```

### File: workflow/DECISIONS.md

```markdown
# Changes to the approved architecture

Baseline: {{architecture path/reference}}. The architecture holds the current
approved design. This log records subsequent rationale, not a competing design.

{{If no subsequent changes exist, write: No subsequent decisions recorded.}}

For each real change, record:
- ID/date; affected requirement/task and architecture section.
- Previous choice -> accepted choice; why; meaningful consequence.
- Decision basis: explicit human decision/reference, or reversible implementation
  detail within already-approved scope. Do not fabricate historical approval.
- Superseded decision if any; architecture/contract references updated.

Unresolved proposals belong in the affected task, not among accepted decisions.
```

### File: .claude/agents/workflow-implementer.md

```markdown
---
name: workflow-implementer
description: Implements a bounded task delegated by the orchestrator within assigned files.
tools: Read, Glob, Grep, Bash, Edit, Write
model: inherit
---

You are a coding worker, not the orchestrator. Follow the assigned task brief and
applicable project instructions. Read referenced contracts and nearby code first.
Implement only in owned paths. Cover the task's behavior and failure cases with
appropriate verification. Follow the brief's authorization limits.

If the brief lacks a necessary contract or file ownership overlaps another worker,
report the conflict before editing affected files. Ask the orchestrator to assign
shared-file changes. Do not create subagents, commit/push, deploy, alter shared
workflow state, or declare project completion. Do not weaken acceptance checks.

Return: task ID; outcome; changed files and workspace/base; checks actually run
with results; unresolved issues; and integration notes. Label incomplete work and
checks you could not run. Keep the report concise; provide artifact paths for
large outputs. The orchestrator integrates and decides completion.
```

### File: .claude/agents/workflow-reviewer.md

```markdown
---
name: workflow-reviewer
description: Reviews an integrated change against its acceptance criteria for correctness and security.
tools: Read, Glob, Grep
model: opus
---

You are an independent reviewer. Read the task's acceptance criteria, supplied
diff artifact, relevant implementation, and check evidence. Do not rely solely
on the implementer's summary. Review the exact integrated scope identified by
the orchestrator. If no usable diff/scope is supplied, request it before a verdict.

Inspect correctness, error paths, regressions, interface compatibility, and
security relevant to the change. For a focused security assignment, examine the
actual trust boundaries, authorization, sensitive data, input handling, and abuse
paths involved. Avoid speculative findings and unrelated style preferences.

You have read/search tools only. Do not edit files, run commands, or claim you
executed tests. Ask the orchestrator to run a missing check and provide its output.

Return findings ordered by impact: file:line, trigger, concrete consequence,
supporting evidence, and suggested fix or verification. Distinguish confirmed
defects from questions. State what you reviewed and the limits of the evidence.
If no issues were found, say so for the reviewed scope; do not claim perfection.
Do not update task status. The orchestrator resolves findings and records proof.
```

## 4. Check the setup and finish

- Resolve every `{{...}}` slot, or replace it with an honest unknown and task.
- Confirm referenced project paths exist or are explicitly planned task outputs.
- Ensure every required architecture outcome maps to work, IDs are unique,
  dependencies resolve without cycles, and a useful first task is actionable.
- Confirm no requirement was invented, dropped, or quietly marked implemented.
- Validate agent frontmatter against the installed runtime when available; record
  file creation separately from actual agent availability. A fresh coding session
  is the normal next step. If native agents are unsupported, retain the role
  briefs as ordinary documents and use sequential work with the review gap stated.
- Check for duplicate active instructions, contradictory decisions, stale imports,
  fabricated checks, and unnecessary project history in startup context.
- Aim for roughly 100 lines/800 words in CLAUDE.md and 20 lines/200 words in HANDOFF.
  These are editing targets, not permission to delete useful evidence. Use both
  word count and readability; huge paragraphs can hide inside a line limit.
- Finish with created/updated paths, the chosen architecture, first actionable
  task, actual capability/verification gaps, and this exact next-session prompt
  with the real step or task substituted:

> Read the project instructions and workflow/HANDOFF.md. Execute Step 1 from
> workflow/TRACKER.md within its defined scope. Delegate independent tasks when
> useful, integrate and verify the result, run the required review, and update the
> tracker and handoff. Continue until the step is complete or a specific external
> blocker prevents further progress.

Setup is complete when these documents are populated and consistent. Product
implementation and its tests are separate work; make no product-readiness claim.
