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
| [`ama-workshop-context.baseline.md`](ama-workshop-context.baseline.md) | Untouched pre-interview context for reference or starting another workshop configuration |
| [`ama-loop-use-case-ledger.md`](ama-loop-use-case-ledger.md) | Cross-run semantic duplicate registry |
| [`ama-loop-use-case-ledger.baseline.md`](ama-loop-use-case-ledger.baseline.md) | Untouched empty ledger for reference or starting an independent ideation history |
| `ideation-runs\<run-id>.md` | Per-run artifact state, backlog, checks, counters, and decisions |

The boundaries are:

- **Orchestrator:** how one iteration starts, persists, and stops.
- **Ideation worker:** how workshop candidates are generated and improved.
- **Goal Card:** what successful completion means.
- **Context:** what assumptions and inputs are approved.
- **Run file:** what happened and what remains.
- **Ledger:** which ideas have already been seen.

### Baseline files

The `.baseline.md` files preserve untouched starting state so another facilitator can see or reuse the lab before configuration and execution add workshop-specific history:

- `ama-workshop-context.baseline.md` contains the pre-interview Cycle 0 context.
- `ama-loop-use-case-ledger.baseline.md` contains the empty pre-run idea registry.

Baseline files are not authoritative workflow state and the `ideation` worker does not read or update them. Active state remains in `ama-workshop-context.md` and `ama-loop-use-case-ledger.md`.

## Why the orchestrator is not an agent

The orchestrator remains a Markdown protocol for this version. Making it another agent would introduce agent-to-agent coordination, invocation semantics, and another hidden context boundary without improving the core lesson.

Keeping it visible and declarative lets students inspect the control loop independently from the worker. A future orchestrator agent is justified when automated worker invocation or multi-worker coordination becomes part of the learning objective.

## Fresh-context model

The `ideation` agent is instructed to treat files as authoritative and conversation history as non-authoritative. Selecting the agent does not itself guarantee a physically fresh model context.

For a defensible fresh-context demonstration, create a new GitHub Copilot app conversation for each iteration. The new worker conversation receives the run ID and reconstructs state from the repository.

## Lifecycle terminology

- **Configuration (Cycle 0):** the pre-run interview that produces approved workshop context. It can use up to three interview **rounds**.
- **Round:** one Cycle 0 question-and-answer pass persisted to `ama-workshop-context.md`. Rounds are not execution work and do not count against the run limit.
- **Run:** one complete attempt to satisfy the Goal Card, beginning after context approval and ending as `Complete` or `Stopped`.
- **Iteration:** one execution pass within a run: `Observe -> Evaluate -> Decide -> Act -> Persist`. `START` executes Iteration 1; each `CONTINUE` executes at most one additional iteration, up to five.
- **Candidate stage:** a candidate's maturity (`discovered`, `gated`, `scored`, `stress-tested`, or `final`). Stages are not rounds or iteration numbers.

The worker does not continue automatically. After each iteration it persists state and returns control to the user. The user inspects the evidence and invokes `CONTINUE` only when another iteration is warranted.

## GitHub Copilot app runbook

### 1. Configure the workshop

1. Open this repository in the GitHub Copilot app.
2. Start a new conversation.
3. Select the repository `ideation` agent.
4. Enter:

   ```text
   START
   ```

Because `ama-workshop-context.md` starts as `Status: Draft`, the worker conducts Cycle 0 in rounds. It persists each round, proposes the completed context, and waits for approval.

To conduct the next Cycle 0 round, enter `START` again in the same conversation. While the context remains `Status: Draft`, `START` continues configuration rather than creating an ideation run. Repeat for up to three interview rounds. A new conversation is optional during Cycle 0 because configuration is a continuous interview and each round is persisted before the next begins.

When the proposed context is complete, approve it explicitly by entering `APPROVE CONTEXT`. Approval is never inferred from agreement in conversation. If the draft context requires a draft Goal Card version, this single instruction adopts both.

### 2. Start the run and execute Iteration 1

