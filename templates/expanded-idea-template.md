# Expanded Idea Template

Template Version: 1

Use this template for the automatic Top 3 expansions and for `EXPAND idea <rank-or-id>`. The result is a
derived design handoff, not proof that the proposed lab kit exists.

## Metadata

| Field | Value |
|---|---|
| Source run | `<run-id>` |
| Final rank | `<rank>` |
| Stable ID | `<candidate-id>` |
| Candidate maturity | `<final or terminal-run state>` |
| Expansion contract | `templates\expanded-idea-template.md`, version 1 |
| Expansion status | `Design hypothesis; not an approved Goal Card or completed lab kit` |
| Output path | `ideation-runs\<run-id>\expanded-idea-<rank>.md` |

## How to read this file

State plainly what this file lets the reader decide and what it does not prove. Use these labels:

- **Known from the run**
- **Validated**
- **Proposed for design**
- **Must decide**
- **To be authored**

## 1. The idea in plain language

Explain the recurring CSA task, what the agent would repeatedly improve, what changes between passes, and
what the final artifact is. Define any fictional domain or role before using its name.

## 2. Why this might deserve a lab

Cover CSA relevance, participant learning, immediate applicability, and the specific outcome-first lesson.
Do not rely on the score as the rationale.

## 3. Concrete participant journey

Describe:

1. what the participant receives;
2. what they edit;
3. what the first check reports;
4. what new information appears at each later stage;
5. what visibly changes;
6. what the final artifact looks like.

## 4. What is assumed, and why

| Assumption or design choice | Status | Why it was introduced | How to validate or decide |
|---|---|---|---|
| `<statement>` | `<label>` | `<reason>` | `<test or interview question>` |

Include every oddly specific domain, role, file, fixture count, threshold, formula, or stage gate. Do not
hide design choices inside a sentence beginning with "Given."

## 5. Proposed starter kit and existence check

| Path or artifact | Exists now? | Minimum contents | Why needed | Authoring burden |
|---|---|---|---|---|
| `<path>` | `Yes - verified` or `No - To be authored` | `<minimum viable shape>` | `<purpose>` | `<small/medium/large contributor>` |

Then answer directly:

- **Can this be mocked with Markdown and Copilot only?**
- **What is the minimum credible mockup?**
- **What must be added before it is workshop-ready?**
- **What is deliberately not being built?**

Do not equate low-code with low-preparation.

## 6. Loop mechanics and evaluator

Define the editable artifact, immutable inputs, deterministic checks, progress tuple, improvement backlog,
regression behavior, and stop decision. Include cheap degenerate attempts and the exact checks that reject
them.

## 7. Iteration-forcing mechanism

Explain what information is unavailable on pass 1, the release condition for each later stage, why a later
stage invalidates at least one plausible earlier solution, and why this controls pass count rather than
work volume.

## 8. Facilitator build and diagnostic plan

Include the participant inputs, planted material, reference solution, defect-to-rule or case-to-rule map,
pass-1/pass-N exemplars, calibration runs, stuck-versus-slow signals, hint ladder, variant cost, and the
derived build-cost label. Distinguish recorded pilot evidence from projections.

## 9. Goal Designer handoff

The block below should be compact enough to attach with the Goal Designer prompt. Prefix every field with
`Candidate`, because the Goal Designer must interview the user before approving it.

### Candidate OBJECTIVE

State the task and beneficiary without assuming unbuilt files are available.

### Candidate OUTPUT

Name the artifact and proposed path.

### Candidate DONE WHEN

List three to five boring, machine-checkable criteria and the anti-gaming checks.

### Candidate QUALITY

List bar-raising rules that do not masquerade as completion checks.

### Candidate CONTEXT

Separate verified existing sources from proposed sources that are `To be authored`. Keep the list minimal.

### Candidate CONSTRAINTS

Include style rules, exclusions, editable versus immutable files, and the required one-line decision note
per cycle.

### Candidate STAGES

Use two to four participant work phases. Do not count setup or debrief as loop stages.

### Candidate STOP-CAPS

Include a hard turn cap and "stalled three turns with no progress means stop and report."

### Preliminary loop-fit verdict

Assess, separately:

| Required ingredient | Present? | Evidence or unresolved issue |
|---|---|---|
| Checkable finish line | `<Yes/No/Uncertain>` | `<why>` |
| Bounded sandbox | `<Yes/No/Uncertain>` | `<why>` |
| Convergent task | `<Yes/No/Uncertain>` | `<why>` |

Conclude `Loop candidate` or `Do not loop yet`. If any ingredient is missing, provide the best single-prompt
version instead.

## 10. Goal Designer interview priorities

List only decisions whose answers materially change the Goal Card, evaluator, feasibility, or build cost.
Make hidden thresholds and fictional-domain choices explicit.

## 11. Selection evidence and alternatives

Include the full score vector and weighted total, nearest alternative and comparative justification,
lessons/memory potential, outcome-based architecture potential, graph-evolution path, and first-run risks.
