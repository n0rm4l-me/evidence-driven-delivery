# Analysis of the method

**Version:** 0.4
**Date:** 2026-09-07
**Subject:** §1 to §12 analyse METHODOLOGY.md v0.3, which the findings here moved to v0.9. §13 analyses the whole model as it stands: METHODOLOGY v0.8 with AUTHORITY 0.1, CONTROL 0.4 and ECONOMY 0.5.
**Stance:** adversarial. The purpose of this document is to find where the method fails, not to justify it.

Findings that imply changes are collected in §12, 24 of them in three batches, and in §13, 10 more, all applied. The analysis in §1 to §11 is deliberately left as it was written, describing v0.3, because it is the reasoning that produced the redesign. Read §12 and §13 for where each finding landed.

---

## §1 The claims, restated so they can be falsified

The method is only analyzable once its promises are turned into statements that could turn out false.

| # | Claim | What would falsify it |
|---|---|---|
| C1 | The true state of work can be derived from artifacts alone, with no human reporting | an initiative whose real state is materially different from what all available artifacts show |
| C2 | Removing the payoff for dishonesty, with no penalty attached, is enough to stop dishonest reporting | teams keep misreporting even though misreporting earns nothing |
| C3 | Paying for declared blockers and documented failures makes honesty the dominant strategy | teams that declare blockers end up worse off than teams that stay quiet |
| C4 | An organization can sustain having no per-person metrics | per-person numbers reappear within two quarters, from any direction |
| C5 | Practices spread through defaults, not through documents | a default is added and adoption does not follow |
| C6 | Rewards spent on capability motivate without displacing intrinsic motivation | teams begin choosing work by its point value rather than its importance |

C1 and C4 are the load-bearing ones. If C1 is false the method has no data. If C4 is false the method becomes a performance management system, which is the one thing it claims not to be.

C2 is the most interesting because it is nearly untestable in isolation: an organization that adopts the method also changes five other things at the same time.

---

## §2 Central finding: the lie surface moved, it did not disappear

The method claims to eliminate misreporting by making claims worthless and artifacts decisive. It succeeds at that specific thing. Nobody can usefully lie about whether a deploy happened.

But every one of the three inputs that decide what an artifact is worth is still set by the party being measured:

**1. The acceptance criterion.** `done = <verifiable fact>` is written before work starts, which prevents inventing success afterwards. It does not prevent choosing a weak criterion beforehand. The rational move under this method is not to lie about results, it is to pre-register a criterion that is cheap to satisfy. Verification stays perfectly objective while the bar quietly drops. This is strictly worse than the old situation in one respect: the low bar is now formally documented and machine-confirmed, so it looks like rigor.

**2. The ground-truth metric.** Mechanism 4 requires a number expressing target system behavior. Whoever defines that number controls what progress means. A team asked to produce its own progress metric will produce one that moves. That is self-reporting again, with a dashboard in front of it.

**3. The size and price of an item.** The price list assigns points per action, and the actor chooses which actions to take (see §4).

So the single most important structural gap: **the method specifies who executes and who verifies, but never specifies who defines.** Definition is the highest-leverage role in the whole system and it is currently unassigned, which means it defaults to the executor.

Fix direction: definition and execution must be separated. The acceptance criterion, the ground-truth metric and the size band are proposed by the executing team and **countersigned by the priority owner** before work starts. This is one extra step, it happens once per item, and without it the rest of the machinery is decorative. See change P1 in §12.

---

## §3 What the method gets right

Kept short deliberately, but these should survive any revision.

- **Artifact-only verification.** Deriving state from things that exist as a by-product of the work is correct and is the part that no existing lightweight practice does systematically.
- **No penalties, ever.** The insight that you never need to detect a lie if an unverified claim is inert is genuinely good, and it is what makes the system politically survivable.
- **Paying for declared blockers and documented failures.** The recognition that honesty must strictly dominate rather than tie with silence is the sharpest idea in the document.
- **Structural absence of per-person metrics.** Making the guarantee a property of the data rather than a promise of behavior is the right way to make it credible.
- **Defaults over documents.** Correct, underused, and it makes accumulated experience actually cumulative.
- **Cancellation counted as a health metric.** Counterintuitive and correct.

---

