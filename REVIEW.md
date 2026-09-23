# Review of your GetCovered agent workflow

Reviewed on 2026-09-23. This is a workflow/documentation review with limited code
inspection to check specific contradictions. I did not run the application,
revalidate historical tests, or modify the GetCovered repository.

I found three Markdown files in `.claude`: `CLAUDE.md`, `memory.md`, and `todo.md`.
The fourth file there is `settings.local.json`. The architecture document is named
`architecture/architecture-decisions.md`, rather than `architecture.md`. I reviewed
the Markdown files and used the README, writeup, manifests, and a few implementation
files as supporting evidence. I did not audit your local permission settings.

## What to keep

Your architecture-first discussion, explicit acceptance criteria, orchestrator
ownership, phase reviews, and written progress are useful foundations. Your rules
also correctly distinguish coding from verified completion. The live browser
check reportedly found a realtime authentication bug after mocked checks passed:
that is a good reason to keep testing across real system boundaries.
See [the recorded finding](../getCovered/getCovered/.claude/memory.md:9).

The main improvement is to make the files easier to keep true as the code changes.
More agent personas or stronger wording would not fix the contradictions below.

## Findings and changes

| Finding in your files | Why it matters | Change in the template |
| --- | --- | --- |
| `CLAUDE.md:93` and architecture §6 still require an Edge Function. `memory.md:10` records a pivot to Next.js `after()`, but `memory.md:38` repeats the old design. | A new session receives incompatible instructions about the same component. | Architecture owns the current design. Accepted changes update its affected section; a decision log holds rationale. |
| `todo.md:54` describes Bearer authentication. `memory.md:10` describes `x-goog-api-key`. | An agent following the old task record could reintroduce a fixed integration error. | Correct superseded current statements in place; retain history only as explicitly historical material. |
| The memory summary reports live E2E success; Step 2/3 headings and task details still say runtime checks are pending. | Completion becomes a matter of which paragraph the agent read last. | One task-state authority, with dated evidence and explicit unfinished states. |
| The tracker still lists README/writeup work as pending, although both files exist. | A future agent may repeat work instead of checking whether it satisfies the requirement. | Inspect existing artifacts before assigning work. Existence is also not sufficient proof of completeness. |
| The rules ask for tight briefs, but the tracker lacks consistent ownership, dependencies, allowed paths, and integration bases. | Domain specialists can collide in shared types, lockfiles, migrations, and workflow files. | One owner per task, explicit edit boundaries, shared-contract references, and an integration plan. |
| Tests are a late named phase, although feature acceptance mentions verification earlier. | Agents can interpret tests as cleanup after implementation. | Each feature includes its own checks; prove one complete flow early. Keep a final integration/release check too. |
| The workflow assumes installed plugin names and review slash commands, including depth arguments. | The same Markdown may request capabilities that a new workstation lacks. | Discover actual capabilities; provide two project-local agent definitions; avoid command/plugin dependencies. |
| `CLAUDE.md` imports all of `memory.md`, including lengthy progress paragraphs. | Every fresh session pays for old narrative and contradictory facts. | Load compact instructions, then read project facts, resume pointers, and relevant task details. |

The first two contradictions also match the inspected code:
[submit.ts](../getCovered/getCovered/app/actions/submit.ts:107) calls `after()`, and
[gemini.ts](../getCovered/getCovered/lib/extraction/gemini.ts:21) sets
`x-goog-api-key`. This establishes what the local code says, not whether the
current deployment works or when the architectural pivot was approved.

Your line limits have not prevented dense context: `CLAUDE.md` is 125 lines/978
words, and `memory.md` is 74 lines/817 words. The import therefore loads roughly
1,795 words from those files before normal task reading. Some of the longest
history paragraphs occupy only one line. Use word count and readability as well
as line count. These are whitespace-based word counts, not token measurements.

One subtle distinction: the existing `tests/live-e2e.test.ts` exercises the real
extraction API path with a synthetic PDF. It does not, by itself, prove the entire
browser upload/authentication/realtime/reviewer flow. Evidence should name the
boundary actually tested instead of using one broad "E2E passed" label.

## What the research supports

