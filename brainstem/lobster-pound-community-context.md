# Lobster Pound Community Runtime Context

Status: **Active**
Context Version: 9
Applies To Goal: `lobster-pound-review-goal-card.md`
Last Updated: 2026-09-07

This file supplies approved source locators and runtime values for the Lobster Pound community-insights run. The
Goal Card remains authoritative for acceptance, quality, stages, and stop-caps.

## OBJECTIVE Steering

- Current run focus: Repeatable-pilot analysis using Graph meeting transcripts and local Copilot meeting summaries as primary evidence, with local transcripts as fallback.
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
| Continuity search roots | Primary output root, then the fallback output root when readable | Prior theme ledger, commitments, and glossary only |
| Coverage disclosure | `Primary meeting evidence processing complete; optional enrichment coverage: <status>.` | Report and run file |

Create the output root and required child directories when absent. Do not write generated community-insights
content into this repository.

## DONE WHEN Parameters

| Parameter | Runtime value | Goal Card check using it |
|---|---:|---|
| Source timezone | `America/New_York` | Coverage, freshness, meeting-date condensation, and source-window boundaries |
| Source window | `2026-08-07T00:00:00-04:00` inclusive through `2026-09-06T00:00:00-04:00` exclusive | Coverage and recurrence |
| Primary meeting occurrences | All reconciled series occurrences within the source window | Coverage |
| Meeting-date digest narrative limit | 20,000 characters | Condensation |
| Digest omission disclosure | Included count, omitted count, material omitted categories, and occurrence-record link | Condensation |
| Reinspection overlap | Trailing seven days | Continuity |
| Optional linked-document budget | 50 documents across the run | Stop-caps |
| Optional-source status | Optional; absence or incomplete retrieval does not block primary analytical completion | Coverage and structure |
| Transcript source preference | Graph first; local `.docx` only after a recorded Graph failure | Coverage and integrity |
| Summary capture fail marker | Literal `Expand all` after extraction | Coverage and integrity |
| Summary length warning | Less than 50% of the in-window summary median | Coverage and integrity |
| Target slices | One primary failed check or stage exit condition per cycle; record every other legitimately affected check | Convergence |
| Occurrence extraction fan-out | Use 2–3 children to cover all occurrence partitions with one shared extraction contract; parent integrates only | Child-agent execution |
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
| Meeting transcripts (preferred) | Microsoft Graph meeting transcripts for `MCAPS Lobster Pound | Show & Tell`, reached through the retrieval chain below | All reconciled occurrences within the frozen source window | Read-only Graph retrieval | Yes |
| Meeting transcripts (fallback) and Copilot meeting summaries | `C:\Users\bspender\OneDrive - Microsoft\AMA\knowledge` | Local summaries for every occurrence; local transcripts only when Graph retrieval fails | Read-only local files | Summaries yes; transcripts conditional |
| Weekly meeting-series metadata | Meeting series named `MCAPS Lobster Pound | Show & Tell` | Reconcile in-window occurrences and locate Graph transcripts | Read-only calendar lookup | Yes |
| Meeting-occurrence conversation | `https://teams.microsoft.com/l/message/19:vGhTXeZ7TqvSIz4Kz_dxn_c-ZKikC1ZobNY7h-jcK5o1@thread.tacv2/1781726708875?tenantId=72f988bf-86f1-41af-91ab-2d7cd011db47&groupId=ae25e647-d5e2-45e6-bbd8-8bb8c59d74f5&parentMessageId=1781726708875&teamName=MCAPS%20Lobster%20Pound%20Community&channelName=Lobster%20Pound` | Optional in-window meeting conversation and occurrence context | Read-only | No |
| Lobster Pound community channel | `https://teams.microsoft.com/l/channel/19%3AvGhTXeZ7TqvSIz4Kz_dxn_c-ZKikC1ZobNY7h-jcK5o1%40thread.tacv2/Lobster%20Pound?groupId=ae25e647-d5e2-45e6-bbd8-8bb8c59d74f5&tenantId=72f988bf-86f1-41af-91ab-2d7cd011db47` | Optional in-window community context and gap repair | Read-only | No |
| Community SharePoint documents | `https://microsoft.sharepoint.com/:f:/r/teams/MCAPSLobsterPound/Shared%20Documents/Forms/AllItems.aspx?id=%2Fteams%2FMCAPSLobsterPound%2FShared%20Documents%2FLobster%20Pound&p=true&share=cgpubhse%2D%5FKRS79VMByp3BgvEgUC6CyLWewVUs2xcMwj%2D3YqHQ` | Optional body inspection within the linked-document budget | Read-only | No |

