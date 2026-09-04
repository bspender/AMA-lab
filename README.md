# AMA Loop Engineering Lab

A small, file-driven lab for designing and running bounded AI work loops.

The repository separates two concerns:

1. **Goal design** turns a recurring task into a checkable, bounded Goal Card.
2. **Loop execution** uses that Goal Card to plan, act, check, adjust, and persist until the work is complete or a stop condition applies.

Everything important is represented in Markdown so the task definition, state, evidence, and decisions remain inspectable outside any single AI conversation.

## Repository map

| Path | Purpose |
|---|---|
| [`goal-designer-prompt.md`](goal-designer-prompt.md) | Interview protocol for deciding whether a task deserves a loop and producing an eight-field Goal Card |
| [`brainstem\loop-orchestrator.md`](brainstem/loop-orchestrator.md) | Domain-neutral control contract for a continuous, bounded, file-backed run |
| [`brainstem\templates\use-case-context.baseline.md`](brainstem/templates/use-case-context.baseline.md) | Optional per-run context for approved sources, runtime parameters, priorities, and tighter constraints |
| [`brainstem\templates\use-case-run.baseline.md`](brainstem/templates/use-case-run.baseline.md) | Copyable schema for persisted run state, evidence, checks, backlog, and cycle decisions |
| [`brainstem\lobster-pound-review-goal-card.md`](brainstem/lobster-pound-review-goal-card.md) | Worked Goal Card for a recurring community-insights task |
| [`brainstem\lobster-pound-community-context.md`](brainstem/lobster-pound-community-context.md) | Active source locators and runtime values for the Lobster Pound example |

## Core model

```text
Goal Designer -> Goal Card -> Loop Orchestrator -> Run state + task artifacts
```

### Goal Card: what success means

Every Goal Card defines eight fields:

1. `OBJECTIVE`
2. `OUTPUT`
3. `DONE WHEN`
4. `QUALITY`
5. `CONTEXT`
6. `CONSTRAINTS`
7. `STAGES`
8. `STOP-CAPS`

The card is authoritative for task scope, acceptance, quality, and stopping behavior.

### Orchestrator: how work proceeds

The orchestrator applies this cycle:

```text
Assess -> Act -> Verify -> Persist and Decide
```

`START` authorizes the agent to continue through all necessary cycles in the same invocation. A cycle does not pause for approval unless the Goal Card requires escalation, a stop-cap applies, or the environment interrupts execution.

### Runtime context: what varies by run

Runtime context is optional. It can supply:

- concrete source locations and time windows;
- parameter values explicitly left open by the Goal Card;
- current priorities;
- repository or path selections;
- additional restrictions; and
- tighter stop-caps.

It cannot weaken, replace, or reinterpret the Goal Card.

### Run file: what happened

The run file is the resumable system of record. It contains:

- Goal Card and context fingerprints;
- current stage and cycle;
- acceptance-check results and evidence;
- ordered backlog;
- progress measures;
- artifact paths;
- one decision note per completed cycle; and
- completion, stop, or interruption state.

Conversation history is non-authoritative. Another agent should be able to resume from the files alone.

## What makes a task loopable?

The Goal Designer tests three ingredients:

| Ingredient | Requirement |
|---|---|
| Checkable finish line | Every completion criterion has a judgment-free pass/fail test |
| Bounded sandbox | Read sources, write locations, exclusions, and prohibited actions are explicit |
| Convergent task | A failed check identifies a bounded repair that can be performed and rechecked |

The outcome may be:

- **Loop it** when all three ingredients are present.
- **Don't loop this** when the task is better expressed as one prompt.
- **One-shot as described, loopable if upgraded** when a missing verification dimension could create convergence.

One-cycle completion is valid. The purpose of the loop is verified completion, not manufacturing extra passes.

## Lobster Pound runbook

This example runs from a durable OneDrive-backed working directory rather than from the repository checkout.
In the paths below, `<OneDrive Root>` is the user's OneDrive root, such as
`C:\Users\<user>\OneDrive - Microsoft`.

### 1. Copy the runtime files

Create `<OneDrive Root>\AMA\brainstem\templates\`, then copy:

| Repository source | OneDrive destination |
|---|---|
| `brainstem\loop-orchestrator.md` | `<OneDrive Root>\AMA\brainstem\loop-orchestrator.md` |
| `brainstem\lobster-pound-review-goal-card.md` | `<OneDrive Root>\AMA\brainstem\lobster-pound-review-goal-card.md` |
| `brainstem\lobster-pound-community-context.md` | `<OneDrive Root>\AMA\brainstem\lobster-pound-community-context.md` |
| `brainstem\templates\use-case-context.baseline.md` | `<OneDrive Root>\AMA\brainstem\templates\use-case-context.baseline.md` |
| `brainstem\templates\use-case-run.baseline.md` | `<OneDrive Root>\AMA\brainstem\templates\use-case-run.baseline.md` |

The resulting layout is:

```text
<OneDrive Root>\AMA\brainstem\
|-- loop-orchestrator.md
|-- lobster-pound-review-goal-card.md
|-- lobster-pound-community-context.md
`-- templates\
    |-- use-case-context.baseline.md
    `-- use-case-run.baseline.md
