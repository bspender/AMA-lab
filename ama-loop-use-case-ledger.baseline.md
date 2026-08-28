# AMA Loop-Engineering Workshop Idea Ledger

Durable cross-run idea registry for workshop use-case ideation. Read before generating candidates; update after every execution iteration.

This is the single cross-run ledger named by the Goal Card STATE FILES table. All runs write here. A run may not persist ideas to a run-specific file instead; doing so satisfies the recording check only nominally and breaks cross-run duplicate detection.

## Rules

- Stable IDs use kebab-case and are never reassigned.
- A renamed or reframed idea keeps its original ID when the CSA job, trigger, loop transformation, and output artifact are materially the same. Where two runs generate the same idea independently, the earlier run's ID is authoritative and the later ID is recorded as an alias.
- A ledgered idea is not eligible as a new idea, regardless of disposition.
- `REVISIT: <idea-id>` requires a new testable hypothesis supplied **by the run**. Do not pre-write revisit hypotheses into this file; that pre-satisfies the gate the revisit rule exists to force.
- Record every genuinely new idea seen, including ideas rejected before scoring.
- Record evidence, not verdicts. Ranks and weighted totals are run-relative and belong in the run file.

### Worked adjudications

The four-field fingerprint is not self-calibrating. Record reference rulings here as they are made, so later runs inherit calibration rather than re-deriving it.

| Pair | Ruling | Reasoning |
|---|---|---|
| | | |

Compare the transformation field first. Sharing a domain noun is not evidence of sameness, and sharing no vocabulary at all is not evidence of difference.

## Registry states

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
- `retired` requires a named exclusion in approved context; a low score is never sufficient, and no `REVISIT` can lift it.
- `not-carried` still blocks duplicate registration. It is not a deletion.

## Run Log

| Run ID | Date | Card | Card Ver | Ctx Ver | Weights (sum/max) | Model | Iterations | Result | Novel added | Run file |
|---|---|---|---:|---:|---|---|---|---|---:|---|

## Carried Candidates

Ideas with disposition `carried`, available for re-evaluation by the next run.

Weighted totals and ranks are deliberately omitted: a score measures how tightly a run specified an idea, not the idea itself, so it is not a durable property. Dimension vectors are retained as reference evidence, tagged with the card version that produced them, so re-evaluation is not re-discovery.

| ID | CSA job | Trigger / input | Loop transformation | Output artifact | Origin | Lifecycle | Disp. | Gates (card ver) | Vector (reference only) | Aliases |
|---|---|---|---|---|---|---|---|---|---|---|

## Known Ideas Not Carried

Recorded to block duplicate registration. Not queued for re-evaluation.

| ID | One-line fingerprint | Origin | Lifecycle | Disp. | Eligible | Failed gates | Evidence |
|---|---|---|---|---|---|---|---|

## Cross-Boundary Disputes

Cases where independent runs scored the same idea materially differently under the same card. These are the highest-value diagnostic evidence the ledger holds: a large spread indicates a dimension the card cannot express, or a finish line one run specified and the other did not.

| Idea | Run A | Run B | Spread | Significance |
|---|---|---|---|---|

## Carry-Forward Provenance

| Field | Value |
|---|---|
| Built | |
| Source runs | |
| Scored under | |
| Distinct ideas known | |
| Carried for re-evaluation | |
| Selection rule | |
| Deliberately omitted | |

Integrity notes:

-
