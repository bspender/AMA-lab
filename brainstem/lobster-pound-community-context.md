# Lobster Pound Community Runtime Context

Status: **Active**
Context Version: 1
Applies To Goal: `lobster-pound-review-goal-card.md`
Last Updated: 2026-08-30

This file supplies approved source locators and runtime values for the Lobster Pound community-insights run. The
Goal Card remains authoritative for acceptance, quality, stages, and stop-caps.

## OBJECTIVE Steering

- Current run focus: Broad discovery across the frozen 30-day window.
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

Create the output root and required child directories when absent. Do not write generated community-insights
content into this repository.

## DONE WHEN Parameters

| Parameter | Runtime value | Goal Card check using it |
|---|---:|---|
| Source timezone | `America/New_York` | Coverage, freshness, daily condensation, and source-window boundaries |
| Source window | Trailing 30 calendar days at run start | Coverage and recurrence |
| Meeting occurrence limit | Four most recent occurrences in the source window | Coverage |
| Daily digest narrative limit | 2,000 characters | Condensation |
| Reinspection overlap | Trailing seven days | Continuity |
| Optional linked-document budget | 50 documents across the run | Stop-caps |

## QUALITY Priorities

1. Preserve traceability from every reported claim and theme change to the original source.
2. Preserve disagreement, minority signals, and uncertainty during daily evidence condensation.
3. Distinguish repeated mentions from independent momentum.

All Goal Card quality rules remain in force.

## CONTEXT Sources

| Source | Locator | Scope or time window | Access mode | Required for this run |
|---|---|---|---|---|
| Lobster Pound Teams channel | `https://teams.microsoft.com/l/channel/19%3AvGhTXeZ7TqvSIz4Kz_dxn_c-ZKikC1ZobNY7h-jcK5o1%40thread.tacv2/Lobster%20Pound?groupId=ae25e647-d5e2-45e6-bbd8-8bb8c59d74f5&tenantId=72f988bf-86f1-41af-91ab-2d7cd011db47` | All in-window channel messages and replies | Read-only | Yes |
| Recurring meeting chat | `https://teams.microsoft.com/l/message/19:vGhTXeZ7TqvSIz4Kz_dxn_c-ZKikC1ZobNY7h-jcK5o1@thread.tacv2/1781726708875?tenantId=72f988bf-86f1-41af-91ab-2d7cd011db47&groupId=ae25e647-d5e2-45e6-bbd8-8bb8c59d74f5&parentMessageId=1781726708875&teamName=MCAPS%20Lobster%20Pound%20Community&channelName=Lobster%20Pound` | In-window meeting-chat messages for the selected occurrences | Read-only | Yes |
| Local meeting knowledge | `C:\Users\bspender\OneDrive - Microsoft\AMA\lobster-pound\knowledge\` | Summary and transcript for each of the four most recent in-window occurrences | Read-only local files | Yes |
| Community SharePoint Documents | `https://microsoft.sharepoint.com/:f:/r/teams/MCAPSLobsterPound/Shared%20Documents/Forms/AllItems.aspx?id=%2Fteams%2FMCAPSLobsterPound%2FShared%20Documents%2FLobster%20Pound&p=true&share=cgpubhse%2D%5FKRS79VMByp3BgvEgUC6CyLWewVUs2xcMwj%2D3YqHQ` | Approved relevant documents within the linked-document budget | Read-only | No |

### Local meeting-artifact discovery

- Match files by a leading `YYYY-MM-DD` date stamp.
- Select the four most recent distinct meeting dates within the frozen 30-day window, or all dates when fewer
  than four exist.
- Require one `*Meeting Summary.docx` and one `*Meeting Transcript.docx` for each selected date.
- Treat a missing or unreadable required artifact as an inaccessible required source.
- Use the filename date as the meeting occurrence date; do not substitute the file modified timestamp.

### Runtime variables

| Name | Value | Used by |
|---|---|---|
| `source_timezone` | `America/New_York` | Window boundaries, timestamps, and daily digest dates |
| `lookback_days` | `30` | Source selection |
| `max_meeting_occurrences` | `4` | Local meeting-artifact discovery |
| `meeting_filename_date_format` | `YYYY-MM-DD` | Local meeting-artifact discovery |

## CONSTRAINTS Additions

- Treat all approved source locations as read-only.
- Do not write to Teams, SharePoint, or the local meeting-knowledge directory.
- Do not read other OneDrive folders merely because they share a parent with an approved path.
- Do not persist Teams content, meeting artifacts, or generated insights in the repository.
- Apply `America/New_York` before assigning evidence to a calendar day or evaluating source-window boundaries.

## STAGES Steering

| Goal Card stage | Runtime focus | Inputs or configuration |
|---|---|---|
| Inventory evidence | Freeze the window and discover the required meeting pairs | Approved source table and local filename rules |
| Condense and reconcile | Discover broadly while using seed themes only as non-exhaustive aids | Daily digest path and narrative limit |
| Verify and repair | Recheck source checkpoints, citations, duplicates, contradictions, and overflow gaps | Seven-day overlap and original source IDs |
| Persist understanding | Write only to the configured output root | Output preferences |

## STOP-CAPS Overrides

No tighter runtime overrides. Inherit all Goal Card stop-caps.

## Runtime Notes

- Existing verified daily digests may be reused when their source checkpoints remain unchanged.
- Reinspect the trailing seven days for late replies, edits, newly available evidence, or changed source sets.
- Meeting summaries and transcripts are local files because those artifacts are not available through the
  approved Teams or SharePoint sources.
