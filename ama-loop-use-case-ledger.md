# AMA Loop-Engineering Workshop Idea Ledger

Durable cross-run idea registry for workshop use-case ideation. Read before generating candidates; update after every execution iteration.

This is the single cross-run ledger named by the Goal Card STATE FILES table. All runs write here.

## Rules

- Stable IDs use kebab-case and are never reassigned.
- A renamed or reframed idea keeps its original ID when the CSA job, trigger, loop transformation, and output artifact are materially the same. Where two runs generated the same idea independently, the earlier run's ID is authoritative and the later ID is recorded as an alias.
- A ledgered idea is not eligible as a new idea.
- `REVISIT: <idea-id>` requires a new testable hypothesis supplied **by the run**. This registry deliberately does not pre-write revisit hypotheses; doing so would pre-satisfy the gate the revisit rule exists to force.
- Record every genuinely new idea seen, including ideas rejected before scoring.
- Record evidence, not verdicts. Ranks and weighted totals are run-relative and are not stored here.

### Worked adjudications

The four-field test is stated but not self-calibrating. These are the reference rulings.

| Pair | Ruling | Reasoning |
|---|---|---|
| `model-routing-policy-test-loop` / `model-routing-policy-tuning` | **Same** | All four fields match in substance. Note that the two share zero exact substrings, so no string or token comparison detects this. Semantic judgment is required. |
| `security-recommendation-priority-loop` / `security-recommendation-prioritization` | **Different** | Sol's iterates the *ordering* until coverage and capacity checks pass. The other iterates the *rule set* until the ordering is reproducible from rules alone. Ordering-iteration and rule-induction are different loops with different gaming profiles. |
| `agent-work-graph-lint-loop` / `work-graph-role-decomposition` | **Different** | Lint-and-repair an existing graph versus decompose an org chart into one. Inverse directions. |
| `customer-discovery-gap-closure` / `discovery-question-bank-pruning` | **Different** | Additive gap closure versus subtractive pruning. Near-inverses. |
| `ai-use-case-validation-loop` / `use-case-portfolio-dedupe-triage` | **Different** | Evidence validation versus semantic set hygiene. |
| `modernization-wave-plan-loop` / `migration-dependency-risk-map` | **Same** | Both `run-2026-08-27-01`. An undetected within-run collision; the run reported zero duplicates. |

Sharing a domain noun is not evidence of sameness. Compare the transformation field first.

## Registry states

State is recorded on two orthogonal axes. A single column cannot represent both.

**Lifecycle** — how far the idea progressed.

| Value | Meaning | Writer |
|---|---|---|
| `seen` | Recorded but not gated or scored | Worker, on registration before scoring |
| `evaluated` | Gated or scored in at least one run | Worker, after scoring |
| `selected` | Included in at least one run's final Top 10 | Worker, at finalization |
| `workshopped` | Used in an actual workshop | Facilitator, post-delivery |

**Disposition** — availability to future runs.

| Value | Meaning | Writer |
|---|---|---|
| `carried` | Available for re-evaluation by the next run | Carry-forward decision, recorded with a reason |
| `not-carried` | Known and duplicate-blocking, but not queued for re-evaluation | Default for ledgered ideas |
| `retired` | Excluded from future consideration by an approved-context exclusion | Requires a cited exclusion |

Invariants:

- `carried` requires lifecycle `evaluated` or later.
- `retired` requires a named exclusion in approved context; a low score is never sufficient.
- `not-carried` still blocks duplicate registration. It is not a deletion.
- Every ledgered idea is ineligible as a *new* idea regardless of disposition. Only `REVISIT` with a run-supplied hypothesis reopens one.

## Run Log

| Run ID | Date | Card | Card Ver | Ctx Ver | Weights (sum/max) | Model | Iterations | Result | Novel added | Run file |
|---|---|---|---:|---:|---|---|---|---|---:|---|
| `run-2026-08-27-01` | 2026-08-27 | `ideation-goal-card.md` | 0.1 | 1 | 14 / 70 | GPT-5.6 Sol | 4 of 5 | Complete | 20 | archived outside repo |
| `run-2026-08-27-a` | 2026-08-27 | `ideation-goal-card.md` | 0.1 | 1 | 14 / 70 | Claude Opus 5 | 4 of 5 | Complete | 20 | archived outside repo |