## §4 Attack surface: what a rational team does with the price list

Take the starter price list literally and divide by effort. Effort figures are rough but the ratios are not sensitive to their precision.

| Action | Points | Realistic effort | Points per day |
|---|---|---|---|
| Declare your own blocker | 20 | 0.05 d | **400** |
| Delete dead config or code | 60 | 1 d | **60** |
| Decompose an initiative | 25 | 0.5 d | **50** |
| Add a CI check as a default | 80 | 2 d | **40** |
| Document a failed experiment | 40 | 1 d | **40** |
| Unblock another team | 50 | 2 d | 25 |
| Automate a manual operation | 70 | 5 d | 14 |
| Pre-production milestone | 30 | 8 d | 3.8 |
| **Production milestone** | **100** | **20 d** | **5** |

The production milestone, which is the only line item that represents the organization's actual goal, is close to the worst-paying activity available. Declaring blockers pays roughly eighty times better than delivering the thing.

This is not a calibration error to be fixed by adjusting numbers. It is structural: **a price list that pays per action will always favour actions that are cheap to complete, and real outcomes are never cheap to complete.** Any per-action scheme drifts toward artifact production.

The gaming strategies follow directly, and none of them require bad faith, only rational response:

- **Blocker inflation.** Every dependency becomes a formally declared blocker. Cheap, honest-looking, and it also transfers responsibility upward, which is a second reward on top of the points.
- **Default spam.** Low-value CI checks that nobody needs, because a check that fires on some violation qualifies. This one is actively harmful: it makes the build slower and noisier while paying well.
- **Deletion farming.** Removing things that were harmlessly dormant, or worse, removing things that turn out to matter.
- **Failure farming.** Cheap experiments run in order to be documented as instructive failures.
- **Decomposition theatre.** Splitting one item into many to collect the decomposition award repeatedly.
- **Criterion sandbagging.** Covered in §2 and worse than all of the above combined.

Fix direction: make the outcome term dominant and proportional rather than flat. Pay for each percentage point of ground-truth progress rather than for reaching a milestone, so a complete migration is worth roughly 1000 points and not 100. Then the cheap items become seasoning instead of the meal. Additionally cap how many times each low-effort line can be claimed per team per quarter. See P2 and P3 in §12.

---

## §5 Internal contradictions

**T1. Unplanned work earns nothing.** Rule 2 grants points only for pre-registered work. Incidents, urgent requests and firefighting are by definition not pre-registered. Under the method as written, the week a team spends saving production earns zero, while a team that had a quiet week collecting CI checks does well. This will be noticed immediately and it will be the first thing that discredits the system. Needs an explicit answer, not an exception clause.

**T2. Accountability is individual, reward is collective.** The owner's name is visible and no score sits next to it (Rule 4), which is correct as protection against scoring people. But it produces a structure where one person carries the visible risk and the group receives the reward. That is a well-known way to make ownership unattractive, and this method needs owners more than it needs almost anything else.

**T3. Per-person numbers are already required.** The metrics section says there are none, "not one". Hypothesis H2's diagnostic in PROBLEM.md counts in-progress items per person, and the whole overload argument depends on that number existing. The distinction intended is load versus performance, and it is a real distinction, but the document currently states an absolute that the method itself violates on page one.

**T4. Bottom-up adoption conflicts with the ritual that gives the method teeth.** The method claims to spread by demonstration rather than mandate, and simultaneously requires a weekly review where someone with authority reassigns work. Authority is precisely what a demonstrating team does not have over its neighbours. So the mechanism that makes it work is the mechanism that cannot spread voluntarily.

**T5. The document violates its own anti-pattern.** "A document longer than two pages does not get applied" appears in a document many times that length. It is acknowledged in the text, which is honest but not a resolution.

**T6. Quarterly repricing punishes long work.** Prices change every quarter and are not retroactive, while initiative milestones take months. A team starting a long item cannot know what it will be worth on delivery. The rational hedge is to prefer work that finishes inside the current pricing period, which is the opposite of what the method wants.

---

## §6 Unstated assumptions

**A1. Every important initiative has a constructible ground-truth number.** True for infrastructure, platform, reliability and migration work. False for most research, design, product discovery, architecture and organizational work. The method currently has nothing to say about work whose outcome is a decision rather than a state change, which is a large fraction of what senior people do.

