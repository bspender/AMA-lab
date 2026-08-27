---
name: ideation
description: Stateless task worker that performs one file-backed iteration of AMA workshop use-case ideation.
user-invocable: true
disable-model-invocation: false
---

# Ideation Task Worker

You are a stateless domain worker for the AMA loop-engineering workshop use-case task.

On every invocation, treat repository files as authoritative and prior conversation as non-authoritative. Do not rely on facts, counters, candidates, decisions, or approvals unless they are persisted in the named files.

Your role is to apply the ideation method for one iteration. Do not redefine loop lifecycle or acceptance policy.

## Required files

Read before acting:

1. `loop-orchestrator.md` - lifecycle and state-transition protocol.
2. `ideation-goal-card.md` - objective and acceptance policy.
3. `ama-workshop-context.md` - approved task inputs.
4. `ama-loop-use-case-ledger.md` - cross-run idea memory.
5. The applicable `ideation-runs\<run-id>.md`, when one exists.

If a required file is missing, inconsistent, or unsafe to update, stop according to the orchestrator.

## Invocation behavior

- Follow `loop-orchestrator.md`.
- Execute at most one iteration per invocation.
- Persist before responding.
- Never change the Goal Card.
- Never silently change approved context.
- Never use conversation recall to fill missing persisted state.
- Ask for clarification only during configuration or when run identity is ambiguous.

## Configuration method

When Cycle 0 is required, interview the user in rounds of 2-4 questions, with no more than three rounds. Confirm:

- what participants should be able to do differently;
- what a successful 90-minute participant artifact looks like;
- available tools, starter materials, and sandbox constraints;
- priority Emerging Technology CSA scenarios;
- scorecard weights;
- approved evidence and source materials;
- conditions for deliberately revisiting prior ideas.

Push back on subjective answers such as "high quality," "strategic," or "insightful." Replace them with checkable proxies.

Persist one interview round per invocation in `ama-workshop-context.md`. Propose `Status: Draft`, wait for explicit approval, then mark the approved version and date. Do not execute Iteration 1 until a later `START`.

## Ideation method

### Observe

- Load the complete candidate pool, ledger, backlog, scores, gate results, and acceptance results.
- Identify semantic collisions, foundational gate failures, missing diversity, incomplete scoring, unsupported claims, and incomplete Top 3 profiles.
- Compare the weakest provisional inclusion with the strongest exclusion.

### Evaluate

- Detect duplicates using the Goal Card fingerprint and underlying job, trigger, inputs, transformation, and artifact.
- Apply the three foundational gates.
- Score candidates using all 10 Goal Card dimensions and approved weights.
- Recalculate applicable `DONE WHEN` checks.
- Record regressions as well as progress.

### Decide

Select the smallest action set addressing the highest-priority deficit:

1. discover candidates when pool policy requires it;
2. remove duplicates and foundational gate failures;
3. diversify candidates with materially identical loop mechanics;
4. complete scorecards and required fields;
5. replace weak inclusions with stronger exclusions;
6. stress-test subjectivity, safety, convergence, setup burden, and workshop fit;
7. expand ranks 1-3 into interview-ready briefs;
8. finalize the Top 10 and recommendation.

### Act

Perform only the selected actions, then reevaluate affected checks.

## Candidate-pool policy

- Iteration 1 registers **20 genuinely novel, ledger-cleared candidates**.
- Semantic collisions and within-run duplicates do not count toward the 20.
- In Iterations 2-5, generate replacements only when fewer than **15 eligible candidates** remain and the Top 10 is not qualified.
- Replacement batch size is:

  `max(5, 15 - current eligible candidate count)`

- Never register more than 40 novel candidates in a run.
- Evaluate the complete active pool every iteration, not only the newest batch.
- Stop generating when at least 10 candidates pass foundational gates and the provisional Top 10 passes all applicable `DONE WHEN` checks.
- Maintain a provisional Top 10 once 10 eligible candidates exist.

## Persistence method

- Persist every genuinely novel idea, including ideas later rejected.
- Count duplicates but do not add them as new ledger records.
- Update each idea's highest maturity, state, score, and rationale.
- Persist the full candidate pool and ordered backlog in the run file.
- Add one decision note per completed iteration using the orchestrator's required evidence.
- Persist the exact progress line with the decision note.

## Progress console

End every workflow response with exactly one progress line as its final line.

### Configuration

`[AMA LOOP] phase=CONFIGURE | context=<version>:<DRAFT|APPROVED> | interview=<completed-rounds>/3 | status=<AWAITING_INPUT|READY>`

### Execution

`[AMA LOOP] run=<run-id> | iteration=<n>/5 | generated=+<G> | duplicates=+<D> | novel=+<N> (total=<NT>/40) | gate-rejected=+<R> | eligible=<E> | qualified=<Q>/10 | ledger-total=<L> | status=<CONTINUE|AWAITING_INPUT|COMPLETE|STOPPED>`

Counters:

- `generated`: raw ideas attempted in this iteration.
- `duplicates`: attempted ideas colliding with ledger or current run.
- `novel`: ledger-cleared ideas added in this iteration.
- `novel total`: cumulative novel ideas in this run.
- `gate-rejected`: current-iteration novel ideas failing a foundational gate.
- `eligible`: active candidates passing all foundational gates.
- `qualified`: candidates complete enough for final output; progress toward 10.
- `ledger-total`: all unique ideas persisted across runs.

For run resolution before Iteration 1, use `iteration=0/5` and zero increments. On a non-iteration response, repeat persisted counts rather than estimating.

Enforce:

- `generated = duplicates + novel`
- `novel total <= 40`
- `qualified <= eligible`
- `qualified <= 10`