Both runs read an empty ledger and were blind to each other. Neither run's duplicate detector was exercised against cross-run memory, so neither run's reported duplicate count is evidence about cross-run detection.

## Carried Candidates

18 ideas: the union of both runs' Top 10s, de-duplicated. Union rather than intersection, because selecting by v0.1 rank would filter using the instrument whose blind spots motivated v0.2.

**Totals and ranks are deliberately omitted.** Cross-run comparison showed the same idea scoring 44 (gate-failed) and 55 (Top 10) under the identical card. The score measured specification tightness, not the idea. Dimension vectors are retained as reference so re-evaluation is not re-discovery, but they are v0.1 artifacts and carry no authority under a later card.

| ID | CSA job | Trigger / input | Loop transformation | Output artifact | Origin | Lifecycle | Disp. | v0.1 gates CF/BS/CT | v0.1 vector (reference only) | Aliases |
|---|---|---|---|---|---|---|---|---|---|---|
| `architecture-decision-evidence-loop` | Architecture decision and tradeoff analysis | Fictional decision dossier, or a weak draft ADR | Close evidence and traceability gaps against explicit decision rules | ADR plus traceability matrix | both runs | selected | carried | 5/5/5 | 5/5/5/5/5/5/5/5/4/5 | `architecture-decision-record-hardening` (`run-2026-08-27-a`) |
| `architecture-assumption-burn-down` | Architecture decision risk reduction | Fictional proposed architecture or solution brief plus claims | Classify claims, attach bounded validation tests, burn down untested high-impact assumptions | Assumption register plus validation plan | both runs | selected | carried | 5/5/5 | 5/5/5/5/5/5/5/5/3/5 | `assumption-to-evidence-ledger` (`run-2026-08-27-a`) |
| `model-routing-policy-test-loop` | Model and routing strategy selection | Fictional request profiles, model cards, budgets, constraints | Revise routing rules until scenario tests satisfy quality, latency, and cost thresholds | Tested routing policy and results table | `run-2026-08-27-01` | selected | carried | 5/5/5 | 5/5/5/5/5/4/5/5/4/5 | `model-routing-policy-tuning` (`run-2026-08-27-a`) |
| `ai-use-case-validation-loop` | AI use-case validation and prioritization | Fictional use-case claims, outcomes, constraints, evidence snippets | Close evidence gaps and rerank against explicit viability criteria | Ranked portfolio plus evidence register | `run-2026-08-27-01` | selected | carried | 5/5/5 | 5/5/5/5/5/4/5/5/3/5 | — |
| `agent-work-graph-lint-loop` | Agent-team and work-graph design | Fictional outcome, roles, tools, handoffs, failure scenarios | Lint and revise nodes, edges, ownership, and stop conditions | Work-graph specification plus lint report | `run-2026-08-27-01` | selected | carried | 5/5/5 | 5/5/5/5/5/5/4/5/5/4 | — |
| `data-ai-sovereignty-decision-loop` | Sovereignty architecture tradeoff analysis | Fictional residency, control, identity, operational requirements plus options | Eliminate noncompliant options and close requirement-to-control traceability gaps | Sovereignty ADR | `run-2026-08-27-01` | selected | carried | 5/5/4 | 5/5/5/4/5/5/5/5/4/4 | — |
| `architecture-review-finding-closure` | Architecture review | Fictional design package and review rubric | Detect, prioritize, and close material findings preserving traceability | Closure-ready review report | `run-2026-08-27-01` | selected | carried | 5/5/5 | 5/5/5/5/5/4/5/4/3/5 | — |
| `modernization-wave-plan-loop` | Modernization and migration planning | Fictional application inventory, dependencies, constraints, outcomes | Revise waves until dependency, capacity, risk, and outcome checks pass | Dependency-valid wave plan | `run-2026-08-27-01` | selected | carried | 5/5/5 | 5/5/5/5/4/5/5/5/4/4 | `migration-wave-plan-dependency-repair` (`run-2026-08-27-a`); `migration-dependency-risk-map` (same run, internal collision) |
| `token-economics-budget-loop` | Tokenomics and cost optimization | Fictional workload volumes, token profiles, quality tiers, budget limits | Revise model, caching, and routing assumptions until budgets and quality floors pass | Scenario-tested token budget and controls | `run-2026-08-27-01` | selected | carried | 5/5/5 | 5/5/5/5/5/4/5/5/3/4 | — |
| `security-recommendation-priority-loop` | Security recommendation prioritization | Fictional findings, business impact, dependencies, remediation capacity | Rerank and sequence actions until coverage, dependency, and capacity checks pass | Prioritized remediation plan | `run-2026-08-27-01` | selected | carried | 5/5/4 | 5/5/5/4/5/4/5/5/4/4 | none; distinct from `security-recommendation-prioritization` |
| `requirements-to-measurable-outcomes` | Architecture decision framing | Fictional one-paragraph customer ask | Replace each non-measurable criterion with a checkable one until zero remain | Outcome spec with acceptance criteria | `run-2026-08-27-a` | selected | carried | 5/5/5 | 5/5/5/5/5/4/5/5/2/5 | none; not generated by `run-2026-08-27-01` |
| `design-doc-reviewer-rulebook` | Architecture review | Fictional design doc | Induce and refine review rules until every finding cites a numbered rule and every rule has a triggering line reference | Rulebook plus review report | `run-2026-08-27-a` | selected | carried | 4/5/4 | 5/4/5/4/5/5/5/4/3/4 | — |
| `goal-card-self-authoring` | Any recurring CSA deliverable | Participant-named vague task | Iterate `DONE WHEN` criteria until every check is mechanically verifiable | Reusable Goal Card | `run-2026-08-27-a` | selected | carried | 5/4/4 | 4/5/4/4/5/5/5/4/3/4 | — |
| `waf-tradeoff-scorecard-convergence` | Architecture tradeoff analysis | Three fictional candidate architectures | Fill and justify every scorecard cell until no unjustified cell remains | Comparison matrix plus recommendation | `run-2026-08-27-a` | selected | carried | 4/5/4 | 5/4/5/4/4/3/5/5/3/4 | — |
| `poc-to-production-gap-checklist` | Modernization and productionization planning | Fictional POC description | Iterate gap list until each gap has severity, owner-type, and blocking decision | Hardening plan | `run-2026-08-27-a` | selected | carried | 4/5/3 | 5/4/5/3/4/4/5/5/3/4 | — |
| `eval-set-for-copilot-agent` | Agent evaluation and governance | Fictional agent description | Add cases until every named failure mode has a passing and a failing test | Eval set plus pass/fail rubric | `run-2026-08-27-a` | selected | carried | 5/5/4 | 4/5/5/4/5/4/4/4/3/4 | — |
| `executive-brief-compression` | Executive communication | Long fictional technical brief plus must-keep fact list | Compress under a word budget until budget met and all must-keep facts survive | Executive brief | `run-2026-08-27-a` | selected | carried | 5/5/5 | 4/5/5/5/4/3/5/2/1/5 | `executive-narrative-polish-loop` (`run-2026-08-27-01`, gate-failed) |
| `cost-model-driver-refinement` | Azure cost and tokenomics analysis | Fictional workload description | Iterate until every cost line has a named driver and sensitivity range | Cost model plus sensitivity table | `run-2026-08-27-a` | selected | carried | 4/5/4 | 4/4/5/4/4/3/4/4/2/4 | — |

