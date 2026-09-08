# The control instrument

**Version:** 0.5
**Date:** 2026-09-07
**Status:** design. Not tested.
**Relation to the rest:** this is the layer that answers "what is the true state of work" without asking anyone. It needs no points, no economy and no budget. [ECONOMY.md](ECONOMY.md) is optional and comes later, or never.

---

## §1 What control means here, and what it does not

Control in this document means exactly one thing: **comparing observed system state against a declared trajectory, computed from artifacts, with the detection of absence as the primary job.**

It is not supervision of people. The instrument is built so that it structurally cannot rank a person or a team, which is not a promise about restraint but a property of what data exists (see METHODOLOGY.md metrics, tier 3).

The distinction matters because the two goals pull apart. An instrument optimized to watch people produces better-crafted reporting, which is the failure the whole method exists to avoid. An instrument optimized to watch initiatives produces information nobody has an incentive to shape.

---

## §2 Invariant 3: unmeasured must never be more comfortable than measured

Two invariants are already stated in ECONOMY.md §2. The control layer needs a third, and it is the one most easily forgotten:

```
measured and progressing  >  measured and stalled  >  unmeasured
```

If losing your instrument is more comfortable than having one, instruments will quietly rot, and no amount of measurement design survives that. The consequences are mechanical:

- an initiative whose counter has no fresh data is reported as **stalled**, not as unknown
- an unmeasured period releases no allocation, exactly as a stalled period does not
- restoring the instrument makes the held allocation available again, so fixing telemetry is always the paying move

This is the same shape as the honesty asymmetry in ECONOMY.md R6: the option that produces information is never the option that costs you.

---

## §3 The chain, and which links were actually weak

Control is a chain, and it is worth naming every link, because the method used to verify one of them thoroughly and four of them not at all.

| # | Link | Covered before | Now |
|---|---|---|---|
| 1 | A priority exists and is ordered | no, assumed | ECONOMY.md R3 |
| 2 | The priority is decomposed into registered items with criteria | partly, no detector | §5 absence detectors |
| 3 | Each initiative has a counter with a completion value | yes, mechanism 4 | plus §7 audit |
| 4 | The counter is instrumented independently of the doer | no, a precondition only | roles in METHODOLOGY.md, §6 here |
| 5 | State is derived from artifacts with no human input | **yes, this was the strong link** | unchanged |
| 6 | Deviation is detected within a stated latency | partly, one number | §8, §10 |
| 7 | A decision follows the deviation | ritual only, unverified | §9 |
| 8 | The decision is executed | **not at all** | §9 |

The original problem statement recorded its own failure criterion as "the report is generated but no decisions are made". That is links 7 and 8, and until now the method had no instrument for either. It verified work objectively and verified decisions not at all.

---

## §4 Coverage is the first number, and it gates the rest

A dashboard over 40% of the work is not control, it is a sample, and it is a biased one: what escapes the system is precisely the work that disappears. So coverage is not one metric among seven, it is the gate.

**Two gate numbers, published above everything else:**

1. **Mapping coverage.** Share of merged changes in the period that map to a registered item **which has an acceptance criterion**. Computed from the code host, needs nobody's cooperation.
2. **Instrument coverage.** Share of registered initiatives whose counter produced fresh data within its stated latency.

**Why the criterion qualifier is in the definition and not a footnote.** Without it, the cheapest way to raise coverage is not to register real work, it is to create shell items and map changes onto them, and coverage is the headline number, so that is the first thing anyone under pressure would do. Shells have no criterion, so counting only criterion-bearing items makes the farm arithmetically useless. The two gate numbers are therefore always published together with the count of items failing the §5 detectors, and both are broken out per initiative, so a farm concentrates visibly instead of averaging into an acceptable total.

**The gate rule.** Below the agreed threshold on either number, the rest of the report is not published. Not published with a caveat, not published in grey: not published. A report that looks authoritative over unknown coverage does more damage than no report, because it converts ignorance into confidence.

**The threshold is fixed before the first report, and every change to it is versioned.** Otherwise the softest number in the instrument is the one that decides whether the instrument publishes at all, agreed by the party the gate constrains, and the predicted failure of the gate is not that anyone overrides it but that the bar drifts down until it is always cleared. So the threshold gets exactly the treatment a declared completion date gets in §8: a current value, a published history of previous values with dates, and no way to change it silently. Lowering it stays a legitimate decision, and a threshold that has been lowered three times is visible as what it is without anyone having to make the accusation.

