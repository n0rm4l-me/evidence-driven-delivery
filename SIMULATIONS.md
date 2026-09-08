# Simulations

**Version:** 0.3
**Date:** 2026-09-07
**Subject:** METHODOLOGY.md v0.3, before [ECONOMY.md](ECONOMY.md) existed. Scenarios are left as written; resolutions are marked inline.

Thought experiments, not evidence. Each scenario states a setup, what happens without the method, what the method does, where it breaks, and what that implies for the design. Implications are cross-referenced to the proposed changes in ANALYSIS.md §12.

The scenarios are chosen to be uncomfortable. A set of simulations where the method wins every time would not be worth writing.

---

## §1 The stalled initiative

**Setup.** A migration has been in progress for fourteen months. Status reports say "in progress, on track". Three engineers are nominally assigned. The initiative has a real ground-truth number: the share of traffic on the new path, currently 12%.

**Without the method.** The initiative is reported monthly in a slide. The slide says 60% complete, because 60% of the planned tickets are closed and the remaining tickets are the hard ones. Nobody is lying: ticket count really is at 60%. The number simply does not mean what it appears to mean.

**With the method.** Two numbers are published side by side: 60% of items closed, 12% of traffic migrated. The gap between them is the finding. It takes one week to surface and it required no new reporting from anyone.

**Where it breaks.** It does not, and this is the scenario the method was designed for. Worth noting what actually did the work: not the points, not the rituals, just publishing one independently observed number next to the self-reported one. Stage 0 of ANALYSIS.md §11 would have caught this in week one.

**Implication.** The cheapest part of the method carries a large share of its value. Argues for a strictly staged rollout.

---

## §2 The engineer who has not moved anything in three weeks

**Setup.** An engineer has three critical items assigned and no movement on any of them for three weeks.

**Without the method.** Read as a discipline problem. Someone has a conversation about commitment. Nothing changes, because nothing about the situation was a commitment problem.

**With the method.** The stall list flags all three. The weekly review asks for one of four outcomes. The load number shows the engineer holds seven in-progress items across three initiatives plus on-call. The diagnosis flips from discipline to overload, and the four outcomes available include reassigning ownership and explicit deferral.

**Where it breaks.** The method needs a per-person load number to reach this conclusion, and the method also states that per-person numbers do not exist. As written, the correct diagnosis is unavailable. This is contradiction T3 and it is not cosmetic: without load data, every overload case presents as a discipline case, which is the exact failure the method exists to prevent.

**Implication.** P7. Load numbers must be explicitly permitted, scoped to the person who owns capacity, and structurally separated from anything resembling performance.

---

## §3 The team that reads the price list carefully

**Setup.** A competent team, no bad faith, told that points buy training budget and protected time for their own technical debt. They read the price list and optimize, which is what competent people do with a published incentive.

**Quarter behavior.** They deliver one pre-production milestone (30) and spend the rest of the quarter on: six CI checks (480), four deletions of dormant config (240), decomposing two initiatives into many pieces (150), eleven declared blockers (220), and three documented cheap failed experiments (120). Total 1240 points, of which 30 came from anything resembling the organization's goal.

Meanwhile the migration they own moved from 12% to 14%.

**Without the method.** They would have done roughly the same amount of real work and produced a vaguer report about it.

**Where it breaks.** Every single claim is legitimate. Every artifact exists. Verification passes cleanly. The method's own health metrics look excellent: throughput up, defaults created, blockers declared early, failures documented. The system reports success while delivery stalls, and there is nobody to blame because nobody did anything wrong.

This is the most dangerous scenario in this document, precisely because it is not adversarial. It is the predictable equilibrium of a per-action price list (ANALYSIS.md §4).

**Implication.** P2 and P3, and they are not optional. Until outcome pricing is proportional and dominant, the economy should not be enabled at all.