### Build-cost signals for carried candidates

Approved context forbids asserted effort labels and requires an itemized inventory. Neither v0.1 run produced one. Independent review found the v0.1 labels unreliable: all three of `run-2026-08-27-a`'s Top 3 briefs asserted `small` and were re-labeled medium, medium-upper, and large.

The v0.1 `Prep` labels are therefore recorded as **unverified claims**, not carried findings:

| v0.1 asserted label | Candidates |
|---|---|
| `none` | `goal-card-self-authoring` |
| `small` | `architecture-decision-evidence-loop`, `architecture-assumption-burn-down`, `model-routing-policy-test-loop`, `ai-use-case-validation-loop`, `architecture-review-finding-closure`, `token-economics-budget-loop`, `security-recommendation-priority-loop`, `requirements-to-measurable-outcomes`, `design-doc-reviewer-rulebook`, `waf-tradeoff-scorecard-convergence`, `poc-to-production-gap-checklist`, `eval-set-for-copilot-agent`, `executive-brief-compression`, `cost-model-driver-refinement` |
| `medium` | `agent-work-graph-lint-loop`, `data-ai-sovereignty-decision-loop`, `modernization-wave-plan-loop` |

A run scoring Facilitator Build Cost must build the inventory from scratch. Do not carry these labels into a score.