**Excluded work is counted, not dropped.** Work legitimately outside the instrument (see §11) is listed with a named owner and appears in the coverage denominator as excluded. Otherwise coverage can be raised by declaring inconvenient work out of scope, which is the first thing anyone would try.

---

## §5 Absence detectors

The method verifies presence of artifacts well. The original symptom was absence: items never created, initiatives never decomposed, work happening outside the system. These detectors are the answer, they are individually trivial, and together they are the part of the instrument that addresses the actual complaint.

| Detector | Computed from | What it catches |
|---|---|---|
| Initiative with zero registered items | planning file plus tracker | a priority that was announced and never started |
| Initiative not decomposed below two weeks | registered items | work too large to be reportable, so nothing can be observed for months |
| Registered item with no `done =` criterion | planning file | acceptance left open to negotiation |
| Criterion present but not in one of the four admissible forms | planning file | prose acceptance, which passes a presence check and still has to be argued with a person (METHODOLOGY.md mechanism 1) |
| Items in progress above the published bound, per person or per team | transition log | the cause of stalls that no blocker explains: priority #1 and priority #9 both moving at zero speed (METHODOLOGY.md mechanism 7) |
| Initiative with no counter | planning file | progress that can only be self-reported |
| Counter with no instrument, or with no fresh data | telemetry | §2, treated as stalled |
| Initiative with no owner, or no registered escalation path | planning file | nobody to receive the deviation |
| Team with no named tiebreak for the period, or with more than one | planning file | contention for capacity that will be settled by escalation volume, which is the ordinary cause of "teams work on whatever is at hand" |
| Merged change not mapped to any item | code host | work happening outside the system |
| Registered item with no activity for 14 days | transition log, git | the ordinary stall |
| Decision recorded and not executed | decision log | §9, the failure the problem statement predicted |
| Counter definition changed mid-period | git history of the planning file | measurement history that is no longer comparable |

Every one of these is a query, not a meeting. None of them asks a human anything.

**Two of the detectors point at the instrument rather than at the work.** Every detector above watches the work, and none watches the operator, so the most likely death of this layer is invisible to it: the realistic failure of a control instrument is not a wrong number, it is a quiet stop. Findings pile up unclosed, the review is skipped for three weeks, the register goes stale, and every published number stays technically true the whole time.

| Meta-detector | Computed from | What it catches |
|---|---|---|
| Age of the oldest unclosed detector finding | the finding log | detection continuing while nothing is done with it, which is the failure criterion of the whole method applied to the instrument itself |
| A review cycle that produced no decision records | decision log | the review stopped happening, or happened and decided nothing |

Both are published beside the two gate numbers, because they say whether the gate numbers are being read by anyone.

---

## §6 Three states, never two

Every initiative and every counter reports one of three states: **progressing**, **stalled**, **unmeasured**. Two states are not enough, because a broken telemetry pipeline returning nothing looks exactly like a week of no progress, and a pipeline that turns a missing value into zero or into "unchanged" produces a calm green report over a system nobody is watching.

Rules: `unmeasured` is as loud as `stalled` in every view; it never silently inherits the previous value; and by invariant 3 it is never the cheaper state to be in.

**Instrument ownership.** The counter's instrument should be owned by someone other than the executing team (see roles in METHODOLOGY.md). Where that is genuinely impossible, the initiative is marked **self-instrumented**, that mark appears in every report about it, and it is excluded from the economy entirely. The compromise is made visible rather than forbidden, which is how this method handles every compromise: an unverifiable claim is not punished, it is simply inert.

**Whose failure an outage is.** Invariant 3 must not punish a team for an instrument it does not own, or the separation rule becomes a liability that teams will refuse. So the state is the same and the consequence is not: an outage in a third party's instrument makes the executing team's allocation **held rather than forfeited**, it becomes a blocker owned by the instrument owner, and declaring it pays the executing team under ECONOMY.md R6. Forfeiture applies only where the executing team owns the instrument itself, or where it knew the data was stale and did not say so.

**The instrument layer measures itself.** Keeping counters alive for other people's initiatives is real work, and unpaid invisible work rots. It is therefore a registered initiative like any other, with its own counter: the share of registered counters reporting inside their stated latency. Without this, the separation rule quietly asks one team for a permanent favour, and the observable consequence of an unpaid favour is that everything drifts to `unmeasured`.

---

## §7 Counter definitions are code, under review, with an audit trail

A counter whose definition can be edited silently makes all of its own history meaningless, because nobody can later reconstruct what was being measured.

