# Lobster Pound Community Runtime Context

Status: **Active**
Context Version: 8
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
| Fallback output root | Session output `output\lobster-pound\`, mirroring the primary root's structure | Used only when the primary root fails the run-start persistence test |
| Digest naming | `digests\<YYYY-MM-DD>.md` | Reusable meeting-date views |
| Occurrence naming | `occurrences\<YYYY-MM-DD>.md` | Uncapped structured evidence record |
| Commitment register | `commitments.md` | Owner-attributed follow-up tasks across occurrences |
| Report naming | `reports\<window-start>_to_<window-end>.md` using ISO dates | Period report |
| Run naming | `runs\<run-id>.md` | Run state and decisions |
| Event log naming | `runs\<run-id>.events.jsonl` | Append-only execution events |
| Coverage disclosure | `Primary knowledge corpus processing complete; optional enrichment coverage: <status>.` | Report and run file |

Create the output root and required child directories when absent. Do not write generated community-insights
content into this repository.

## DONE WHEN Parameters

| Parameter | Runtime value | Goal Card check using it |
|---|---:|---|
| Source timezone | `America/New_York` | Coverage, freshness, meeting-date condensation, and source-window boundaries |
| Source window | `2026-08-07T00:00:00-04:00` inclusive through `2026-09-06T00:00:00-04:00` exclusive | Coverage and recurrence |
| Primary meeting occurrences | All occurrences represented in the knowledge folder within the source window | Coverage |
| Meeting-date digest narrative limit | 20,000 characters | Condensation |
| Digest omission disclosure | Included count, omitted count, material omitted categories, and occurrence-record link | Condensation |
| Reinspection overlap | Trailing seven days | Continuity |
| Optional linked-document budget | 50 documents across the run | Stop-caps |
| Optional-source status | Optional; absence or incomplete retrieval does not block primary analytical completion | Coverage and structure |
| Target slices | One primary failed check or stage exit condition per cycle; record every other legitimately affected check | Convergence |
| Conditional child fan-out | Use 2–3 children only when the target slice has separable evidence partitions or complementary checks | Child-agent execution |
| Maximum child execution | 3 children per cycle and 12 total launches across the run; delegation depth 1; one transient-failure retry per child | Bounded execution |
| Cycle budget posture | Retain the 10-cycle Goal Card cap; preflight must show a credible convergence path within it | Bounded execution |

## QUALITY Priorities

1. Preserve traceability from every reported claim and theme change to the original source.
2. Preserve disagreement, minority signals, and uncertainty during meeting-date evidence condensation.
3. Distinguish repeated mentions from independent momentum.

All Goal Card quality rules remain in force.

## CONTEXT Sources

| Source | Locator | Scope or time window | Access mode | Required for this run |
|---|---|---|---|---|
| Meeting transcripts and summaries | `C:\Users\bspender\OneDrive - Microsoft\AMA\knowledge` | All transcript and AI meeting-summary documents representing occurrences within the frozen source window | Read-only local files | Yes |
| Weekly meeting-series metadata | Meeting series named `MCAPS Lobster Pound | Show & Tell` | Reconcile expected in-window occurrences against available primary documents | Read-only | Attempt required |
| Meeting-occurrence conversation | `https://teams.microsoft.com/l/message/19:vGhTXeZ7TqvSIz4Kz_dxn_c-ZKikC1ZobNY7h-jcK5o1@thread.tacv2/1781726708875?tenantId=72f988bf-86f1-41af-91ab-2d7cd011db47&groupId=ae25e647-d5e2-45e6-bbd8-8bb8c59d74f5&parentMessageId=1781726708875&teamName=MCAPS%20Lobster%20Pound%20Community&channelName=Lobster%20Pound` | Optional in-window meeting conversation and occurrence context | Read-only | No |
| Lobster Pound community channel | `https://teams.microsoft.com/l/channel/19%3AvGhTXeZ7TqvSIz4Kz_dxn_c-ZKikC1ZobNY7h-jcK5o1%40thread.tacv2/Lobster%20Pound?groupId=ae25e647-d5e2-45e6-bbd8-8bb8c59d74f5&tenantId=72f988bf-86f1-41af-91ab-2d7cd011db47` | Optional in-window community context and gap repair | Read-only | No |
| Community SharePoint documents | `https://microsoft.sharepoint.com/:f:/r/teams/MCAPSLobsterPound/Shared%20Documents/Forms/AllItems.aspx?id=%2Fteams%2FMCAPSLobsterPound%2FShared%20Documents%2FLobster%20Pound&p=true&share=cgpubhse%2D%5FKRS79VMByp3BgvEgUC6CyLWewVUs2xcMwj%2D3YqHQ` | Optional body inspection within the linked-document budget | Read-only | No |

### Evidence processing rules

