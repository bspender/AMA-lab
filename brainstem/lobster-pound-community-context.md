# Lobster Pound Community Runtime Context

Status: **Active**
Context Version: 2
Applies To Goal: `lobster-pound-review-goal-card.md`
Last Updated: 2026-09-06

This file supplies approved source locators and runtime values for the Lobster Pound community-insights run. The
Goal Card remains authoritative for acceptance, quality, stages, and stop-caps.

## OBJECTIVE Steering

- Current run focus: Repeatable-pilot analysis using the staged source snapshot as the primary evidence input.
- Priority outcomes: Identify what happened, what recurred or changed, and what can be learned from the community.
- Intended audience or consumer: The user.
- Seed themes: Second brain, Obsidian, Skill Shack, Scout's future, and announcements.
- Seed handling: Treat seed themes as non-exhaustive discovery aids, not required findings or privileged conclusions.
- Deprioritized work: Personal assessments, exhaustive attachment review, and conclusions outside the approved sources.

## OUTPUT Preferences

| Setting | Value | Goal Card allowance |
|---|---|---|
| Output root | `C:\Users\bspender\OneDrive - Microsoft\AMA\brainstem\insights\lobster-pound\` | All Goal Card artifacts |
| Digest naming | `digests\<YYYY-MM-DD>.md` | Reusable daily conversation digests |
| Report naming | `reports\<window-start>_to_<window-end>.md` using ISO dates | Period report |
| Run naming | `runs\<run-id>.md` | Run state and decisions |
| Acquisition disclosure | `Snapshot processing complete; upstream acquisition incomplete.` | Report and run file |

Create the output root and required child directories when absent. Do not write generated community-insights
content into this repository.

## DONE WHEN Parameters

| Parameter | Runtime value | Goal Card check using it |
|---|---:|---|
| Source timezone | `America/New_York` | Coverage, freshness, daily condensation, and source-window boundaries |
| Source window | `2026-08-07T00:00:00-04:00` inclusive through `2026-09-06T00:00:00-04:00` exclusive | Coverage and recurrence |
| Meeting occurrence limit | Four most recent occurrences in the source window | Coverage |
| Daily digest narrative limit | 2,000 characters | Condensation |
| Reinspection overlap | Trailing seven days | Continuity |
| Optional linked-document budget | 50 documents across the run | Stop-caps |
| Snapshot status | `INCOMPLETE` upstream acquisition; complete processing required for accepted records | Coverage and structure |

## QUALITY Priorities

1. Preserve traceability from every reported claim and theme change to the original source.
2. Preserve disagreement, minority signals, and uncertainty during daily evidence condensation.
3. Distinguish repeated mentions from independent momentum.

All Goal Card quality rules remain in force.

## CONTEXT Sources

| Source | Locator | Scope or time window | Access mode | Required for this run |
|---|---|---|---|---|
| Snapshot dataset map | `C:\Users\bspender\OneDrive - Microsoft\AMA\lobster-pound\source-gathers\dataset-map.json` | Dataset contract, source families, fixed baseline, identifiers, hashes, gaps, and conflicts | Read-only local file | Yes |
| Snapshot manifest | `C:\Users\bspender\OneDrive - Microsoft\AMA\lobster-pound\source-gathers\manifest.md` | Counts, fingerprints, acquisition status, and known omissions | Read-only local file | Yes |
| Captured channel evidence | `C:\Users\bspender\OneDrive - Microsoft\AMA\lobster-pound\source-gathers\evidence\channel-messages.jsonl` | In-window channel roots, ordinary replies, and available meeting-conversation replies | Read-only local file | Yes |
| Captured meeting transcripts | `C:\Users\bspender\OneDrive - Microsoft\AMA\lobster-pound\source-gathers\evidence\meeting-transcripts.jsonl` and `transcripts\` | Transcript provenance plus highest-fidelity VTT bodies | Read-only local files | Yes |
| Captured local meeting artifacts | `C:\Users\bspender\OneDrive - Microsoft\AMA\lobster-pound\source-gathers\evidence\local-meeting-artifacts.jsonl` and `local-meetings\` | Summary/transcript provenance plus extracted text | Read-only local files | Yes |
| Snapshot conflicts | `C:\Users\bspender\OneDrive - Microsoft\AMA\lobster-pound\source-gathers\evidence\cowork-conflicts.jsonl` and `evidence\scout-conflicts.jsonl` | Quarantined same-identity disagreements | Read-only local files | Yes |
| Live Lobster Pound Teams channel | `https://teams.microsoft.com/l/channel/19%3AvGhTXeZ7TqvSIz4Kz_dxn_c-ZKikC1ZobNY7h-jcK5o1%40thread.tacv2/Lobster%20Pound?groupId=ae25e647-d5e2-45e6-bbd8-8bb8c59d74f5&tenantId=72f988bf-86f1-41af-91ab-2d7cd011db47` | Optional delta discovery or gap repair | Read-only | No |
| Live recurring meeting conversation | `https://teams.microsoft.com/l/message/19:vGhTXeZ7TqvSIz4Kz_dxn_c-ZKikC1ZobNY7h-jcK5o1@thread.tacv2/1781726708875?tenantId=72f988bf-86f1-41af-91ab-2d7cd011db47&groupId=ae25e647-d5e2-45e6-bbd8-8bb8c59d74f5&parentMessageId=1781726708875&teamName=MCAPS%20Lobster%20Pound%20Community&channelName=Lobster%20Pound` | Optional delta discovery; known incomplete enumeration path | Read-only | No |
| Community SharePoint Documents | `https://microsoft.sharepoint.com/:f:/r/teams/MCAPSLobsterPound/Shared%20Documents/Forms/AllItems.aspx?id=%2Fteams%2FMCAPSLobsterPound%2FShared%20Documents%2FLobster%20Pound&p=true&share=cgpubhse%2D%5FKRS79VMByp3BgvEgUC6CyLWewVUs2xcMwj%2D3YqHQ` | Optional body inspection within the linked-document budget | Read-only | No |