**Resolved.** This scenario is the reason [ECONOMY.md](ECONOMY.md) exists. The same quarter is repriced in ECONOMY.md §4: the farm drops from 1240 points to roughly 357, five of the six farming categories pay exactly zero because no counter exists behind them, and the one honest blocker declaration rises from 20 to 90 because it was a stall on the highest-priority initiative. No action had to be judged fake or unimportant for that to happen.

---

## §4 The week production burned

**Setup.** A major incident. The team spends nine days on containment, root cause and remediation. None of it was pre-registered.

**With the method.** Rule 2 grants zero points for work that was not pre-registered. The team ends the quarter behind the team that had a quiet quarter adding CI checks.

**Where it breaks.** Immediately and loudly. The first time this happens, the method loses the room, and it deserves to. Worse, the incentive it creates is grotesque: a team that has learned the rules will pre-register speculative items in order to have something to claim against when interrupted, which is paperwork invented purely to satisfy the reward system.

A tempting fix is to grant points for incident work. That is also wrong, because it pays for firefighting and therefore for a fragile system. The right shape is: incident work is not paid, and the post-incident default that prevents recurrence is paid well. That is already in the price list at 80 points, and it needs to be much higher for this class, because it is the single highest-value artifact an incident can produce.

Second necessary element: time consumed by unplanned work must be **visible as capacity loss** so that a quarter half-eaten by incidents does not read as a quarter of poor delivery.

**Implication.** P4, with the shape above rather than a blanket exception.

---

## §5 The initiative with no ground truth

**Setup.** An initiative to improve the architecture review process. Real, valuable, and there is no production metric that expresses it.

**With the method.** Mechanism 4 requires a ground-truth number. The team is asked to supply one. Under pressure to be measurable, they produce "number of reviews completed" and a dashboard for it.

**Where it breaks.** The metric is now a count of an activity, defined by the team performing the activity, displayed as objective evidence. This is self-reporting with better graphics, and it is worse than an honest qualitative status because it is harder to argue with. Within a quarter the team is optimizing review throughput, which is unrelated to review quality and probably inversely related to it.

**Implication.** P11. The method must state its boundary out loud: work whose outcome is a decision or a change in judgment is out of scope, and the correct action is to leave it outside the system rather than to manufacture a number. Also reinforces P1: if the team defines its own ground truth, the definition step has already failed.

---

## §6 The manager who does not want the initiative measured

**Setup.** A manager has four engineers justified by an initiative that has not moved in eight months. The initiative is not dead on paper. On paper it is 70% complete.

**With the method.** Stage 0 publishes the ground-truth number. The initiative shows 8% and no movement.

**What actually happens.** The manager does not object to the method. Objecting would look like objecting to transparency. Instead, over the following weeks:

- questions the metric definition, reasonably, at length
- proposes that the initiative be split into phases, of which phase 1 is complete
- suggests aligning the report with the existing quarterly goal process, so it can be reviewed properly rather than weekly
- asks, helpfully, whether the data can be broken down per person, to identify where support is needed

Three of those four requests are lethal and all four are reasonable.

**Where it breaks.** The method has no defense against reasonable requests. Its threat model is a misreporting engineer; its real opponent is an articulate stakeholder with an interest in ambiguity, and it never names that opponent (ANALYSIS.md §7).

**Implication.** P12, plus P1 (metric definitions countersigned, so relitigating them is a decision by the priority owner rather than a negotiation) and P5 (the per-person breakdown must be impossible rather than declined).

---

## §7 Two teams, four quarters: divergence

**Setup.** Team A owns a hard two-year platform migration with one deliverable per quarter. Team B owns a stream of small independent improvements. Both competent, both honest. Points buy capability, and capability increases output by roughly 15% per quarter per unit purchased.

Using the current flat price list:

| Quarter | A points | A cumulative | A capacity | B points | B cumulative | B capacity |
|---|---|---|---|---|---|---|
| 1 | 130 | 130 | 1.00 | 420 | 420 | 1.00 |
| 2 | 130 | 260 | 1.00 | 480 | 900 | 1.15 |
| 3 | 130 | 390 | 1.00 | 550 | 1450 | 1.32 |
| 4 | 130 | 520 | 1.00 | 640 | 2090 | 1.52 |