**A2. Production instrumentation exists, is trusted, and is not owned by the team being measured.** The third part is usually false.

**A3. Work is decomposable into two-week pieces with observable outcomes.** Often true, sometimes genuinely false: some changes are atomic and only observable on completion.

**A4. The organization wants the state of work to become knowable.** This is the largest assumption in the method and it is treated as self-evident. See §7.

**A5. Cancellation is politically affordable.** Cancelling an initiative is an admission that the decision to start it was wrong, and that decision usually belongs to someone senior. The method counts cancellations as a health metric without acknowledging what each one costs the person who authorized the work.

---

## §7 Reframe: the resistance does not come from where the method expects

The method's threat model is an engineer who misreports. Look at who gains and who loses.

Engineers gain: overload becomes visible instead of being read as laziness, blockers get escalated instead of absorbed, nobody is scored individually, and reporting work largely disappears because state is derived.

The parties who lose are the ones whose position depends on ambiguity:

- a manager whose headcount is justified by an initiative that is quietly dead
- anyone who has already promised a date that the forecast will contradict
- anyone whose team's contribution looks larger in narrative than in artifacts
- whoever authorized an initiative that objective measurement will show should be cancelled

So expect the strongest opposition from above, not below. And expect it to arrive as two reasonable-sounding requests, both of which are fatal:

1. **"Let us align this with the existing goal-setting process."** This converts diagnostic metrics into targets and destroys them (Goodhart). It sounds like sensible integration.
2. **"Can we see this broken down per person?"** This is C4 dying. It sounds like sensible curiosity, and it will be asked by someone who means no harm.

The method needs a prepared answer to both, and the answer has to be structural rather than a policy: the numbers required to answer request 2 must not exist anywhere, including in intermediate outputs and CSV exports. See P5 in §12.

---

## §8 A dynamic the method creates: divergence between teams

Points buy capability. Capability increases output. Output earns points. This loop is intentional and it is the most attractive property of the design.

It also compounds, and compounding produces divergence. Two teams starting equal do not stay equal, and under the current price list the team that pulls ahead is the one doing cheap visible work, not the one doing hard important work (§4). The team carrying the multi-quarter migration accumulates the fewest points, buys the least training and the least protected time, and therefore falls further behind, while doing the work the organization most needs.

Left alone this ends in a stable bad equilibrium: strategically critical work becomes the work no team wants, because taking it means forgoing capability growth for a year.

Quantified in SIMULATIONS.md §7. Fix direction: proportional outcome pricing (P2) removes most of it, and a floor allocation independent of points removes the rest. See P6.

---

## §9 Honest positioning against existing practice

| Element | Already standard practice in | Does EDD add anything |
|---|---|---|
| Flow metrics, aging work, throughput forecasting | Kanban, Actionable Agile | No. It uses them as-is |
| Deriving state from delivery artifacts | DORA, engineering-metrics platforms | Partly. Extends it from delivery to initiative progress |
| Blameless treatment of failure | SRE practice | No, adopted directly |
| Pre-registered acceptance criteria | test-driven work, acceptance criteria in agile | Only in that it makes them a precondition for reward |
| Practices as enforced defaults | platform engineering, policy-as-code | No, adopted directly |
| Structural refusal to produce per-person data | rare, mostly informal | Yes, as an explicit design rule |
| Paying for declared blockers and documented failures | not seen elsewhere | **Yes. This is the actual contribution** |

The honest summary: roughly 80% of the method is existing practice reassembled, one part is novel and valuable (the payoff asymmetry that makes disclosure dominant), and one part is novel and dangerous (the per-action points economy, see §4).

That ratio is not a weakness for internal use. It matters if this becomes a product, because the marketing claim has to rest on the 20%, and the 20% has never been tested.

---

## §10 Staged failure modes

**Month 1.** Failure looks like: the report is generated and nobody acts on it. Cause: no escalation authority. Detection: count decisions made on flagged items. Zero after four weekly reviews means stop.

**Quarter 1.** Failure looks like: teams have learned the price list and are farming it (§4). Detection: ratio of points earned from outcome lines to points earned from all other lines. If outcome lines are below half, the price list is broken.

