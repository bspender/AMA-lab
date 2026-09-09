# AMA Loop Engineering Lab

This lab teaches you how to design and inspect an AI work loop with clear
limits.

You will learn how to:

1. turn a vague task into a clear goal;
2. define what passing means before work begins;
3. let an agent repair one important gap at a time;
4. watch progress while the agent works;
5. inspect why the run completed or stopped.

All instructions and run state use Markdown files. You do not need to build a
workflow engine.

## The main idea

An AI answer can look complete without being trustworthy. A loop adds a clear
finish line and a way to repair failed checks.

```text
Design the goal -> Start the run -> Check the work -> Repair a gap -> Check again
```

More cycles do not automatically mean more learning. Each cycle should make a
visible change that helps the work pass.

The worked example also separates **new evidence** from **repair work**:

- a new weekly run advances the fixed fiscal-year window;
- cycles inside that run repair gaps without moving the window.

## Repository files

| File | What you learn from it |
|---|---|
| [`goal-designer-prompt.md`](goal-designer-prompt.md) | How to challenge vague requests and produce a structured Goal Card |
| [`lab-intent.md`](lab-intent.md) | The student learning goals, class flow, and teaching guardrails |
| [`brainstem/loop-orchestrator.md`](brainstem/loop-orchestrator.md) | How a run selects work, checks progress, records state, and stops |
| [`brainstem/templates/use-case-run.baseline.md`](brainstem/templates/use-case-run.baseline.md) | What the run records so you can inspect and resume it |
| [`brainstem/templates/use-case-context.baseline.md`](brainstem/templates/use-case-context.baseline.md) | How to provide settings that may change from one run to another |
| [`brainstem/lobster-pound-review-goal-card.md`](brainstem/lobster-pound-review-goal-card.md) | A worked Goal Card for incremental fiscal-year community review |
| [`brainstem/lobster-pound-community-context.md`](brainstem/lobster-pound-community-context.md) | The approved paths, dates, sources, and limits for the worked example |

## How the files work together

```text
Goal Designer
    |
    v
Goal Card ---------> Runtime context
    |                     |
    +----------+----------+
               |
               v
        Loop Orchestrator
               |
               v
      Run file + task files
```

### Goal Card

The Goal Card says what success means. It has eight sections:

1. `OBJECTIVE`
2. `OUTPUT`
3. `DONE WHEN`
4. `QUALITY`
5. `CONTEXT`
6. `CONSTRAINTS`
7. `STAGES`
8. `STOP-CAPS`

### Runtime context

The context file supplies values for one run, such as paths, dates, source names,
source requirement groups, and tighter limits. The Goal Card defines how
required, degraded, fallback, and optional evidence are handled. The context
defines which approved sources have those roles for this run. The complete
classification is frozen before Cycle 1, so a later edit cannot turn a failing
required source into an optional one.

### Loop orchestrator

The orchestrator controls the run:

```text
Assess -> Act -> Verify -> Persist and Decide
```

Each cycle chooses one **target slice**: a small repair aimed at one main failed
check or stage goal. The same repair may also improve other checks.

### Run file

The run file records what happened. It contains the current checks, target slice,
backlog, child-agent activity, cycle history, progress, and stop decision.

Chat history is not the official record. Another agent should be able to resume
from the files.

## Part 1: Design a Goal Card

You can complete this part without access to the Lobster Pound sources.

### Step 1: Open the Goal Designer

Open `goal-designer-prompt.md` and use its full contents as the instruction in an
AI assistant.

### Step 2: Describe a recurring task

Start with a real task or a simple example:

```text
Review our weekly project updates and make a good summary.
```

The Goal Designer should challenge words such as "good," "complete," or
"insightful." It should ask what visible evidence would prove that the result is
ready.

### Step 3: Answer the short interview

The Goal Designer asks up to three questions at a time. Give exact answers when
you can:

- name the audience;
- name the output file or result;
- name required and optional sources;
- explain what usually goes wrong;
- set read, write, approval, and stop limits.

If you do not know a threshold, ask the designer to label a starting value as a
`Pilot assumption`.

### Step 4: Review the result

The final response should contain:

1. a verdict on whether the task should use a loop;
2. the most important wording improvements;
3. a Goal Card with all eight sections;
4. one example of a failed check, repair, and recheck;
5. what the first run should teach you.

The prompt returns the Goal Card in chat. Save it as a Markdown file if you want
to run it.

## Part 2: Run the Lobster Pound example

This part uses files outside the repository. You need:

- Copilot Cowork or another agent that can read and write local files;
- approved access to Microsoft Graph meeting transcripts for the named meeting series;
- approved access to the Copilot meeting summaries in the configured knowledge folder;
- optional access to the named Teams and SharePoint locations.

The preferred transcript evidence comes from Microsoft Graph. The required
Copilot meeting summaries and fallback transcript copies are under:

```text
C:\Users\bspender\OneDrive - Microsoft\AMA\knowledge
```

The run retrieves Graph transcripts first and uses a local transcript only after
recording that Graph retrieval failed. Meeting chat, community chat, and
SharePoint documents are optional supporting sources. Graph recordings, Graph AI
insights, and SharePoint recording folders are outside this example.

The runtime context defines the fiscal-year start, first Friday boundary, weekly
increment, and demo catch-up boundary. The example creates one separate
cumulative run for each configured Friday boundary. Each local `.docx` summary
or fallback transcript must be directly under the knowledge folder, not in a
child folder.

Each weekly run checks every expected occurrence and source checkpoint in its
cumulative window. It reuses verified unchanged occurrence records and digests,
extracts only new or changed weeks, and then rebaselines themes, commitments,
glossary terms, taxonomy, and open questions.

### Step 1: Study the worked files

Read:

- `brainstem\lobster-pound-review-goal-card.md`;
- `brainstem\lobster-pound-community-context.md`.

Before changing anything, find:

1. the fiscal-year start, first weekly boundary, and catch-up boundary;
2. required and optional sources;
3. the output location;
4. the 16 finish-line checks;
5. the cycle and stall limits.

### Step 2: Update the local paths

The worked files use paths for the current example owner. If you are running the
lab elsewhere, replace those paths before you start.

Replace every occurrence of the example owner's output and knowledge paths in
both worked files. Also update optional source links if they differ in your
environment.

Search both files again after editing to confirm that no old local path remains.

Do not point the output root at the source folder.

### Step 3: Copy the runtime files

Create:

```text
<OneDrive Root>\AMA\brainstem\templates\
```

These files are required to run the worked example:

| Repository file | Destination |
|---|---|
| `brainstem\loop-orchestrator.md` | `<OneDrive Root>\AMA\brainstem\loop-orchestrator.md` |
| `brainstem\lobster-pound-review-goal-card.md` | `<OneDrive Root>\AMA\brainstem\lobster-pound-review-goal-card.md` |
| `brainstem\lobster-pound-community-context.md` | `<OneDrive Root>\AMA\brainstem\lobster-pound-community-context.md` |
| `brainstem\templates\use-case-run.baseline.md` | `<OneDrive Root>\AMA\brainstem\templates\use-case-run.baseline.md` |

This file is a reference for designing a different runtime context. The worked
example does not need it:

| Repository file | Optional destination |
|---|---|
| `brainstem\templates\use-case-context.baseline.md` | `<OneDrive Root>\AMA\brainstem\templates\use-case-context.baseline.md` |

`<OneDrive Root>` is usually similar to:

```text
C:\Users\<user>\OneDrive - Microsoft
```

### Step 4: Open the working folder

Start Copilot Cowork with this folder:

```text
<OneDrive Root>\AMA\brainstem\
```

### Step 5: Load the instructions

Send:

```text
Read @lobster-pound-review-goal-card.md and @lobster-pound-community-context.md to be orchestrated by @loop-orchestrator.md and then wait for more instructions.
```

This loads the files. It does not start the run.

### Step 6: Start the loop

Send:

```text
START goal=lobster-pound-review-goal-card.md context=lobster-pound-community-context.md
```

The agent creates or resumes one fixed-window weekly run. It continues until:

- every `DONE WHEN` check passes;
- a stop limit applies; or
- the environment interrupts the run.

Before creating a new run, the agent confirms that its Friday boundary has
passed and every non-cancelled meeting inside it has completed. If not, it
reports the next eligible boundary without creating a run or consuming that
weekly position.

Send `START` once for that weekly run. Do not prompt the agent again between
cycles unless it reports an interruption or asks for a decision required by the
Goal Card.

When the run completes, send the same `START` instruction again to create the
next cumulative weekly run. The first run uses the fiscal-year start and first
Friday boundary from the runtime context. The next run keeps that evidence and
advances the boundary by the configured weekly increment. Continue until the
configured catch-up boundary is complete. If the final boundary is already
complete, the agent reports that the demo is caught up instead of rebuilding it.

```text
Run 1: <fiscal-year-start> -> <first-Friday-boundary> exclusive
Run 2: <fiscal-year-start> -> <first-Friday-boundary + weekly increment> exclusive
Run 3: <fiscal-year-start> -> <first-Friday-boundary + two weekly increments> exclusive
...
Final run: <fiscal-year-start> -> <catch-up-boundary> exclusive
```

A run's end date never changes between cycles. A later week belongs to a new
run.

### Step 7: Watch the run

Cowork should show short milestone messages followed by:

```text
[USE-CASE LOOP] run=<run-id> | cycle=<n>/<max> | stage=<goal-stage> | checks=<passed>/<total> | stall=<n>/<cap> | status=<IN_PROGRESS|COMPLETE|STOPPED>
```

You may see the same line more than once. Repeated lines show that the process is
still alive. They do not prove that the work improved. Use the run file's check
results, cycle changes, and recorded repair results to judge progress.

The example keeps a 10-cycle limit. Each cycle should choose one main repair
without turning the first cycle into one large pass.

For occurrence extraction, the worked context normally uses one child for the
new weekly occurrence. If several occurrences are new or changed, it uses two or
three children to cover them with the same extraction contract. The parent
validates and integrates every result and remains the only writer of the
official run and task files.

### Step 8: Inspect the output

The context writes results under:

```text
<OneDrive Root>\AMA\brainstem\insights\lobster-pound\
```