- the counter's definition, its instrument and its denominator live in the planning file in git
- changing any of them is a commit with review by the priority owner
- every report shows, next to each counter, when its definition last changed
- a definition changed inside the current period flags the initiative automatically, and the period is compared on both definitions or not at all

**The denominator rule from ECONOMY.md R2a repeats here because it is the most common cheat available:** the denominator comes from a system inventory, never from a list the executing team supplied. Otherwise scope shrinks at registration, the counter honestly reaches 100%, and the real problem is untouched.

**For replacement work the denominator is the old state, not the new one.** Adoption of the new path and removal of the old one are different facts, and only the second one is the outcome. A counter denominated on adoption reaches its completion value with the replaced thing still deployed, still configured, still paid for and still able to take traffic, and it does so honestly, which makes this the most likely way a completed initiative here will turn out not to exist. So the counter counts remaining rows of the old inventory down to zero, and the criterion names the removal (METHODOLOGY.md mechanism 1). This matters most in exactly the domain the method claims: migration and decommissioning.

---

## §8 Trajectory of record, and the forecast gap

Control is comparison against something. Without a declared trajectory the strongest available statement is "flat this week", which is a fact but not a signal.

**Resolving the contradiction this creates.** METHODOLOGY.md states there are no estimates, and ECONOMY.md R3a introduced quarterly targets and a declared completion date, which is an obligation. Both survive under one distinction:

- an **estimate** is a number produced by the party that will be judged on it. Those do not exist here, and that is the part worth protecting.
- a **trajectory of record** is owned by the priority owner: start value, target per period, declared completion date. The team proposes it, the priority owner owns it, and deviation from it is the control signal rather than an accusation.

**The forecast gap, which is the strongest early warning available.** Independently of the trajectory, forecast the completion date by Monte Carlo simulation over observed throughput and counter movement. Then publish one number:

> does the forecast still intersect the declared completion date, and by how much has that gap moved this period

This is worth more than the trajectory comparison alone, because it turns "we are slightly behind each week" into a dated statement about the end, produced without asking anyone for a commitment and without anyone being able to shape it. A gap that grows for three consecutive periods is a schedule that has already failed, months before the date arrives.

**The trajectory is versioned, and the history of declared dates is published beside the current one.** The gap is measured against the current declared date, so without this the gap has no memory: attacking the forecast is weak, since it is arithmetic over observed movement, but declaring a new date is legitimate, resets the gap to zero, and can be repeated every quarter, leaving an initiative permanently on track and never arriving. Versioning does not forbid the reset, which is often the correct decision. It makes a date that has moved four times visible as what it is, without anyone having to make the accusation out loud.

**How movement is counted.** Per initiative-quarter, excluding the first declaration, with the size of each move published beside the count. A raw count makes a long initiative look worse than a short one for behaving correctly, so the party measured on it would rationally hold a portfolio of short work, which is the preference the trajectory of record exists to remove (METHODOLOGY.md Roles).

---

## §9 Closing the loop on decisions

Deviation detection is worthless if nothing follows, and the problem statement recorded exactly that as the way this fails. So decisions are treated as artifacts, with the same standard applied to them as to work.

**A decision record has four fields and cannot be saved without them:** what was decided (one of the four review outcomes), who acts, by when, and what observable fact will show it happened.

**The observable fact is not free text.** Given free text, "a comment in the item" satisfies the field, and decision verification degrades into the same negotiation the acceptance criterion used to be, one level up. Because the four outcomes are a closed vocabulary, their evidence can be enumerated too: the owner changed in the register, the critical flag was dropped, the item was closed as will-not-do, or a blocker record was created and assigned to a named person outside the team. If none of the four fits, what happened was not a decision. Verification is then a query rather than a judgement, which is the same trick the method uses everywhere else.

**Mechanics:**

- every weekly review **opens** with last period's decisions that did not execute, before any new item is discussed
- a decision not executed by its date is itself a deviation, detected by query, not by memory
- choosing "continue, with a named blocker and a named person who will clear it" twice in a row on the same blocker escalates automatically one level above the priority owner. Repeating a decision is not a decision. Where the priority owner is at the top of the chain and no such level exists, escalation instead widens the audience to the parties depending on the outcome, per METHODOLOGY.md Roles: escalation is visibility to people with an interest, and a superior is only the cheapest instance of it
- an item that passes two consecutive reviews without landing on one of the four outcomes becomes the fourth outcome automatically, which was already the rule and now has a detector behind it
- two of the four outcomes change the priority order: deferring with the flag dropped, and closing as will-not-do. The owner still chooses them, and they take effect only when the priority owner countersigns the record, within the same five working days as ECONOMY.md R3a. Otherwise the review can quietly reorder the priorities it exists to serve

