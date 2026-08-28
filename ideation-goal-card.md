# Goal Card: AMA Loop-Engineering Workshop Use-Case Ideation

Goal Card Version: 0.2
Status: **Approved 2026-08-28**
Task Worker: `ideation`
Requires Context Version: 2

> This version exists because `run-2026-08-27-a` completed all v0.1 `DONE WHEN` checks and still produced a
> recommendation that reversed under a build-practicality lens. That is an instrument gap, not a judgment
> error: v0.1 contains no dimension capable of moving a rank on facilitator build cost, no gate that
> distinguishes a machine-checkable finish line from a vacuously satisfiable one, and no requirement that a
> candidate name what forces a second pass. See "Change Record" for the six deltas and their evidence.

## OBJECTIVE

Identify and rank exactly 10 distinct workshop use cases most likely to teach loop engineering to Emerging Technology Cloud Solution Architects within a 90-minute Azure Master Architect program for senior Microsoft CSAs.

Prefer candidates a facilitator can actually build, calibrate, and re-run as a repeatable lab.

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
- iteration-forcing mechanism;
- facilitator build-cost label;
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
16. Full 12-dimension scorecard and total.
17. Nearest alternative and comparative justification.
18. Assumptions requiring validation.
19. Remaining design-interview questions for creating that lab's Goal Card.
20. First-run risks and what to watch.
21. **Facilitator reference solution and diagnostic guide** - the answer key: worked converged artifact, defect-to-rule mapping, pass-1 versus pass-N exemplars, stuck-versus-slow diagnostics, and the hint ladder.
22. **Facilitator artifact inventory and derived build-cost label** - the itemized inventory required by approved context, with the label derived from it rather than asserted.
23. **Iteration-forcing mechanism** - what makes a second and third pass necessary, and why it controls pass count rather than work volume.

After the profiles, choose one recommended lab candidate and justify the choice.

## DONE WHEN

- Exactly 10 final candidates are ranked 1 through 10 with no ties.
- Every final candidate has a unique stable ID and fingerprint.
- No current candidate duplicates another candidate or an ineligible ledger entry.
- Every final candidate passes the checkable-finish-line, bounded-sandbox, convergent-task, and gaming-resistance gates.
- Every final candidate has all 12 scorecard values as integers from 1 to 5.
- Every weighted total is calculated correctly.
- The Top 10 comparison contains every required field.
- Ranks 1-3 each contain all 23 interview-ready brief fields.
- Each Top 3 brief identifies unresolved questions rather than inventing context.
- Each Top 3 candidate is compared with its nearest alternative.
- **Every final candidate names an iteration-forcing mechanism, and that mechanism is shown to control pass count rather than work volume.**
- **Each Top 3 build-cost label is derived from an itemized facilitator artifact inventory rather than asserted.**
- **Each Top 3 brief states how its finish line resists vacuous satisfaction.**
- One candidate is recommended as the best teaching vehicle.
- **The recommended candidate has one recorded pilot dry run reporting observed pass count, stop reason, and whether the finish line held.**
- Every new idea seen during the run is recorded in the ledger.
- The run file contains one decision note and progress line per iteration.
- No more than five execution iterations were used.

## QUALITY

- Optimize for teaching loop engineering, not novelty or generic AI appeal.
- Prefer work a senior CSA could adapt immediately.
- Prefer labs a facilitator can build once and re-run, over labs that are elegant but expensive to author or calibrate.
- Make state, checks, backlog changes, and stop decisions visible.
- Favor outcome-based architecture reasoning.
- Treat graph evolution as optional and require justification.
- Penalize toy demos, infrastructure-heavy setup, large datasets, autonomous swarms, subjective finish lines, and tasks unlikely to converge in 90 minutes.
- **Penalize finish lines that are machine-checkable but satisfiable without the intended reasoning.** Mechanical citation, vacuous options, and blanket labeling satisfy form without intent.
- **Do not treat artifact page count, input length, or word count as a proxy for facilitator preparation effort.** Cost lives in calibration and the answer key.
- **Do not treat work volume as evidence of iteration count.** Seeded defects, checklist length, and finding counts control how much work exists in a pass, not how many passes occur.
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
| Gaming Resistance | The finish line cannot be satisfied vacuously; passing requires the intended reasoning, and cheap degenerate outputs are detectably inadequate |
| Loop Visibility | State, evaluation, improvements, and stop decisions are observable |
| Lessons-Learned Potential | Reusable rules, failure patterns, or memory |
| Immediate Applicability | Adaptable to real CSA work immediately |
| Outcome-Based Architecture Potential | Architecture choices connect to measurable outcomes |
| Graph Evolution Potential | A justified path to a multi-role work graph |
| Workshop Fit | Meaningful result and learning moment within 90 minutes |
| Facilitator Build Cost | Low total authoring burden: few inputs, small answer key, little calibration, cheap to re-variant |

