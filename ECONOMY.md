# The contribution economy, closed form

**Version:** 0.6
**Date:** 2026-09-07
**Status:** design. Not tested. Supersedes the starter price list in METHODOLOGY.md v0.3.
**Stage:** this is stage 3 of the adoption order and it is optional. Everything in [CONTROL.md](CONTROL.md) works without any of it. Do not start here.
**Depends on:** the Roles section of METHODOLOGY.md, adopted in v0.5. Every rule below assumes that criteria, counters and allocations are set by someone other than the earning team.

This document exists for one reason: the starter price list could be farmed with fake or low-importance work, and that could not be fixed by adjusting numbers. The design below is intended to make farming arithmetically impossible rather than forbidden.

---

## §1 Why the per-action price list cannot be repaired

The starter price list paid a flat amount per completed action: 80 for a default, 60 for a removal, 20 for a declared blocker. Three properties follow from that shape alone, independently of the numbers chosen:

1. **The claimant controls supply.** A team decides how many qualifying actions to produce. If each action pays a fixed amount, points are limited only by how many cheap qualifying actions exist, and cheap qualifying actions are unlimited in any real system.
2. **Cheap actions dominate.** Points divided by effort favours whatever is quickest to complete. Real outcomes are never quick, so the organization's actual goal is always the worst-paying item on the list (measured in ANALYSIS.md §4: delivering the outcome paid roughly 5 points per day, declaring a blocker roughly 400).
3. **Importance is not represented.** A price list of action types cannot distinguish a removal that matters from a removal that does not, because both produce the same artifact.

Adjusting the numbers changes nothing about any of the three. Any scheme in which the earner controls how many payable units exist will be farmed by rational people acting in good faith. So the shape has to change, not the calibration.

---

## §2 The two invariants

Everything below is machinery for enforcing these. If a rule ever conflicts with an invariant, the rule is wrong.

**Invariant 1: the ordering.** For any team, over any period:

```
deliver the outcome  >  disclose a blocker or a failed approach  >  silence  =  unverified claim  =  0
```

Delivery must pay strictly the most, disclosure must pay strictly more than nothing, and silence and false claims must both pay exactly zero with no penalty attached. The starter price list violated the first relation, which is the whole defect.

**Invariant 2: no self-owned point source.** Every point issued must trace to a counter that is defined, instrumented and owned by someone other than the team earning it, and whose remaining distance to completion is finite and known.

Invariant 2 is the anti-farming rule, and it yields a single test to apply to any proposed point source:

> Can this team increase its points without moving a number that someone else defined and bounded?

If yes, the source is farmable and must not exist. This test is what the starter price list failed on eight of nine rows.

---

## §3 The rules

**R1. The pool is fixed before the period begins.**
Total points issued per quarter are set in advance and do not depend on how many items are created, closed, or claimed. The pool scales only with available team capacity (see R7), never with activity.

Consequence: creating work cannot create points. A team that invents twenty items has not added a single point to the system; if any of those items were to receive an allocation, it could only come out of allocations to real priorities, and only the priority owner can do that. Fake work stops being a policy violation and becomes arithmetic that does not work.

**R2. A point source must be a bounded counter owned by someone else.**
Each initiative registers exactly one counter expressing target system behavior, with a start value, a completion value, an owner who is not the earning team, and an instrument that produces the number without human entry. No point source may exist outside a registered counter.

**R2a. The denominator comes from an inventory, not from a list.**
"Share of services meeting the policy" must be computed against the discovered set of services from a system inventory, never against a list of services the team supplied. Otherwise scope can be shrunk at registration and 100% can be reached while the real problem is untouched. This is the most commonly available cheat in any migration and closing it costs one query.

Consequence: point sources are finite. The ceiling on what any initiative can ever pay equals the real work remaining in it, so there is nothing to farm past that point.

**R3. Allocation happens before execution and is done by the priority owner.**
Before the quarter, the priority owner divides the pool across registered initiatives in priority order, and countersigns for each one: the acceptance criterion, the counter, the quarter's target value, and the declared completion date. The team proposes; the priority owner decides.

**R3a. The countersignature has a deadline, and work is never blocked by it.**
If the priority owner has not countersigned within five working days, the item may start as **provisionally registered** and the delay escalates one level above the priority owner, or, where no such level exists, to the outside audience defined in METHODOLOGY.md Roles. Provisional registration carries no allocation, so the definer cannot be bypassed and cannot become a reason not to work either. Without this rule the definer role turns into a queue, and the rational response to a queue is to start unregistered, which destroys coverage.