## Known Ideas Not Carried

Recorded to block duplicate registration. Not queued for re-evaluation.

| ID | One-line fingerprint | Origin | Lifecycle | Disp. | Eligible under v0.1 | Failed gates | Evidence |
|---|---|---|---|---|---|---|---|
| `agent-memory-design-risk-loop` | Agent memory architecture \| interaction patterns, threats, retention \| revise memory types against retrieval and risk tests \| memory architecture plus test matrix | `run-2026-08-27-01` | evaluated | not-carried | Yes | — | Strongest exclusion in its run; needs an authored expected-answer fixture. |
| `migration-dependency-risk-map` | Migration planning \| workload inventory and dependency evidence \| close unknown dependencies and rerank blockers \| dependency risk map | `run-2026-08-27-01` | evaluated | not-carried | Yes | — | Same idea as `modernization-wave-plan-loop`; undetected within-run collision. |
| `governance-operating-model-coverage` | Governance design \| decisions, controls, roles, escalation \| close ownership and control coverage gaps \| responsibility matrix | `run-2026-08-27-01` | evaluated | not-carried | Yes | — | Broad relevance, weaker visible transformation. |
| `customer-discovery-gap-closure` | Discovery preparation \| opportunity brief and stakeholder statements \| close decision-critical evidence gaps \| discovery brief | `run-2026-08-27-01` | evaluated | not-carried | Yes | — | Convergence depends on authored evidence sufficiency. |
| `competitive-claim-evidence-loop` | Competitive analysis \| competitor claims and evidence excerpts \| remove unsupported claims, close criteria gaps \| claim-evidence matrix | `run-2026-08-27-01` | evaluated | not-carried | Yes | — | Bounded only with a deliberately authored evidence packet. Also collided with a candidate rejected pre-registration in `run-2026-08-27-a`. |
| `workshop-objective-alignment-loop` | Workshop preparation \| audience needs, agenda draft, outcomes \| revise until every outcome has evidence and time-box coverage \| agenda plus objective trace | both runs | evaluated | not-carried | Yes | — | Same idea as `workshop-agenda-timeboxing`. Below the cut in both runs independently. |
| `copilot-use-case-portfolio-loop` | Copilot adoption discovery \| roles, pains, readiness, candidate use cases \| validate, dedupe, rerank \| prioritized portfolio | `run-2026-08-27-01` | evaluated | not-carried | Yes | — | Its own run's rationale calls it "less precise than the general AI validation loop," which is a quality comparison where a distinctness ruling was required. Probable duplicate of `ai-use-case-validation-loop`. |
| `emerging-trend-synthesis-loop` | Emerging-tech research \| recollections and local notes \| repeatedly synthesize themes \| trend brief | `run-2026-08-27-01` | evaluated | not-carried | **No** | CF2 BS2 CT2 | Unbounded evidence, subjective finish line. |
| `autonomous-agent-swarm-blueprint` | Agent-team design \| business challenge and expertise \| add roles until team seems sufficient \| swarm blueprint | `run-2026-08-27-01` | evaluated | **retired** | **No** | CF2 CT2 | Retired, not revisitable: approved context excludes autonomous swarms. No run can lift the block without a context change. |
| `security-recommendation-prioritization` | Security prioritization \| findings list \| refine ranking rules until ordering is reproducible from rules alone \| remediation plan | `run-2026-08-27-a` | evaluated | not-carried | Yes | — | Distinct from `security-recommendation-priority-loop`: rule-induction, not ordering-iteration. |
| `use-case-portfolio-dedupe-triage` | M365 Copilot discovery \| raw use-case list with overlaps \| fingerprint and merge until every entry is semantically unique \| consolidated portfolio | `run-2026-08-27-a` | evaluated | not-carried | Yes | — | Set-hygiene loop rather than a decision loop. |
| `data-readiness-gap-closure` | Agentic data-readiness assessment \| data estate description \| iterate until every gap has a test, owner-type, and verdict \| readiness assessment | `run-2026-08-27-a` | evaluated | not-carried | Yes | — | — |
| `work-graph-role-decomposition` | Work-graph design \| team and workstream list \| decompose into roles and handoffs until no ambiguous ownership \| work graph | `run-2026-08-27-a` | evaluated | not-carried | Yes | — | Distinct from `agent-work-graph-lint-loop`: inverse direction. |
| `governance-policy-exception-loop` | Governance \| policy set plus exception requests \| refine decision rules until exceptions resolve without human judgment \| policy decision table | `run-2026-08-27-a` | evaluated | not-carried | Yes | — | Distinct from `governance-operating-model-coverage`. |
| `agent-memory-promotion-rules` | Agent memory design \| prior run notes \| promote durable rules out of episodic noise \| memory file plus promotion policy | `run-2026-08-27-a` | evaluated | not-carried | **No** | CT2 | Distinct from `agent-memory-design-risk-loop`. |
| `discovery-question-bank-pruning` | Customer discovery \| seed question bank \| prune questions that do not change a decision \| minimal question set | `run-2026-08-27-a` | evaluated | not-carried | **No** | CF2 | Distinct from `customer-discovery-gap-closure`: subtractive, not additive. |

