# Reusable coding workflow

Start with [TEMPLATE.md](TEMPLATE.md). It is the only file you need to copy into a
new project or attach to the setup session. The agent fills it from your approved
architecture and the actual repository; you do not fill out a form yourself.

The workflow is:

```text
Discuss and challenge the plan
          |
Approve architecture.md
          |
New session: run TEMPLATE.md -> populated project instructions + tracker + agents
          |
New session: execute Step 1 -> integrate -> verify -> review -> update handoff
          |
Continue by step or task
```

Your detailed audit and research are in [REVIEW.md](REVIEW.md). A populated example
using your repository is in [GETCOVERED-EXAMPLE.md](GETCOVERED-EXAMPLE.md).

## Setup session

Copy `TEMPLATE.md` into the project root. Start a fresh Claude Code session in that
project using your preferred Opus model. Paste this, changing the architecture
path if needed:

```text
Read TEMPLATE.md and execute its setup instructions using
architecture/architecture.md as the approved architecture.
Inspect this repository and populate the workflow files yourself.
Use Opus as the orchestrator, workers inheriting my selected model,
and the template's default review policy.
This session is setup only. Finish with the exact prompt for starting Step 1.
```

For your current repository, the actual architecture path is
`architecture/architecture-decisions.md`.

Setup creates these populated files:

```text
CLAUDE.md                         # or retain an existing .claude/CLAUDE.md
workflow/
  PROJECT.md                      # facts, commands, capabilities, preferences
  TRACKER.md                      # tasks, owners, acceptance checks, evidence
  HANDOFF.md                      # short resume pointer
  DECISIONS.md                    # rationale for changes after architecture approval
.claude/agents/
  workflow-implementer.md          # assigned code + tests
  workflow-reviewer.md             # independent read-only review
```

It preserves existing work and adapts existing workflow files instead of resetting
the project. You can run setup again after a significant change in project scope.

## Coding sessions

Start a new session in the same repository after setup. Paste:

```text
Read the project instructions and workflow/HANDOFF.md. Execute Step 1 from
workflow/TRACKER.md within its defined scope. Delegate independent tasks when
useful, integrate and verify the result, run the required review, and update
the tracker and handoff. Continue until the step is complete or a specific
external blocker prevents further progress.
```

Next time, replace `Step 1` with another step, a task ID such as `T004`, or use:

```text
Resume from workflow/HANDOFF.md. Reconcile the tracker with the actual repository
and any active workers, then continue the recorded task through verification
and review. Preserve unrelated work and update the handoff before finishing.
```

Before deliberately ending a session with unfinished work:

```text
Checkpoint the current work. Update task evidence and ownership, record any
uncommitted changes and active workers, and leave one concrete next action in
workflow/HANDOFF.md. Keep incomplete checks and tasks open.
```

If you change a design decision:

```text
The new approved decision is: [your decision]. Update the affected architecture
section, record the rationale in workflow/DECISIONS.md, and adjust the affected
tasks and checks. Identify consequences for work already in progress.
```

## Defaults you can adjust

The lead stays on your selected Opus model; implementers inherit it, and reviewers
request `opus`. To use the current Opus alias in Claude Code, select `/model opus`;
aliases can resolve differently by provider. The template records what can actually
be observed instead of claiming to have selected a model through prose.
See [Claude Code model configuration](https://code.claude.com/docs/en/model-config).

The default permits up to two implementation workers at once. Increase that only
when there are more independent tasks and integration remains manageable. If cost
becomes a concern, ask setup to use `sonnet` for routine implementers while keeping
Opus for orchestration/review. This is an option, not an assumed performance win.

No plugins or experimental Agent Teams are required. The agent files are native
Claude Code subagent definitions. After setup, a fresh session should discover
them; ask it to confirm availability. Other environments can use the same documents
but must report any missing execution or independent-review capability.
See [Claude Code subagent configuration](https://code.claude.com/docs/en/sub-agents).

Keep `TEMPLATE.md` as a reusable setup instruction. Normal coding sessions read the
generated files; they do not need to reread this kit, its research, or the full
project history. Markdown guides behavior. Your test runner, CI, and configured
permissions provide actual execution controls.