```

The active context writes generated artifacts beneath
`<OneDrive Root>\AMA\brainstem\insights\lobster-pound\`; it does not write results back to this repository.

### 2. Load the contracts

Start an AI session with `<OneDrive Root>\AMA\brainstem\` as its working directory. Send:

```text
Read @loop-orchestrator.md, @lobster-pound-review-goal-card.md, @lobster-pound-community-context.md, and @templates/use-case-context.baseline.md, then wait for further instructions.
```

This first instruction loads the control contract, Goal Card, active runtime context, and context schema without
starting work.

### 3. Start or resume the loop

Send:

```text
START goal=lobster-pound-review-goal-card.md context=lobster-pound-community-context.md
```

The orchestrator creates or resumes a run and continues until:

- every `DONE WHEN` check passes;
- a Goal Card stop-cap applies; or
- the execution environment forces an interruption.

Because the Goal Card declares an output root and run-file location, the omitted `run` argument resolves beneath
`<OneDrive Root>\AMA\brainstem\insights\lobster-pound\runs\`.

### 4. Inspect persisted status

Read state without performing work:

```text
STATUS [run=<run-file-path>]
```

`START` and `STATUS` are ordinary instructions, not slash commands.

## Designing another Goal Card

Open [`goal-designer-prompt.md`](goal-designer-prompt.md) in an AI assistant and use it as the instruction. The
Goal Designer conducts up to three interview rounds, challenges vague or judgment-laden criteria, and returns
either a Goal Card or a reason not to loop the task.

Use [`brainstem\templates\use-case-context.baseline.md`](brainstem/templates/use-case-context.baseline.md) when a Goal Card needs
run-specific source locations, parameters, or tighter constraints. Runtime context is optional and cannot weaken
the Goal Card.

## Resume and interruption behavior

If an environment limit interrupts execution, the agent persists completed work, leaves the run `In Progress`, records the interruption reason, and reports the exact `START` instruction needed to resume.

On resume, the agent reloads the Goal Card, optional context, run file, artifacts, and required inputs. If the Goal Card changed during the run, the orchestrator stops rather than mixing acceptance policies.

## Progress and stopping

Progress must be a persisted, checkable state change, such as:

- a failed check passing;
- measurable distance to a threshold decreasing;
- a required artifact appearing;
- a stage exit condition passing; or
- a blocking backlog item being resolved.

More prose, tool calls, or cycles do not count as progress.

Successful completion requires every `DONE WHEN` check to pass. Reaching a fixed point with failed checks is a stall, not success. A stopped run is a valid and useful result when it reports the failed checks, supporting evidence, and smallest next action.

## Worked example: community insights

[`brainstem\lobster-pound-review-goal-card.md`](brainstem/lobster-pound-review-goal-card.md) models a recurring 30-day synthesis of a Teams community. It demonstrates:

- complete source accounting within an approved sandbox;
- reusable daily evidence condensation;
- weekly theme evolution rather than disconnected summaries;
- original-source citations;
- duplicate, freshness, contradiction, and continuity checks;
- incremental reuse with a trailing reinspection window; and
- explicit privacy, access, and publication boundaries.

The example is a task contract, not bundled data or a simulated integration. Running it requires an execution environment with authorized access to the sources named by the card. The repository does not contain Teams messages, transcripts, credentials, or copied source bodies.

## Design principles

- Files, not chat history, hold authoritative state.
- Goal Cards define acceptance; context only configures a run.
- Mechanical checks must reject cheap, superficially compliant answers.
- Discovery-dependent checks belong only in tasks that genuinely require retrieval or verification.
- Expensive operations use total-run budgets rather than artificial per-cycle rationing.
- Failed checks should produce repairable backlog items.
- Durable artifacts should be reused across recurring runs when their source checkpoints remain valid.
- Safety, access boundaries, and escalation authority remain explicit.

## Scope

This is an experimental lab for reasoning about autonomous task loops. It is not a workflow engine, scheduler, Teams connector, or replacement for platform-native orchestration. Its value is the visible contract: the task, evidence, progress, and stopping logic can all be inspected and revised directly.
