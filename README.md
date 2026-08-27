# strategery

My day-to-day reasoning partner and constant work in progress.

## File-driven loop lab

This repository demonstrates loop engineering in GitHub Copilot CLI and GitHub Copilot app without depending on a `/goal` command.

The implementation is intentionally representative rather than a replacement for `/goal`. A stateless task worker applies a local Goal Card one iteration at a time, persists state in Markdown, and exposes progress for inspection.

## Architecture

| File | Responsibility |
|---|---|
| [`.github\agents\ideation.agent.md`](.github/agents/ideation.agent.md) | Stateless domain worker: generation, deduplication, gating, scoring, pruning, and Top 3 expansion |
| [`loop-orchestrator.md`](loop-orchestrator.md) | Bare control plane: load, configure, resolve, execute one iteration, persist, and stop |
| [`ideation-goal-card.md`](ideation-goal-card.md) | Declarative objective, output, acceptance policy, scorecard, constraints, and stop caps |
| [`ama-workshop-context.md`](ama-workshop-context.md) | Approved interview answers and task assumptions |
| [`ama-loop-use-case-ledger.md`](ama-loop-use-case-ledger.md) | Cross-run semantic duplicate registry |
| `ideation-runs\<run-id>.md` | Per-run artifact state, backlog, checks, counters, and decisions |

The boundaries are:

- **Orchestrator:** how one iteration starts, persists, and stops.
- **Ideation worker:** how workshop candidates are generated and improved.
- **Goal Card:** what successful completion means.
- **Context:** what assumptions and inputs are approved.
- **Run file:** what happened and what remains.
- **Ledger:** which ideas have already been seen.

## Why the orchestrator is not an agent

The orchestrator remains a Markdown protocol for this version. Making it another agent would introduce agent-to-agent coordination, invocation semantics, and another hidden context boundary without improving the core lesson.

Keeping it visible and declarative lets students inspect the control loop independently from the worker. A future orchestrator agent is justified when automated worker invocation or multi-worker coordination becomes part of the learning objective.

## Fresh-context model

The `ideation` agent is instructed to treat files as authoritative and conversation history as non-authoritative. Selecting the agent does not itself guarantee a physically fresh model context.

For a defensible fresh-context demonstration, create a new GitHub Copilot app conversation for each iteration. The new worker conversation receives the run ID and reconstructs state from the repository.

## GitHub Copilot app runbook

### 1. Configure

1. Open this repository in the GitHub Copilot app.
2. Start a new conversation.
3. Select the repository `ideation` agent.
4. Enter:

   ```text
   START
   ```

Because `ama-workshop-context.md` starts as `Status: Draft`, the worker conducts Cycle 0 in rounds. It persists each round, proposes the completed context, and waits for approval.

To conduct the next Cycle 0 round, enter `START` again in the same conversation. While the context remains `Status: Draft`, `START` continues configuration rather than creating an ideation run. Repeat for up to three interview rounds. A new conversation is optional during Cycle 0 because configuration is a continuous interview and each round is persisted before the next begins.

When the proposed context is complete, explicitly approve it. After the worker persists `Status: Approved`, start a new conversation with the `ideation` agent and enter `START` to create the run and execute Iteration 1. This is the first point where fresh context matters to the demonstration: the execution worker must reconstruct its inputs from approved files rather than the configuration conversation.

### 2. Inspect

The worker executes exactly one iteration, then updates:

- `ideation-runs\<run-id>.md`;
- `ama-loop-use-case-ledger.md`;
- the progress console.

Inspect the candidate pool, gate failures, backlog, decision note, and counters.

### 3. Continue with fresh context

Start another new conversation, select `ideation`, and enter:

```text
CONTINUE run=<run-id>
```

Repeat with a new conversation for each iteration. The run can use no more than five iterations.

## GitHub Copilot CLI runbook

Use `/agent` to select the repository `ideation` agent, then enter `START`. For a fresh-context demonstration, begin a new conversation before each continuation, select `ideation`, and enter:

```text
CONTINUE run=<run-id>
```

The control words are ordinary task instructions, not slash commands.

## Controls

| Intent | Instruction |
|---|---|
| Configure or begin Iteration 1 | `START` |
| Show state without changing it | `STATUS run=<run-id>` |
| Execute one more iteration | `CONTINUE run=<run-id>` |
| Reconfigure workshop assumptions | `RECONFIGURE` |
| Start another ideation run | `NEW RUN` |
| Resume a named run | `RESUME run=<run-id>` |
| Reevaluate a prior idea | `REVISIT: <idea-id>` |

## Ideation policy

Iteration 1 registers 20 genuinely novel, ledger-cleared candidates. Later iterations add replacements only when fewer than 15 eligible candidates remain:

`max(5, 15 - eligible candidate count)`

Every iteration evaluates the complete active pool. A run may register no more than 40 novel candidates.

Ideas are identified semantically:

`CSA job | trigger/input | loop transformation | output artifact`

Changing a title does not create a new idea. Duplicates are counted but not persisted as new records. Novel ideas failing foundational gates remain in the ledger so later runs do not rediscover them.

## Result shape

The final artifact contains:

1. A concise ranked comparison of all 10 candidates.
2. Interview-ready profiles for ranks 1-3.
3. A recommendation for the best lab candidate.

Each Top 3 profile contains enough information to begin a separate design interview and create a new Goal Card for that lab. Missing decisions remain explicit questions rather than invented assumptions.

## Progress console

Every worker response ends with:

```text
[AMA LOOP] run=<run-id> | iteration=<n>/5 | generated=+<G> | duplicates=+<D> | novel=+<N> (total=<NT>/40) | gate-rejected=+<R> | eligible=<E> | qualified=<Q>/10 | ledger-total=<L> | status=<status>
```

The `+` counters report current-iteration activity. `eligible` is the active pool passing foundational gates. `qualified` is progress toward the final 10. `ledger-total` is historical coverage, including rejected ideas.

## Stop behavior

The loop stops when:

- every `DONE WHEN` check passes;
- five iterations complete;
- two consecutive iterations show no measurable progress;
- required state cannot be safely read or written;
- 10 eligible, nonduplicate ideas cannot be justified; or
- the 40-candidate discovery cap is exhausted.

Stopping without success is valid. The worker reports unmet checks instead of filling the list with weak or duplicate ideas.

## Future evolution

The local Goal Card can later map to a GitHub Issue:

- issue body: Objective, Output, Context, and Constraints;
- task list: `DONE WHEN` checks;
- labels or project fields: stage, status, owner, and risk;
- comments: iteration decisions and progress;
- linked artifacts: run state, ledger, and final output.

That evolution replaces the persistence adapter without changing the Goal Card contract.