After one year team B has four times the accumulated capability, having bought training, tooling and protected time. Team A, carrying the initiative the organization considers strategic, has bought almost nothing and its capacity has not grown.

**Where it breaks.** Two ways, and the second is worse than the first.

First: the reward is inversely correlated with strategic importance.

Second and more damaging: engineers can read this table too. By quarter three, the strategic migration is the assignment nobody wants, because accepting it means a year of no capability growth. The method has made the most important work in the organization the least attractive work in the organization, without anyone intending it.

**Implication.** P2 removes most of the effect, because under proportional pricing A's migration is worth roughly 1000 points spread across its progress rather than 130 per quarter. P6 removes the residue with a floor allocation independent of points.

**Mostly resolved.** Under [ECONOMY.md](ECONOMY.md) R3, allocation follows priority, so team A's strategic migration carries the largest share of the pool and B's stream of small improvements earns only what its own registered counters are worth. The divergence inverts back to the intended direction. P6 is still worth having for a team whose counter genuinely moves slowly through no fault of its own.

---

## §8 The blocker used as a shield

**Setup.** A team is behind for ordinary reasons: the work is harder than expected. They declare a blocker on another team's dependency, which is real but not actually what is holding them up.

**With the method.** They collect 20 points, the blocker becomes a manager's metric, and their own stall is now attributed externally.

**Where it breaks.** Partially. The dependency is real, so the claim is not false, and the method deliberately does not punish. What limits the damage is the ground-truth number: the initiative still does not move, and after the blocker is cleared it still does not move. So the shield works for one review cycle and not for three.

**Assessment.** This is an acceptable failure. It costs one cycle, it is self-limiting, and hardening against it would require adjudicating intent, which would destroy the no-penalty property that makes the whole system work. Worth stating in the method that the correct response to blocker inflation is nothing, because the outcome metric already handles it.

**Implication.** No change. Document the reasoning so that a future reader does not "fix" it.

---

## §9 The innocent question that kills it

**Setup.** Quarter 2. The method is working. A director, genuinely supportive, sees the team points and asks which teams are contributing most, so that the good ones can be recognized at the all-hands.

**With the method.** The data exists. Team totals are the entire basis of the economy, so a team ranking is one sort away.

**What happens next.** Recognition is given. Within a quarter, teams are managing their point totals rather than their systems. One quarter after that, someone asks for the same view per person, because a team is only as good as its members. C4 is now false, and every honest disclosure line in the price list inverts: declaring a blocker becomes an admission of weakness in a ranked comparison.

**Where it breaks.** The method's protection against this is a stated principle, and stated principles do not survive contact with an org chart. Team-level aggregates are inherently rankable, which means the economy carries the seed of its own destruction in a way the observability layer does not.

**Implication.** P5, and a hard consequence worth stating plainly: the contribution economy is structurally less safe than the rest of the method. That is another argument for ANALYSIS.md §11's staging, where the economy arrives last and only if everything before it held.

---

## §10 The pilot succeeds and does not spread

**Setup.** One quarter, one initiative, good results. Stalls surfaced, two items cancelled, a forecast that turned out accurate. The team likes it, mostly because they stopped writing status reports.

**With the method.** The plan was for other teams to copy it because it removes work for them.

**What happens.** One team copies it. Four do not. The reason is not resistance to the idea: adopting it requires their manager to accept that their initiatives become measurable in public, and that is a cost paid by the manager while the benefit accrues to the engineers. So the answer is "interesting, let us look at it next quarter", indefinitely.

**Where it breaks.** Contradiction T4. Demonstration spreads a practice when the adopter captures the benefit. Here the adopter and the beneficiary are different people.

**Implication.** For internal use, accept that spread requires a mandate at some point and plan the moment deliberately. For a product, this is the central go-to-market problem: the buyer is the person whose ambiguity gets removed. Worth recording as the primary commercial risk.