**The one number that says whether control exists at all:** share of detected deviations that received a decision within one review cycle, and share of those decisions that executed by their date. If either is near zero, you do not have a control problem, you have an authority problem, and no further instrumentation will help. This is the failure criterion the problem statement wrote down in advance, now measured.

---

## §10 Stated detection latency

An instrument without a stated latency cannot be held to anything. These are targets, and missing them is a defect in the instrument, not in a person.

| Signal | Target latency | Source |
|---|---|---|
| Instrument stopped reporting | 24 hours | telemetry |
| Merged change not mapped to an item | 24 hours | code host |
| Counter not moving | 7 days | telemetry |
| Registered item with no activity | 14 days | transition log, git |
| Forecast no longer intersects the declared date | one period | computed |
| Decision not executed | next review | decision log |
| Initiative with no owner, criterion, counter or escalation path | at registration, blocking | planning file |
| Criterion not in one of the four admissible forms | at registration, blocking | planning file |
| Items in progress above the published bound | 7 days | transition log |
| A review cycle that produced no decision records | next review | decision log |
| Oldest unclosed detector finding | weekly, with the report | finding log |

---

## §11 What this instrument deliberately does not do

Stated so that nobody builds these later by accident.

**It does not measure people.** No per-person or per-team ranking exists in any output, including intermediate files and exports. Load numbers exist for capacity decisions only, are current-state only, and are visible only to whoever owns that person's capacity.

The precise form of that guarantee matters, because the loose form is false. The claim is that **the system does not produce evaluation data**, not that evaluation is impossible. Load numbers are the one deliberate hole, opened knowingly: without them every case of overload reads as a case of poor discipline, which is a worse and far more common failure. What limits the hole is that a performance narrative needs a trend, and load is current state with no history, no aggregation and no export. A determined manager can misuse any number. The defense is that misuse takes effort and leaves the misuser holding a number the instrument never endorsed.

**It does not cover work whose outcome is a decision or a change in judgment.** Research, design exploration, architecture choices. Manufacturing a counter for those produces an activity count dressed as evidence, which is worse than an honest qualitative status because it is harder to argue with. Such work is listed as excluded, with a named owner, and counted in the coverage denominator so that the coverage number stays honest.

**It does not reward prevention,** and cannot: an incident that did not happen leaves no change in system state. Prevention has to be recognized outside the instrument, deliberately and by hand.

**It does not adjudicate attribution.** If a counter moved partly for reasons unrelated to the team, that is accepted. Arguing about the split costs more than the information is worth, and the counter is finite anyway.

---

## §12 The first run

Everything above is design. This section is the first quarter, and it exists because the three things below are not design problems, which is why they were missing: they are operating problems, and operating problems are what kill instruments in month one.

**Day one is a test, not a build.** Claim C1, that the true state of work can be derived from artifacts alone, carries the entire method and has never been checked once. Argument cannot settle it. The test: take three initiatives, derive their state from artifacts only, then ask the people doing the work, privately and without showing them the derived answer, what the true state is. Compare the two.

- if they agree, C1 has survived first contact and everything downstream is worth building
- if they diverge, the divergence is the most valuable thing this project can produce, and it arrives before anything has been built

It costs about a day, needs no adoption by anyone, and it is the only available test that can fail early enough to save the effort. The result is recorded whatever it says.

**The register is bootstrapped by transcription.** Most of the detectors in §5 need a list of initiatives with owners, and no such list exists in week 1, so "stage 0 needs nobody's consent" holds for the coverage and stall halves and not for this one. The bootstrap: the operator transcribes the already-published priority list into the register, marks every row `transcribed` rather than `agreed`, and publishes it. Transcription needs no authority because it asserts nothing new, and it is falsifiable on sight, which is the fastest way to get a register corrected: a wrong owner is disputed within a day, while a missing register is never disputed at all. Rows stay `transcribed` until countersigned, and the count of each is published.

**The backlog gets a one-time intake rule.** With items untouched for years, the stall detector fires on hundreds of them in its first run, and a report with four hundred findings gets ignored in exactly the way no report gets ignored. A twenty-minute review cannot absorb that and should not try. So the monthly kill is applied once, at the start: everything untouched beyond a stated age is closed by default, with a claim window in which anyone can reopen an item by giving it an owner and a criterion. Nothing is deleted, nobody is asked to justify anything, and what survives the window is the real backlog. After that the stall detector runs normally, over a set small enough to act on.

