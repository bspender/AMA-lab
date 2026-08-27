# Goal Card: AMA Loop-Engineering Workshop Use-Case Ideation

Goal Card Version: 0.1
Task Worker: `ideation`

## OBJECTIVE

Identify and rank exactly 10 distinct workshop use cases most likely to teach loop engineering to Emerging Technology Cloud Solution Architects within a 90-minute Azure Master Architect program for senior Microsoft CSAs.

Provide a concise comparison of all 10 and expand the Top 3 into interview-ready briefs for designing a separate Goal Card for each potential workshop lab.

## OUTPUT

Produce:

1. A concise ranked Top 10 comparison.
2. Three expanded lab-candidate briefs for ranks 1-3.
3. An updated cross-run idea ledger.
4. A completed, resumable run file.

### Top 10 comparison

Include one row per candidate with:

- rank;
- stable ID and name;
- one-line fingerprint;
- artifact produced;
- visible loop mechanic;
- total score;
- one-sentence comparative justification.

### Top 3 interview-ready briefs

For each of the Top 3 include:

1. Why a senior Emerging Technology CSA would care.
2. Proposed participant artifact.
3. Draft Goal Card objective.
4. Three to five boring, checkable `DONE WHEN` criteria.
5. Named bounded sandbox.
6. Why repeated passes converge.
7. What students visibly observe changing between iterations.
8. Likely quality rules.
9. Required source inputs and context.
10. Constraints and exclusions.
11. Suggested stages and stop caps.
12. Example improvement backlog.
13. Lessons-learned and memory potential.
14. Outcome-based architecture potential.
15. Graph-evolution path, or why it should remain a single-agent loop.
16. Full 10-dimension scorecard and total.
17. Nearest alternative and comparative justification.
18. Assumptions requiring validation.
19. Remaining design-interview questions for creating that lab's Goal Card.
20. First-run risks and what to watch.

After the profiles, choose one recommended lab candidate and justify the choice.

## DONE WHEN

- Exactly 10 final candidates are ranked 1 through 10 with no ties.
- Every final candidate has a unique stable ID and fingerprint.
- No current candidate duplicates another candidate or an ineligible ledger entry.
- Every final candidate passes the checkable-finish-line, bounded-sandbox, and convergent-task gates.
- Every final candidate has all 10 scorecard values as integers from 1 to 5.
- Every weighted total is calculated correctly.
- The Top 10 comparison contains every required field.
- Ranks 1-3 each contain all 20 interview-ready brief fields.
- Each Top 3 brief identifies unresolved questions rather than inventing context.
- Each Top 3 candidate is compared with its nearest alternative.
- One candidate is recommended as the best teaching vehicle.
- Every new idea seen during the run is recorded in the ledger.
- The run file contains one decision note and progress line per iteration.
- No more than five execution iterations were used.

## QUALITY

- Optimize for teaching loop engineering, not novelty or generic AI appeal.
- Prefer work a senior CSA could adapt immediately.
- Make state, checks, backlog changes, and stop decisions visible.
- Favor outcome-based architecture reasoning.
- Treat graph evolution as optional and require justification.
- Penalize toy demos, infrastructure-heavy setup, large datasets, autonomous swarms, subjective finish lines, and tasks unlikely to converge in 90 minutes.
- Label assumptions rather than inventing evidence.
- Use comparative justification instead of generic praise.
- Keep ranks 4-10 concise; reserve detailed analysis for ranks 1-3.

### Scorecard

Score each dimension from **1 (weak) to 5 (excellent)** using approved weights:

| Dimension | High-score meaning |
|---|---|
| CSA Relevance | Recurring, consequential work for Emerging Technology CSAs |
| Checkable Finish Line | Explicit and machine-checkable completion |
| Bounded Sandbox | Safe, isolated work with clear boundaries |
| Convergent Task | Each pass measurably approaches completion |
| Loop Visibility | State, evaluation, improvements, and stop decisions are observable |
| Lessons-Learned Potential | Reusable rules, failure patterns, or memory |
| Immediate Applicability | Adaptable to real CSA work immediately |
| Outcome-Based Architecture Potential | Architecture choices connect to measurable outcomes |
| Graph Evolution Potential | A justified path to a multi-role work graph |
| Workshop Fit | Meaningful result and learning moment within 90 minutes |

A candidate scoring below 3 in Checkable Finish Line, Bounded Sandbox, or Convergent Task is ineligible. A high total cannot compensate for a failed foundational dimension.

## CONTEXT

Use only:

- `ama-workshop-context.md`;
- this Goal Card;
- `ama-loop-use-case-ledger.md`;
- the current run file;
- source materials explicitly approved in context.

Do not require external research unless approved context permits it.

## CONSTRAINTS

- Maximum execution iterations: **5**.
- Configuration and run resolution do not count as iterations.
- Execute at most one iteration per invocation.
- Use equal scorecard weighting unless approved context says otherwise.
- Never use live customer data or perform live customer or production actions.
- Do not change this Goal Card or approved context during a run.
- Stop early when all `DONE WHEN` checks pass.
- Stop after two consecutive iterations without measurable progress.
- Never register more than 40 genuinely novel candidates in one run.
- A ledgered idea is not eligible as new.
- `REVISIT: <idea-id>` requires a new testable hypothesis and retains the stable ID.

Use stable kebab-case IDs and this identity fingerprint:

`CSA job | trigger/input | loop transformation | output artifact`

Renaming or cosmetically reframing an idea does not make it new.

## STAGES

Candidate maturity states:

1. `discovered`
2. `gated`
3. `scored`
4. `stress-tested`
5. `final`

Stages are not iteration numbers. Candidates may advance, regress, be replaced, or be rejected.

## STOP CAPS

Stop on the first applicable condition:

- all `DONE WHEN` checks pass;
- five execution iterations complete;
- two consecutive iterations produce no measurable improvement;
- required context, ledger, or run state cannot be safely read or written;
- fewer than 10 eligible, nonduplicate ideas can be justified;
- the 40-novel-candidate cap is exhausted without a qualifying Top 10.

Stopping without success is valid. Report unmet checks instead of filling gaps with weak or duplicate ideas.

## STATE FILES

| State | Path |
|---|---|
| Orchestration protocol | `loop-orchestrator.md` |
| Approved context | `ama-workshop-context.md` |
| Cross-run idea ledger | `ama-loop-use-case-ledger.md` |
| Per-run state | `ideation-runs\<run-id>.md` |

Ledger states are:

- `seen`
- `evaluated`
- `selected`
- `workshopped`
- `retired`
- `revisit-eligible`
