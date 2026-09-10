# Continuous Use-Case Loop Orchestrator

This file defines a reusable control contract for one bounded, file-backed autonomous run. It is independent
of any domain, use case, Goal Card, or task worker.

`START` authorizes the executing agent to run all remaining cycles in the same invocation. Completing a cycle
is not a reason to return control to the user. The agent persists state and immediately starts the next cycle
until the Goal Card is satisfied, a stop-cap applies, or the execution environment forces an interruption.

## Responsibilities

| Component | Owns |
|---|---|
| Orchestrator | Run resolution, cycle mechanics, persistence, transition rules, and response shape |
| Goal Card | Objective, output, acceptance checks, quality rules, input contract, constraints, stages, and stop-caps |
| Runtime context | Optional per-run values, priorities, steering, sources, and tighter limits |
| Run file | Authoritative state, evidence, checks, backlog, metrics, and cycle decisions |
| Executing agent | Domain work needed to move the artifact toward the Goal Card |

The Goal Card is authoritative. Runtime context may parameterize choices the Goal Card leaves open, add
constraints, prioritize work, or tighten stop-caps. It must not weaken or replace the Goal Card.

## Controls

Only these controls are part of this contract:

- `START goal=<goal-card-path> [context=<context-path>] [run=<run-file-path>]`
- `STATUS [run=<run-file-path>]`

`START` creates or resumes one run and continues cycling without waiting between cycles. When `run` is
omitted, resume the single non-terminal run for the named Goal Card. When none exists, resolve any run sequence
declared by the Goal Card and runtime context before creating a new run. If every declared boundary is already
complete, report the latest completed run without mutation. If multiple non-terminal runs match, stop before
mutation and report the candidate paths.

`STATUS` reads persisted state without performing work, rechecking acceptance, changing counters, or
modifying files.

These are ordinary instructions, not slash commands.

## Inputs and precedence

### Goal Card

The Goal Card is required and must contain all eight named fields:

1. `OBJECTIVE`
2. `OUTPUT`
3. `DONE WHEN`
4. `QUALITY`
5. `CONTEXT`
6. `CONSTRAINTS`
7. `STAGES`
8. `STOP-CAPS`

The Goal Card defines the stages. The orchestrator must not insert generic drafting, review, or approval
stages into the run.

### Optional runtime context

The `runtime context` file is optional. `<community-reference>-context.md` defines the recommended structure.

- If no `runtime context` path is supplied, or the supplied path does not exist, continue with neutral runtime
  context and record `Runtime-Context: none` in the run file.
- Missing optional `runtime context` is never a configuration or approval gate.
- Reload the `runtime context` file at the start of every cycle so deliberate runtime steering can affect the next
  decision.
- Record the observed runtime context version or content fingerprint in each cycle log entry.
- Freeze runtime values that define the run's acceptance boundary, such as source-window start and end plus the
  complete source allowlist, roles, requirement groups, and classifications, before Cycle 1. A later context change
  may steer work inside that boundary but may not expand, shrink, move, or weaken it. Record a changed boundary as
  deferred input for a new run.
- If the `runtime context` conflicts with the Goal Card, follow the Goal Card and record the ignored conflict.
- If the `runtime context` points outside the Goal Card's sandbox, do not use that source.

A missing optional `runtime context` file is different from a missing input required by the Goal Card. Required task
inputs remain subject to the Goal Card's checks and stop-caps.

Precedence is:

1. safety and platform restrictions;
2. Goal Card;
3. optional runtime context;
4. prior run decisions;
5. agent defaults.

## Preflight

Before Cycle 1, validate the run as a loop:

| Test | Passing condition |
|---|---|
| Checkable finish line | Every `DONE WHEN` item has an explicit evaluation procedure that yields a recorded pass/fail result with evidence |
| Bounded sandbox | Allowed inputs, write locations, and prohibited actions are explicit |
| Convergent task | A failed check or stage condition can produce a smaller actionable backlog |
| Feasible cycle budget | A credible sequence of target slices can reach the finish line within the cycle cap, allowing one slice to advance multiple legitimately affected checks |
| Bounded execution | `STOP-CAPS` defines a hard cycle cap and a no-progress stall cap |
| Bounded delegation | The run either records that delegation is unnecessary or defines child count, launch, recursion, write ownership, and integration bounds |