**The operating cost is stated, and exceeding it is a defect in the instrument.** Every signal here has a stated detection latency, and the instrument's own weekly load had no number anywhere, which means it is paid out of one person's goodwill until the day they stop. The estimate, to be corrected against reality: the order of a week to set up the queries and the register, then the order of half a day per week to operate, most of it spent chasing detector findings to closure rather than computing anything. If the real figure runs above the published one, the fix is to remove mechanisms, not to absorb the difference quietly. Removal is always available: stage 0 on its own is a legitimate permanent state.

**What the first run publishes.** Two numbers, one list, one comparison: the two coverage gate numbers, the stall list after intake, and the result of the C1 test. Not a dashboard. The first run exists to establish that the numbers can be produced at all and that they match reality, and any view built before that is a view of an unvalidated number.

**And the stop rule.** No further mechanism enters the method until the first run has produced a number ([ANALYSIS.md](ANALYSIS.md) §13). Three analysis passes have each added machinery, machinery is what the operator pays for every week, and the cost of being wrong about design is now lower than the cost of being wrong about operation.

---

## Changelog

| Version | Date | What and why |
|---|---|---|
| 0.5 | 2026-09-07 | Fixes from the third analysis pass ([ANALYSIS.md](ANALYSIS.md) §13), most of which are about operating the instrument rather than designing it. §12 added, covering the first run: the C1 test on day one, since the claim the whole method rests on has never been checked and cannot be checked by argument (F11, P34); the register bootstrapped by transcription, because most detectors need a register that does not exist in week 1 (F8, P32); a one-time intake rule, because the stall detector's first run over a multi-year backlog produces a report nobody can act on; and a stated operating cost, because an unstated cost is paid by the operator until they stop (F9). §5 gained a detector for work in progress above the published bound (F1) and one for a criterion that is present but not in an admissible form (F2), plus two meta-detectors pointing at the instrument itself, since every existing detector watched the work and none watched the operator, and the realistic death of a control layer is a quiet stop rather than a wrong number (F6, P30). §4: the coverage threshold is now published and versioned like a declared date, which closes METHODOLOGY.md open question 7 (F5, P29). §7: for replacement work the counter is denominated on the old inventory, because a counter denominated on adoption completes honestly while the replaced thing is still deployed (F7, P31). §8: date movement is counted per initiative-quarter (F4, P28). |
| 0.4 | 2026-09-07 | The repeated-blocker escalation in §9 gained the audience alternative. The author stated the authority chain and the priority owner turned out to be its top, so "escalates one level above the priority owner" pointed at nobody and the loop closed on paper only. Escalation is now defined as widening the audience to the parties depending on the outcome, with a superior treated as the cheapest instance of that rather than as the mechanism itself. Also added the countersignature requirement for the two review outcomes that change the priority order, a gap found while writing [AUTHORITY.md](AUTHORITY.md): the ownership grant let the owner defer or cancel an initiative alone, so the review could reorder the priorities it exists to serve. |
| 0.3 | 2026-09-07 | Added the tiebreak detector to §5. The priority owner role assumed a single ordering existed over initiatives competing for the same teams, and in the organization this was written for the ordering is set per project, so no such thing exists. The requirement turns out to be weaker than one decisive party per organization: uniqueness per contended resource is enough, and its two failure states (no named tiebreak for a team, more than one) are queryable rather than political. |
| 0.2 | 2026-09-07 | Fixes from the second simulation run ([SIMULATIONS.md](SIMULATIONS.md) §12), four of which were defects in machinery added the same day. N1: mapping coverage now counts only items that have a criterion, because shell items were the cheapest way to raise the headline gate number, and both gates are broken out per initiative. N4: an outage in a third party's instrument holds the allocation instead of forfeiting it, since invariant 3 as written punished teams for failures they could not repair, and keeping instruments alive became a registered initiative with its own counter so the separation rule stops depending on an unpaid favour. N3: the observable fact in a decision record is drawn from a closed list, because free text reproduced the acceptance-criterion negotiation one level up. N7: the trajectory is versioned and declared dates are published as a history, because resetting the date reset the forecast gap and could be repeated indefinitely. N6: narrowed the tier 3 claim in writing to what is actually true. |
| 0.1 | 2026-09-07 | First version, written after the observation that the method verified presence of artifacts well while the original problem was absence. Adds coverage as a gate, ten absence detectors, three counter states with invariant 3, counter definition audit, the trajectory of record with the forecast gap, and verification that decisions execute. Resolves the estimate versus obligation contradiction between METHODOLOGY.md and ECONOMY.md R3a by separating an estimate from a trajectory of record. |