**Keep persistent instructions small and consistent.** Claude Code loads project
instructions at startup, and imported files also consume context. Its documentation
recommends concise instructions and identifies contradictions as a source of
unreliable behavior. Your `.claude/CLAUDE.md` location is supported; moving it to
the root is not the important fix. The template retains whichever location already
exists. [Claude Code memory documentation](https://code.claude.com/docs/en/memory).

**Give the agent an observable completion signal.** Official guidance emphasizes
checks it can execute, explicit verification criteria, and evidence of results.
The template puts acceptance checks in each task and requires validation after
integration. It does not treat a confident worker report as passing evidence.
[Claude Code best practices](https://code.claude.com/docs/en/best-practices).

**Separate initialization from incremental execution.** Anthropic's work on long
running agents describes a first session that establishes durable project state,
then coding sessions that implement bounded features and leave usable progress
records. This closely fits your existing three-session pattern. The template uses
your approved architecture as input and keeps setup separate from product coding.
It does not copy that article's automatic-commit behavior, since commits remain
subject to your project preferences.
[Effective harnesses for long-running agents](https://www.anthropic.com/engineering/effective-harnesses-for-long-running-agents).

**Use real agent definitions and constrained roles.** Project subagents can be
defined in `.claude/agents/`, with explicit tools and model selection. The kit
provides a coding worker and a reviewer with only read/search tools. The lead
supplies a scoped diff and runs any checks the reviewer requests. These roles
cover the recurring responsibilities without requiring a specialist plugin pack.
[Claude Code subagents](https://code.claude.com/docs/en/sub-agents).

**Parallel work needs independence.** Agent Teams add coordination and token costs;
the official guidance warns about same-file conflicts and describes the feature
as experimental. Native subagents are sufficient for this workflow's default.
Use teams when workers need ongoing peer coordination, after you have a reason
for the extra machinery. Worktrees separate filesystems; integration still needs
ownership, a known starting point, and verification.
[Claude Code Agent Teams](https://code.claude.com/docs/en/agent-teams).

**Delegate outcomes, boundaries, and deliverables.** Anthropic's multi-agent
research system benefited from explicit objectives, output formats, and division
of work. Its results concern research workloads, so they are not evidence that
adding more agents will make this coding project proportionally faster. The task
brief in this kit applies that coordination lesson without borrowing performance
claims. [How Anthropic built its multi-agent research system](https://www.anthropic.com/engineering/multi-agent-research-system).

**Add complexity when it earns its cost.** Anthropic's broader agent guidance favors
simple patterns and evaluation before adding machinery. Here the lead may code
directly when handoff and integration would cost more than the task. There is no
mandatory delegation quota, ritual replanning, or separate specialist for every
file type. [Building effective agents](https://www.anthropic.com/engineering/building-effective-agents).

**Use executable controls for repeatable enforcement.** Hooks run code at defined
events and can implement checks that prose alone cannot enforce. Once a project's
fast validation commands are reliable, wire them into the existing CI and, when
useful, a narrowly scoped hook. This generic starter installs no hook because it
cannot know every future project's commands or side effects. A universal full-test
Stop hook would be an untested operational choice.
[Claude Code hooks reference](https://code.claude.com/docs/en/hooks).

The filenames, state names, two-worker default, task-card format, and default review
cadence are my design choices for your workflow. They are not official Anthropic
requirements or experimentally proven optimal settings. Markdown cannot guarantee
that an agent follows them; evaluate the workflow on actual tasks.

Validation of this kit: checked that the standalone template contains all seven
file blueprints, that agent metadata and Markdown fences are well formed, that
placeholder delimiters are balanced, and that local document links resolve. The
workflow has not been trialed in a new live Claude Code session, so no speed or
instruction-adherence improvement is claimed as measured.

## How to improve it after using it

Try the kit on one modest feature and one change spanning an integration boundary.
Record time to a verified result, human corrections, review findings, integration
conflicts, and token/cost data if your environment exposes them. Separate waiting
for services or human decisions from coding time.

Change one thing at a time. If handoffs create rework, tighten the task contract or
use fewer workers. If reliable independent work dominates, try another worker. If
cost matters, compare routine Sonnet workers with your Opus baseline on comparable
tasks. Do not select a cheaper model solely because it reports confidence, or call
a task faster because verification was omitted.

After a repeated failure, add one specific preventative instruction or check.
Remove stale rules and unnecessary process. Keep the strongest lesson from your
existing project: the job is finished when the required behavior works and the
next session can accurately tell what happened.
