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

## Repository files

| File | What you learn from it |
|---|---|
| [`goal-designer-prompt.md`](goal-designer-prompt.md) | How to challenge vague requests and produce a structured Goal Card |
| [`lab-intent.md`](lab-intent.md) | The student learning goals, class flow, and teaching guardrails |
| [`brainstem/loop-orchestrator.md`](brainstem/loop-orchestrator.md) | How a run selects work, checks progress, records state, and stops |
| [`brainstem/templates/use-case-run.baseline.md`](brainstem/templates/use-case-run.baseline.md) | What the run records so you can inspect and resume it |
| [`brainstem/templates/use-case-context.baseline.md`](brainstem/templates/use-case-context.baseline.md) | How to provide settings that may change from one run to another |
| [`brainstem/lobster-pound-review-goal-card.md`](brainstem/lobster-pound-review-goal-card.md) | A worked Goal Card for a 30-day community review |
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
and tighter limits. It may narrow the Goal Card. It may not weaken the Goal
Card's finish line.

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
- approved access to the meeting documents in the configured knowledge folder;
- optional access to the named Teams and SharePoint locations.

The main evidence is the in-window meeting transcripts and AI meeting summaries
under:

```text
C:\Users\bspender\OneDrive - Microsoft\AMA\knowledge
```

Meeting details, meeting chat, community chat, and SharePoint documents are
optional supporting sources. The repository does not contain this content.

The example reviews August 7 through September 5, 2026. September 6 is not
included. Each primary `.docx` file must be directly under the knowledge folder,
not in a child folder.

### Step 1: Study the worked files

Read:

- `brainstem\lobster-pound-review-goal-card.md`;
- `brainstem\lobster-pound-community-context.md`.

Before changing anything, find:

1. the source window;
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

The agent creates or resumes a run. It continues until:

- every `DONE WHEN` check passes;
- a stop limit applies; or
- the environment interrupts the run.

Send `START` once. Do not prompt the agent again between cycles unless it reports
an interruption or asks for a decision required by the Goal Card.

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

The parent agent may use two or three child agents when a target slice has clear,
separate parts. The parent remains the only writer of the official run and task
files.

### Step 8: Inspect the output

The context writes results under:

```text
<OneDrive Root>\AMA\brainstem\insights\lobster-pound\
```

If that root rejects a declared format after a labeled source is opened, the
worked context allows the same Markdown artifacts and JSONL event sidecar under
`output\lobster-pound\` in the Cowork session. The run file records which root
was used and why. Fallback files are not automatically copied back to the
primary root.

Start with the run file in `runs\`. Inspect:

1. **Loop Preflight** — Was the goal safe, checkable, and possible within the
   cycle limit?
2. **Work Event Log** — Are cycle starts, validation failures, retries, and
   cycle endings backed by sequential events in the `.events.jsonl` sidecar?
3. **DONE WHEN Results** — Which checks passed or failed, and what evidence was
   recorded?
4. **Slice and Cycle History** — Why was each repair chosen, and what changed?
5. **Backlog Decision History** — Why did remaining work move up or down?
6. **Child Activity Log** — Which work was delegated and accepted?
7. **Stop Reason and final cycle decision** — Why did the run complete or stop?
8. **Persisted Progress Line** — What was the final cycle, stage, check count,
   stall count, and status?

Open the matching `.events.jsonl` file and confirm that sequence numbers are
continuous and its events match the Markdown cycle summaries.

Inspect the files that the run created. A completed run should include the final
report plus occurrence records, digests, commitments, the theme ledger, theme
files, glossary, taxonomy, and open questions named by the Goal Card. A stopped
or interrupted run may contain only part of that set. Do not treat a missing
final report as a separate error when the run did not complete.

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
7. Why did the run complete, stop, or get interrupted?

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

Child agents are optional. The agent should use them only when a target slice
can be divided into separate, useful parts.

### A source cannot be read

Required source failures block successful completion. Optional source failures
should be recorded as gaps without being treated as proof that nothing happened.

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