If any test fails, do not execute the task as a loop. Create or update the run file as `Stopped`, identify the
failed preflight test, and respond with `don't loop this` plus the best single-prompt formulation supported by
the Goal Card.

Resolve all runtime parameters before work begins. A runtime context value may fill a variable or choice
explicitly left open by the Goal Card. It may not create a new acceptance policy.
Persist the resolved acceptance boundary and source-classification fingerprint in the run file. Every cycle
evaluates the same boundary; collecting a later time period or changing which evidence is required needs a new run
rather than a new cycle.
The feasible-cycle-budget test is a capacity check based on current evidence, not a static cycle plan. Record its
assumptions, then allow observed results to determine later slices.

### Run-start persistence test

When source access may apply a sensitivity label or other write restriction, test persistence after creating the
run file. The `persistence_test` event follows the verified `run_initialized` event:

1. read one representative required source using the same access path planned for the run;
2. append and verify a `persistence_test` event in the event sidecar;
3. update and reread the actual run file;
4. verify that both files remain readable and consistent.

Resolve the write location before Cycle 1. Attempt the primary output root first. If the write or reread fails for
an environmental reason, such as permission, sensitivity label, quota, or an unavailable path, and the Goal Card
allows a fallback output root, repeat the same test against that fallback using the same artifact formats. Copy the
current run state and event sidecar to the fallback and continue there only after both can be updated and reread.
Never change an artifact's format to satisfy a write restriction.

Record `Output-Root-Resolution: primary | fallback` in run metadata. When fallback is used, also record the primary
failure reason and open one non-blocking gap with the attempted remedy and result. Only when no fallback is allowed,
or the fallback test also fails, set the run to `Stopped` with reason `unsafe persistence` and return the incomplete
handback defined by the Goal Card. This is an environment failure, not a `don't loop this` verdict. Do not create a
separate probe file and do not require deletion support.

After resolving the writable output root, and before changing any cross-run state named by the Goal Card, inspect
only its approved continuity roots. When valid prior state is available, record its run ID, paths, and fingerprints,
copy the selected state into the resolved output root, reread it, then append and verify `continuity_selected`. When
no prior state is readable, record `Prior Run: none` and the continuity limitation. Never merge conflicting state
sets or imply that an unreadable session-local fallback is durable across sessions.

## Convergence and target slices

The unit of iteration is one **target slice**, not a broad pass over the artifact. A target slice is the smallest
coherent fix that can produce a measurable improvement to one primary failed check or one stage exit condition.
Goal Card stages remain the only stages; target slices, cycle mechanics, and child-agent roles must not be
represented as additional stages.

Before `Act`, persist one target slice containing:

- a stable slice ID and one-sentence fix objective;
- the primary failed check or stage exit condition it is intended to improve;
- the specific backlog item IDs, source partition, and artifact scope in bounds;
- the expected measurable delta and verification method;
- the child-agent plan, or the reason no delegation is useful.

One cycle integrates only its target slice. Tightly coupled prerequisite changes may be included when they are
necessary to verify that slice, but unrelated backlog items wait for later cycles. Do not turn Cycle 1 into a
full-task implementation: establish the baseline, select the highest-value fix slice, and improve only that slice.
Assessment may inspect enough context to choose safely, but inspection must not become unbounded action on other
slices. A slice has one primary target, but it may legitimately advance other affected checks; verify and record
those effects rather than forcing one check per cycle.

At cycle end, re-rank the remaining backlog from observed results. The next slice is chosen dynamically; do not
predeclare one static stage or slice per anticipated cycle. A stage may span several slices and advances only when
its Goal Card exit conditions pass. Append the completed slice, expected and observed delta, affected checks, and
decision rationale to the cycle history. Append every material backlog rank change and its evidence to the backlog
decision history. These histories are part of the evidence that the run converged rather than followed a hidden
static plan.

## Work Event Log

`runs\<run-id>.events.jsonl` is the authoritative live record of execution. Append one compact JSON object when
each event occurs. Never rewrite, delete, reorder, or reconstruct prior lines. The Markdown run file contains a
derived event summary and current state.

Every event line contains:

- `seq`: integer, starting at 1 and increasing by exactly 1;
- `ts`: event time with timezone;
- `cycle`, `event`, and `slice`;
- `check` or `artifact` when applicable;
- `attempt`, `observed`, and `next` for validation failures;
- `operation`, `source`, `error`, and `fallback` for failed source or tool operations;
- `checks_passing`, `stall`, and `decision` when applicable.