**Quarter 2.** Failure looks like: someone senior asks for a per-team or per-person ranking and gets one. Detection: the existence of any artifact that ranks people or teams. This one is terminal, not degraded.

**Year 1.** Failure looks like: the method still runs, the metrics are green, and nothing about delivery has improved. Cause: the metrics became the work. Detection: compare an outcome the method never measured (an independent business or reliability outcome) against the method's own numbers. If they diverge, the method is being satisfied rather than used.

---

## §11 Minimum viable subset

This answers open question 3 in METHODOLOGY.md. The full method is far more than any organization adopts at once, and the parts have very different risk profiles.

**Stage 0, week 1, requires nobody's consent.** Derive state from artifacts. Publish one list: initiatives, owner, last movement, days stalled. Change nothing else. This alone tests C1 and produces the political capital needed for everything after it.

**Stage 1, month 1, requires an owner with authority.** Add: one named owner per initiative, a countersigned acceptance criterion, the weekly review with four outcomes, and monthly cancellation. No points anywhere.

**Stage 2, quarter 2, only if stages 0 and 1 held.** Add: ground-truth progress metric per initiative and forecasting from throughput.

**Stage 3, quarter 3 at the earliest, and optional.** The contribution economy, with proportional outcome pricing.

Prediction to be checked rather than believed: stages 0 to 2 deliver most of the effect, and stage 3 carries most of the risk. If that prediction holds, the economy is a differentiator for a product and a liability for a first adoption, and those two facts pull in opposite directions.

---

## §12 Proposed changes to the method

All accepted by the author on 2026-09-07 and applied. The Fixes column points at the section above that produced each one; the last column records where it landed.

| # | Change | Fixes | Priority |
|---|---|---|---|
| P1 | Introduce an explicit definer role. Acceptance criterion, ground-truth metric and size band are proposed by the team and countersigned by the priority owner before work starts | §2, the central gap | **done: METHODOLOGY.md v0.5 Roles, plus the span limit in v0.6** |
| P2 | Replace flat milestone points with proportional outcome points (points per percentage point of ground-truth progress), making outcome the dominant term | §4, §8 | **done in ECONOMY.md R4** |
| P3 | Cap claims per low-effort line item per team per quarter | §4 | **superseded: ECONOMY.md R1 and R2 remove the sources entirely, so no cap is needed** |
| P4 | Define how unplanned work (incidents, urgent requests) is treated, rather than leaving it at zero | T1 | **done in ECONOMY.md R7**, through capacity accounting rather than an exception |
| P5 | State that data enabling per-person or per-team ranking must not exist in any output, including intermediate files and exports | T3, §7, C4 | **done: METHODOLOGY.md metrics tier 3, CONTROL.md §11** |
| P6 | Add a capability floor independent of points, so a team doing hard invisible work cannot fall below it | §8 | **done: ECONOMY.md R9** |
| P7 | Resolve the per-person contradiction explicitly: load numbers are permitted and are read by the owner of capacity, performance numbers do not exist | T3 | **done: metrics tier 2, with the claim narrowed honestly in CONTROL.md §11** |
| P8 | Give the owner of an initiative a stake matched to the visible risk they carry, or stop naming a single owner | T2 | **done differently: ownership redefined as a grant of authority rather than exposure, METHODOLOGY.md Roles** |
| P9 | Freeze prices for the duration of an already-registered item | T6 | **done: ECONOMY.md R10** |
| P10 | Add a one-page version, and demote the current document to an appendix | T5 | **done: [ONEPAGE.md](ONEPAGE.md)** |
| P11 | State the applicability boundary explicitly: work whose outcome is a decision rather than an observable state change is out of scope for now | A1 | **done: METHODOLOGY.md "Who this is for", CONTROL.md §11, with excluded work counted rather than dropped** |
| P12 | Add the two prepared answers to the predictable requests from above (goal-process integration and per-person breakdown) | §7 | **done: METHODOLOGY.md "Two requests you will receive"** |

### The second batch, from the control-instrument review

P1 to P12 came from reading the method as an incentive model. These came from asking a different question: would this actually tell you the true state of work without asking anyone. That question exposed a different class of gap, because the method verified presence thoroughly and absence not at all, while the original complaint was entirely about absence.

