# Use-Case Run

## Metadata

| Field | Value |
|---|---|
| Run ID | |
| Status | In Progress |
| Goal Card | |
| Goal Version / Fingerprint | |
| Runtime Context | none |
| Context Version / Fingerprint | none |
| Acceptance Boundary | |
| Run Sequence Position | |
| Boundary Start | |
| Boundary End (Exclusive) | |
| Prior Boundary End (Exclusive) | none |
| Source Classification Fingerprint | |
| Created | |
| Updated | |
| Cycle | 0 |
| Maximum Cycles | |
| Stall Count | 0 |
| Stall Cap | |
| Current Goal Stage | |
| Current Target Slice | none |
| Output Root Resolution | |
| Resolved Output Root | |
| Primary Root Failure | |
| Prior Run | none |
| Continuity Sources | none |
| Continuity Fingerprints | none |
| Event Log Path | |
| Event Count | 0 |
| Last Event Sequence | 0 |
| Latest Event | none |
| Artifact Paths | |
| Interruption Reason | |
| Stop Reason | |

## Loop Preflight

| Test | Result | Evidence |
|---|---|---|
| Checkable finish line | Pending | |
| Bounded sandbox | Pending | |
| Convergent task | Pending | |
| Feasible cycle budget | Pending | |
| Bounded execution | Pending | |
| Bounded delegation | Pending | |

## Resolved Runtime Configuration

| Setting | Value | Source |
|---|---|---|
| | | Goal Card or context |

## Source Checkpoints and Reuse Plan

Compare the complete fixed input boundary with the prior run before action. Reuse an artifact only after its
current input checkpoint and saved artifact fingerprint are verified.

| Input Partition | Required Checkpoints | Fallback or Optional Checkpoints | Quality Result | Prior Artifact | Decision | Evidence |
|---|---|---|---|---|---|---|
| | | | | | New / Reprocess / Reconcile / Reuse | |

## Work Event Log

The authoritative event record is `<run-id>.events.jsonl`. This table is a derived cycle-level view, rebuilt from
the sidecar at cycle boundaries. Never add a row without matching sidecar events.

| Cycle | Started | Ended | Slice ID | Primary Target | Validation Failures | Checks Before | Checks After | Decision |
|---:|---|---|---|---|---:|---:|---:|---|
| | | | | | | | | |

## Current Target Slice

One target slice is active per cycle. Persist it before action or child dispatch.

| Field | Value |
|---|---|
| Slice ID | none |
| Slice Status | none |
| Fix Objective | |
| Primary Failed Check / Stage Exit | |
| Backlog Item IDs | |
| Source Partition | |
| Artifact Scope | |
| Expected Measurable Delta | |
| Verification Method | |
| Delegation Decision | |

## Child Activity Log

Add one row per launch before dispatch, update that row with its outcome, and retain completed rows across cycles.
The parent is the sole writer to authoritative artifacts and integrates results in declared child-ID order.

| Cycle | Slice ID | Child ID | Launch | Task Boundary | Input Partition | Integration Order | Status | Accepted Contribution or Failure |
|---:|---|---|---:|---|---|---:|---|---|
| | | | | | | | | |

## Artifact State

Record the current artifact paths, existence, and relevant machine-checkable properties.

| Artifact | State | Evidence |
|---|---|---|
| | | |

## DONE WHEN Results

Copy every check from the operative Goal Card. Do not summarize multiple checks into one row.

| ID | Check | Result | Evidence | Last Checked |
|---|---|---|---|---|
| DW-01 | | Pending | | |

## Goal Stage State

Use only stages named by the Goal Card.

| Stage | State | Entry Evidence | Exit Evidence |
|---|---|---|---|
| | Pending | | |

## Ordered Backlog

This table is the current ranking. Give each item a stable ID.

| Priority | Backlog ID | Action | Failed Check or Stage | State |
|---:|---|---|---|---|
| 1 | | | | Pending |

## Backlog Decision History

Append every material addition, removal, split, merge, or rank change.

| Cycle | Backlog ID | Prior Rank | New Rank | Decision and Rationale | Evidence |
|---:|---|---:|---:|---|---|
| | | | | | |

## Progress Metrics

| Metric | Baseline | Current | Target | Last Delta |
|---|---:|---:|---:|---:|
| Passing DONE WHEN checks | 0 | 0 | | 0 |
| | | | | |

## Slice and Cycle History

Derive one summary row for every completed cycle from the event sidecar. Do not reconstruct missing events.

| Cycle | Timestamp | Context Version / Fingerprint | Slice ID | Goal Stage | Primary Target | Why This Slice | Expected Delta | Observed Delta | Affected Checks | Decision |
|---:|---|---|---|---|---|---|---|---|---|---|
| | | | | | | | | | | |

## Persisted Progress Line

`[USE-CASE LOOP] run=<run-id> | cycle=<n>/<max> | stage=<goal-stage> | checks=<passed>/<total> | stall=<n>/<cap> | status=<IN_PROGRESS|COMPLETE|STOPPED>`