**Scoring direction.** All dimensions score 5 as best. Facilitator Build Cost is inverted in plain language: **5 means cheapest to build**, 1 means most expensive. Score it from the artifact inventory required by approved context, not from impression.

**Foundational gates.** A candidate scoring below 3 in Checkable Finish Line, Bounded Sandbox, Convergent Task, or Gaming Resistance is ineligible. A high total cannot compensate for a failed foundational dimension.

**Gaming Resistance is a gate, not a bonus.** A candidate whose checks pass on a degenerate answer teaches the counter-pattern it is meant to refute: it lets the loop terminate early and rewards prompt-and-hope.

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
- A ledgered idea is not eligible as new, regardless of its disposition. `not-carried` blocks duplicate registration; it is not a deletion. The `DONE WHEN` phrase "ineligible ledger entry" means any ledger entry, since all of them are ineligible as new.
- A ledger candidate with disposition `retired` may not be reopened by `REVISIT`; only a change to approved context can lift the exclusion that retired it.
- `REVISIT: <idea-id>` requires a new testable hypothesis and retains the stable ID. The hypothesis must be authored by the run. A hypothesis pre-written into the ledger does not satisfy this gate.
- **A Goal Card version change is a qualifying changed constraint for revisit, provided the run names the testable hypothesis the change creates.** A revisit run must re-evaluate carried candidates rather than re-discover them.

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

## Change Record

Maximum total score changes from **70** to **85**. Weight sum changes from 14 to 17. Scores from runs using v0.1 are not comparable to v0.2 totals and must be recomputed, not carried.

| # | Delta | Evidence from `run-2026-08-27-a` |
|---|---|---|
| 1 | Added **Facilitator Build Cost** dimension, weight 2 | The run's own recommendation reversed under a build lens. v0.1 could not express this: approved context only asks to penalize *otherwise similar* candidates, which is a tie-break nudge and never moved a rank. |
| 2 | Build-cost label must be derived from an itemized artifact inventory | All three Top 3 briefs asserted `small`. Independent review re-labeled them medium, medium-upper, and large. A label no one can check is not a check. |
| 3 | Added brief field 21, facilitator reference solution and diagnostic guide | All 20 v0.1 fields omit the answer key. It is the single largest uncounted cost and the reason rank 3 is genuinely `large`. |
| 4 | Added **Gaming Resistance** as a scored dimension and fourth foundational gate | v0.1 gates on "machine-checkable," which a vacuous answer can satisfy. Read-only rules prevent editing the evaluator, not satisfying it mechanically. |
| 5 | Added iteration-forcing mechanism as brief field 23 and a `DONE WHEN` check | The v0.1 run argued that seeded defect density gave deterministic control over pass count. It does not: defect density controls work items per pass, not the number of passes. v0.1 had no field where that error could surface. |
| 6 | Added a recorded pilot dry run for the recommended candidate | v0.1 permitted recommending a lab that had never been executed once, so calibration risk stayed invisible until after selection. |

Deltas 1, 4, and 5 would each independently have changed the v0.1 outcome.

## Version History

| Version | Status | Weight sum / Max | Gates | DONE WHEN | Brief fields | Notes |
|---|---|---|---:|---:|---:|---|
| 0.1 | Superseded | 14 / 70 | 3 | 14 | 20 | Weights: CSA 1, Checkable 1, Sandbox 1, Convergent 1, Loop Visibility 2, Lessons 1, Immediate Applicability 2, Own-Brain Amplification 2, Graph Extensibility 1, Workshop Fit 2. Gates: Checkable, Sandbox, Convergent, each >= 3. Used by `run-2026-08-27-01` and `run-2026-08-27-a`. |
| 0.2 | Approved 2026-08-28 | 17 / 85 | 4 | 18 | 23 | Adds Gaming Resistance (weight 1, fourth gate) and Facilitator Build Cost (weight 2, inverted so 5 is cheapest). See Change Record. |

Prior versions are recoverable from git history. This file is the operative card at every version; the version is stamped in the header, not the filename, so that changes remain diffable.