| # | Change | Fixes | Landed in |
|---|---|---|---|
| P13 | Coverage becomes a gate rather than one metric among several: below threshold the report is not published at all | a dashboard over an unknown share of the work converts ignorance into confidence | CONTROL.md §4 |
| P14 | Absence detectors, each a query and not a meeting | the original symptom, which no mechanism addressed | CONTROL.md §5, METHODOLOGY.md mechanism 6 |
| P15 | Decisions become verifiable artifacts, and non-execution is itself a detected deviation | the failure the problem statement predicted in advance and had no instrument for | CONTROL.md §9, the rituals |
| P16 | Three counter states, with invariant 3: unmeasured is never more comfortable than measured | missing data silently reading as unchanged, and telemetry that profitably rots | CONTROL.md §2, §6, ECONOMY.md R11 |
| P17 | Trajectory of record, and the forecast gap as the primary early warning | there was nothing to compare observations against, so the strongest available statement was "flat this week" | CONTROL.md §8 |
| P18 | Counter definitions as reviewed code with an audit trail | a definition that can change silently makes its own history meaningless | CONTROL.md §7 |

### The third batch, from the second simulation run

Written after re-running the simulations against the result. Four of these are defects in machinery from P13 to P18, and one is a defect created by P16. That is the useful signal: each mechanism that closes a hole opens a smaller one, so the test is whether the holes shrink, not whether they stop appearing. Full scenarios in SIMULATIONS.md §12.

| # | Change | Fixes | Landed in |
|---|---|---|---|
| P19 | Mapping coverage counts only items that have a criterion, both gates are published per initiative | shell items were the cheapest way to raise the headline gate number | CONTROL.md §4 |
| P20 | The definer role has a published span limit | thirty initiatives per priority owner turns the countersignature into a rubber stamp, which is self-definition that looks like rigor | METHODOLOGY.md Roles |
| P21 | Decision evidence comes from a closed list, not free text | free text reproduced the acceptance-criterion negotiation one level up | CONTROL.md §9 |
| P22 | An outage in a third party's instrument holds the allocation instead of forfeiting it, and maintaining instruments is registered, allocated work | P16 punished teams for failures they could not repair, which made the separation rule a liability they would rationally refuse | CONTROL.md §6, ECONOMY.md R11 |
| P23 | The trajectory is versioned and declared dates are published as a history | resetting the date reset the forecast gap, indefinitely and legitimately | CONTROL.md §8 |
| P24 | The tier 3 guarantee is stated in its true, narrower form | the loose form of the claim was false | CONTROL.md §11 |

---

## §13 Third pass, against the whole model

The first pass read the method as an incentive system. The second asked whether it would report the true state of work. The third (SIMULATIONS.md §12) attacked the machinery those two added. This pass asks a different question again: **taken as a whole, does this model act on the problem it was written for, and can it be operated for a quarter by the people who have to operate it.** Subject is the full set: METHODOLOGY.md v0.8, AUTHORITY.md v0.1, CONTROL.md v0.4, ECONOMY.md v0.5.

### First, coverage of the original symptom list

The most basic audit available, and it had never been run: take PROBLEM.md's nine observed symptoms and name what in the model acts on each.

| Symptom | What acts on it | Verdict |
|---|---|---|
| 1. Priorities exist and are ordered | priority owner, allocation in priority order | addressed |
| 2. Distributed tasks go nowhere | stall detector, review with four outcomes, verified execution of decisions | addressed |
| 3. Teams work on whatever is at hand | the tiebreak per contended resource, and allocation | **half addressed, see F1** |
| 4. No tracking and no reporting | artifact-derived state, the two gate numbers | addressed |
| 5. Items sit untouched for years | monthly kill, forecast gap, versioned dates | addressed in steady state, **not on day one, see F8** |
| 6. Everyone manages their own items | register, countersigned criteria, separation of definer and executor | addressed |
| 7. Some work never enters the system | mapping coverage, unmapped-change detector | addressed |
| 8. Rolling up is impossible | one bounded counter per initiative | addressed |
| 9. No objective control of any kind | the whole control layer | addressed |

Eight of nine have a mechanism pointed at them. The exception is the interesting one, and it produced the strongest finding of this pass.

### F1. There is no bound on work in progress, and the model's own diagnosis says priority means nothing without one