### Evidence processing rules

- Inventory every `.docx` file directly under the knowledge root, record its SHA-256 fingerprint, and select in-window local summaries and transcript fallbacks by meeting-occurrence date.
- Reconcile the calendar series before declaring occurrence coverage complete. Record the lookup result as a sidecar event because it determines the required occurrence set.
- Retrieve the Graph transcript for every reconciled occurrence before selecting a transcript source. Fingerprint the retrieved VTT body, not its URL.
- Prefer the Graph transcript. Use a local transcript only after a verified Graph lookup failure has been logged as `source_lookup_failed` and the local fallback has been read, fingerprinted, and logged as `fallback_selected`.
- When Graph and local transcripts both exist, record both word counts and the local-to-Graph ratio. Keep the local copy classified as a rejected fallback rather than mixing both bodies as independent evidence.
- Pair the chosen transcript and local Copilot summary by occurrence date. Record missing, ambiguous, duplicate, or unreadable required sources as blocking coverage gaps; do not rewrite source files.
- During inventory, the parent computes the word count of every in-window summary and the in-window median, then includes that fixed median and warning floor in every child extraction packet.
- Apply the summary capture-quality check before removing copied Teams UI text. Literal `Expand all` means the notes were copied while collapsed: log `capture_quality_failed`, classify the summary as degraded, and disclose the limitation. `Collapse all` is the expected expanded marker. A summary below 50% of the parent-supplied in-window median word count receives the same warning unless inspected structure shows it is genuinely short.
- A degraded summary does not stop preflight. Continue with the available transcript, preserve any usable summary evidence, and qualify claims that would depend on missing summary detail.
- After capture-quality checks, remove `Meeting notes`, `Expand all`, `Collapse all`, and `Are these notes useful?` from analyzed text because they describe the capture UI rather than the meeting.
- Record the retrieval or extraction method for every primary source. For VTT transcripts, calculate uncovered gaps from one cue's end to the next cue's start; never treat the distance between cue start times as a gap. Record first and last cue times and uncovered gaps greater than five minutes. Qualify absence-shaped claims when real transcript gaps exist.
- Produce one uncapped occurrence record per in-window meeting date before drafting its digest. Use short Markdown sections and tables, not a new data format.
- Give each material evidence item in an occurrence record a stable ID and record its type, short paraphrase or minimal excerpt, speaker when material, source ID, timecode when available, themes, and whether it appears in the digest.
- Each occurrence record also captures disagreements, commitments, and details omitted from the digest. It must not copy full source bodies.
- Produce one capped digest per in-window meeting date as a view over its occurrence record. State material-record counts included and omitted, name materially omitted categories, and link to the occurrence record.
- Add every explicit owner-attributed follow-up task from inspected meeting summaries to `commitments.md`. Keep the status open unless later inspected evidence supports another status.
- Use meeting-series metadata to identify occurrences and locate Graph transcripts; it does not substitute for transcript or summary content.
- Assign optional chat or channel records by their own timestamps after applying `America/New_York`.
- De-duplicate optional records by stable source identity when available, and record retrieval time and scope.
- Classify optional records with no surfaced author or body as `body_unavailable` unless the source explicitly identifies them as system, reaction, join, or deleted records. Never infer the record type from missing fields alone.
- Record optional-record counts by classification in the run source manifest and coverage disclosure.
- Give every authorized optional source an explicit disposition: attempted with result, or not attempted with reason. Silence is not a valid disposition.
- Classify an image-only optional record as `visual_content_unavailable`, distinct from `body_unavailable`.
- Treat unavailable or incomplete optional evidence as unknown, never as zero activity.