- Inventory every `.docx` file directly under the knowledge root, record its SHA-256 fingerprint, and select in-window documents by meeting-occurrence date.
- Pair transcripts and summaries by occurrence date. Record missing, ambiguous, duplicate, or unreadable primary documents as blocking coverage gaps; do not rewrite source files.
- Attempt the meeting-series metadata lookup before declaring occurrence coverage complete. Reconcile every discovered in-window occurrence against the knowledge-folder pairs. If access fails, record the attempt and qualify occurrence coverage as corpus-only rather than upstream-complete.
- Inspect the body of every selected primary document and keep transcript evidence distinguishable from meeting-summary evidence.
- Record the extraction method for every primary document. For timecoded transcripts, record the first and last timecodes plus every observed gap greater than five minutes; otherwise record that timecodes are unavailable. When a transcript has such a gap, qualify absence-shaped claims for that occurrence and open a coverage gap.
- Produce one uncapped occurrence record per in-window meeting date before drafting its digest. Use short Markdown sections and tables, not a new data format.
- Give each material evidence item in an occurrence record a stable ID and record its type, short paraphrase or minimal excerpt, speaker when material, source ID, timecode when available, themes, and whether it appears in the digest.
- Each occurrence record also captures disagreements, commitments, and details omitted from the digest. It must not copy full source bodies.
- Produce one capped digest per in-window meeting date as a view over its occurrence record. State material-record counts included and omitted, name materially omitted categories, and link to the occurrence record.
- Add every explicit owner-attributed follow-up task from inspected meeting summaries to `commitments.md`. Keep the status open unless later inspected evidence supports another status.
- Use meeting-series metadata only to verify series and occurrence context; it does not substitute for a primary document.
- Assign optional chat or channel records by their own timestamps after applying `America/New_York`.
- De-duplicate optional records by stable source identity when available, and record retrieval time and scope.
- Classify optional records with no surfaced author or body as `body_unavailable` unless the source explicitly identifies them as system, reaction, join, or deleted records. Never infer the record type from missing fields alone.
- Record optional-record counts by classification in the run source manifest and coverage disclosure.
- Give every authorized optional source an explicit disposition: attempted with result, or not attempted with reason. Silence is not a valid disposition.
- Classify an image-only optional record as `visual_content_unavailable`, distinct from `body_unavailable`.
- Treat unavailable or incomplete optional evidence as unknown, never as zero activity.

### Runtime variables

| Name | Value | Used by |
|---|---|---|
| `source_timezone` | `America/New_York` | Window boundaries, timestamps, and meeting-date digest dates |
| `source_window_start` | `2026-08-07T00:00:00-04:00` | Source selection |
| `source_window_end` | `2026-09-06T00:00:00-04:00` | Source selection |
| `knowledge_root` | `C:\Users\bspender\OneDrive - Microsoft\AMA\knowledge` | Primary transcript and meeting-summary discovery |
| `meeting_series_name` | `MCAPS Lobster Pound | Show & Tell` | Required lookup attempt for occurrence and identity verification |
| `meeting_series_root_id` | `1781726708875` | Meeting-conversation classification |
| `conditional_children_per_slice` | `2-3` | Use only for real parallel evidence partitions or complementary checks |
| `max_children_per_cycle` | `3` | Child-agent execution bound |
| `max_child_launches_per_run` | `12` | Every initial launch, retry, and interruption re-dispatch counts |
| `max_delegation_depth` | `1` | Prevent child agents from spawning descendants |

## CONSTRAINTS Additions

- Treat all approved source locations as read-only.
- Do not write to the knowledge folder, Teams, or SharePoint.
- Do not read other OneDrive folders merely because they share a parent with an approved path.
- Do not persist Teams content, meeting artifacts, or generated insights in the repository.
- Apply `America/New_York` before assigning evidence to a calendar day or evaluating source-window boundaries.
- Do not rewrite or silently repair primary documents or optional-source records; record gaps and conflicts in run state.
- After reading one representative required `.docx`, update and reread the actual run file before broad analysis. Do not create a disposable probe file or require delete support.
- Keep authoritative artifact and run-file writes with the parent agent; child agents inspect bounded partitions and return results for deterministic integration.

## STAGES Steering

| Goal Card stage | Runtime focus | Inputs or configuration |
|---|---|---|
| Inventory evidence | Verify output writes, inventory and fingerprint the knowledge corpus, and pair in-window primary documents by occurrence | Knowledge root and exact source window |
| Condense and reconcile | Build occurrence records, capped digests, and the commitment register from primary transcripts and summaries, adding optional context only when inspected | Evidence processing rules, output paths, and narrative limit |
| Verify and repair | Recheck source checkpoints, citations, duplicates, contradictions, and overflow gaps | Seven-day overlap and original source IDs |
| Persist understanding | Write only to the configured output root | Output preferences |

## STOP-CAPS Overrides

No tighter runtime overrides. Inherit all Goal Card stop-caps.

## Runtime Notes

- Existing verified digests may be reused when their primary and optional source checkpoints remain unchanged.
- When the knowledge corpus changes, reinspect new or changed documents plus the trailing seven days.
- Meeting metadata, meeting chat, community chat, and SharePoint retrieval are optional enrichment and do not block primary analytical completion.
- Analytical completion means complete processing of the in-window primary knowledge corpus, not exhaustive Microsoft 365 acquisition.
- Use two or three child agents only when a slice safely decomposes; otherwise use one or none and record why.
- Preserve the 10-cycle cap as design pressure. Each slice has one primary target but may advance multiple affected checks when the evidence supports it.
- Content and run-state artifacts remain Markdown at either root; the event sidecar remains JSONL. If the primary root rejects either declared format, use the fallback rather than converting to `.docx` or another format.
- Fallback output does not provide cross-run continuity with the primary root. Record that limitation as a gap; do not add automatic promotion or synchronization in this pilot.
