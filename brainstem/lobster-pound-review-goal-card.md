## Goal Card

### OBJECTIVE

Produce a trustworthy, meeting-centered understanding of a frozen 30-day **MCAPS Lobster Pound Community** evidence window for the user: what happened, what recurred or changed, and what can be learned—using meeting transcripts and summaries as primary evidence while preserving week-to-week theme evolution, evidence provenance, and optional-source limitations.

### OUTPUT

Maintain under `C:\Users\bspender\OneDrive - Microsoft\AMA\brainstem\insights\lobster-pound\`:

- `theme-ledger.md` — themes, states, evidence IDs, changes, contradictions, gaps
- `themes\<theme-id>.md` — evolving theme records and relationships
- `glossary.md` and `taxonomy.md`
- `open-questions.md`
- `commitments.md` — owner-attributed follow-up tasks with raised date, source, theme, status, and status evidence
- `runs\<run-id>.md` — source manifest, current checks, gaps, backlog, and cycle summaries
- `runs\<run-id>.events.jsonl` — append-only live event record used to derive cycle history
- `occurrences\<YYYY-MM-DD>.md` — uncapped structured evidence record for the occurrence, including material claims, attribution when needed, source IDs or timecodes, disagreements, commitments, and digest omissions
- `digests\<YYYY-MM-DD>.md` — reusable meeting-date view capped at 20,000 narrative characters, with source IDs, a source checkpoint, and an omission summary linking to the occurrence record
- `reports\<period>.md` — final synthesis; prior reports remain immutable

Primary output root: `C:\Users\bspender\OneDrive - Microsoft\AMA\brainstem\insights\lobster-pound\`.

When the runtime context declares a fallback output root and the primary root fails the run-start persistence test
for an environmental reason, write the identical artifact set and directory structure to the fallback root using
the declared formats: Markdown content and run-state files plus the JSONL event sidecar. Do not convert artifacts
to `.docx` or another format to obtain write access.

Persist source IDs, timestamps, and links—not copied source bodies.

### DONE WHEN

All checks pass:

1. **Coverage:** Every in-window transcript and meeting summary in the approved knowledge folder is inventoried and inspected. Each in-window meeting occurrence has its available transcript and summary paired by occurrence date; a missing counterpart, unreadable document, or fingerprint mismatch produces an incomplete handback, not success. Attempt the approved meeting-series lookup and reconcile discovered in-window occurrences against those pairs. If access fails, record the attempt and describe coverage as corpus-only rather than upstream-complete. Optional-source coverage is measured and reported separately.
2. **Condensation:** Every primary document is classified in the source manifest as material evidence, duplicate, or no material signal and assigned to exactly one meeting-occurrence date. Each active meeting date has an uncapped occurrence record and one capped digest combining its transcript and summary plus any inspected optional evidence relevant to that occurrence. The digest states how many material records it includes and omits, identifies materially omitted categories, and links to the occurrence record.
3. **Evidence:** Every factual claim, latest update, and theme-state change cites an inspected source body using source ID/link and timestamp.
4. **Recurrence:** A “recurring” theme has non-duplicate evidence from at least two distinct weeks and two independent source items.
5. **Freshness:** The report states the frozen source window, review timestamp, newest primary occurrence, and optional-source retrieval times when applicable. No claim is described as “current” unless the supporting source was verified within 24 hours of run time; otherwise findings are qualified by their evidence boundary.
6. **Latest update:** Each theme’s latest timestamp equals the newest inspected, non-duplicate evidence associated with that theme.
7. **Duplicates:** Zero unresolved duplicate candidates; duplicate echoes do not count as independent momentum.
8. **Contradictions:** Zero unresolved blocking contradictions. Non-blocking disagreement is explicitly represented.
9. **Evolution:** Every theme change records prior state, new state, effective week, evidence IDs, and rationale.
10. **Gaps:** Every recorded gap has an attempted remedy and result.
11. **Privacy:** Zero private-chat, other-channel, attachment, or unapproved-source content appears in persisted artifacts.
12. **Integrity:** Every required primary file is readable, fingerprinted, uniquely inventoried, paired by meeting-occurrence date, and records its extraction method. Each timecoded transcript records its first and last timecodes and observed gaps greater than five minutes; transcripts without timecodes record that limitation. Absence-shaped claims are qualified when transcript gaps exist. Ambiguous dates, duplicate candidates, and conflicting versions remain quarantined until resolved.
13. **Continuity:** Reuse existing digests when their primary and optional source checkpoints are unchanged. When the knowledge corpus changes, reinspect new or changed documents plus the trailing seven days, update only affected digests, and record each change. The run reconciles changes against the prior ledger and immutable prior report.
14. **Structure:** The report answers all three objective questions, labels primary analytical coverage separately from optional enrichment coverage, gives every authorized optional source an explicit attempted/not-attempted disposition with result or reason, records every check as pass/fail with evidence, and names the resolved output root plus the primary-root failure reason when fallback was used.
15. **Commitments:** Every explicit owner-attributed follow-up task found in an inspected meeting summary is recorded once in `commitments.md` with a stable ID, owner, raised date, source ID, related theme when known, and status. A commitment is marked done, superseded, or lapsed only with cited evidence; otherwise it remains open.
16. **Live logging:** The event sidecar contains verified, sequential `run_initialized`, `cycle_started`, validation, and `cycle_ended` events written during execution. Every completed cycle and every validation failure or pass produces a matching sidecar event, and the Markdown cycle summary is derived from those events. Missing, reordered, or reconstructed events fail this check.

These thresholds are **pilot assumptions** to recalibrate after the first run.

### QUALITY

- Label claims and themes **Provisional** or **Confirmed**; confirmation requires reading the source body.
- Represent emerging, strengthening, stable, weakening, split, merged, or superseded states—not merely mention counts.
- Separate repeated mentions from independent momentum.
- Do not infer consensus from volume. Consensus or breadth claims require participant-level verification and contrary-evidence review.
- Preserve disagreement and uncertainty rather than flattening them.
- Distinguish inaccessible evidence from evidence of absence.
- Open linked documents before using their claims.
- Use minimal necessary excerpts and avoid unnecessary identity exposure.
- Meeting-date digests do not replace original-source citations.
- Meeting chat alone cannot establish recurrence, consensus, or momentum.
- Material disagreement or minority signals must not be silently dropped.
- Occurrence records preserve material attribution and specifics even when the digest omits them.
- Digest omissions must be visible and addressable; a digest never replaces its occurrence record.
- Do not infer that a commitment is complete from silence or age.
- State “Primary knowledge corpus processing complete; optional enrichment coverage: <status>” in the report and run file.
- Never interpret a missing source record as evidence that no activity occurred.

### CONTEXT

Read only:

- All in-window meeting transcripts and meeting summaries under `C:\Users\bspender\OneDrive - Microsoft\AMA\knowledge`
- Approved metadata or details for the weekly meeting series named **MCAPS Lobster Pound | Show & Tell**; attempt required for occurrence reconciliation
- Optional read-only inspection of the approved **Lobster Pound** Teams channel and meeting-occurrence conversation
- Optional read-only inspection of up to 50 documents from the approved community SharePoint folder across the full run
- Existing state and prior reports under `C:\Users\bspender\OneDrive - Microsoft\AMA\brainstem\insights\lobster-pound\`

### CONSTRAINTS

- Write only beneath the resolved output root: the primary root, or the fallback root declared by the runtime context when the primary root is unwritable. No other location.
- Never access private chats, other channels, attachments, or unapproved links.
- Never publish, message, react, edit source content, delete, or change permissions.
- Never independently declare information official, confidential, or consensus.
- Escalate ambiguous attribution, sensitive judgments, access expansion, and theme merges/redefinitions with multiple defensible interpretations.
- Each cycle records one line: `Decision: <continue|complete|stop> — <check result or state change that justifies it>.`
- The 20,000-character limit excludes source IDs, links, timestamps, headings, and Markdown table scaffolding.
- Treat the knowledge corpus and optional sources as read-only: do not rewrite, normalize, reorder, or silently repair source evidence.
- Because this run reads labeled `.docx` sources, before broad analysis read one representative required source, append and verify a sidecar event, then update and reread the actual run file. Stop with an `unsafe persistence` incomplete handback only if both the primary root and any declared fallback root fail.
- Keep the `.events.jsonl` sidecar in the same resolved `runs\` folder as its Markdown run file. Never rewrite prior event lines.

### STAGES

1. **Inventory evidence:** Freeze the 30-day window, perform the run-start persistence test, validate and fingerprint all in-window primary documents, pair them by meeting occurrence, and build the run source manifest.
2. **Condense and reconcile:** Create uncapped occurrence records, capped meeting-date digests with omission summaries, and the commitment register; then reconcile evidence by week into the evolving ledger.
3. **Verify and repair:** Check coverage, provenance, recurrence, freshness, contradictions, privacy, gaps, and continuity; repair failures.
4. **Persist understanding:** Update permitted state files and write the period report only when every completion check passes.

**Progress measures:** passed checks, missing required sources, unsupported claims, unrecorded commitments, missing live events, unresolved duplicates, blocking contradictions, unattempted gaps, and themes with fully traceable state changes.

### STOP-CAPS

- Maximum **10 cycles**.
- Stop after **3 consecutive cycles with no material change** in checks, gaps, blockers, or artifact state.
- Maximum **50 optional linked documents across the entire run**; required scoped messages and transcripts are not rationed.
- Stop early with an incomplete handback for inaccessible required sources, unclear privacy or permissions, unresolved blocking contradictions, unsafe persistence, or exhausted limits.
- Failed checks never become success merely because the work reached a fixed point.
