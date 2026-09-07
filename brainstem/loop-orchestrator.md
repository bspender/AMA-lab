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
omitted, resume the single non-terminal run for the named Goal Card; create a new run when none exists. If
multiple non-terminal runs match, stop before mutation and report the candidate paths.

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
The feasible-cycle-budget test is a capacity check based on current evidence, not a static cycle plan. Record its
assumptions, then allow observed results to determine later slices.

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

On a new run:

1. create the run file from the contract below;
2. record the Goal Card path, version or fingerprint, and resolved stop-caps;
3. record the context path and current version or fingerprint, or `none`;
4. set `Status: In Progress`, `Cycle: 0`, and `Stall Count: 0`;
5. persist before beginning Cycle 1.

On a resumed run, restore all state from the run file. Conversation history is non-authoritative.

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
   - Restore the current Goal Card stage, failed checks, backlog, metrics, and stall count.
   - Evaluate current artifact evidence against every applicable `DONE WHEN` check.
   - Identify regressions, blocked inputs, and the highest-priority measurable gap.
   - Select and persist one target slice that can improve a primary failed check or stage exit condition.
   - Define the expected delta, verification method, and bounded child-agent plan.
   - Do not plan work solely to appear active.
2. **Act**
   - Perform only the persisted target slice inside the Goal Card sandbox.
   - Dispatch bounded child tasks when useful, then validate and integrate them under the child-agent contract.
   - Follow the Goal Card's current stage and quality rules.
3. **Verify**
   - Re-run the target slice's verification method and every affected `DONE WHEN` evaluation procedure.
   - Record pass, fail, evidence, and the check time.
   - Update the ordered backlog and Goal Card stage.
   - Calculate measurable progress against the previous persisted cycle.
4. **Persist and Decide**
   - Write the artifact first, then atomically update the run file.
   - Append exactly one slice-and-cycle history row plus any material backlog decision rows.
   - If every `DONE WHEN` check passes, mark `Complete`.
   - Otherwise set `Stall Count` to `0` when the cycle made measurable progress, or increment it by `1` when the
     cycle made no measurable progress. Persist it before evaluating stop-caps.
   - If a Goal Card stop-cap applies, mark `Stopped`.
   - Else immediately begin the next cycle and dynamically select its target slice in this same invocation.

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
5. if the target slice is incomplete, resume it with the same cycle number and re-dispatch only children that are
   not already integrated; every re-dispatch consumes a run-level launch;
6. if the prior cycle decision is fully persisted and no target slice is active, begin a fresh cycle at the prior
   cycle number plus one;
7. state that the same `START` instruction resumes the run.

An environmental interruption is not a designed pause between cycles.

## Run-file contract

Every run file must contain these sections. `templates\use-case-run.baseline.md` is a copyable baseline.

### Metadata

- run ID and status: `In Progress`, `Complete`, or `Stopped`;
- Goal Card path and starting version or fingerprint;
- optional context path and latest observed version or fingerprint;
- created and updated timestamps;
- current and maximum cycle;
- stall count and stall cap;
- current Goal Card stage;
- current target slice and its expected delta;
- child-agent limits, launch count, and integration state;
- artifact paths;
- interruption reason, when applicable;
- terminal stop reason, when applicable.

### Authoritative state

- loop preflight results;
- resolved runtime configuration;
- current target slice;
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

Emit the line at these milestones:

1. run initialization or resume;
2. cycle start after the target slice is persisted;
3. child dispatch after the planned activity rows are persisted;
4. each child result after its status and integration decision are persisted;
5. completion of `Act`;
6. completion of `Verify`;
7. cycle persistence and continue/complete/stop decision;
8. interruption handling.

The line may repeat unchanged when a milestone does not change its fields. Do not suppress these repetitions:
they demonstrate liveness. `cycle` is the active persisted attempt, `checks` uses the fixed set of Goal Card
`DONE WHEN` checks, and `stage` uses only the current Goal Card stage. Replace line breaks or `|` characters in a
stage name with a single space so the line remains parseable. Persist durable state changes before reporting them,
but a liveness-only heartbeat does not require an otherwise unnecessary run-file write. Console heartbeats never
substitute for required run-file persistence.

## Response contract

### Complete

Report:

1. the completed artifact paths;
2. cycle count and acceptance result;
3. any non-blocking evidence gaps;
4. the persisted progress line.

### Stopped

Report:

1. the stop reason;
2. artifact and run-file paths;
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

The final line for every response is:

`[USE-CASE LOOP] run=<run-id> | cycle=<n>/<max> | stage=<goal-stage> | checks=<passed>/<total> | stall=<n>/<cap> | status=<IN_PROGRESS|COMPLETE|STOPPED>`
