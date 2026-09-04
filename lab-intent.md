# Lab Handoff Summary

## Concept

A 90-minute lab that teaches senior technical practitioners how to engineer reliable AI-enabled loops.

The experience contrasts **outcome-first, evidence-bounded iteration** with “prompt-and-hope” approaches that rely on model capability, excessive context, or a single plausible response. Participants build a workflow that evaluates its own progress, responds to feedback, preserves uncertainty, and stops only when explicit acceptance conditions are satisfied.

## Learning North Star

Participants should leave able to design a loop that:

- Defines a checkable outcome before execution.
- Operates within bounded inputs and constraints.
- Makes state, progress, decisions, and gaps visible.
- Uses deterministic checks where appropriate.
- Revises work across meaningful passes.
- Detects regressions and unsupported conclusions.
- Stops for an evidence-based reason.

The key lesson is that **iteration count is not the same as learning**. Later passes should be forced by new evidence, evaluator feedback, or constraints that invalidate an earlier plausible answer—not merely by increasing work volume.

## North-Star Demonstration

A strong demonstration is a bounded research and sensemaking workflow. It processes a fictional collaboration history to:

- Separate material, duplicate, and low-signal content.
- Produce periodic summaries.
- Maintain themes and their evolution over time.
- Develop a glossary and taxonomy.
- Identify trends and meaningful state changes.
- Preserve unanswered questions and evidence gaps.
- Produce a traceable synthesis without overstating conclusions.

The same mechanics can transfer to architecture decisions, remediation, recommendation auditing, model routing, memory policy, governance, observability, discovery, and cost allocation.

## Design Principles

**Make iteration consequential.** Each stage should change the problem state and require revision.

**Separate checking from judgment.** Mechanical checks can prove completeness and traceability; they do not necessarily prove semantic correctness.

**Design against cheap passes.** The evaluator must reject tactics such as deleting required content, marking everything unknown, selecting every option, storing nothing, or degrading outcomes merely to reduce cost.

**Expose the loop.** Inputs, current conclusions, evidence links, feedback, regressions, open questions, and stop decisions should remain visible.

**Keep content subordinate to learning.** Use a small synthetic corpus so processing does not crowd out loop design and refinement.

## Potential Modalities

| Modality | Best use | Primary constraint |
|---|---|---|
| Facilitator-led demo | Clearly demonstrate the difference between generation and engineered iteration | Limited participant practice |
| Guided hands-on lab | Build practical skill within a controlled 90-minute experience | Requires tight scope and predictable branching |
| Self-paced repository lab | Enable repeatable, independent learning | Needs excellent scaffolding and recovery guidance |
| Safe bring-your-own capstone | Demonstrate transfer to authentic work | Content variability, privacy, and unpredictable duration |
| Short scenario variants | Show that the method generalizes across technical domains | Must preserve the loop mechanics rather than become prompt exercises |

## Minimum Viable Demo

1. Provide a bounded fictional evidence set.
2. Define the required output and explicit acceptance contract.
3. Produce an initially plausible result.
4. Evaluate completeness, traceability, duplicates, gaps, and prohibited shortcuts.
5. Release new evidence or constraints that invalidate part of the result.
6. Revise while preserving change history and unresolved issues.
7. Apply a semantic or adversarial review.
8. Stop only when checks pass and remaining uncertainty is explicit.

## Indicators of Success

- Participants distinguish meaningful iteration from repeated generation.
- Each cycle visibly changes the artifact or understanding.
- Material claims are supported, qualified, or unresolved.
- Mechanical checks catch omissions and gaming.
- Semantic review catches plausible but incorrect conclusions.
- The stop decision is explicit and evidence-based.
- Participants can transfer the pattern to another technical problem.

## Open Design Decisions

The next design phase should determine:

- The smallest corpus that still creates meaningful synthesis.
- How later evidence is staged without unnecessary tooling.
- Which checks are deterministic versus judgment-based.
- How adversarial claim validation is performed.
- Which modality is the primary experience.
- How much workshop time is reserved for inspection, revision, and reflection.