**R3b. Targets and dates are coupled.**
The sum of an initiative's quarterly targets must reach completion by its declared date. Lowering this quarter's target therefore requires either raising a later one or moving the declared completion date in public.

Consequence: sandbagging is still possible, but it can no longer hide. It becomes an explicit statement that the initiative will take longer, made by the priority owner rather than by the team, in front of whoever cares about the date.

**R4. Release is proportional to counter movement, with no lumps.**
An initiative's quarterly allocation is released in proportion to how far its counter moved toward the quarter's target. No flat fees, no milestone bonuses, no payment for reaching a stage.

Consequence: partial progress is credited honestly, and there is no threshold to game around. Also no reason to hold a finished change back to land it in a better quarter.

**R5. Cross-team benefit is confirmed by the beneficiary, out of a fixed pool.**
Where an outcome is claimed to benefit another team, that team confirms it. Because the pool is fixed, a team that confirms a benefit it did not receive is giving away a share of a pool it competes for.

Consequence: collusion is possible but no longer free. It has a price, paid by the colluder.

**R5a. Where more than one team executes, the shares are declared at registration.**
Paying the owning team in full and undivided holds while cross-team initiatives are the exception. Where teams are organized by discipline they are the rule, so contributing teams earn nothing for most of the work they actually do, and the rational response is to prefer initiatives your own team owns, which fragments delivery in exactly the way this method exists to stop.

So the split is part of what gets countersigned under R3: the executing teams propose shares of the initiative's allocation, the priority owner countersigns them alongside the criterion, the counter, the target and the date, and release under R4 divides by those shares. Where no shares are declared, the initiative pays its owner alone, and that is recorded in the register at registration rather than discovered at settlement.

Three properties make this the cheap version. It needs no attribution data, because it is a statement of intent before the work rather than a measurement after it. It produces no comparison between teams, because shares belong to one initiative and are never summed into a table (METHODOLOGY.md metrics, tier 3). And a disagreement about shares surfaces before work starts, where the tiebreak already applies, instead of at settlement, where nothing does.

Consequence for farming: shares are frozen for the period exactly as allocations are under R10, so no team can claim a larger share of an initiative once it turns out to be moving.

**R6. Disclosure is paid out of the initiative's own allocation, as a fraction of the progress not made.**
Two cases, both requiring a prior public commitment that the team stands to lose:

- **Declared blocker.** When a team declares a blocker on a registered initiative, the allocation for the progress it will now fail to make is held, and 25% of the held amount is released immediately to the declaring team. The remainder is released if the blocker is cleared and progress resumes.
- **Retired approach.** When a team establishes that the registered approach does not work and records which default changes as a result, 40% of the initiative's remaining quarterly allocation is released, the approach is re-registered, and the total scope and counter stay unchanged.

Consequence, and this is the part that makes the model work: the disclosure payment scales with the importance of what is stalled, because it is a fraction of the allocation, and allocations follow priority. Stalling the top-priority initiative pays the most to say so, immediately, which is exactly the behavior the whole method is trying to buy.

Consequence for farming: neither payment can be manufactured. A blocker with no registered stall behind it pays zero, and a team can only fail to make a given quarter's progress once. Retiring an approach pays less than delivering it and leaves the team owning the same scope, so faking a failure buys 40% and forfeits the other 60% of work it must still do.

Neither payment adds to the pool. Both are drawn from the initiative's own allocation, so R1 is preserved exactly.

**R7. The denominator is available capacity, not items.**
Allocations and all reporting are expressed per team-week of available capacity. Time consumed by unplanned work (incidents, urgent external requests) reduces available capacity for the period.

Consequence: a quarter half-consumed by an incident reads as a quarter with half the capacity, not as a quarter of poor delivery, and nobody has to invent a reward for firefighting to make the numbers fair. Preventing recurrence pays through R2 as a registered counter, which is the correct place for it.

**R8. The invariant is measured every quarter, not assumed.**
Compute the share of issued points traceable to movement, or documented non-movement, of a counter the earning team does not own. The target is 100%. Anything below it names a leak, and the leak is a design defect to be found and closed, never a person to be corrected.

The result is a single organization-wide number. It is never computed per team, because a per-team version of it is a ranking, and a ranking is the one artifact that must not exist (METHODOLOGY.md metrics, tier 3).

**R9. A capability floor exists independently of points.**
Every team receives a minimum allocation of protected time and training regardless of what it earned. Without a floor, a team whose counter genuinely moves slowly, and multi-quarter platform work is exactly that, loses capability every quarter while doing the work the organization most needs, and the most important assignment in the organization becomes the one nobody wants.

