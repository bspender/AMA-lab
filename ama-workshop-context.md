# AMA Loop-Engineering Workshop Context

Status: Draft
Context Version: 1
Goal Card: `ideation-goal-card.md`
Goal Card Version: 0.1
Task Worker: `ideation`
Approved On:

This file contains interview-derived inputs for the ideation Goal Card. It is configuration, not orchestration and not the Goal Card itself. Complete it during Cycle 0 and set `Status: Approved` only after explicit approval.

## Desired Participant Outcomes

- Define outcomes, measurable properties, and feedback loops before choosing an implementation or supplying extensive model context.
- Build a role-relevant agentic workflow whose progress can be evaluated across iterations.
- Recognize prompt-and-hope as a counter-pattern when success depends primarily on model capability rather than explicit checks and feedback.

## Successful 90-Minute Participant Artifact

- A working demo that provides value for the participant's CSA role.
- The demo has an explicit, checkable finish line.
- The demo operates inside a named, bounded sandbox.
- Persisted iteration evidence shows incremental changes converging toward the stated goal.

## Available Tools

- GitHub Copilot CLI or GitHub Copilot app
- Local Markdown files for Goal Card, context, run state, and memory
- No additional development tools or scripts are assumed.

## Starter Materials

- Prefer candidates requiring no starter package so participants build the loop from zero to hero and spend their time on loop engineering rather than learning instructor-provided tools.
- Allow pre-existing structure when it materially improves the illustration; evaluate this per scenario rather than imposing a universal package.
- Label instructor preparation effort for any supporting evidence:
  - `small`: about one hour to create by rapid, AI-assisted authoring;
  - `medium`: about one day;
  - `large`: definitely more than one day.
- Penalize otherwise similar candidates with greater instructor preparation effort.

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
- A candidate meets the immediate-applicability proxy when a CSA can adapt its loop pattern to at least one listed work type in less than one day using existing Copilot access and safe local inputs.

### Target Audience and Relevance Evidence

Assume a Microsoft Cloud Solution Architect working across Data & AI, Application Innovation, and Emerging Technology scenarios.

| Work category | Relevant work types |
|---|---|
| Traditional delivery | Architecture reviews; customer discovery; migration planning; modernization planning; design documentation; workshop preparation; solution recommendations |
| Strategic advisory | Competitive analysis; use-case validation; Azure cost optimization; data and AI sovereignty; agentic developer enablement; governance and operating models; AI transformation planning; tokenomics and cost analysis |
| Emerging technology | Researching agentic patterns; evaluating agent frameworks; comparing models and model-routing strategies; agentic cybersecurity; agent-team design; work-graph design; second-brain architectures; agentic data-readiness assessments; agent memory and learning systems; graph engineering patterns; human/agent operating models |
| Microsoft platform | M365 Copilot adoption and use-case discovery; M365 Copilot readiness; Copilot Studio agent design, evaluation, governance, and operating models; Security Copilot workflow assessment; security recommendation prioritization; agentic data readiness; AI use-case validation; agent-team design; model comparison and use-case alignment; tokenomics analysis and optimization; agent memory and second-brain design; organization structure versus work-graph analysis |

## Scorecard Weights

Use `1` for equal weighting unless Cycle 0 approves another value.

| Dimension | Weight |
|---|---:|
| CSA Relevance | 1 |
| Checkable Finish Line | 1 |
| Bounded Sandbox | 1 |
| Convergent Task | 1 |
| Loop Visibility | 2 |
| Lessons-Learned Potential | 1 |
| Immediate Applicability | 2 |
| Outcome-Based Architecture Potential | 2 |
| Graph Evolution Potential | 1 |
| Workshop Fit | 2 |

## Approved Evidence and Source Materials

- Repository-local fictional inputs created for the selected scenario.
- Participants' general professional expertise.
- No external web sources, live tenants, customer materials, or unapproved evidence.

## Assumptions

- The audience consists of senior Microsoft Cloud Solution Architects.
- The workshop duration is 90 minutes.
- The learning objective is to make loop mechanics visible through hands-on work.
- Participants should experience outcome-first agentic design as a counter-pattern to relying on extensive prompt context and model capability alone.
- The exact architecture decision artifact, sandbox contents, and convergence measures remain to be selected.

## Exclusions

- Live customer or production actions.
- Live customer data.
- Product tutorials or technology demonstrations without an outcome-first feedback loop.
- Candidates that cannot map to at least one approved audience work type.
- Candidates whose finish line depends primarily on subjective participant preference or assumed model quality.
- Category coverage for its own sake; relevance breadth does not compensate for weak loop-engineering instruction.

## Revisit Policy

- Previously ledgered ideas require `REVISIT: <idea-id>` and a new testable hypothesis.
- A revisit is allowed only when a changed constraint, new evidence, or materially different loop mechanic creates that named, testable hypothesis.
- A lower prior rank, a new run, or cosmetic reframing is not sufficient.

## Interview Record

### Round 1

- Completed: 2026-08-27.
- Observable behavior: participants define outcomes, measurable properties, and feedback loops before implementation, then use them to drive iterative improvement.
- Successful artifact: a working, role-relevant demo with a checkable finish line, bounded sandbox, and visible convergence across incremental rounds.
- Highest-priority scenario: architecture decision and tradeoff analysis.
- Checkable interpretation accepted for configuration: outcome definition precedes solution construction, iteration evidence is persisted, and progress can be evaluated without relying on subjective model quality.
- Open for later rounds: tools and starter materials, specific sandbox constraints, remaining priority scenarios, weights, approved evidence, and revisit conditions.

### Round 2

- Completed: 2026-08-27.
- Starter-material default: prefer zero-to-hero candidates needing no starter package; allow scenario-specific pre-existing structure when it materially improves the teaching demonstration.
- Instructor preparation labels: `small` is about one hour, `medium` is about one day, and `large` is definitely more than one day.
- Evidence boundary: repository-local fictional inputs plus participants' general expertise; no web research or tenant access.
- Execution environment: GitHub Copilot CLI or GitHub Copilot app with repository-local Markdown files only.
- Open for Round 3: additional priority scenarios, scorecard weights, detailed exclusions, revisit conditions, and final context approval.

### Round 3

- Completed: 2026-08-27.
- Proposed audience input was challenged as too broad to operate as a priority list or coverage requirement.
- Decision: rank cross-domain CSA decision loops first and use the categorized work types as relevance evidence rather than a Top 10 quota.
- Immediate-applicability proxy: a CSA can adapt the loop pattern to at least one listed work type in less than one day using existing Copilot access and safe local inputs.
- Weighting decision: set Loop Visibility, Immediate Applicability, Outcome-Based Architecture Potential, and Workshop Fit to `2`; keep all other scorecard weights at `1`.
- Revisit decision: require a named testable hypothesis caused by a changed constraint, new evidence, or materially different loop mechanic.
- Draft configuration is complete and awaiting explicit approval.

## Approval Record

Approved By:
Approval Note:
