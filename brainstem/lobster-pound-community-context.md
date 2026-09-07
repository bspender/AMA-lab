# Lobster Pound Community Runtime Context

Status: **Active**
Context Version: 3
Applies To Goal: `lobster-pound-review-goal-card.md`
Last Updated: 2026-09-07

This file supplies approved source locators and runtime values for the Lobster Pound community-insights run. The
Goal Card remains authoritative for acceptance, quality, stages, and stop-caps.

## OBJECTIVE Steering

- Current run focus: Repeatable-pilot analysis using the meeting transcripts and summaries in the approved knowledge folder as primary evidence.
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
| Coverage disclosure | `Primary knowledge corpus processing complete; optional enrichment coverage: <status>.` | Report and run file |

Create the output root and required child directories when absent. Do not write generated community-insights
content into this repository.

## DONE WHEN Parameters

| Parameter | Runtime value | Goal Card check using it |
|---|---:|---|
| Source timezone | `America/New_York` | Coverage, freshness, daily condensation, and source-window boundaries |
| Source window | `2026-08-07T00:00:00-04:00` inclusive through `2026-09-06T00:00:00-04:00` exclusive | Coverage and recurrence |
| Primary meeting occurrences | All occurrences represented in the knowledge folder within the source window | Coverage |
| Daily digest narrative limit | 2,000 characters | Condensation |
| Reinspection overlap | Trailing seven days | Continuity |
| Optional linked-document budget | 50 documents across the run | Stop-caps |
| Optional-source status | Optional; absence or incomplete retrieval does not block primary analytical completion | Coverage and structure |

## QUALITY Priorities

1. Preserve traceability from every reported claim and theme change to the original source.
2. Preserve disagreement, minority signals, and uncertainty during daily evidence condensation.
3. Distinguish repeated mentions from independent momentum.

All Goal Card quality rules remain in force.

## CONTEXT Sources

| Source | Locator | Scope or time window | Access mode | Required for this run |
|---|---|---|---|---|
| Meeting transcripts and summaries | `C:\Users\bspender\OneDrive - Microsoft\AMA\knowledge` | All transcript and AI meeting-summary documents representing occurrences within the frozen source window | Read-only local files | Yes |
| Weekly meeting-series metadata | Meeting series named `MCAPS Lobster Pound | Show & Tell` | Optional series identity, schedule, occurrence, organizer, and meeting-detail verification | Read-only | No |
| Meeting-occurrence conversation | `https://teams.microsoft.com/l/message/19:vGhTXeZ7TqvSIz4Kz_dxn_c-ZKikC1ZobNY7h-jcK5o1@thread.tacv2/1781726708875?tenantId=72f988bf-86f1-41af-91ab-2d7cd011db47&groupId=ae25e647-d5e2-45e6-bbd8-8bb8c59d74f5&parentMessageId=1781726708875&teamName=MCAPS%20Lobster%20Pound%20Community&channelName=Lobster%20Pound` | Optional in-window meeting conversation and occurrence context | Read-only | No |
| Lobster Pound community channel | `https://teams.microsoft.com/l/channel/19%3AvGhTXeZ7TqvSIz4Kz_dxn_c-ZKikC1ZobNY7h-jcK5o1%40thread.tacv2/Lobster%20Pound?groupId=ae25e647-d5e2-45e6-bbd8-8bb8c59d74f5&tenantId=72f988bf-86f1-41af-91ab-2d7cd011db47` | Optional in-window community context and gap repair | Read-only | No |
| Community SharePoint documents | `https://microsoft.sharepoint.com/:f:/r/teams/MCAPSLobsterPound/Shared%20Documents/Forms/AllItems.aspx?id=%2Fteams%2FMCAPSLobsterPound%2FShared%20Documents%2FLobster%20Pound&p=true&share=cgpubhse%2D%5FKRS79VMByp3BgvEgUC6CyLWewVUs2xcMwj%2D3YqHQ` | Optional body inspection within the linked-document budget | Read-only | No |

### Evidence processing rules

- Inventory every `.docx` file directly under the knowledge root, record its SHA-256 fingerprint, and select in-window documents by meeting-occurrence date.
- Pair transcripts and summaries by occurrence date. Record missing, ambiguous, duplicate, or unreadable primary documents as blocking coverage gaps; do not rewrite source files.
- Inspect the body of every selected primary document and keep transcript evidence distinguishable from meeting-summary evidence.
- Produce one digest per in-window meeting-occurrence date, using the primary transcript and summary as its core.
- Use meeting-series metadata only to verify series and occurrence context; it does not substitute for a primary document.
- Assign optional chat or channel records by their own timestamps after applying `America/New_York`.
- De-duplicate optional records by stable source identity when available, and record retrieval time and scope.
- Treat unavailable or incomplete optional evidence as unknown, never as zero activity.

### Runtime variables

| Name | Value | Used by |
|---|---|---|
| `source_timezone` | `America/New_York` | Window boundaries, timestamps, and daily digest dates |
| `source_window_start` | `2026-08-07T00:00:00-04:00` | Source selection |
| `source_window_end` | `2026-09-06T00:00:00-04:00` | Source selection |
| `knowledge_root` | `C:\Users\bspender\OneDrive - Microsoft\AMA\knowledge` | Primary transcript and meeting-summary discovery |
| `meeting_series_name` | `MCAPS Lobster Pound | Show & Tell` | Optional meeting-series lookup and identity verification |
| `meeting_series_root_id` | `1781726708875` | Meeting-conversation classification |

## CONSTRAINTS Additions

- Treat all approved source locations as read-only.
- Do not write to the knowledge folder, Teams, or SharePoint.
- Do not read other OneDrive folders merely because they share a parent with an approved path.
- Do not persist Teams content, meeting artifacts, or generated insights in the repository.
- Apply `America/New_York` before assigning evidence to a calendar day or evaluating source-window boundaries.
- Do not rewrite or silently repair primary documents or optional-source records; record gaps and conflicts in run state.
- Verify Markdown create/read/delete capability in the output root before beginning analysis.

## STAGES Steering

| Goal Card stage | Runtime focus | Inputs or configuration |
|---|---|---|
| Inventory evidence | Verify output writes, inventory and fingerprint the knowledge corpus, and pair in-window primary documents by occurrence | Knowledge root and exact source window |
| Condense and reconcile | Build meeting-date digests from primary transcripts and summaries, adding optional context only when inspected | Evidence processing rules, digest path, and narrative limit |
| Verify and repair | Recheck source checkpoints, citations, duplicates, contradictions, and overflow gaps | Seven-day overlap and original source IDs |
| Persist understanding | Write only to the configured output root | Output preferences |

## STOP-CAPS Overrides

No tighter runtime overrides. Inherit all Goal Card stop-caps.

## Runtime Notes

- Existing verified digests may be reused when their primary and optional source checkpoints remain unchanged.
- When the knowledge corpus changes, reinspect new or changed documents plus the trailing seven days.
- Meeting metadata, meeting chat, community chat, and SharePoint retrieval are optional enrichment and do not block primary analytical completion.
- Analytical completion means complete processing of the in-window primary knowledge corpus, not exhaustive Microsoft 365 acquisition.