### Snapshot processing rules

- Validate the dataset map, manifest, required file presence, record counts, and declared SHA-256 fingerprints before analysis.
- Filter records into the exact source window above using `createdDateTime`.
- De-duplicate by `sourceType + containerId + sourceId`; do not rewrite primary JSONL.
- Assign every conversation record to its own `createdDateTime` calendar day in `America/New_York`.
- Identify available meeting-conversation records by their relationship to meeting-series root `1781726708875`.
- Produce one daily digest that combines channel roots, ordinary replies, and available meeting-conversation replies for that day.
- Keep transcript and meeting-summary evidence distinguishable within the combined daily digest.
- Quarantine the conflicted SharePoint identity unless the accepted snapshot records explicit adjudication.
- Treat missing meeting-conversation records as unknown, never as zero activity.

### Runtime variables

| Name | Value | Used by |
|---|---|---|
| `source_timezone` | `America/New_York` | Window boundaries, timestamps, and daily digest dates |
| `source_window_start` | `2026-08-07T00:00:00-04:00` | Source selection |
| `source_window_end` | `2026-09-06T00:00:00-04:00` | Source selection |
| `max_meeting_occurrences` | `4` | Local meeting-artifact discovery |
| `source_gather_root` | `C:\Users\bspender\OneDrive - Microsoft\AMA\lobster-pound\source-gathers\` | Snapshot validation and evidence loading |
| `meeting_series_root_id` | `1781726708875` | Meeting-conversation classification |

## CONSTRAINTS Additions

- Treat all approved source locations as read-only.
- Do not write to Teams, SharePoint, or the staged source-gather directory.
- Do not read other OneDrive folders merely because they share a parent with an approved path.
- Do not persist Teams content, meeting artifacts, or generated insights in the repository.
- Apply `America/New_York` before assigning evidence to a calendar day or evaluating source-window boundaries.
- Do not rewrite or silently repair primary JSONL records; record gaps and conflicts in run state.
- Verify Markdown create/read/delete capability in the output root before beginning analysis.

## STAGES Steering

| Goal Card stage | Runtime focus | Inputs or configuration |
|---|---|---|
| Inventory evidence | Verify output writes and validate the accepted snapshot | Dataset map, manifest, hashes, and exact source window |
| Condense and reconcile | Combine all captured conversation streams by calendar day while discovering broadly | Snapshot processing rules, daily digest path, and narrative limit |
| Verify and repair | Recheck source checkpoints, citations, duplicates, contradictions, and overflow gaps | Seven-day overlap and original source IDs |
| Persist understanding | Write only to the configured output root | Output preferences |

## STOP-CAPS Overrides

No tighter runtime overrides. Inherit all Goal Card stop-caps.

## Runtime Notes

- Existing verified daily digests may be reused when their source checkpoints remain unchanged.
- When the accepted snapshot changes, reinspect new or changed records plus the trailing seven days.
- Live retrieval is optional enrichment and does not block completion of the repeatable pilot.
- Analytical completion means complete processing of the accepted snapshot, not exhaustive Microsoft 365 acquisition.