After the worker persists `Status: Approved`, start a new conversation with the `ideation` agent and enter `START` to create the run and execute Iteration 1. This is the first point where fresh context matters to the demonstration: the execution worker must reconstruct its inputs from approved files rather than the configuration conversation.

Iteration 1 builds the initial pool, applies the foundational gates, scores the active pool, and creates a provisional ranking when at least 10 candidates are eligible. In cold-start mode the pool is 20 novel candidates; in revisit mode it is the carried set plus a novel backfill. The worker then persists:

- `ideation-runs\<run-id>.md`;
- `ama-loop-use-case-ledger.md`;
- the progress console.

### 3. Review and continue one iteration at a time

Inspect the candidate pool, gate failures, scores, provisional ranking, backlog, decision note, and counters. If the run reports `CONTINUE`, start another new conversation, select `ideation`, and enter:

   ```text
   CONTINUE run=<run-id>
   ```

Each continuation reevaluates and reranks the complete active pool, then addresses the highest-priority unfinished work. Depending on the evidence, that may mean generating replacements, removing weak candidates, completing scores, stress-testing the provisional Top 10, expanding the Top 3, or finalizing the recommendation.

Ranking is progressive rather than a separate pass after candidate generation. The provisional order can change in every iteration as candidates fail gates, receive complete scores, or are compared more rigorously.

Repeat only while the worker reports `CONTINUE`. The run ends early when every `DONE WHEN` check passes, or stops at the first applicable stop condition, including the five-iteration cap.

## GitHub Copilot CLI runbook

Use `/agent` to select the repository `ideation` agent, then follow the same lifecycle:

1. Enter `START` while context is `Draft` to conduct each Cycle 0 interview round.
2. Approve the completed context with `APPROVE CONTEXT`.
3. Begin a new conversation, select `ideation`, and enter `START` to execute Iteration 1.
4. Review persisted state and use `CONTINUE run=<run-id>` for one additional iteration at a time.

The control words are ordinary task instructions, not slash commands.

## Controls

| Intent | Instruction |
|---|---|
| Configure or begin Iteration 1 | `START` |
| Approve the draft context (and the Goal Card version it requires) | `APPROVE CONTEXT` |
| Approve a draft Goal Card against already-approved context | `APPROVE GOAL CARD` |
| Show state without changing it | `STATUS run=<run-id>` |
| Execute one more iteration | `CONTINUE run=<run-id>` |
| Reconfigure workshop assumptions | `RECONFIGURE` |
| Start another ideation run | `NEW RUN` |
| Resume a named run | `RESUME run=<run-id>` |
| Reevaluate a prior idea | `REVISIT: <idea-id>` |

## Ideation policy

Iteration 1 runs in one of two modes, chosen by reading the ledger.

In **cold-start mode**, when the ledger holds no carried candidates, Iteration 1 registers 20 genuinely novel, ledger-cleared candidates.

In **revisit mode**, when the ledger holds candidates with disposition `carried`, Iteration 1 admits those candidates and re-scores them under the operative card, then generates novel candidates to backfill:

`max(10, 30 - carried candidate count)`

Carried candidates are re-scored, not re-discovered. Prior gate results and weighted totals do not carry forward; only dimension vectors carry, as reference evidence tagged with the card version that produced them.

Later iterations in either mode add replacements only when fewer than 15 eligible candidates remain:

`max(5, 15 - eligible candidate count)`

Every iteration evaluates the complete active pool. A run may register no more than 40 novel candidates; carried candidates are exempt because they are not novel.

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
[AMA LOOP] run=<run-id> | mode=<COLD|REVISIT> | iteration=<n>/5 | carried=<C> | generated=+<G> | duplicates=+<D> | novel=+<N> (total=<NT>/40) | gate-rejected=+<R> | eligible=<E> | qualified=<Q>/10 | ledger-total=<L> | status=<status>
```

The `+` counters report current-iteration activity. `mode` is fixed at Iteration 1 and does not change mid-run. `carried` is the count of ledger candidates admitted for re-scoring, zero in cold-start mode. `eligible` is the active pool passing foundational gates, carried and novel combined. `qualified` is progress toward the final 10. `ledger-total` is historical coverage, including rejected ideas.

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