**Severity: high.** PROBLEM.md H2 states it plainly: priority only means something when capacity is bounded, and with fifteen concurrent items priority #1 and priority #9 move at the same speed, which is zero. The diagnostic for it exists (metrics tier 2, items in progress per person). **No mechanism anywhere sets a bound.**

Everything the model does about symptom 3 orders *what should be worked on*: the tiebreak, the allocation, the countersigned trajectory. Nothing limits *how much is open at once*. So the model can be fully adopted, every detector can be truthful, and the top priority can still crawl, because attention is divided nine ways and no artifact anywhere says so.

The second-order damage is worse than the first. Every stalled initiative under this condition reports as stalled correctly, and the review then chooses outcome 1, "continue, with a named blocker and a named person who will clear it", except there is no blocker to name. There is only division of attention, which the vocabulary of the review cannot express. The escalation machinery then fires on a blocker that does not exist, twice, and widens the audience for a problem stated in the wrong terms.

**Fix, P25.** A published bound on concurrent work in progress, per person and per team, adopted at stage 1, with a detector for breaches. It is a default rather than an instruction, it needs only the authority a discipline manager already has, it costs nothing to compute from data the instrument already reads, and it is the single cheapest lever available on the original complaint.

### F2. The acceptance criterion is still free text, which is exactly the defect that was closed one level up

**Severity: high.** SIMULATIONS.md N3 found that a free-text observable fact turned decision verification into the same negotiation the acceptance criterion used to be, and the fix was to draw decision evidence from a closed vocabulary. The same fix was never applied to the criterion itself.

As written, `done = <verifiable fact>` is prose with an example beside it. So `done = the migration is complete` passes the "item with no criterion" detector, counts toward criterion-gated mapping coverage, which is the headline gate number after N1's fix, and leaves acceptance to a human reading a sentence. That violates C3 and the method's own "manual verification" anti-pattern, and it restores §2's central finding in its residual form: the lie surface returns to definition, now with a gate number certifying it.

**Fix, P26.** Criteria come from a closed set of admissible forms: a named metric with a threshold and the query that reads it; a named CI check that must pass; the absence of a named artifact from a named inventory; a state value for every row of an inventory. The detector then checks the *form*, not the presence of the string. Work whose acceptance cannot be written in one of those forms is registered as excluded with a named owner, which the model already supports, instead of being given a prose criterion that looks compliant.

### F3. Cross-discipline initiatives are the common case, and the model's answer to them is the one it calls crude

**Severity: high in stage 3, medium below it.** METHODOLOGY.md failure mode 4 says an initiative has exactly one owner and points go to the owning team undivided, and open question 3 admits this is crude. In a chain organized by discipline, most real initiatives need two or three of those disciplines, so the crude case is not an edge, it is the default path.

Consequence: contributing teams earn nothing from most of the work they actually do. R5 does not help, because it confirms *benefit received* rather than contribution made. The rational response is to prefer initiatives your own team owns, which is precisely the fragmentation the method exists to remove, and it would be produced by the reward system rather than despite it.

**Fix, P27.** Contribution shares are declared at registration and countersigned with everything else, never computed afterwards. This works because it is a definition-time decision: it needs no attribution data, produces no per-team comparison, and a disagreement about shares surfaces before the work instead of after it, where the tiebreak already applies. Where no shares are declared, the initiative pays its owner only, and that is stated at registration so the choice is visible rather than discovered at settlement.

### F4. The date-movement measure punishes long initiatives, which are the ones the organization is failing at

**Severity: medium.** One of the four measures on the priority owner is how often declared completion dates moved. A three-year decommissioning will legitimately re-declare more often than a one-quarter change. As a raw count, the safest portfolio to hold is short initiatives, so the measure quietly reintroduces the preference for work that finishes inside the current period that R10 was written to remove, this time in the definer's incentives rather than the team's.

**Fix, P28.** Normalize to moves per initiative-quarter, exclude the first declaration, and publish the size of each move rather than only the count. A date that moved once by a year and a date that slipped two weeks four times are different facts and currently score the same.

### F5. The gate threshold is agreed by the party the gate constrains