---

## §11 What the simulations changed

| Scenario | Verdict | Change implied |
|---|---|---|
| §1 stalled initiative | method works, and the cheapest part did the work | staged rollout |
| §2 stalled engineer | fails as written, cannot diagnose overload | P7 |
| §3 team reads price list | fails badly, no bad faith required | P2, P3, do not enable economy first |
| §4 incident week | fails and discredits the system | P4 |
| §5 no ground truth | fails, produces a fake metric | P11, P1 |
| §6 manager resists | fails, no defense against reasonable requests | P12, P1, P5 |
| §7 divergence | fails, inverts strategic priority | P2, P6 |
| §8 blocker as shield | acceptable failure, self-limiting | none, document why |
| §9 innocent ranking question | fails, terminal | P5, economy last |
| §10 pilot does not spread | fails, and it is the commercial risk too | accept mandate, record risk |

Seven of ten scenarios fail as the method is currently written, and one thing accounts for four of them: the contribution economy. The observability and ritual layers hold up in every scenario except §2, which is a documentation contradiction rather than a design flaw.

That is the most useful output of this exercise: **the part of the method that is novel is also the part that fails most of the simulations, and the part that is borrowed is the part that works.** For internal adoption this argues for shipping the borrowed part first. For a product it is a warning, because the novel part is the only thing that would differentiate it.

**Status after ECONOMY.md.** §3, §4 and §7 have been addressed by redesigning the economy rather than by patching prices. §5 and §6 depend on the definer role (P1), which ECONOMY.md assumes but METHODOLOGY.md has not yet adopted. §2 and §9 are untouched and remain the two most dangerous open items, and they are dangerous in the same way: both are about per-person and per-team numbers existing at all. Neither is a pricing problem, so neither can be fixed by pricing.

---

## §12 Second run, against METHODOLOGY.md v0.5

Everything above was run against v0.3. This section re-tests it against the current method (v0.5 plus [CONTROL.md](CONTROL.md) and [ECONOMY.md](ECONOMY.md) v0.2), and then attacks the machinery that was added, which is the part with no evidence behind it at all.

### The ten original scenarios, re-tested

| Scenario | Then | Now | What carries it |
|---|---|---|---|
| §1 stalled initiative | passed | passes | unchanged, and still the cheapest part of the method |
| §2 stalled engineer | **failed**, overload undiagnosable | **passes** | metrics tier 2: load exists, is current-state only, and is read by whoever owns capacity |
| §3 team reads the price list | **failed badly** | **passes** | ECONOMY R1, R2, R4: five of six farming categories have no counter behind them and pay nothing |
| §4 incident week | **failed**, zero for saving production | **passes** | ECONOMY R7: unplanned work reduces available capacity rather than looking like poor delivery |
| §5 no ground truth | **failed**, produced a fake metric | **passes** | the boundary is now explicit: such work stays outside the instrument and is counted as excluded |
| §6 manager resists measurement | **failed**, no defense | **partly** | counter definitions are countersigned and audited, so relitigating one is a decision by the priority owner rather than a negotiation. His fourth request is answered in advance. But see N7: the phase-split request is still available |
| §7 divergence between teams | **failed**, inverted priority | **passes** | ECONOMY R3 allocation follows priority, R9 floor catches the residue |
| §8 blocker as a shield | acceptable | acceptable | unchanged, self-limiting, deliberately not hardened |
| §9 innocent ranking question | **failed, terminal** | **passes structurally** | tier 3: no cross-team table exists, earnings are not rendered side by side, R8 is one org-wide number. See N6 for the one remaining hole |
| §10 pilot does not spread | failed | **unchanged** | still true, and now honest: stage 1 and up need authority, which is stated rather than wished away |

Nine of ten now hold, against three of ten before. The two that do not are §10, which is a fact about organizations rather than a design defect, and the residue of §6 and §9 examined below.

