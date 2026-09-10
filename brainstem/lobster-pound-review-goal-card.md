## Goal Card

### OBJECTIVE

Build a trustworthy, meeting-centered understanding of the **MCAPS Lobster Pound Community** fiscal year to date, one fixed cumulative scheduled run at a time: what happened, what recurred or changed, and what can be learned—using every source the runtime context classifies as required primary evidence while preserving week-to-week theme evolution, evidence provenance, and optional-source limitations.

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
- `reports\<period>.<run-id>.INCOMPLETE.md` — immutable, clearly labelled, non-authoritative synthesis when a run stops before all checks pass

Primary output root: `C:\Users\bspender\OneDrive - Microsoft\AMA\brainstem\insights\lobster-pound\`.

When the runtime context declares a fallback output root and the primary root fails the run-start persistence test
for an environmental reason, write the identical artifact set and directory structure to the fallback root using
the declared formats: Markdown content and run-state files plus the JSONL event sidecar. Do not convert artifacts
to `.docx` or another format to obtain write access.

Persist source IDs, timestamps, and links—not copied source bodies.

### DONE WHEN

All checks pass:

1. **Coverage:** The run records one fixed cumulative fiscal-year window and one frozen source classification, and never changes either between cycles. Every meeting occurrence in that window has at least one required primary evidence requirement. Every such requirement defined by the runtime context is reconciled and has a current source checkpoint. A missing preferred source satisfies its requirement only when an approved fallback in the same requirement group is inspected and the fallback is logged. New or changed required evidence is inspected; unchanged occurrence artifacts are reused only after their source checkpoints and saved artifacts are verified. An unsatisfied required evidence requirement, unreadable required source, or fingerprint mismatch produces an incomplete handback, not success. A present but degraded required source opens a visible coverage gap but does not block analysis of other available evidence. Every optional source has an explicit disposition; missing optional evidence is a non-blocking gap and never evidence of no activity.
2. **Condensation:** Every source classified as required primary evidence is represented in the source manifest as material evidence, duplicate, fallback, degraded capture, unchanged, changed, or no material signal and assigned to exactly one meeting-occurrence date. Each meeting date in the cumulative window has an uncapped occurrence record and one capped digest combining its required primary evidence plus any inspected optional evidence relevant to that occurrence. A new or changed week is extracted and integrated; a verified unchanged week is not re-extracted. The digest states how many material records it includes and omits, identifies materially omitted categories, and links to the occurrence record.
3. **Evidence:** Every factual claim, latest update, and theme-state change cites an inspected source body using source ID/link and timestamp.
4. **Recurrence:** A “recurring” theme has non-duplicate evidence from at least two distinct weeks and two independent source items.
5. **Freshness:** The report states the fixed cumulative fiscal-year window, review timestamp, newest primary occurrence, and optional-source retrieval times when applicable. No claim is described as “current” unless the supporting source was verified within 24 hours of run time; otherwise findings are qualified by their evidence boundary.
6. **Latest update:** Each theme’s latest timestamp equals the newest inspected, non-duplicate evidence associated with that theme.
7. **Duplicates:** Zero unresolved duplicate candidates; duplicate echoes do not count as independent momentum.
8. **Contradictions:** Zero unresolved blocking contradictions. Non-blocking disagreement is explicitly represented.
9. **Evolution:** Every theme change records prior state, new state, effective week, evidence IDs, and rationale.
10. **Gaps:** Every recorded gap has an attempted remedy and result.
11. **Privacy:** Zero private-chat, other-channel, attachment, or unapproved-source content appears in persisted artifacts.
12. **Integrity:** Every required primary source is readable, fingerprinted, uniquely inventoried, assigned to its meeting occurrence, and records its retrieval or extraction method. Preferred and fallback sources follow the order frozen from the runtime context. When transcript cue end times are available, gaps use cue-end-to-next-start coverage rather than differences between cue starts. When cue end times are unavailable, gap measurement is recorded as unavailable and absence-shaped claims are qualified; start-time differences must not be reported as gaps. Every source with a runtime capture-quality rule records its result before capture metadata is removed. Ambiguous dates, duplicate candidates, and conflicting versions remain quarantined until resolved.
13. **Continuity:** After resolving the writable output root and before changing state, resolve the latest valid prior scheduled fiscal-year run from the approved continuity search roots. Record its cumulative window, run ID, artifact paths, and fingerprints. Carry forward the theme ledger, theme detail files, commitments, glossary, taxonomy, and open questions, preserving stable IDs and unresolved state. Verify prior occurrence records and digests against current source checkpoints; reuse unchanged artifacts in place or copy them when roots differ, and reprocess only new or changed occurrences. Reconcile changed evidence chronologically from its occurrence forward. Never infer commitment completion or overwrite prior meaning without cited new evidence. Prior reports remain immutable. A session-local fallback is best-effort continuity only and must not be described as durable across Cowork sessions.
14. **Structure:** Every terminal run writes a readable synthesis. A completed run uses `reports\<period>.md`; a stopped run uses `reports\<period>.<run-id>.INCOMPLETE.md`, labels it incomplete and non-authoritative, and states the stop reason, failed checks, available findings, evidence limits, and smallest next action. The synthesis answers the objective questions to the extent supported, labels required-primary coverage separately from optional enrichment coverage, gives every optional source an explicit attempted/not-attempted disposition with result or reason, records every check as pass/fail with evidence, and names the resolved output root plus the primary-root failure reason when fallback was used.
15. **Commitments:** Every explicit owner-attributed follow-up task found in inspected required primary evidence is recorded once in `commitments.md` with a stable ID, owner, raised date, source ID, related theme when known, and status. A commitment is marked done, superseded, or lapsed only with cited evidence; otherwise it remains open.
16. **Live logging:** The event sidecar contains verified, sequential `run_initialized`, `cycle_started`, validation, and `cycle_ended` events written during execution. Required-source lookup results, source checkpoint comparisons, reused artifacts, lookup failures, tool failures that change the plan, required-source fallbacks, and failed capture-quality checks are recorded when they occur and before any fallback or repair. Every completed cycle and every validation failure or pass produces a matching sidecar event, and the Markdown cycle summary is derived from those events. Missing, reordered, or reconstructed events fail this check.

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
- Follow the preferred, fallback, required, and optional source classifications frozen from the runtime context.
- A missing required source produces an incomplete handback. A present but degraded required source is disclosed and
  usable within its stated limits. A missing optional source is a non-blocking gap with an explicit disposition.
- Material disagreement or minority signals must not be silently dropped.
- Occurrence records preserve material attribution and specifics even when the digest omits them.
- Digest omissions must be visible and addressable; a digest never replaces its occurrence record.
- Do not infer that a commitment is complete from silence or age.
- Treat each scheduled run as a cumulative fiscal-year rebaseline. Preserve earlier evidence and explain how the new
  or changed interval affected themes, commitments, glossary terms, taxonomy, and open questions.
- State “Primary meeting evidence processing complete; optional enrichment coverage: <status>” in the report and run file.
- Never interpret a missing source record as evidence that no activity occurred.

### CONTEXT

Read only:

- The complete source allowlist in the runtime context's `CONTEXT Sources` table, frozen before Cycle 1. Each row must
  be classified as required primary evidence, conditional fallback, optional evidence, occurrence metadata, or
  continuity state.
- No source omitted from that frozen table, even when it is reachable through an approved service or parent folder.

### CONSTRAINTS

- Write only beneath the resolved output root: the primary root, or the fallback root declared by the runtime context when the primary root is unwritable. No other location.
- Never access private chats, other channels, attachments, or unapproved links.
- Never publish, message, react, edit source content, delete, or change permissions.
- Never independently declare information official, confidential, or consensus.
- Escalate ambiguous attribution, sensitive judgments, access expansion, and theme merges/redefinitions with multiple defensible interpretations.
- Each cycle records one line: `Decision: <continue|complete|stop> — <check result or state change that justifies it>.`
- The 20,000-character limit excludes source IDs, links, timestamps, headings, and Markdown table scaffolding.
- Treat the knowledge corpus and optional sources as read-only: do not rewrite, normalize, reorder, or silently repair source evidence.
- When reading a required source may apply a sensitivity label or another write restriction, before broad analysis read one representative required source, append and verify a sidecar event, then update and reread the actual run file. Stop with an `unsafe persistence` incomplete handback only if both the primary root and any declared fallback root fail.
- Keep the `.events.jsonl` sidecar in the same resolved `runs\` folder as its Markdown run file. Never rewrite prior event lines.
- Freeze every runtime source row, role, requirement classification, locator, and scope before Cycle 1. A context
  reload may not change a required source to optional, introduce a new source, or otherwise change the evidence
  needed to pass the active run.
- Freeze the cumulative source-window start and end before Cycle 1. A cycle must not add another interval or move
  the finish line; only a new run may advance to the next configured boundary.

### STAGES

1. **Inventory evidence:** Resolve and freeze the next cumulative fiscal-year window and source classification, perform the run-start persistence test, resolve the prior scheduled run, reconcile every expected occurrence and required source in the cumulative window, and compare current source checkpoints with prior state.
2. **Condense and reconcile:** Apply one consistent extraction contract to every new or changed occurrence, reuse verified unchanged occurrence records and digests, and integrate evidence chronologically into the carried fiscal-year state.
3. **Verify and repair:** Check coverage, provenance, recurrence, freshness, contradictions, privacy, gaps, and continuity; repair failures.
4. **Persist understanding:** Update permitted state files. Write the completed period report when every check passes, or write the clearly labelled `.INCOMPLETE.md` synthesis before a stopped handback.

**Progress measures:** passed checks, cumulative weeks covered, new/changed/reused occurrences, missing or degraded required sources, preferred-source retrievals and fallbacks, unsupported claims, unrecorded commitments, carried-forward state, missing live events, unresolved duplicates, blocking contradictions, unattempted gaps, and themes with fully traceable state changes.

### STOP-CAPS

- Maximum **10 cycles**.
- Stop after **3 consecutive cycles with no material change** in checks, gaps, blockers, or artifact state.
- Maximum **50 optional linked documents across the entire run**; sources classified as required are not rationed.
- Stop early with an incomplete handback for inaccessible required sources, unclear privacy or permissions, unresolved blocking contradictions, unsafe persistence, or exhausted limits.
- Failed checks never become success merely because the work reached a fixed point.