**Severity: medium.** METHODOLOGY.md open question 7 names the risk (the threshold simply gets lowered until the report can be published) and nothing in the model answers it. "The agreed threshold" has no owner, no publication rule and no history, which makes it the softest number in a document otherwise built on refusing soft numbers.

**Fix, P29.** The threshold is set once before the first report and published, and any change to it is versioned exactly like a declared completion date, using the machinery P23 already built. Lowering it stays legitimate and stops being invisible.

### F6. Nothing detects that the instrument itself was abandoned

**Severity: medium.** Eleven detectors point at the work. None points at the operator. The realistic death of a control layer is not a wrong number, it is a quiet stop: findings accumulate unclosed, the review is skipped for three weeks, the register goes stale, and every number still published remains technically true. AUTHORITY.md §7 residual 4 names this and measures nothing.

**Fix, P30.** Two meta-detectors, computed from artifacts the instrument already holds and published beside the two gates: the age of the oldest unclosed detector finding, and whether the last review produced decision records at all.

### F7. A counter can complete while the outcome does not exist

**Severity: medium, and highest in the exact domain the model claims.** "Share of traffic served by the new path" reaches 100% while the old path is still deployed, still configured, still costing money and still able to take traffic. The counter is honest, the initiative reads complete, and nothing was decommissioned. This is Campbell's law at the level of the counter rather than the metric, and migration work is where the model says it applies best.

**Fix, P31.** Where an initiative replaces something, the criterion must include removal of the replaced state, and the counter's completion value is defined against the inventory of the old state rather than the adoption of the new one. Same shape as R2a: the denominator decides what the number means.

### F8. The first run has no design, and it is the most likely place for the model to die

**Severity: medium, and it is the nearest in time.** Three things arrive together in week 1.

- **The register does not exist,** so seven of the eleven detectors cannot run: every initiative-level detector needs a list of initiatives with owners. The adoption table says stage 0 needs nobody's consent, which is true of the code-host and tracker halves and false of this one.
- **The stall detector fires on years of backlog.** Symptom 5 guarantees it. A report with four hundred findings is ignored in exactly the way no report is ignored, and the twenty-minute review over red items only cannot absorb it.
- **Nobody has costed the operator's week,** which is F9.

**Fix, P32.** A first-run section in the control document: the register is bootstrapped by transcribing the already-published priority list, marked as transcribed rather than agreed, which needs nobody's consent and is falsifiable on sight; a one-time intake rule closes everything untouched beyond a stated age by default with a claim window, which is the monthly kill applied once at the start; and the first-run output is deliberately two numbers and one list rather than a dashboard.

### F9. The operating cost of the instrument has never been stated

**Severity: medium.** Every signal in the model has a stated detection latency, and the instrument's own weekly load has no number anywhere. An unstated cost is paid by the operator out of goodwill until the day they stop, and then everything above degrades silently rather than visibly. This matters more here than in a tool with a vendor, because the operator is one person in a chain that has no level above the priority owner to notice.

**Fix, part of P32.** State an estimate of the operator's weekly hours, publish the actual against it, and treat exceeding it as a defect in the instrument rather than as a failure of the person, exactly as a missed detection latency is treated.

### F10. Delegated countersignature invites selection, not only leniency

**Severity: low to medium.** AUTHORITY.md §4 priced reciprocal leniency between countersigners and left the prior question open: who chooses which initiatives a countersigner takes. Someone measured on date movement and decision execution prefers short, safe, well-instrumented initiatives, and the long migration ends up with whoever is least able to refuse.

**Fix, P33.** Countersignature assignment is not volunteered. It follows a stated mapping recorded in the register, by discipline or round robin, and the list per countersigner is published together with the span count.

### F11. The model has never been checked against reality once, and the cheapest possible check has not been scheduled

**Severity: high as a process defect, zero as a design defect.** Claim C1 is load-bearing: the true state of work can be derived from artifacts alone. Three passes of analysis and two simulation runs have argued about it and none of them tested it, because it cannot be tested by argument.

The test costs about a day and needs no adoption at all: take three initiatives, derive their state from artifacts, then ask the people doing the work privately what the true state is, and compare. If the two agree, C1 survives its first contact and everything downstream is worth building. If they diverge, the divergence itself is the most valuable finding this project can produce, and it arrives before anything has been built.

