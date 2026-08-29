# AMA Loop-Engineering Workshop Context

Status: **Draft**
Context Version: 3
Goal Card: `ideation-goal-card.md`
Goal Card Version: 0.3
Task Worker: `ideation`
Approved On: Pending

This file contains current inputs for the ideation Goal Card. It is configuration, not orchestration, run
history, or the Goal Card itself. Complete it during Cycle 0 and set `Status: Approved` only after explicit
approval.

## Desired Participant Outcomes

- Define outcomes, measurable properties, and feedback loops before choosing an implementation or
  supplying extensive model context.
- Build a role-relevant agentic workflow whose progress can be evaluated across iterations.
- Recognize prompt-and-hope as a counter-pattern when success depends primarily on model capability rather
  than explicit checks and feedback.

## Successful 90-Minute Participant Artifact

- A working demo that provides value for the participant's CSA role.
- The demo has an explicit, checkable finish line.
- The demo operates inside a named, bounded sandbox.
- Persisted iteration evidence shows incremental changes converging toward the stated goal.

## Available Tools

- GitHub Copilot CLI or GitHub Copilot app.
- Local Markdown files for Goal Card, context, run state, and memory.
- No additional development tools or scripts are assumed.

## Starter Materials

- Prefer candidates requiring no starter package so participants build the loop from zero to hero and
  spend their time on loop engineering rather than learning instructor-provided tools.
- Allow pre-existing structure when it materially improves the illustration; evaluate this per scenario
  rather than imposing a universal package.
- Facilitator preparation effort is a scored dimension, not a tie-break. See Scorecard Weights.

### Facilitator Artifact Inventory

Derive every effort label from this itemized inventory. Do not assert a label.

| # | Inventory item | What to record |
|---|---|---|
| 1 | Participant input files | Count and approximate length |
| 2 | Seeded defects or planted material | Count, and whether each maps to a rule the participant can discover |
| 3 | Facilitator answer key | Reference converged artifact, defect-to-rule mapping, pass-1 versus pass-N exemplars |
| 4 | Calibration runs | Number of pilot executions needed to set difficulty so the loop neither collapses in one pass nor fails to converge |
| 5 | Diagnostic guide | Stuck-versus-slow signals and the hint ladder |
| 6 | Variant cost | Work to produce one additional cohort or domain variant |

### Derived Effort Labels

- `small` (about one hour): two or fewer input files; no seeded-defect calibration; the answer key is a
  single reference artifact; no hint ladder needed; variants are text substitutions.
- `medium` (about one day): any one of seeded defects requiring calibration, an answer key needing a
  defect-to-rule mapping, or at least one pilot run required to set difficulty.
- `large` (more than one day): any one of no unique correct reference solution, multiple required
  calibration runs, or variants that require re-authoring the answer key.

Artifact page count, input word count, and brief length are **not** valid proxies for preparation effort.
Cost concentrates in calibration and the answer key.

## Sandbox Constraints

- No live customer data.
- No production or live customer actions.
- No web research or tenant access during the lab.
- Use repository-local fictional inputs and participants' general expertise.
- The working surface is GitHub Copilot CLI or GitHub Copilot app plus repository-local Markdown files.

## Priority Emerging Technology CSA Scenarios

- First priority: architecture decision and tradeoff analysis.
- Rank cross-domain CSA decision loops ahead of narrow product or workload coverage.
- Use the work types below as evidence of audience relevance, not as a quota requiring equal representation.
- A candidate meets the immediate-applicability proxy when a CSA can adapt its loop pattern to at least one
  listed work type in less than one day using existing Copilot access and safe local inputs.

### Target Audience and Relevance Evidence

Assume a Microsoft Cloud Solution Architect working across Data & AI, Application Innovation, and Emerging
Technology scenarios.

| Work category | Relevant work types |
|---|---|
| Traditional delivery | Architecture reviews; customer discovery; migration planning; modernization planning; design documentation; workshop preparation; solution recommendations |
| Strategic advisory | Competitive analysis; use-case validation; Azure cost optimization; data and AI sovereignty; agentic developer enablement; governance and operating models; AI transformation planning; tokenomics and cost analysis |
| Emerging technology | Researching agentic patterns; evaluating agent frameworks; comparing models and model-routing strategies; agentic cybersecurity; agent-team design; work-graph design; second-brain architectures; agentic data-readiness assessments; agent memory and learning systems; graph engineering patterns; human-agent operating models |
| Microsoft platform | M365 Copilot adoption and use-case discovery; M365 Copilot readiness; Copilot Studio agent design, evaluation, governance, and operating models; Security Copilot workflow assessment; security recommendation prioritization; agentic data readiness; AI use-case validation; agent-team design; model comparison and use-case alignment; tokenomics analysis and optimization; agent memory and second-brain design; organization structure versus work-graph analysis |

## Scorecard Weights

Use the configured weights below.

| Dimension | Weight |
|---|---:|
| CSA Relevance | 1 |
| Checkable Finish Line | 1 |
| Bounded Sandbox | 1 |
| Convergent Task | 1 |
| Gaming Resistance | 1 |
| Loop Visibility | 2 |
| Lessons-Learned Potential | 1 |
| Immediate Applicability | 2 |
| Outcome-Based Architecture Potential | 2 |
| Graph Evolution Potential | 1 |
| Workshop Fit | 2 |
| Facilitator Build Cost | 2 |

Weight sum: **17**. Maximum total: **85**.

## Evidence and Source Materials

- Repository-local fictional inputs created for the selected scenario.
- Participants' general professional expertise.
- No external web sources, live tenants, customer materials, or unapproved evidence.

## Assumptions

- The audience consists of senior Microsoft Cloud Solution Architects.
- The workshop duration is 90 minutes.
- The learning objective is to make loop mechanics visible through hands-on work.
- Participants should experience outcome-first agentic design as a counter-pattern to relying on extensive
  prompt context and model capability alone.
- The exact architecture decision artifact, sandbox contents, and convergence measures remain to be
  selected.

## Exclusions

- Live customer or production actions.
- Live customer data.
- Product tutorials or technology demonstrations without an outcome-first feedback loop.
- Candidates that cannot map to at least one approved audience work type.
- Candidates whose finish line depends primarily on subjective participant preference or assumed model
  quality.
- Category coverage for its own sake; relevance breadth does not compensate for weak loop-engineering
  instruction.

## Revisit Policy

- Previously ledgered ideas require `REVISIT: <idea-id>` and a new testable hypothesis.
- A revisit is allowed only when a changed constraint, new evidence, or materially different loop mechanic
  creates that named, testable hypothesis.
- A lower prior rank, a new run, or cosmetic reframing is not sufficient.
- A material Goal Card or context change qualifies only when the run names the resulting hypothesis and
  re-evaluates carried candidates rather than re-discovering them.

## Interview Record

No interview responses are recorded in this harness snapshot. Populate this section only during a new
Cycle 0 configuration interview; the current-state fields above remain proposed defaults until explicit
approval.