Before each append, read the last line and next sequence number. After appending, reread the last line and verify
the sequence number and event. If an event cannot be appended and verified, stop rather than continue with an
unrecorded run. A run with reconstructed, missing, or reordered events cannot complete successfully.

When the platform has no native append operation, logical append is allowed: read the small sidecar, republish it
with every prior byte unchanged and exactly one new JSON line added, then verify the last line. Do not republish
the larger Markdown run file for each event; update it only at run initialization, cycle boundaries, interruption,
and terminal state.

Required durable checkpoints are:

- `run_initialized` or `run_resumed`;
- `persistence_test`, when the representative-source test applies;
- `cycle_started`, after the cycle number and target slice are persisted;
- `validation_failed`, before a retry, with the saved artifact or candidate, failed rule, observed value, and next
  repair;
- `validation_passed`, after validating the reread saved artifact;
- `source_lookup_completed`, when a required lookup establishes the evidence scope or selected source;
- `source_lookup_failed`, before using a fallback for a required source;
- `tool_failed`, when a non-source tool error changes the next action or evidence coverage;
- `fallback_selected`, after verifying the replacement source or path;
- `capture_quality_failed`, before continuing with a degraded required source;
- `continuity_selected`, after verifying prior state selected for carry-forward;
- `source_checkpointed`, after comparing the current source checkpoint with prior state;
- `artifact_reused`, after rereading and validating an unchanged prior artifact;
- `incomplete_synthesis_written`, after validating a Goal Card-required stopped-run synthesis;
- `cycle_ended`, with the observed delta and continue, complete, or stop decision;
- `interrupted` or `stopped`, when applicable.

Record required-source retrieval errors that trigger fallback as `source_lookup_failed`. Use `tool_failed` for
non-source tool errors that change the next action or evidence coverage. Record timeouts, permission failures, and
quality-gate failures before they change the next action. Record the selected fallback only after it is read and
verified. Multiple validation attempts belong inside one target slice unless they change the primary target. Derive
the Slice and Cycle History from the sidecar at each cycle boundary; do not remember or reconstruct it separately.

## Child-agent execution

Child agents are optional execution units inside a target slice, not independent loop owners. Use multiple child
agents only when the selected slice has separable evidence partitions or complementary checks. Two or three
children are appropriate when those boundaries are real; otherwise use one or none. Never create make-work solely
to satisfy an agent count.

Unless the Goal Card or runtime context sets tighter bounds, use:

- maximum 3 child agents per cycle;
- maximum 12 child launches across the run;
- maximum delegation depth 1: child agents must not spawn descendants;
- maximum 1 retry for a failed child task.

Before dispatch, add planned rows to the child activity log with stable child IDs, task boundaries, allowed inputs,
expected result shape, and integration order. Every child must receive the Goal Card constraints and the current
target slice. Child tasks must be non-overlapping or explicitly complementary. Every launch, including a retry or
interruption re-dispatch, consumes one run-level launch. Retry only a transient failure and never retry an already
integrated child result.

The executing parent agent is the sole writer to authoritative artifacts and the run file. Children inspect
read-only inputs and return bounded results or write only to declared isolated scratch paths. The parent validates
and integrates results serially in declared child-ID order, never completion order. Record failures, overlap,
conflicts, rejected results, retries, and accepted contributions. A child result cannot expand the target slice;
newly discovered work becomes backlog for a later cycle.

## Run resolution

Resolve the run path in this order:

1. the explicit `run=<run-file-path>` value;
2. the Goal Card's declared output root and run-file location; or
3. `<goal-directory>\runs\<goal-stem>\<run-id>.md` when the Goal Card does not declare one.

Use a stable run ID such as `YYYYMMDD-HHMMSS-<short-slug>`. Create the parent directories when needed.
The event-log path is the run-file path with `.md` replaced by `.events.jsonl`.

On a new run:

1. resolve the proposed acceptance boundary and any Goal Card eligibility rule before creating files or consuming a
   run-sequence position. If the boundary is not yet eligible, report the observed condition and next eligible
   boundary without creating a run;