### Transcript retrieval

Resolve each occurrence transcript with this chain:

1. Call `outlook_calendar-ListCalendarView` with `start`, `end`, `subject="Lobster Pound"`, and
   `time_zone="America/New_York"`. Do not pass a restrictive `select` value because it can suppress
   `onlineMeeting.joinUrl`.
2. Take `onlineMeeting.joinUrl` from the matching event.
3. Call `graph-ListMeetingTranscripts(join_url=<joinUrl>)`. A recurring series can share one join URL, so filter
   transcripts by `createdDateTime` on the target occurrence date in `America/New_York`; never assume list order.
   If more than one candidate remains, prefer a transcript interval that overlaps the calendar occurrence. If
   candidates still tie, retrieve them and choose the VTT with the largest word count. Record every rejected
   same-day candidate and the selection reason.
4. Call `graph-GetMeetingTranscript(join_url=<joinUrl>, transcript_id=<selected-id>)` and retrieve the chosen VTT
   body.

Record `createdDateTime`, `endDateTime`, `callId`, `contentCorrelationId`, and `transcriptContentUrl` when returned,
plus the VTT body fingerprint. If any required call fails or returns no matching transcript, log the failed
operation and observed result before selecting the local transcript fallback.

Do not attempt Graph recordings or Graph AI insights in this run. SharePoint `Recordings` and `MeetingOrg` contain
video only and are outside scope. The approved Copilot summaries remain the local `.docx` files.

### Cross-run continuity

Before extracting new occurrence evidence:

1. After the run-start persistence test resolves the writable output root, search the primary output root and the
   readable fallback output root for the latest valid prior run.
2. Select one coherent prior state set; do not merge conflicting roots. Prefer the newest completed run, then the
   newest safely interrupted run with readable state files.
3. Read and fingerprint only `theme-ledger.md`, `commitments.md`, and `glossary.md`. Record the selected prior run,
   paths, fingerprints, and any rejected candidate in the new run file.
4. Copy the selected state into the current resolved output root before changing it. Preserve stable theme,
   commitment, and glossary IDs.
5. Add new evidence or explicit status history; never replace prior meaning or close a commitment from silence,
   age, or disappearance.
6. Disclose that theme detail files, taxonomy, open questions, digests, and reports are not copied between roots.
   Never claim those artifacts have cross-root continuity from the three carried state files.

If no prior state is readable, record `Prior Run: none` and start a new baseline. This is a visible continuity gap,
not a reason to stop the current evidence review. The Cowork fallback is best-effort continuity within a session; do
not claim it remains readable from a later Cowork session.

### Consistent occurrence extraction

Use one shared extraction packet and result shape for every occurrence. Each packet contains the chosen transcript,
local summary, source fingerprints, the parent-computed in-window summary median and warning floor,
capture-quality result, optional evidence assigned to that date, and the same evidence fields and quality rules.

When more than one occurrence is in scope, partition every occurrence across two or three child agents. A child may
handle more than one date so the run remains within the child limits. The parent must not author one occurrence
while children author others; it validates and integrates all returned occurrence records in date order. If child
execution is unavailable, the parent may process all occurrences only after recording that exception and must still
apply the identical extraction packet and validation rules to every date.

### Runtime variables