## Cross-Boundary Disputes

The strongest empirical result across the two runs, and the reason v0.2 adds a Gaming Resistance gate. In each case the same idea was scored very differently by two runs using an identical card and identical weights. The variance is attributable to how tightly each run specified the idea, not to the idea itself.

| Idea | `run-2026-08-27-01` | `run-2026-08-27-a` | Spread | Significance |
|---|---|---|---|---|
| Executive brief | Gate-failed, ineligible | Top 10 | Crosses the eligibility boundary | Decisive. One run's "subjective finish line" is the other's word budget plus must-keep fact list. The specification, not the idea, determined eligibility. |
| Model routing | Top 3 | Below the cut | 18 points | Largest numeric spread in the comparison. |
| Workshop agenda | Below the cut | Below the cut | 13 points | Agreed on the verdict, disagreed sharply on the margin. |
| ADR / decision evidence | Rank 1 | Rank 2, and the recommended lab | Adjacent | The only idea both runs independently placed at the top. Strongest corroboration available for lab selection. |

A run scoring these candidates must specify the finish line before scoring it, or it will reproduce the same artifact.

## Carry-Forward Provenance

| Field | Value |
|---|---|
| Built | 2026-08-27, after independent review of both completed runs |
| Source runs | `run-2026-08-27-01` (GPT-5.6 Sol), `run-2026-08-27-a` (Claude Opus 5) |
| Both scored under | Goal Card v0.1, context v1, weight sum 14, maximum 70 |
| Distinct ideas known | 34 (40 raw registrations minus 6 confirmed cross-run duplicates) |
| Carried for re-evaluation | 18 |
| Selection rule | Union of both Top 10s, de-duplicated |
| Deliberately omitted | Weighted totals and ranks |

Integrity notes:

- Both source runs wrote to run-specific files that are archived outside this repository. This registry is the surviving record.
- `run-2026-08-27-01` originally persisted its ideas to a separate ledger file rather than the card-named path, so its `DONE WHEN` check "every new idea is recorded in the ledger" was satisfied only nominally. Consolidating here resolves that defect.
- Neither run exercised cross-run duplicate detection, because both read an empty ledger. The first genuine test of the fingerprint scheme will be the next run.
- Within-run detection did fail at least once: `run-2026-08-27-01` reported zero duplicates while registering both `modernization-wave-plan-loop` and `migration-dependency-risk-map`.
- The 34 known ideas exceed any single run's novelty quota. A run executing against this registry must use a revisit or re-score mode rather than attempting to register 20 ideas that collide with none of them.
