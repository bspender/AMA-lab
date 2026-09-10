# Loop Engineering Lab: Learning Intent

## Purpose

This 90-minute lab teaches students how to give an AI agent a clear goal, let it
work through problems, and know when the work is truly done.

The main lesson is simple:

> Repeating a prompt is not the same as learning.

A useful loop checks its work. When a check fails, the agent chooses a small
target slice, makes the bounded change, checks again, and records what happened.

## What students should learn

By the end of the lab, students should be able to:

1. turn a vague request into a clear Goal Card;
2. write finish-line checks that produce a recorded pass or fail result;
3. set clear limits on sources, files, actions, cycles, and cost;
4. explain why a task should use a loop—or why one prompt is enough;
5. distinguish a run, cycle, stage, and target slice;
6. follow how one bounded action changes the work from one cycle to the next;
7. tell the difference between real progress and more activity;
8. inspect the final run history and explain why the agent stopped.

Students do not need to build a workflow engine. They learn by reading and
changing plain Markdown files.

## The operating model

The terms describe different levels of the work:

| Term | What it controls | How progress is measured | What ends it |
|---|---|---|---|
| **Run** | One bounded attempt against a frozen Goal Card, source classification, and acceptance boundary | Fixed `DONE WHEN` pass count plus persisted artifact, source, gap, backlog, and stall measures | `Complete` when every check passes; `Stopped` when preflight or a stop-cap prevents completion. An environmental interruption leaves the run `In Progress` so it can resume |
| **Cycle** | One `Assess -> Act -> Verify -> Persist and Decide` iteration inside the run | The persisted expected-versus-observed delta for one target slice, affected check results, backlog change, and stall change | A verified `cycle_ended` event and a `continue`, `complete`, or `stop` decision. `continue` starts the next cycle without another user prompt |
| **Stage** | A Goal Card-defined phase that says what kind of work is currently in scope | The stage's recorded exit evidence and the applicable `DONE WHEN` checks or artifact state | Its exit conditions pass. A stage may span several cycles, and a cycle is not automatically a stage |
| **Target slice** | The smallest coherent action integrated by one cycle | Its declared measurable delta and verification method | The slice is verified and integrated at cycle end, or an interrupted slice resumes under the same cycle number |

The **continuous loop** is the cycle sequence inside one run. Stages organize
that sequence; they are not additional loops. The worked fiscal cadence is a
separate sequence of scheduled runs. One `START` authorizes the agent to continue
through all cycles in one run, subject to environmental interruption. Another
`START` is required after a terminal run to select the next configured boundary.
The Markdown contract is not a calendar scheduler.

The orchestrator is an instruction and persistence contract interpreted by an
agent, not a workflow engine that mechanically enforces every rule. Students
must compare the run's claimed checks with its event sidecar and current
artifacts. A self-declared pass is not sufficient when those records disagree.

## The learning path

### 1. Start with a vague task

Students begin with a request such as:

`Review this community and make a good report.`

They identify what is missing:

- Who is the report for?
- What files should be created?
- Which sources may be used?
- What does "good" mean?
- How will the agent know it is done?
- What should happen when evidence is missing?

### 2. Design the goal

Students use `goal-designer-prompt.md`. The Goal Designer challenges vague words,
asks short questions, and returns a Goal Card with eight parts:

1. `OBJECTIVE`
2. `OUTPUT`
3. `DONE WHEN`
4. `QUALITY`
5. `CONTEXT`
6. `CONSTRAINTS`
7. `STAGES`
8. `STOP-CAPS`

The Goal Designer may also recommend using one prompt instead of a loop. That is
a valid result.

### 3. Study a worked Goal Card

Students inspect `brainstem\lobster-pound-review-goal-card.md`.

The example asks the agent to build a fiscal-year-to-date understanding of
Lobster Pound community meetings through separate cumulative scheduled runs. Graph
meeting transcripts and local Copilot meeting summaries are the main evidence;
local transcript copies are fallbacks. Teams conversations and SharePoint
documents are optional supporting sources.

Students should notice that the card separates:

- the result from the work steps;
- required sources from optional sources;
- finish-line checks from quality guidance;
- successful completion from an incomplete but honest stop.

They should apply the operating model above: a run freezes one configured
evidence boundary, stages organize the Goal Card work, and cycles integrate one
target slice at a time without moving that boundary.

### 4. See what changes for one run

Students inspect `brainstem\lobster-pound-community-context.md`.

The context file supplies exact paths, dates, source names, and run settings. It
may narrow the Goal Card, but it may not weaken the Goal Card's finish line.

This teaches a useful split:

- the Goal Card says what success means;
- the Goal Card says how missing, degraded, fallback, and optional evidence are
  handled;
- the context file says which approved sources have those roles for this run.

The source classification is frozen before Cycle 1. A context edit cannot make
a failing required source optional during the run.

### 5. Start one run

Students use `brainstem\loop-orchestrator.md` to start the worked example.

