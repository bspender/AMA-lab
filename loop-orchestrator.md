# File-Driven Loop Orchestrator

This file defines the control plane for a visible, bounded, file-backed loop. It is a teaching approximation of goal-driven behavior for GitHub Copilot CLI and GitHub Copilot app, not a `/goal` implementation.

The selected task worker executes this protocol. The orchestrator contains no task-specific generation, scoring, pruning, or artifact-building method.

## Responsibilities

| Component | Owns |
|---|---|
| Orchestrator | Invocation lifecycle, state transitions, iteration boundary, persistence requirement, and stopping |
| Task worker | Domain-specific method performed during one iteration |
| Goal Card | Objective, output, acceptance policy, constraints, and stop caps |
| Context | Approved task inputs and assumptions |
| Run file | Authoritative state for one run |
| Cross-run memory | Durable knowledge shared across runs |

## User controls

- `START` - configure if needed; otherwise create a run and execute Iteration 1.
- `CONTINUE run=<run-id>` - execute exactly one next iteration.
- `STATUS run=<run-id>` - report persisted state without mutation.
- `APPROVE CONTEXT` - approve the draft context version, stamping it approved with the date. Required before any run may execute against it.
- `APPROVE GOAL CARD` - approve a draft Goal Card version independently of context.
- `RECONFIGURE` - invalidate context and restart configuration.
- `NEW RUN` - create a run without discarding approved context or cross-run memory.
- `RESUME run=<run-id>` - resume a named run.
- `EXPAND idea <rank-or-id> [run=<run-id>]` - after a run is terminal, create one task-worker-specific
  expansion without consuming an iteration or mutating run state.
- Goal Card controls may add task-specific behavior.

Approval is explicit and never inferred. A draft is not approved by discussing it, by agreeing with it in conversation, or by issuing `START`.

When a draft Goal Card declares `Requires Context Version: <n>` and the draft context is that version, `APPROVE CONTEXT` adopts both together; they are one instrument and approving half of it would leave the weights and the acceptance policy out of sync. `APPROVE GOAL CARD` exists for the case where a card is revised against already-approved context.

These are ordinary instructions, not slash commands.

## Invariants

1. The Goal Card defines success.
2. The task worker defines how domain work is performed.
3. Files, not conversation history, are authoritative.
4. Configuration does not consume an iteration.
5. `START` or `CONTINUE` executes at most one iteration.
6. State is persisted before every workflow response.
7. A new iteration never begins in the same invocation.
8. The worker ends every response with its task-specific progress line.

## Invocation protocol

### 1. Load

The task worker reads:

- this orchestrator;
- its Goal Card;
- approved context;
- cross-run memory;
- the named run file, when continuing or resuming.

If required state is unavailable, conflicting, or unsafe to update, stop without consuming an iteration.

### 2. Configure when required

Configuration is required when context is missing, not approved, explicitly invalidated, or materially conflicts with the request.

The task worker:

1. applies its task-specific interview method;
2. persists one interview round per invocation;
3. proposes context with `Status: Draft`;
4. waits for explicit approval;
5. marks approved context with its version and approval date;
6. waits for `START`.

### 3. Resolve the run

- Create a run for `START` or `NEW RUN` when no applicable run exists.
- Load the named run for `CONTINUE` or `RESUME`.
- Ask for a run ID if more than one in-progress run is possible.
- Validate Goal Card and context versions.
- Restore the artifact, backlog, metrics, check results, iteration count, and stall count.

Run resolution does not consume an iteration.

### 4. Execute one iteration

The task worker performs exactly one:

`Observe -> Evaluate -> Decide -> Act -> Persist`

The worker applies its domain method while respecting the Goal Card. It must:

- evaluate checkable evidence;
- select the smallest action set addressing the highest-priority failure;
- work only inside the approved sandbox;
- update the artifact and backlog;
- recheck affected acceptance criteria;
- persist a decision note and progress metrics.

### 5. Decide the transition

After persistence:

1. If every `DONE WHEN` check passes, mark the run `Complete`.
2. Else if any Goal Card stop cap applies, mark it `Stopped`.
3. Else mark it `In Progress` and wait for `CONTINUE`.

Do not manufacture activity when no legal action can improve the result.

## Run-file minimum

Every run file records:

- run ID and status;
- worker, Goal Card, and context versions;
- timestamps;
- current and maximum iteration;
- artifact state or artifact path;
- maturity state;
- ordered backlog;
- `DONE WHEN` results;
- task metrics;
- stall count;
- one decision note and progress line per iteration;
- final stop reason.

## Response contract

For an in-progress run:

1. State what changed.
2. State the most important remaining failure.
3. Tell the user to invoke `CONTINUE run=<run-id>`.
4. End with the task worker's progress line.

For a completed or stopped run:

1. Produce the Goal Card's final output.
2. Report acceptance results and stop reason.
3. Persist terminal state.
4. End with the task worker's progress line.

For `STATUS`, do not consume an iteration or estimate new counters.

For `EXPAND`, do not consume an iteration or mutate authoritative run state. The task worker owns the
derived-artifact contract and must repeat persisted counters rather than estimate new ones.