**R10. Allocations are frozen for the duration of a registered item.**
An item registered under one allocation is settled under that allocation, even if the next period reprices its initiative. Otherwise a team starting long work cannot know what it will be worth on delivery, and the rational hedge is to prefer work that finishes inside the current period, which is the opposite of what any of this is for.

**R11. Unmeasured is never cheaper than measured, and the cost lands on whoever owns the instrument.**
An initiative whose counter has no fresh data releases no allocation, exactly as a stalled one does not, and the withheld amount becomes available again when the instrument is restored. This is invariant 3 in CONTROL.md §2, and it exists because a reward system that quietly pays teams whose telemetry broke will get telemetry that stays broken.

Attribution is part of the rule rather than a refinement of it. Where the instrument belongs to a third party, the executing team's allocation is **held, not forfeited**, the outage is a blocker owned by the instrument owner, and declaring it pays the executing team under R6. Forfeiture applies only where the executing team owns the instrument, or knew the data was stale and did not say so. Written without that clause, R11 penalizes a team for a failure it cannot repair, and the rational response is to refuse the separation rule that created the dependency.

Consequence for the instrument owner: maintaining counters is registered work with its own counter (CONTROL.md §6), so it is allocated and released like anything else. An organization that will not pay for its own measurement layer does not get one, and that is better learned at allocation time than six months later.

**R12. Redemption is not discretionary, and the budget is not new money.**
Points convert against a catalogue agreed before the period begins: training, conference attendance, hardware, licenses, tools, an extra environment, protected time for work the team chooses. Conversion inside the catalogue needs no second approval. The budget owner funds the pool before the period and does not approve individual purchases.

This is the rule that decides whether stage 3 is real. If each purchase can be refused on its merits, points are a promise rather than a currency, teams price them at zero inside one quarter, and invariant 1 collapses silently: disclosure was still the highest-paying action, but the payment was worthless. A budget owner who cannot commit before the period should not start stage 3 at all.

Two practical consequences worth stating, because they change who needs to agree to any of this:

- **No new budget is required.** Almost every organization already has a discretionary capability budget handed out on request with approval. Stage 3 does not ask for more money, it asks that an existing budget be allocated by what was earned instead of by who asked. That is a much smaller thing to negotiate.
- **The cheapest currency is protected time, and it costs nothing.** The capability floor in R9 is denominated in time, not money, so the minimum viable budget owner is whoever can grant a team uninterrupted time. That party is usually the same manager who owns capacity, and it is legitimate for the budget owner and the priority owner to be the same person: the separation rule covers {defines, executes, instruments} only. Where they do coincide, R12 matters twice as much, because the same party then sets the allocation and holds the means of honouring it.

---

## §4 The farming quarter, repriced

The same team as SIMULATIONS.md §3, same behavior, no bad faith. Under the old price list they earned 1240 points, of which 30 related to the organization's goal.

Setup under this design: five teams, pool of 5000 for the quarter, allocated by the priority owner before it starts. This team owns initiative I1 (the top priority migration, counter at 12%, quarter target 30%, allocation 2000) and contributes to I3 (policy conformance, allocation 900).

| What they did | Old | New | Why |
|---|---|---|---|
| Migration moved 12% to 14% | 30 | **222** | 2000 x (14-12)/(30-12) |
| Six CI checks, one of which moves I3's counter by 5% | 480 | **45** | five are attached to no counter and pay nothing; one earns its share of I3 |
| Four deletions of dormant config | 240 | **0** | no registered decommission counter, so no source exists |
| Decomposing two initiatives | 150 | **0** | decomposition is a precondition for registration, not a payable outcome |
| Eleven declared blockers | 220 | **~90** | one registered stall on I1, paid as 25% of the held allocation; the other ten have no stall behind them |
| Three cheap documented failures | 120 | **0** | none of them was the registered approach |
| **Total** | **1240** | **~357** | |

Two things to notice. First, the farm collapsed on its own without anyone judging any single action to be fake or unimportant: five of the six categories pay zero because no counter exists behind them. Second, the one honest disclosure now pays 90 rather than 20, because it was a stall on the highest-priority initiative in the organization.

Compare a team that actually delivered: I1 from 12% to 30% releases the full 2000. Delivery pays roughly six times the entire farming quarter. Invariant 1 holds.

---

## §5 What is still open

Stated plainly, because a closure document that claims completeness is the least trustworthy kind.

