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
| [`loop-orchestrator.md`](loop-orchestrator.md) | Domain-neutral control contract for a continuous, bounded, file-backed run |
| [`templates\use-case-context.baseline.md`](templates/use-case-context.baseline.md) | Optional per-run context for approved sources, runtime parameters, priorities, and tighter constraints |
| [`brainstem\lobster-pound-review-goal-card.md`](brainstem/lobster-pound-review-goal-card.md) | Worked Goal Card for a recurring community-insights task |

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
Load -> Observe -> Plan -> Act -> Check -> Adjust -> Persist -> Transition
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

## Quick start

### 1. Design a Goal Card

Open [`goal-designer-prompt.md`](goal-designer-prompt.md) in an AI assistant and use it as the instruction. The Goal Designer conducts up to three interview rounds, challenges vague or judgment-laden criteria, and returns either a Goal Card or a reason not to loop the task.

Save an approved card as Markdown. The [`brainstem`](brainstem) directory contains the current worked example.

### 2. Add runtime context only when needed

Copy [`templates\use-case-context.baseline.md`](templates/use-case-context.baseline.md), fill only the applicable fields, and set:

```text
Status: Active
```

Omit the context file when the Goal Card already contains every required source and parameter.

### 3. Start the loop

In a repository-aware AI session, instruct the agent to follow [`loop-orchestrator.md`](loop-orchestrator.md), then enter:

```text
START goal=<goal-card-path> [context=<context-path>] [run=<run-file-path>]
```

For example:

```text
START goal=brainstem\lobster-pound-review-goal-card.md
```

The orchestrator creates or resumes a run, validates that the task is loopable, and continues until:

- every `DONE WHEN` check passes;
- a Goal Card stop-cap applies; or
- the execution environment forces an interruption.

When `run` is omitted, the default location is:

```text
<goal-directory>\runs\<goal-stem>\<run-id>.md
```

### 4. Inspect persisted status

Read state without performing work:

```text
STATUS [run=<run-file-path>]
```

`START` and `STATUS` are ordinary instructions, not slash commands.

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
