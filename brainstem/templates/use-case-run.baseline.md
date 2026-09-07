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
| Created | |
| Updated | |
| Cycle | 0 |
| Maximum Cycles | |
| Stall Count | 0 |
| Stall Cap | |
| Current Goal Stage | |
| Current Target Slice | none |
| Artifact Paths | |
| Interruption Reason | |
| Stop Reason | |

## Loop Preflight

| Test | Result | Evidence |
|---|---|---|
| Checkable finish line | Pending | |
| Bounded sandbox | Pending | |
| Convergent task | Pending | |
| Bounded execution | Pending | |
| Bounded delegation | Pending | |

## Resolved Runtime Configuration

| Setting | Value | Source |
|---|---|---|
| | | Goal Card or context |

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
| Candidate Selection Rubric | |

## Child Execution Manifest

The parent is the sole writer to authoritative artifacts and integrates results in declared child-ID order.

| Child ID | Task Boundary | Allowed Inputs | Expected Result | Integration Order | Attempts | Status | Integration Decision |
|---|---|---|---|---:|---:|---|---|
| | | | | | 0 | | |

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

| Priority | Action | Failed Check or Stage | State |
|---:|---|---|---|
| 1 | | | Pending |

## Progress Metrics

| Metric | Baseline | Current | Target | Last Delta |
|---|---:|---:|---:|---:|
| Passing DONE WHEN checks | 0 | 0 | | 0 |

## Cycle Log

Append exactly one row for every completed cycle.

| Cycle | Timestamp | Context Version / Fingerprint | Checked | Result | Action | Measurable Delta | Decision Note |
|---:|---|---|---|---|---|---|---|

## Console Milestones

Record the latest persisted state associated with each required console heartbeat.

| Timestamp | Milestone | Cycle | Slice ID | Child ID | State Persisted |
|---|---|---:|---|---|---|
| | Run initialized | 0 | none | | Yes |

## Persisted Progress Line

`[USE-CASE LOOP] run=<run-id> | cycle=<n>/<max> | stage=<goal-stage> | checks=<passed>/<total> | stall=<n>/<cap> | status=<IN_PROGRESS|COMPLETE|STOPPED>`
