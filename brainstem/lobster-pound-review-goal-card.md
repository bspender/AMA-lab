## Goal Card

### OBJECTIVE

Produce a trustworthy 30-day understanding of the **MCAPS Lobster Pound Community** for the user: what happened, what recurred or changed, and what can be learned—while preserving week-to-week theme evolution and evidence provenance.

### OUTPUT

Maintain under `C:\Users\bspender\OneDrive - Microsoft\AMA\brainstem\insights\lobster-pound\`:

- `theme-ledger.md` — themes, states, evidence IDs, changes, contradictions, gaps
- `themes\<theme-id>.md` — evolving theme records and relationships
- `glossary.md` and `taxonomy.md`
- `open-questions.md`
- `runs\<run-id>.md` — source manifest, checks, gaps, backlog, cycle decisions
- `digests\<YYYY-MM-DD>.md` — reusable daily conversation digest, capped at 2,000 narrative characters, with source IDs and a source checkpoint.
- `reports\<period>.md` — final synthesis; prior reports remain immutable

Persist source IDs, timestamps, and links—not copied source bodies.

### DONE WHEN

All checks pass:

1. **Coverage:** The four most recent meeting occurrences within the frozen 30-day window (or all occurrences if fewer than four) have their accessible transcripts inspected. Every scoped item is covered by either a newly generated digest of channel messages, replies, and meeting-chat messages or a previously verified digest whose source checkpoint remains unchanged. Inaccessible required sources produce an incomplete handback, not success.
2. **Condensation:** Every conversation item is classified in the source manifest as material evidence, duplicate, or no material signal. Each active day has a digest with evidence IDs; overflow is logged as a gap.
3. **Evidence:** Every factual claim, latest update, and theme-state change cites an inspected source body using source ID/link and timestamp.
4. **Recurrence:** A “recurring” theme has non-duplicate evidence from at least two distinct weeks and two independent source items.
5. **Freshness:** The source snapshot is at most 24 hours old. “Current” claims have evidence from the final seven days.
6. **Latest update:** Each theme’s latest timestamp equals the newest inspected, non-duplicate evidence associated with that theme.
7. **Duplicates:** Zero unresolved duplicate candidates; duplicate echoes do not count as independent momentum.
8. **Contradictions:** Zero unresolved blocking contradictions. Non-blocking disagreement is explicitly represented.
9. **Evolution:** Every theme change records prior state, new state, effective week, evidence IDs, and rationale.
10. **Gaps:** Every recorded gap has an attempted remedy and result.
11. **Privacy:** Zero private-chat, other-channel, attachment, or unapproved-source content appears in persisted artifacts.
12. **Continuity:** Reuse existing daily digests. Reinspect new or changed items plus the trailing seven days for late replies, edits, or newly available evidence. Update only affected digests and record each change. The run reconciles changes against the prior ledger and immutable prior report.
13. **Structure:** The report answers all three objective questions and the run file records every check as pass/fail with evidence.

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
- Daily digests do not replace original-source citations.
- Meeting chat alone cannot establish recurrence, consensus, or momentum.
- Material disagreement or minority signals must not be silently dropped.

### CONTEXT

Read only:

- The approved **Lobster Pound** Teams channel, including replies, for the 30-day snapshot window
- All recurring community meeting occurrences whose scheduled start falls within the frozen 30-day window, including each transcript and in-window meeting chat
- Up to 50 approved linked documents across the full run
- Existing state and prior reports under `C:\Users\bspender\OneDrive - Microsoft\AMA\brainstem\insights\lobster-pound\`

### CONSTRAINTS

- Write only beneath `C:\Users\bspender\OneDrive - Microsoft\AMA\brainstem\insights\lobster-pound\`.
- Never access private chats, other channels, attachments, or unapproved links.
- Never publish, message, react, edit source content, delete, or change permissions.
- Never independently declare information official, confidential, or consensus.
- Escalate ambiguous attribution, sensitive judgments, access expansion, and theme merges/redefinitions with multiple defensible interpretations.
- Each cycle records one line: `Decision: <continue|complete|stop> — <check result or state change that justifies it>.`
- The 2000-character limit excludes source IDs, links, and timestamps.

### STAGES

1. **Inventory evidence:** Freeze the 30-day window, retrieve required sources, and build the source manifest.
2. **Condense and reconcile:** Create bounded daily digests, then reconcile evidence by week into the evolving ledger.
3. **Verify and repair:** Check coverage, provenance, recurrence, freshness, contradictions, privacy, gaps, and continuity; repair failures.
4. **Persist understanding:** Update permitted state files and write the period report only when every completion check passes.

**Progress measures:** passed checks, missing required sources, unsupported claims, unresolved duplicates, blocking contradictions, unattempted gaps, and themes with fully traceable state changes.

### STOP-CAPS

- Maximum **10 cycles**.
- Stop after **3 consecutive cycles with no material change** in checks, gaps, blockers, or artifact state.
- Maximum **50 optional linked documents across the entire run**; required scoped messages and transcripts are not rationed.
- Stop early with an incomplete handback for inaccessible required sources, unclear privacy or permissions, unresolved blocking contradictions, unsafe persistence, or exhausted limits.
- Failed checks never become success merely because the work reached a fixed point.
