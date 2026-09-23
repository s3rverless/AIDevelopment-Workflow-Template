# Populated example using GetCovered

These are filled examples of the generated project facts, task cards, and handoff.
They illustrate how setup should handle an existing project with conflicting
records. They are not an installed workflow or a claim that the application was
tested today. Your original repository has not been changed.

For a new project, TEMPLATE.md generates the complete files and full requirement
coverage from that project's architecture. This example shows only the workflow
reconciliation tasks relevant to the review, not the entire original roadmap.

## Example: workflow/PROJECT.md

- Purpose: renters-insurance document intake with AI extraction and human review.
- Architecture: `architecture/architecture-decisions.md`; it contains stale pipeline
  choices requiring reconciliation before treating every section as current.
- Observed stack: Next.js 16.2.6, React 19.2.4, Zod, Supabase clients, Vitest;
  source: `package.json`. Listed versions are from this repository, not generic defaults.
- Pipeline code: `app/actions/submit.ts` invokes extraction using Next.js `after()`;
  `lib/extraction/gemini.ts` sends the key in the `x-goog-api-key` header.
- Realtime implementation: `lib/supabase/client.ts` sets the session access token
  before subscription; historical live verification is reported in old memory.
- Requested lead: Opus. Actual model in a future Claude session: UNKNOWN until
  exposed by that runtime. Implementers inherit; reviewers request `opus`.
- Capabilities of that future session: UNKNOWN; discover at setup. Installed plugins
  mentioned in old memory are historical claims, not a verified capability list.
- Authorization carried from the existing rules: no commit or push unless asked.

| Purpose | Command/procedure at repository root | Evidence | Status of this review |
| --- | --- | --- | --- |
| Development | `npm run dev` | `package.json` | Present, not run |
| Offline tests | `env -u RUN_LIVE npm test` | Scripts and the live-test environment guard | Present, not run |
| Targeted test | `env -u RUN_LIVE npm test -- tests/policy.test.ts` | Vitest script and test path | Present, not run |
| Lint | `npm run lint` | `package.json` | Present, not run |
| Build | `npm run build` | `package.json` | Present, not run |
| Full user flow | Renter upload -> extraction -> realtime update -> reviewer decision | Acceptance requirements and historical memory | Not reverified |

`env -u RUN_LIVE` is appropriate for this macOS example because that test enables
live calls for any nonempty `RUN_LIVE` value, including `0`. A future initializer
should inspect its own platform and test environment instead of copying this
command blindly. The live extraction test calls a paid provider when enabled;
it is a separate check from the full user flow.

Environment variable names observed in project documentation include
`NEXT_PUBLIC_SUPABASE_URL`, `NEXT_PUBLIC_SUPABASE_PUBLISHABLE_KEY`,
`SUPABASE_SECRET_KEY`, and `GEMINI_API_KEY`. No values belong in workflow files.

## Example: workflow/TRACKER.md

### T001 — Reconcile the documented pipeline and current code

- Step: workflow maintenance before further feature development.
- State: READY.
- Dependencies: none.
- Owner/session: unassigned.
- Workspace/base: existing repository; capture current Git status before edits.
- Allowed write paths: architecture and workflow documentation only.
- Shared boundaries: one orchestrator writes these documents; application files
  and existing unrelated edits are excluded.
- Acceptance: the current pipeline design has one unambiguous description; old
  Bearer/Edge Function statements are explicitly superseded or corrected; historical
  verification reports are distinguished from checks of the present revision.
- Verification: compare the relevant statements with `submit.ts`, `gemini.ts`,
  and `client.ts`; check current documents for contradictory active statements.
- Evidence: inspection during this review confirms the local code choices; no
  application commands were run and historical approval was not independently proven.
- Review: documentation consistency check pending.
- Blocker/next action: inspect the recorded pivot and its authority. If its approval
  cannot be established, ask only about that design discrepancy; do not guess.

### T002 — Establish current verification evidence

- Step: baseline verification.
- State: BACKLOG.
- Dependencies: T001.
- Owner/session: unassigned.
- Workspace/base: assign after confirming the existing uncommitted changes.
- Allowed write paths: workflow evidence only initially; implementation fixes need
  a bounded task or an explicitly expanded scope.
- Acceptance: local checks and required user-flow checks have dated outcomes with
  revision/scope and limitations; historical claims are not presented as new runs.
- Verification: inspect command prerequisites, then run applicable local checks.
  Confirm the intended test environment and authorization before live checks.
- Evidence/review: not run in this review.
- Blocker/next action: determine the available local environment, browser tools,
  and test-service access without exposing credentials.

### T003 — Audit the existing delivery documentation

- Step: original Step 5, scoped to checking and finishing existing artifacts.
- State: BACKLOG.
- Dependencies: T001, T002.
- Owner/session: unassigned.
- Allowed write paths: `README.md`, `writeUp.md`, referenced progress documentation.
- Acceptance: actual existing artifacts cover the original delivery requirements
  and agree with current behavior; missing material is completed without recreating
  already-satisfactory content.
- Verification: compare the original Step 5 requirements to the files and validate
  the documented run procedure in an appropriate environment.
- Evidence: README and AI usage note exist; completeness and reproducibility have
  not been established by this review.
- Review: pending.
- Blocker/next action: inspect each requirement against the existing content.

## Example: workflow/HANDOFF.md

- Updated: 2026-09-23, workflow review example.
- Resume task: T001 in the example tracker.
- Immediate next action: reconcile the pipeline statements and establish the
  accepted decision before treating the architecture as current.
- Working tree: inspection found pre-existing changes, including
  `app/actions/document.ts`; recapture Git status before any editing.
- Workers: none launched by this review.
- Read next: `.claude/memory.md:10`, architecture §6, `app/actions/submit.ts:107`,
  and `lib/extraction/gemini.ts:21`.
- Open question: whether existing records establish approval for the documented
  pivot; see T001. No new product decision is assumed here.

## Example: workflow/DECISIONS.md

Baseline: `architecture/architecture-decisions.md`.

No new accepted architecture decision was made by this review. The older memory
reports a pivot to Next.js `after()` and inline payloads, and the code supports
that observation. Reconciliation belongs in T001 until its decision basis is clear.
Do not invent a dated approval entry merely to make the log look complete.