If that root rejects a declared format after a labeled source is opened, the
worked context allows the same Markdown artifacts and JSONL event sidecar under
`output\lobster-pound\` in the Cowork session. The run file records which root
was used and why. At the next run, the agent checks both approved roots when
they are readable and carries forward the expected prior fiscal-year state plus
verified occurrence records and digests. It does not synchronize unrelated
files. The Cowork fallback provides only best-effort continuity within a
session; a later session may not be able to reopen it.

Start with the run file in `runs\`. Inspect:

1. **Loop Preflight** — Was the goal safe, checkable, and possible within the
   cycle limit?
2. **Work Event Log** — Are cycle starts, required-source lookups, source
   checkpoints, artifact reuse, tool failures, fallbacks, validation results,
   and cycle endings backed by sequential events in the `.events.jsonl`
   sidecar?
3. **DONE WHEN Results** — Which checks passed or failed, and what evidence was
   recorded?
4. **Source Checkpoints and Reuse Plan** — Which weeks were new, changed, or
   safely reused?
5. **Slice and Cycle History** — Why was each repair chosen, and what changed?
6. **Backlog Decision History** — Why did remaining work move up or down?
7. **Child Activity Log** — Which work was delegated and accepted?
8. **Stop Reason and final cycle decision** — Why did the run complete or stop?
9. **Persisted Progress Line** — What was the final cycle, stage, check count,
   stall count, and status?

Open the matching `.events.jsonl` file and confirm that sequence numbers are
continuous and its events match the Markdown cycle summaries.

Inspect the files that the run created. A completed run should include the final
report plus occurrence records, digests, commitments, the theme ledger, theme
files, glossary, taxonomy, and open questions named by the Goal Card. A stopped
run should include a clearly labelled, non-authoritative `.INCOMPLETE.md`
synthesis with its available findings, evidence limits, failed checks, and next
action. An interrupted run may contain only part of that set.

### Step 9: Read status without doing work

To read the only active run, send:

```text
STATUS
```

To name a run file, replace the example path with the real path and send:

```text
STATUS run=C:\path\to\runs\20260907-090000-lobster-pound.md
```

Do not type square brackets or placeholder text. `START` and `STATUS` are normal
instructions, not slash commands.

### Step 10: Resume an interrupted run

If the environment interrupts the run, use the exact `START` instruction shown
in the interruption response. The agent reloads the run file and continues the
unfinished target slice.

If the Goal Card changed after the run began, the orchestrator stops instead of
mixing two different finish lines.

## Part 3: Explain what the loop learned

Use the run file to answer:

1. What was the first failed check?
2. Why did the agent choose its first target slice?
3. What visible state changed?
4. Which other checks improved from the same work?
5. Why was the next backlog item chosen?
6. Did child agents divide real work, or only create more activity?
7. Which earlier weeks were reused instead of re-extracted, and what proved they
   were unchanged?
8. Why did the run complete, stop, or get interrupted?

If you cannot answer these questions from the run file, the run did not make its
learning path clear enough.

## Common problems

### The run says `don't loop this`

One of the starting checks failed. Read the evidence in **Loop Preflight**. Make
the finish line, repair path, boundaries, or cycle plan clearer before trying
again.

### The run stops before completion

A stopped run is not automatically a failure. Check the stop reason, failed
checks, and smallest next action. An honest incomplete result is better than an
unsupported success.

### No child agents appear

Child agents are optional for general Goal Cards. The Lobster Pound context
uses one child for one new or changed occurrence, or two or three children for
multiple changed partitions. If no occurrence needs extraction, no child is
needed. If Cowork cannot launch a required child, the run records the exception
and applies the same extraction packet itself.

### A later week appears during a run

The active run keeps the source window it recorded before Cycle 1. It logs the
new boundary as deferred input and leaves it for the next run. Expanding the
window inside a cycle would move the finish line.

### The next weekly boundary is not ready

The agent checks the proposed boundary before creating a run. A future boundary
or a meeting still in progress is reported as not yet eligible. The weekly
position remains available for a later `START`.

### A source cannot be read

Required source failures block successful completion. Optional source failures
should be recorded as gaps without being treated as proof that nothing happened.
For transcripts, a Graph failure selects the approved local fallback only after
the failure and fallback are recorded in the event sidecar.

A present but degraded required source does not disappear from the analysis. The
run records the quality problem, limits claims that depend on missing detail,
and continues with the other available evidence.

### The output path cannot be written

The Goal Card reads one representative required source, then updates and rereads
the actual run file before broad analysis. This catches write restrictions that
appear only after labeled content is opened. The worked context then tries its
Markdown fallback root. The run stops only if that fallback is absent or also
fails.

## What counts as progress

Progress is a recorded change such as:

- a failed check passing;
- fewer missing sources;
- fewer unsupported claims;
- a required file appearing;
- a conflict or gap being resolved.

More words, tool calls, child agents, or cycles are not progress by themselves.

## Scope

This repository is an educational lab. It is not a scheduler, Teams connector,
SharePoint connector, or production workflow engine.

Its purpose is to make the goal, evidence, repairs, progress, and stop decision
easy to inspect and improve.