The first run freezes the cumulative window defined by the fiscal-year start and
the first position in the runtime context's boundary schedule. After it
completes, another `START` selects the next position. Each later run checks the
full cumulative window, reuses verified unchanged weeks, and extracts only new
or changed occurrences.

Before creating a run, the agent verifies that the proposed configured boundary
has passed and every scheduled, non-cancelled occurrence inside it has
completed. An ineligible boundary is reported without consuming a run.

Within that run, the orchestrator continuously executes cycles. Each cycle:

1. checks the current state;
2. chooses one target slice tied to a failed check or stage exit condition;
3. performs that slice;
4. checks the affected finish-line items;
5. records the result and chooses whether to continue.

One slice has one main target and a declared measurable delta. It may establish
missing state, repair a failure, or legitimately improve other checks when the
same work affects them.

A cycle never adds another interval. Moving the configured boundary would
change the finish line, so it requires a new run.

The 10-cycle limit is intentional. It pushes the agent to choose useful slices
without turning the first cycle into one large, hidden pass.

Goal Card stages are not mapped one-to-one to cycles. A stage can require
several slices, and the run advances it only after recording evidence that its
work and applicable checks are satisfied. Reaching the final stage does not
complete the run by itself; all `DONE WHEN` checks must still pass.

### 6. Watch the run

During the run, students see short milestone messages and a repeated status
line. Repeated lines show that the process is still alive. They do not prove
that the work improved.

Students use the final run file—not console activity—to judge progress at all
three levels: the cycle's observed delta, the stage's exit evidence, and the
run's fixed acceptance checks.

The worked context uses one child when one occurrence is new or changed. It uses
two or three children when several occurrences are new or changed.
Every child follows one shared extraction contract. The parent agent validates
and integrates the results and remains responsible for the final files and run
history.

### 7. Inspect what the loop learned

After the run, students inspect the run file created from
`brainstem\templates\use-case-run.baseline.md`.

The most important sections are:

- **Work Event Log:** Does the JSONL sidecar contain sequential events for source lookups, failures, fallbacks, and retries as they happened?
- **Source reuse:** Did the run verify the full cumulative source window and avoid re-extracting unchanged weeks?
- **Continuity:** Did the run preserve readable prior fiscal-year state before integrating the new or changed week, while disclosing session-fallback limits?
- **DONE WHEN Results:** Which checks passed, failed, and why?
- **Goal Stage State:** What stage was active, what evidence allowed it to
  advance, and did it span more than one cycle?
- **Current Target Slice:** What measurable change did this cycle attempt?
- **Slice and Cycle History:** What did each cycle try, and what changed?
- **Backlog Decision History:** Why did the next problem move up or down?
- **Child Activity Log:** What work was delegated, and what was accepted?
- **Stop Reason and final cycle decision:** Why did the run complete or stop?
- **Persisted Progress Line:** What was the final state?
- **Incomplete synthesis:** If the run stopped, did it still produce a clearly
  labelled, non-authoritative summary of supported findings and failed checks?

The history should make the path to the result easy to explain. If the file only
shows that more work happened, the loop did not demonstrate learning.

## What counts as progress

Progress is a visible change such as:

- a failed finish-line check now passes;
- a stage exit condition now has persisted evidence;
- a missing source is found or clearly recorded as unavailable;
- an unsupported claim is fixed or removed;
- a conflict is resolved or clearly preserved;
- a required file is created;
- an open gap is closed.

These do not count as progress by themselves:

- more words;
- more tool calls;
- more child agents;
- more cycles;
- a confident answer without stronger evidence.

## Suggested 90-minute flow

| Time | Student activity |
|---:|---|
| 10 minutes | Compare a vague request with a checkable goal |
| 20 minutes | Use the Goal Designer and review its pushback |
| 15 minutes | Read the worked Goal Card and runtime context |
| 30 minutes | Start one run and watch its cycle-level target slices |
| 15 minutes | Inspect the run history and discuss what changed |

If the live run takes longer, the instructor may provide a completed run file
separately for the final inspection.

## Signs the lab worked

The lab is successful when students can:

- explain why one check failed;
- name the target slice chosen for the next cycle;
- point to evidence that the slice produced its expected delta;
- explain why a stage did or did not advance;
- explain why an interrupted run is not a completed or stopped run;
- explain why another tempting action was left for later;
- identify a task that does not need a loop;
- describe the reason the example completed, stopped, or was interrupted.

## Teaching guardrails

- Keep the source set small enough that students can focus on the loop.
- Do not create extra cycles just for the demonstration.
- Do not treat every quality concern as a simple machine check.
- Do not hide missing evidence or disagreement.
- Do not use child agents when the work cannot be divided safely.
- Treat a clear, incomplete stop as better than unsupported success.

## Current lab boundary

The repository contains the instructions and templates. It does not contain the
Lobster Pound source documents or Microsoft 365 content.

Running the worked example requires approved access to the paths and services
listed in `brainstem\lobster-pound-community-context.md`. Students without that
access can still complete the Goal Design portion. They can inspect a completed
run only when the instructor supplies one separately.
