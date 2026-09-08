# Loop Engineering Lab: Learning Intent

## Purpose

This 90-minute lab teaches students how to give an AI agent a clear goal, let it
work through problems, and know when the work is truly done.

The main lesson is simple:

> Repeating a prompt is not the same as learning.

A useful loop checks its work. When a check fails, the agent chooses a small
repair, makes the change, checks again, and records what happened.

## What students should learn

By the end of the lab, students should be able to:

1. turn a vague request into a clear Goal Card;
2. write finish-line checks that produce a recorded pass or fail result;
3. set clear limits on sources, files, actions, cycles, and cost;
4. explain why a task should use a loop—or why one prompt is enough;
5. follow how one small repair changes the work from one cycle to the next;
6. tell the difference between real progress and more activity;
7. inspect the final run history and explain why the agent stopped.

Students do not need to build a workflow engine. They learn by reading and
changing plain Markdown files.

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

The example asks the agent to review a 30-day window of Lobster Pound community
meetings. Graph meeting transcripts and local Copilot meeting summaries are the
main evidence; local transcript copies are fallbacks. Teams conversations and
SharePoint documents are optional supporting sources.

Students should notice that the card separates:

- the result from the work steps;
- required sources from optional sources;
- finish-line checks from quality guidance;
- successful completion from an incomplete but honest stop.

### 4. See what changes for one run

Students inspect `brainstem\lobster-pound-community-context.md`.

The context file supplies exact paths, dates, source names, and run settings. It
may narrow the Goal Card, but it may not weaken the Goal Card's finish line.

This teaches a useful split:

- the Goal Card says what success means;
- the context file says what is true for this run.

### 5. Run the loop

Students use `brainstem\loop-orchestrator.md` to start the worked example.

Each cycle:

1. checks the current state;
2. chooses one small target slice;
3. performs that slice;
4. checks the affected finish-line items;
5. records the result and chooses whether to continue.

One slice has one main target. It may also improve other checks when the same
work honestly affects them.

The 10-cycle limit is intentional. It pushes the agent to choose useful slices
without turning the first cycle into one large, hidden pass.

### 6. Watch the run

During the run, students see short milestone messages and a repeated status
line. Repeated lines show that the process is still alive. They do not prove
that the work improved.

Students use the final run file—not console activity—to decide whether the loop
made progress.

The worked context uses two or three child agents to cover all meeting-date
extraction partitions with one shared contract. The parent agent validates and
integrates the results and remains responsible for the final files and run
history.

### 7. Inspect what the loop learned

After the run, students inspect the run file created from
`brainstem\templates\use-case-run.baseline.md`.

The most important sections are:

- **Work Event Log:** Does the JSONL sidecar contain sequential events for source lookups, failures, fallbacks, and retries as they happened?
- **Continuity:** Did the run identify and preserve readable prior themes, commitments, and glossary entries before adding new evidence, while disclosing session-fallback limits?
- **DONE WHEN Results:** Which checks passed, failed, and why?
- **Slice and Cycle History:** What did each cycle try, and what changed?
- **Backlog Decision History:** Why did the next problem move up or down?
- **Child Activity Log:** What work was delegated, and what was accepted?
- **Stop Reason and final cycle decision:** Why did the run complete or stop?
- **Persisted Progress Line:** What was the final state?

The history should make the path to the result easy to explain. If the file only
shows that more work happened, the loop did not demonstrate learning.

## What counts as progress

Progress is a visible change such as:

- a failed finish-line check now passes;
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
| 30 minutes | Start the loop and watch its target slices |
| 15 minutes | Inspect the run history and discuss what changed |

If the live run takes longer, the instructor may provide a completed run file
separately for the final inspection.

## Signs the lab worked

The lab is successful when students can:

- explain why one check failed;
- name the repair chosen for the next slice;
- point to evidence that the repair helped;
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