### N1. The coverage gate gets farmed

**Setup.** Coverage is 62%, the threshold is 80%, and the report is therefore not published. Someone wants it published.

**What happens.** The cheapest path is not to register real work, it is to create shell items and map changes onto them. Mapping coverage reaches 95% in a week.

**What holds.** Shell items have no counter and no criterion, so instrument coverage does not move, and three absence detectors light up at once: items with no `done =`, initiatives with no counter, initiatives not decomposed.

**What breaks.** Mapping coverage on its own is farmable, and it is the headline number. Publishing it alone would be worse than publishing nothing, which is exactly the failure the gate exists to prevent.

**Fix applied.** Mapping coverage counts only changes mapped to items that have a criterion, and both gate numbers are published together with the count of items failing the detectors. Coverage is also reported per initiative, so a shell farm concentrates visibly instead of averaging out.

### N2. The definer becomes a rubber stamp

**Setup.** One priority owner, thirty initiatives, each needing a countersigned criterion, counter and trajectory.

**What holds.** R3a keeps work from being blocked: after five days an item may start provisionally, with no allocation, and the delay escalates.

**What breaks.** Not the queue, the attention. With thirty initiatives the countersignature takes a minute each and becomes a signature on whatever the team proposed. Self-definition is restored, now with a formal approval on top, which is worse than the honest original because it looks like rigor. This is the same pathology as criterion sandbagging, moved one level up.

**Fix applied.** The definer role has a stated span limit. Beyond roughly ten concurrent initiatives per priority owner the role is nominal and must be split, and the number of initiatives per priority owner is itself published. A role whose capacity is not bounded is not a control, it is a formality.

### N3. Decision records become a checkbox

**Setup.** Decisions now require four fields: what, who, by when, and the observable fact.

**What happens.** Teams learn to fill them satisfiably. "Who: me. By when: next week. Observable fact: a comment in the item."

**What holds.** Repeating outcome 1 twice escalates, and the share of decisions executed by their date is public.

**What breaks.** With a free-text observable fact, decision verification degrades into the same negotiation the acceptance criterion used to be.

**Fix applied.** The observable fact is not free text. The four outcomes are a closed vocabulary, so their evidence can be enumerated: owner changed in the register, critical flag dropped, item closed as will-not-do, or a named blocker record created and assigned to a named person outside the team. Anything else is not one of the four outcomes. Because the vocabulary is closed, verification is a query.

### N4. Nobody wants to own instruments for other teams

**Setup.** The separation rule requires the counter's instrument to be owned by someone other than the executing team. In practice this lands on a platform team: thirty counters to keep alive, no allocation for the work.

**What happens.** Instruments rot. Initiatives go `unmeasured`. Under R11 unmeasured releases no allocation, so the executing team loses its allocation because of a failure it does not own and cannot repair.

**What breaks.** This is a defect introduced by the fix, not by the original design. R11 was written to stop teams hiding behind broken telemetry, and as written it also punishes teams whose telemetry was broken by someone else.

**Fix applied.** Two parts. First, when the instrument owner is a third party, an outage makes the allocation **held rather than forfeited**, it becomes a blocker owned by the instrument owner, and declaring it pays the executing team under R6. Second, keeping instruments alive is itself a registered initiative with its own counter, the share of counters reporting inside their stated latency. The measurement layer measures itself, and the work of maintaining it becomes visible and paid instead of being a favour.

### N5. Unmeasured as a hiding place

**Setup.** A team would rather not be measured and simply stops maintaining its counter.

**Verdict.** Closed. Invariant 3 and R11 make unmeasured cost exactly what stalling costs, and restoring the instrument releases what was held, so visibility is always the paying move. The variant where a team makes the counter noisy instead of absent is caught by the definition audit in CONTROL.md §7, since every definition change is a reviewed commit and a changed definition mid-period flags the initiative automatically.

The one honest caveat is N4: this only works when the team can actually repair its own instrument.

### N6. The load view leaks into a performance review