**Fix, P34.** The C1 comparison is the first item of the first run, ahead of any tooling, and its result is recorded whatever it says.

### F12. Accepted without change: the model is now larger than its own anti-pattern allows

The repository is about two thousand lines across nine documents, and the method's own anti-pattern list says a document longer than two pages does not get applied. ONEPAGE.md answers this for participants, and the honest statement of the shape is: one page for the many, everything else for the one person who operates the instrument. That is the correct ratio rather than a violation.

What is a real risk is the pattern of these passes themselves. Each one adds machinery, and machinery is what the operator pays for every week. So this pass ends with a stop rule rather than a proposal: **no further mechanism enters the model until the first run has produced a number.** The next document to be written should be the tooling, and the next thing after that should be a result.

### Dispositions

| # | Change | From | Severity | Landed in |
|---|---|---|---|---|
| P25 | A published bound on concurrent work in progress, per person and per team, with a breach detector | F1 | high | METHODOLOGY.md mechanism 7, CONTROL.md §5, adoption stage 1, PROBLEM.md success criterion 11 |
| P26 | Acceptance criteria come from a closed set of admissible forms, and the detector checks the form | F2 | high | METHODOLOGY.md mechanism 1, CONTROL.md §5, §7 |
| P27 | Contribution shares are declared at registration and countersigned, never computed afterwards | F3 | high | ECONOMY.md R5a, METHODOLOGY.md failure mode 4 |
| P28 | Date movement is normalized per initiative-quarter, excludes the first declaration, and publishes move sizes | F4 | medium | METHODOLOGY.md Roles, CONTROL.md §8 |
| P29 | The coverage threshold is published once and versioned like a declared date | F5 | medium | CONTROL.md §4, closes METHODOLOGY.md open question 7 |
| P30 | Two meta-detectors on the instrument itself: oldest unclosed finding, and whether the review produced decisions | F6 | medium | CONTROL.md §5, §10 |
| P31 | Where an initiative replaces something, the criterion includes removal of the replaced state and the counter is denominated against the old inventory | F7 | medium | METHODOLOGY.md mechanism 1, CONTROL.md §7 |
| P32 | A first-run design: register bootstrap by transcription, one-time backlog intake, stated operator cost | F8, F9 | medium | CONTROL.md §12 |
| P33 | Countersignature assignment follows a stated mapping and is not volunteered | F10 | low | AUTHORITY.md §4 |
| P34 | The C1 comparison against privately reported state is the first item of the first run | F11 | process | CONTROL.md §12 |

Ten findings, nine of them fixable in the documents and one (F11) fixable only by running something. The ratio worth noting: this pass found one gap in what the model *acts on* (F1), one repeat of an already-diagnosed defect at a different level (F2), one mismatch between the model's unit of work and the organization's shape (F3), and six defects in operating reality rather than in design. That is the expected profile for a model whose design has been attacked three times and whose operation has never been examined at all.

---

## Changelog

| Version | Date | What and why |
|---|---|---|
| 0.4 | 2026-09-07 | Third pass, added as §13, against the whole model rather than one document: does it act on the original symptom list, and can it be operated. Audited PROBLEM.md's nine symptoms against the mechanisms and found symptom 3 only half addressed, which produced the strongest finding of the pass: the model has no bound on work in progress although its own diagnosis (H2) says priority means nothing without one. Ten findings, P25 to P34, with fixes applied. Ends with a stop rule: no further mechanism before the first run produces a number. |
| 0.3 | 2026-09-07 | Recorded the disposition of all twelve original changes, every one of which was accepted and applied. Added P13 to P18 from the control-instrument review, which asked whether the method would report the true state of work rather than whether its incentives were sound, and P19 to P24 from the second simulation run. Sections §1 to §11 still describe v0.3 deliberately. |
| 0.2 | 2026-09-06 | Marked P2, P3 and P4 as resolved by [ECONOMY.md](ECONOMY.md), which was written directly in response to §4. P3 turned out to be unnecessary once the point sources themselves were removed. Sections §1 to §11 are left as written, so the analysis that produced the redesign stays readable. |
| 0.1 | 2026-09-06 | First analysis of METHODOLOGY.md v0.3. Central finding: the lie surface moved from state to definition, and the definer role is unassigned. Twelve proposed changes, none applied. |
