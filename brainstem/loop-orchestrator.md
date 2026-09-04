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
| Checkable finish line | Every `DONE WHEN` item has a mechanical pass/fail test |
| Bounded sandbox | Allowed inputs, write locations, and prohibited actions are explicit |
| Convergent task | A failed check or stage condition can produce a smaller actionable backlog |
| Bounded execution | `STOP-CAPS` defines a hard cycle cap and a no-progress stall cap |

If any test fails, do not execute the task as a loop. Create or update the run file as `Stopped`, identify the
failed preflight test, and respond with `don't loop this` plus the best single-prompt formulation supported by
the Goal Card.

Resolve all runtime parameters before work begins. A runtime context value may fill a variable or choice
explicitly left open by the Goal Card. It may not create a new acceptance policy.

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
   - Reload the Goal Card, optional context, run file, artifact, and named inputs.
   - Restore the current Goal Card stage, failed checks, backlog, metrics, and stall count.
   - Evaluate current artifact evidence against every applicable `DONE WHEN` check.
   - Identify regressions, blocked inputs, and the highest-priority measurable gap.
   - Select the smallest legal action set that can improve a failed check or advance a Goal Card stage.
   - Do not plan work solely to appear active.
2. **Act**
   - Perform the selected work inside the Goal Card sandbox.
   - Follow the Goal Card's current stage and quality rules.
3. **Verify**
   - Re-run every affected mechanical check.
   - Record pass, fail, evidence, and the check time.
   - Update the ordered backlog and Goal Card stage.
   - Calculate measurable progress against the previous persisted cycle.
4. **Persist and Decide**
   - Write the artifact first, then atomically update the run file.
   - Append exactly one cycle decision note.
   - If every `DONE WHEN` check passes, mark `Complete`.
   - Else if a Goal Card stop-cap applies, mark `Stopped`.
   - Else update the stall count and immediately begin the next cycle in this same invocation.

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
4. do not increment the cycle for incomplete work;
5. state that the same `START` instruction resumes the run.

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
- artifact paths;
- interruption reason, when applicable;
- terminal stop reason, when applicable.

### Authoritative state

- loop preflight results;
- resolved runtime configuration;
- current artifact state;
- every `DONE WHEN` result with evidence;
- Goal Card stage results;
- ordered backlog;
- progress metrics;
- one decision note per completed cycle.

Each completed-cycle note uses:

`Cycle <n> - checked: <evidence>; result: <passed and failed checks>; action: <change>; delta: <measurable progress>; decision: <continue or stop and why>.`

Persist enough evidence that another agent can resume without conversation history.

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