2. create the run file from the contract below and an empty event-log sidecar;
3. record the Goal Card path, version or fingerprint, and resolved stop-caps;
4. record the fixed acceptance boundary, including source-window values and the source-classification fingerprint;
5. record the context path and current version or fingerprint, or `none`;
6. set `Status: In Progress`, `Cycle: 0`, and `Stall Count: 0`;
7. append and verify `run_initialized` in the event log;
8. save and reread the run file before Cycle 1.

On a resumed run, restore all state from the run file and event log, append and verify `run_resumed`, then save and
reread the run file before continuing. Conversation history is non-authoritative.

Reload the Goal Card at the start of every cycle. If its version or content fingerprint differs from the one
that started the run, persist `Status: Stopped` with reason `Goal Card changed during run`. Do not combine
checks from different Goal Card versions in one run.

## Continuous cycle

One cycle is:

`Assess -> Act -> Verify -> Persist and Decide`

While the run is `In Progress`:

1. **Assess**
   - For a fresh cycle, set and persist `Cycle` to the prior cycle number plus one before any other cycle work. An
     interrupted active slice keeps its cycle number.
   - Reload the Goal Card, optional context, run file, artifact, and named inputs.
   - Keep using the acceptance boundary persisted at run initialization. Defer any later boundary change to a new
     run and record that decision. This includes changes to source roles, requirement groups, and classifications.
   - Restore the current Goal Card stage, failed checks, backlog, metrics, and stall count.
   - Evaluate current artifact evidence against every applicable `DONE WHEN` check.
   - Identify regressions, blocked inputs, and the highest-priority measurable gap.
   - Select and persist one target slice that can improve a primary failed check or stage exit condition.
   - Define the expected delta, verification method, and bounded child-agent plan.
   - Append and verify the `cycle_started` event before beginning action.
   - Do not plan work solely to appear active.
2. **Act**
   - Perform only the persisted target slice inside the Goal Card sandbox.
   - Dispatch bounded child tasks when useful, then validate and integrate them under the child-agent contract.
   - Follow the Goal Card's current stage and quality rules.
3. **Verify**
   - Validate candidate content before writing when possible, returning actionable violations instead of aborting
     before the repair can be recorded.
   - After every artifact write, reread the saved file and run the target slice's verification method and every
     affected `DONE WHEN` evaluation procedure against that reread content.
   - Never mark a check passed from in-memory content, a planned edit, or a successful write response alone.
   - Before each retry, append and verify a `validation_failed` event containing the rule, observed value, attempt,
     and next repair. Append and verify `validation_passed` only after the saved artifact passes.
   - Record pass, fail, evidence, and the check time.
   - Update the ordered backlog and Goal Card stage.
   - Calculate measurable progress against the previous persisted cycle.
4. **Persist and Decide**
   - Write the artifact first, then atomically update the run file.
   - Append exactly one slice-and-cycle history row plus any material backlog decision rows.
   - If every `DONE WHEN` check passes, mark `Complete`.
   - Otherwise set `Stall Count` to `0` when the cycle made measurable progress, or increment it by `1` when the
     cycle made no measurable progress. Persist it before evaluating stop-caps.
   - If a Goal Card stop-cap applies and the Goal Card declares an incomplete synthesis, write, validate, and
     reread that clearly labelled non-authoritative artifact, then append and verify
     `incomplete_synthesis_written`, before marking `Stopped`. Skip it only when unsafe persistence is the stop
     reason.
   - If a Goal Card stop-cap applies, mark `Stopped`.
   - Append and verify the `cycle_ended` event with the decision.
   - When the decision is stop, append and verify `stopped` after `cycle_ended`.
   - Rebuild the Markdown Slice and Cycle History from the event sidecar, update `Updated`, save the run file, and
     reread it at every cycle boundary.
   - If continuing, immediately begin the next cycle and dynamically select its target slice in this same invocation.

Do not emit a final response merely because a cycle completed. Do not ask the user to enter `START` between
cycles.

Progress means at least one persisted, checkable improvement: a failed check passed, a numeric distance to a
threshold decreased, a required artifact appeared, a stage exit condition passed, or a blocking backlog item
was resolved. More prose, more tool calls, or a larger artifact is not progress by itself.

## Interruption behavior

The environment may impose a time, tool, permission, or invocation limit before the run becomes terminal.
Before returning:

1. persist completed work and current check results;
2. leave `Status: In Progress`;
3. set `Interruption Reason`;
4. persist the target-slice status and every child status or integration decision;
5. append and verify the `interrupted` event;
6. if the target slice is incomplete, resume it with the same cycle number and re-dispatch only children that are
   not already integrated; every re-dispatch consumes a run-level launch;
7. if the prior cycle decision is fully persisted and no target slice is active, begin a fresh cycle at the prior
   cycle number plus one;
8. state that the same `START` instruction resumes the run.

An environmental interruption is not a designed pause between cycles.

## Run-file contract

Every run file must contain these sections. `templates\use-case-run.baseline.md` is a copyable baseline.

### Metadata

- run ID and status: `In Progress`, `Complete`, or `Stopped`;
- Goal Card path and starting version or fingerprint;
- optional context path and latest observed version or fingerprint;
- fixed acceptance boundary, including source-window start and end when applicable;
- frozen source allowlist and classification fingerprint;
- run-sequence position and prior boundary when the Goal Card defines incremental runs;
- created and updated timestamps;
- current and maximum cycle;
- stall count and stall cap;
- current Goal Card stage;
- current target slice and its expected delta;
- output-root resolution and, when fallback is used, the primary-root failure reason;
- prior run and continuity-source paths or `none`, with source fingerprints;
- child-agent limits, launch count, and integration state;
- artifact paths;
- interruption reason, when applicable;
- terminal stop reason, when applicable.

### Authoritative state

- loop preflight results;
- resolved runtime configuration;
- current target slice;
- event-log path, line count, last sequence number, and latest event;
- retained child activity and integration results;
- current artifact state;
- every `DONE WHEN` result with evidence;
- Goal Card stage results;
- ordered backlog;
- append-only backlog decision history;
- progress metrics;
- append-only slice-and-cycle history.

Persist enough evidence that another agent can resume without conversation history.

## Console progress protocol

The progress line is both the final response footer and a live console heartbeat for environments where the run
file is not visible during execution. It may be preceded by one short narration line naming the milestone, slice,
or child, but emit the heartbeat itself as the exact standalone line defined below without a prefix, suffix, code
fence, or changed field order.

Emit the line only after appending and verifying one of these durable event checkpoints:

1. run initialization or resume;
2. cycle start;
3. validation failure or validation pass;
4. cycle end;
5. interruption or stop.

The short narration line is required. At cycle start, name the slice, primary target, and why it was chosen. For a
validation failure, name the rule, observed value, attempt, and next repair. At cycle end, name the observed delta,
check-count change, decision, and next slice when continuing. `cycle` is the active persisted attempt, `checks`
uses the fixed set of Goal Card `DONE WHEN` checks, and `stage` uses only the current Goal Card stage. Replace line
breaks or `|` characters in a stage name with a single space so the line remains parseable. Do not emit decorative
heartbeats without a verified event.

## Response contract

### Complete

Report:

1. the completed artifact paths;
2. cycle count and acceptance result;
3. any non-blocking evidence gaps;
4. the persisted progress line.

### Stopped

Before responding, when the Goal Card declares an incomplete synthesis and the resolved output root is writable,
write, validate, and reread it if it does not already exist. Append and verify `incomplete_synthesis_written` before
the terminal `stopped` event. When unsafe persistence prevents this artifact, record that reason rather than
claiming it was written.

Report:

1. the stop reason;
2. artifact and run-file paths, including the incomplete synthesis when the Goal Card declares one;
3. failed `DONE WHEN` checks and evidence;
4. the smallest next action outside this run;
5. the persisted progress line.

### Interrupted

Report:

1. what was persisted;
2. the interruption reason;
3. the exact `START` instruction that resumes the run;
4. the persisted progress line.

### Status

Report only persisted state and the persisted progress line. Do not estimate or re-evaluate.

### Boundary not eligible

When a proposed run-sequence boundary fails its eligibility rule before a run is created, report the proposed
boundary, observed condition, and next eligible action. State that no run or sequence position was created. Do not
emit a progress heartbeat because no run exists.

The final line for every run-backed response is:

`[USE-CASE LOOP] run=<run-id> | cycle=<n>/<max> | stage=<goal-stage> | checks=<passed>/<total> | stall=<n>/<cap> | status=<IN_PROGRESS|COMPLETE|STOPPED>`
