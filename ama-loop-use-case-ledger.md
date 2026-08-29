# AMA Loop-Engineering Workshop Idea Ledger

Durable cross-run idea registry for workshop use-case ideation. Read before generating candidates; update
after every execution iteration.

This is the single cross-run ledger named by the Goal Card STATE FILES table. All runs write here.

## Rules

- Stable IDs use kebab-case and are never reassigned.
- A renamed or reframed idea keeps its original ID when the CSA job, trigger, loop transformation, and
  output artifact are materially the same.
- Where two runs generate the same idea independently, the earlier ID is authoritative and the later ID is
  recorded as an alias.
- A ledgered idea is not eligible as a new idea, regardless of disposition.
- `REVISIT: <idea-id>` requires a new testable hypothesis supplied by the run. Do not pre-write revisit
  hypotheses into this file.
- Record every genuinely new idea seen, including ideas rejected before scoring.
- Record evidence, not verdicts. Ranks and weighted totals are run-relative and belong in the run file.

### Worked Adjudications

The four-field fingerprint is not self-calibrating. Record reference rulings here as they are made so later
runs inherit calibration rather than re-deriving it.

| Pair | Ruling | Reasoning |
|---|---|---|

Compare the transformation field first. Sharing a domain noun is not evidence of sameness, and sharing no
vocabulary is not evidence of difference.

## Registry States

State is recorded on two orthogonal axes. A single column cannot represent both.

**Lifecycle** - how far the idea progressed.

| Value | Meaning | Writer |
|---|---|---|
| `seen` | Recorded but not gated or scored | Worker, on registration before scoring |
| `evaluated` | Gated or scored in at least one run | Worker, after scoring |
| `selected` | Included in at least one run's final Top 10 | Worker, at finalization |
| `workshopped` | Used in an actual workshop | Facilitator, post-delivery |

**Disposition** - availability to future runs.

| Value | Meaning | Writer |
|---|---|---|
| `carried` | Available for re-evaluation by the next run | Carry-forward decision, recorded with a reason |
| `not-carried` | Known and duplicate-blocking, but not queued for re-evaluation | Default for ledgered ideas |
| `retired` | Excluded from future consideration by an approved-context exclusion | Requires a cited exclusion |

Invariants:

- `carried` requires lifecycle `evaluated` or later.
- `retired` requires a named exclusion in approved context; a low score is never sufficient.
- `not-carried` still blocks duplicate registration. It is not a deletion.
- Every ledgered idea is ineligible as a new idea regardless of disposition. Only `REVISIT` with a
  run-supplied hypothesis reopens one.

## Run Log

| Run ID | Date | Card | Card Ver | Ctx Ver | Weights (sum/max) | Model | Iterations | Result | Novel added | Run file |
|---|---|---|---:|---:|---|---|---|---|---:|---|

## Carried Candidates

Ideas with disposition `carried`, available for re-evaluation by the next run.

Weighted totals and ranks are deliberately omitted because they are run-relative. Dimension vectors may be
retained as reference evidence only when tagged with the card version and weight sum that produced them.

| ID | CSA job | Trigger / input | Loop transformation | Output artifact | Origin | Lifecycle | Disp. | Gates (card ver) | Vector (reference only) | Aliases |
|---|---|---|---|---|---|---|---|---|---|---|

### Build-Cost Evidence for Carried Candidates

Facilitator Build Cost must be derived from the approved inventory rather than carried forward as an
unsupported label.

| ID | Participant inputs | Planted material | Answer key | Calibration | Diagnostics | Variant cost | Label / score | Evidence version |
|---|---|---|---|---|---|---|---|---|

## Known Ideas Not Carried

Recorded to block duplicate registration. Not queued for re-evaluation.

| ID | One-line fingerprint | Origin | Lifecycle | Disp. | Eligible | Failed gates | Evidence |
|---|---|---|---|---|---|---|---|

## Cross-Boundary Disputes

Record cases where separate runs score the same idea materially differently under the same card. A large
spread can indicate an instrument gap or a finish line specified differently between runs.

| Idea | Run A | Run B | Spread | Significance |
|---|---|---|---|---|

## Carry-Forward Provenance

| Field | Value |
|---|---|
| Built | |
| Source runs | |
| Scored under | |
| Distinct ideas known | 0 |
| Carried for re-evaluation | 0 |
| Selection rule | |
| Deliberately omitted | Weighted totals and ranks |

Integrity notes:

-