**1. Instrument capture.** If the earning team owns the telemetry that produces its counter, the counter is self-reported with extra steps. Pricing cannot fix this, so it is handled structurally instead: the separation rule in METHODOLOGY.md forbids the collapse, and where the collapse is genuinely unavoidable the initiative is marked `self-instrumented` in every report about it and is excluded from the economy. What remains is that someone has to notice the marking, which is a human step and therefore a real residual.

**2. Definer capture.** A priority owner who is generous to a favoured team, or who is measured on the same initiative, can allocate their way to a good-looking result. The fixed pool prices this (generosity to one initiative visibly starves their others) but does not remove it. Residual risk, and it moves the integrity requirement from many engineers to one role, which is a smaller surface but a more concentrated one.

**3. Prevention still pays nothing.** An incident that never happened, an argument that stopped a bad design, a colleague unstuck in a corridor. Unchanged from METHODOLOGY.md failure mode 1, and not improved by anything here. The honest position: this model measures change in system state and prevention leaves none, so prevention has to be recognized outside the economy, deliberately and by hand.

**4. Initiatives with no constructible counter.** Out of scope by construction now, rather than served badly. See ANALYSIS.md change P11.

**5. Counter movement caused by someone else.** If a counter moves for reasons unrelated to the team's work, the allocation is released anyway. Left unaddressed on purpose: adjudicating attribution costs more than the points, and the failure is self-limiting because the counter is finite.

**6. Every number here is arbitrary.** The pool size, the 25%, the 40%. The shape is the claim; the calibration is not.

**7. Declared shares can be wrong.** A team that ends up doing much more than its declared share under R5a is still paid the declared one, because revising shares mid-period reopens the attribution argument the declaration exists to avoid. The correction available is the next period's declaration. This is a deliberate trade: a known mispricing recorded in the register before the work beats an unresolvable argument after it.

---

## Changelog

| Version | Date | What and why |
|---|---|---|
| 0.6 | 2026-09-07 | Added R5a after the third analysis pass ([ANALYSIS.md](ANALYSIS.md) §13 F3) found that the crude answer to shared initiatives was also the common path: in a chain organized by discipline most initiatives need two or three disciplines, so paying the owner undivided left contributing teams earning nothing for most of their real work, and the rational response to that is to prefer initiatives your own team owns, which is the fragmentation the method exists to remove. Shares are now declared at registration and countersigned with everything else, never computed afterwards, which needs no attribution data and produces no comparison between teams. Residual 7 records the price of that choice: a share declared wrong stays wrong until the next period. |
| 0.5 | 2026-09-07 | R3a gained an alternative for the case where no level exists above the priority owner. The author stated the actual authority chain, and the priority owner sits at the top of it, so the countersignature deadline escalated to a level that does not exist and the rule silently had no enforcement. The delay now escalates to the outside audience defined in METHODOLOGY.md Roles instead. |
| 0.4 | 2026-09-07 | Added R12 after the author asked who the budget owner should be, which exposed that the whole document specified how points are issued and never specified how they are honoured. If each purchase can be refused on its merits, points are a promise rather than a currency, teams price them at zero within a quarter, and invariant 1 collapses silently: disclosure is still nominally the highest-paying action while the payment is worthless. R12 also records the two things that make stage 3 affordable, namely that no new budget is required (an existing discretionary capability budget stops being allocated by request) and that the cheapest currency is protected time, which costs nothing. |
| 0.3 | 2026-09-07 | Fixed R11 after the second simulation run (SIMULATIONS.md §12 N4) found that it punished a team for an instrument outage it neither owned nor could repair, which made the separation rule a liability teams would rationally refuse. Outages in a third party's instrument now hold the allocation rather than forfeiting it, and maintaining the measurement layer became registered, allocated work. |
| 0.2 | 2026-09-07 | The definer role this document depended on was adopted into METHODOLOGY.md v0.5, so the conditional dependency is resolved. Added R3a (countersignature deadline with provisional registration, because a definer without a deadline becomes a queue and the response to a queue is to start unregistered), R9 (capability floor, so slow-moving strategic work does not starve), R10 (allocations frozen for registered items), R11 (unmeasured is never cheaper than measured). Restricted the R8 invariant check to a single organization-wide number, because a per-team version of it is a ranking. Marked the whole document as optional stage 3. |
| 0.1 | 2026-09-06 | First closed form of the economy, written in response to the farming loophole found in ANALYSIS.md §4 and SIMULATIONS.md §3. Replaces per-action pricing with a fixed pool allocated against bounded, externally owned counters, because any scheme where the earner controls the supply of payable units can be farmed by rational people in good faith. Resolves P2 and P3, and resolves P4 through capacity accounting rather than through an exception for unplanned work. |
