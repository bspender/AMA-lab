# Goal Card: AMA Loop-Engineering Workshop Use-Case Ideation

Goal Card Version: 0.3
Status: **Draft**
Task Worker: `ideation`
Requires Context Version: 3

## OBJECTIVE

Identify and rank exactly 10 distinct workshop use cases most likely to teach loop engineering to Emerging Technology Cloud Solution Architects within a 90-minute Azure Master Architect program for senior Microsoft CSAs.

Prefer candidates a facilitator can actually build, calibrate, and re-run as a repeatable lab.

Provide a concise comparison of all 10 and expand the Top 3 into interview-ready briefs for designing a separate Goal Card for each potential workshop lab.

## OUTPUT

Produce:

1. A concise ranked Top 10 comparison.
2. Three dedicated expanded lab-candidate files for ranks 1-3.
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

### Expanded idea files

Write each Top 3 expansion to:

`ideation-runs\<run-id>\expanded-idea-<rank>.md`

Each file follows `templates\expanded-idea-template.md` and is independently understandable without the run
file. The template organizes each expansion around the downstream Goal Designer interview:

1. plain-language idea and reader orientation;
2. evidence-status legend and provenance;
3. concrete participant journey and visible loop;
4. assumptions and design choices, including why each was introduced;
5. proposed starter kit with existence status, minimum contents, and authoring burden;
6. minimum credible mockup versus workshop-ready build;
7. candidate evaluator, convergence measure, gaming attacks, and iteration-forcing mechanism;
8. facilitator reference solution, diagnostics, inventory, and derived build-cost label;
9. complete Goal Designer handoff covering candidate Objective, Output, Done When, Quality, Context,
   Constraints, Stages, and Stop-Caps;
10. preliminary "should this loop?" assessment against a checkable finish line, bounded sandbox, and
    convergent task;
11. remaining interview questions rather than invented decisions;
12. scorecard, nearest alternative, lessons, architecture potential, graph path, and first-run
    risks.

Any input not verified at a repository path must be labeled **To be authored**, not described as though it
already exists. Any unapproved choice must be labeled **Proposed for design** or **Must decide**.

After the profiles, choose one recommended lab candidate and justify the choice.

## DONE WHEN

- Exactly 10 final candidates are ranked 1 through 10 with no ties.
- Every final candidate has a unique stable ID and fingerprint.
- No current candidate duplicates another candidate or an ineligible ledger entry.
- Every final candidate passes the checkable-finish-line, bounded-sandbox, convergent-task, and gaming-resistance gates.
- Every final candidate has all 12 scorecard values as integers from 1 to 5.
- Every weighted total is calculated correctly.
- The Top 10 comparison contains every required field.
- Ranks 1-3 each have a dedicated file at the required path and contain every template section.
- Every expanded file is independently understandable without reading the run file.
- Every named input and facilitator artifact has an existence status; no missing artifact is phrased as
  available.
- Every expanded file separates the minimum credible mockup from the calibrated workshop-ready build.
- Every expanded file contains an attachable Goal Designer handoff with all eight Goal Card fields clearly
  marked as candidate inputs rather than approved decisions.
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
- Write expansions for a reader who has not seen the run. Define fictional domains, roles, fixtures,
  thresholds, and stage mechanics before using them.
- Explain why each proposed input exists and whether it must be authored; specificity without provenance is
  a hidden assumption, not useful context.
- Keep the Goal Designer handoff compact enough to attach as context, while placing rationale and build
  detail in the surrounding sections.

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
- `templates\expanded-idea-template.md`;
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
| Expansion contract | `templates\expanded-idea-template.md` |
| Derived expanded ideas | `ideation-runs\<run-id>\expanded-idea-<rank>.md` |

Ledger states are:

- `seen`
- `evaluated`
- `selected`
- `workshopped`
- `retired`
- `revisit-eligible`

## Change Record

When this Goal Card changes, record the version, operative contract delta, and reason. Keep run-specific
evidence in the applicable run file rather than here.

## Version History

| Version | Status | Weight sum / Max | Gates | DONE WHEN | Brief fields | Notes |
|---|---|---|---:|---:|---:|---|

Add one row when a version is approved or superseded. Prior versions remain recoverable from git history.