**Setup.** Tier 2 exists: items in progress per person, visible to whoever owns that person's capacity. A manager screenshots it into a performance conversation.

**Verdict.** Nothing in the method prevents this, and nothing can. This is the one deliberate hole in the tier 3 guarantee, and it was opened knowingly, because without load data every case of overload reads as a case of poor discipline, which is a worse failure and a more common one.

**What limits it.** Current state only, so there is no trend, and a performance narrative needs a trend. No aggregation, no history, no export.

**What this costs the method's claim.** The honest version of the guarantee is narrower than originally written: the system does not produce evaluation data, which is not the same as making evaluation impossible. A determined manager can misuse any number. The defense is that misuse requires effort and leaves the misuser holding a number the system never endorsed.

### N7. The forecast gap is politically explosive

**Setup.** Month 2. The forecast says the declared completion date misses by seven months. It is computed from observed throughput, published, and contradicts a date a director has already promised outside the organization.

**What happens.** Attacking the forecast's method is available but weak, since it is arithmetic over observed movement. The effective move is legitimate and repeatable: declare a new trajectory. The gap resets to zero. Do it every quarter and the initiative is permanently on track while never arriving. This is the phase-split request from §6, in its most defensible form.

**What breaks.** The forecast gap measures deviation from the current declared date, so a system that lets the date move has no memory.

**Fix applied.** The trajectory is versioned and the history of declared completion dates is a first-class artifact published beside the current one. A date that has moved four times is not a schedule, and the report says so without anyone having to make the accusation. Resetting remains legitimate, and it stops being free.

### What the second run changed

| Finding | Severity | Disposition |
|---|---|---|
| N1 mapping coverage is farmable with shell items | high, it is the headline number | fixed: criterion-gated coverage, both gates published together, per-initiative breakdown |
| N2 the definer role has an attention limit | high, silently voids the main fix | fixed: stated span limit, published load per priority owner |
| N3 free-text decision evidence | medium | fixed: closed outcome vocabulary implies enumerable evidence |
| N4 R11 punishes teams for other parties' instrument failures | high, introduced by the previous fix | fixed: held not forfeited, plus the instrument layer measures itself |
| N5 unmeasured as a hiding place | closed | no change needed |
| N6 the load view can be misused | accepted | claim narrowed in writing rather than defended |
| N7 the declared date can be reset indefinitely | high | fixed: versioned trajectory, published date history |

Four of the seven new findings are defects in machinery that was added in the same session, and one of them (N4) was created by a fix. That ratio is the useful signal here: every mechanism added to close a hole opens a smaller one, so the method should be judged by whether the holes shrink, not by whether they disappear.

The pattern across both runs is consistent. Every failure traces to one of three things: a number defined by the party it measures, a state that is cheaper than being visible, or a decision nobody verified. Those are worth treating as the standing test for any future addition.

---

## Changelog

| Version | Date | What and why |
|---|---|---|
| 0.3 | 2026-09-07 | Second run, added as §12. Re-tested all ten original scenarios against METHODOLOGY.md v0.5 with [CONTROL.md](CONTROL.md) and ECONOMY.md v0.2: nine now hold against three before, with §2 and §9 closed by the metric tiers. Added seven new scenarios attacking the mechanisms added in v0.5, of which four found real defects and one (N4) found a defect created by a fix. All seven dispositions applied to METHODOLOGY.md v0.6, CONTROL.md v0.2 and ECONOMY.md v0.3. Scenarios §1 to §11 left unchanged. |
| 0.2 | 2026-09-06 | Recorded the resolution of §3, §4 and §7 by [ECONOMY.md](ECONOMY.md), and noted in §11 that §2 and §9 remain open because they are about the existence of per-person and per-team numbers, not about pricing. Scenarios themselves left unchanged. |
| 0.1 | 2026-09-06 | Ten scenarios against METHODOLOGY.md v0.3. Seven fail as written; four of those trace to the contribution economy. |