| Name | Value | Used by |
|---|---|---|
| `source_timezone` | `America/New_York` | Window boundaries, timestamps, and meeting-date digest dates |
| `source_window_start` | `2026-08-07T00:00:00-04:00` | Source selection |
| `source_window_end` | `2026-09-06T00:00:00-04:00` | Source selection |
| `knowledge_root` | `C:\Users\bspender\OneDrive - Microsoft\AMA\knowledge` | Required local summary and fallback transcript discovery |
| `transcript_source_preference` | `graph_first` | Transcript source selection |
| `meeting_subject_filter` | `Lobster Pound` | Calendar lookup |
| `meeting_series_name` | `MCAPS Lobster Pound | Show & Tell` | Required occurrence and transcript lookup |
| `summary_capture_fail_marker` | `Expand all` | Collapsed-summary detection |
| `summary_words_median_warning_floor` | `0.50` | Thin-summary warning |
| `meeting_series_root_id` | `1781726708875` | Meeting-conversation classification |
| `occurrence_extraction_children` | `2-3` | Cover all occurrence partitions with one shared contract |
| `max_children_per_cycle` | `3` | Child-agent execution bound |
| `max_child_launches_per_run` | `12` | Every initial launch, retry, and interruption re-dispatch counts |
| `max_delegation_depth` | `1` | Prevent child agents from spawning descendants |

## CONSTRAINTS Additions

- Treat all approved source locations as read-only.
- Do not write to the knowledge folder, Teams, or SharePoint.
- Do not read other OneDrive folders merely because they share a parent with an approved path.
- Do not persist Teams content, meeting artifacts, or generated insights in the repository.
- Do not access Graph recordings, Graph AI insights, or SharePoint recording folders.
- Apply `America/New_York` before assigning evidence to a calendar day or evaluating source-window boundaries.
- Do not rewrite or silently repair primary documents or optional-source records; record gaps and conflicts in run state.
- After reading one representative required `.docx`, update and reread the actual run file before broad analysis. Do not create a disposable probe file or require delete support.
- Keep authoritative artifact and run-file writes with the parent agent; child agents inspect bounded partitions and return results for deterministic integration.
- Log required-source failures and quality-gate failures before selecting a fallback or continuing with degraded evidence.

## STAGES Steering

| Goal Card stage | Runtime focus | Inputs or configuration |
|---|---|---|
| Inventory evidence | Verify output writes, reconcile occurrences, retrieve and fingerprint Graph transcripts, validate local summaries and fallbacks, and resolve prior continuity state | Transcript retrieval, knowledge root, continuity roots, and exact source window |
| Condense and reconcile | Apply the shared extraction packet through bounded children, then build occurrence records, capped digests, and the commitment register | Evidence processing rules, consistent extraction, output paths, and narrative limit |
| Verify and repair | Recheck source checkpoints, citations, duplicates, contradictions, and overflow gaps | Seven-day overlap and original source IDs |
| Persist understanding | Write only to the configured output root | Output preferences |

## STOP-CAPS Overrides

No tighter runtime overrides. Inherit all Goal Card stop-caps.

## Runtime Notes

- Existing verified digests may be reused when their Graph transcript, local summary, fallback, and optional source checkpoints remain unchanged.
- When a primary source or continuity artifact changes, reinspect affected occurrences plus the trailing seven days.
- Meeting metadata, meeting chat, community chat, and SharePoint retrieval are optional enrichment and do not block primary analytical completion.
- Analytical completion means complete processing of reconciled Graph transcripts and local Copilot summaries, not exhaustive Microsoft 365 acquisition.
- Use two or three child agents to cover every occurrence extraction partition with the same contract. Keep all authoritative writes and integration with the parent.
- Preserve the 10-cycle cap as design pressure. Each slice has one primary target but may advance multiple affected checks when the evidence supports it.
- Content and run-state artifacts remain Markdown at either root; the event sidecar remains JSONL. If the primary root rejects either declared format, use the fallback rather than converting to `.docx` or another format.
- At run start, inspect both approved output roots when readable for prior theme, commitment, and glossary state. Carry one selected valid state set into the current resolved root; do not synchronize entire output trees. A session-local fallback provides only best-effort continuity and may be unavailable to a later Cowork session.
