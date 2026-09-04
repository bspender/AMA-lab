# Use-Case Runtime Context

Status: **Inactive**
Context Version: 1
Applies To Goal: `<goal-card-path>`
Last Updated: Pending

This optional file supplies per-run configuration and steering. It is not a Goal Card, approval gate, run
history, or acceptance policy. Copy it beside a Goal Card, fill only the applicable fields, and set
`Status: Active`.

If this file is absent or inactive, the orchestrator proceeds using the Goal Card alone.

## OBJECTIVE Steering

Optional choices about emphasis within the Goal Card's objective.

- Current run focus:
- Priority outcomes:
- Intended audience or consumer:
- Deprioritized work:

## OUTPUT Preferences

Optional output values where the Goal Card permits runtime selection.

| Setting | Value | Goal Card allowance |
|---|---|---|
| Output root | | |
| Naming convention | | |
| Format option | | |

## DONE WHEN Parameters

Values for parameters explicitly referenced by the Goal Card. Do not add, remove, weaken, or reinterpret
acceptance checks here.

| Parameter | Runtime value | Goal Card check using it |
|---|---|---|
| | | |

## QUALITY Priorities

Optional ordering or emphasis among Goal Card quality rules.

1.

Quality rules not listed here remain in force.

## CONTEXT Sources

Concrete inputs authorized for this run. A source listed here is usable only when the Goal Card permits that
source type and location.

| Source | Locator | Scope or time window | Access mode | Required for this run |
|---|---|---|---|---|
| | | | `read-only` | `yes` or `no` |

### Repository configuration

| Repository | Ref or branch | Included paths | Excluded paths | Purpose |
|---|---|---|---|---|
| | | | | |

### Runtime variables

| Name | Value | Used by |
|---|---|---|
| | | |

## CONSTRAINTS Additions

Additional restrictions may tighten the Goal Card but must not relax it.

- Additional access boundaries:
- Additional exclusions:
- Sensitive-data handling:
- Tools disabled for this run:

## STAGES Steering

Stage names must match the Goal Card. This section may focus a stage; it must not add, remove, reorder, or
redefine stages.

| Goal Card stage | Runtime focus | Inputs or configuration |
|---|---|---|
| | | |

## STOP-CAPS Overrides

Only tighter values are valid. Leave blank to inherit the Goal Card.

| Cap | Runtime value | Goal Card value |
|---|---:|---:|
| Maximum cycles | | |
| No-progress cycles | | |
| Maximum elapsed time | | |

## Runtime Notes

Short-lived steering or known conditions for this run:

-

The orchestrator reloads this file every cycle and records the observed version or content fingerprint in the
run file. Change the version or `Last Updated` value when changing runtime steering during an active run.
