# Authority: who holds which role, and what each level may do

**Version:** 0.2
**Date:** 2026-09-07
**Status:** design. Not tested.
**Relation to the rest:** [METHODOLOGY.md](METHODOLOGY.md) Roles states what the four roles must satisfy. This document assigns them to an ordinary reporting chain, enumerates what each level may and may not do, and then checks every authority-dependent mechanism in the method against that assignment. If the two disagree, METHODOLOGY.md wins and this document is the defect.

---

## §1 The chain this assumes

Four levels above the teams, described by function rather than by title, because titles differ per organization and the method is neutral about them. Substitute your own names; what matters is the function in the middle column.

| Level | Function | Authority it actually has |
|---|---|---|
| **L1** | owns the capacity of several teams, top of the chain | can interrupt work already in progress, and does |
| **L2** | delivery across several initiatives, reporting to L1 | influence, coordination, no capacity authority |
| **L3** | delivery of one initiative or a few, reporting to L2 | influence inside an initiative, no capacity authority |
| **L4** | managers of the discipline teams, one per discipline (for example engineering, reliability, quality) | assignment inside their own discipline |
| **L5** | the teams | do the work |

Two properties of this shape decide everything below. It is **vertical**: L1 sits above the executing teams in a single line. And L1 is the **top**: there is no level above to receive an escalation. Both are the common case, and both are handled explicitly rather than assumed away.

---

## §2 The assignment

| Method role | Held by | Why not the others |
|---|---|---|
| **Priority owner** | **L1**, with per-initiative countersignature delegated to L4 as described in §4 | L2 and L3 fail check 1: they influence capacity rather than command it, and appointing them alongside L1 recreates the negotiation the role exists to end. L4 alone would be the forbidden collapse for its own teams |
| **Instrument operator** (register, review, detectors, trajectory of record) | **L2** | needs no authority over capacity, which is exactly what L2 lacks. This is the natural place for a middle delivery role, and forcing it to be priority owner instead is the common mistake |
| **Initiative owner** (the named owner on the executing side) | **L3** | ownership here is a grant of authority to propose and to declare blockers, not a target. It belongs with the party closest to the work that is not the party countersigning it |
| **Instrument owner** (the telemetry behind one counter) | **an L4 discipline that does not execute that initiative** | the separation rule constrains the party, not the reporting line, so a chain containing several disciplines can satisfy it internally and in both directions at no cost |
| **Verifier** | **a query**, maintained by L2 and changeable only by a countersigned commit | never a person, in any case |
| **Budget owner** (stage 3 only, optional) | **L1** | permitted to coincide with the priority owner: the separation rule covers {defines, executes, instruments} only. Where they coincide, ECONOMY.md R12 matters twice as much, because the same party sets the allocation and holds the means of honouring it |

Read the assignment against the separation rule: **defines** is L1 (or a delegated L4 outside the executing discipline), **executes** is L3 with L5, **instruments** is a different L4. Three distinct parties, no collapse, and the chain supplies all three without hiring anyone.

---

## §3 What each level may and may not do

The prohibitions matter more than the permissions. Each one closes a specific way the method degrades into theatre.

**L1, priority owner.**

May: order the initiatives; interrupt work in progress; allocate capacity and, in stage 3, points; countersign each initiative's acceptance criterion, counter, quarterly target, declared completion date and, where more than one team executes it, the contribution shares (ECONOMY.md R5a); countersign a change to the declared date, which then appears in the published date history; countersign review outcomes that change the priority order; hold the tiebreak per team per period; grant protected time.

May not: propose the criterion, the counter or the trajectory, because proposing and countersigning the same thing is self-definition with a formal step added; own an instrument; act as verifier; delegate the tiebreak; suppress a detector output, a gate number or a published report; hold more than roughly ten countersignatures personally, per the span limit.

**L2, instrument operator.**

May: maintain the register and the planning file; run the absence detectors and chase each finding to closure; keep the trajectory of record current and publish the forecast gap; publish the two coverage gate numbers; run the weekly review, which opens with the previous period's unexecuted decisions; record decision artifacts; trigger the audience escalation in §5 when a decision repeats or a countersignature deadline expires.

May not: change the priority order; reassign anyone's capacity; countersign a criterion, counter, target or date; edit a counter definition, a denominator or a verifier query except by a commit reviewed by L1, which flags the initiative for the period; choose what appears in the report. The agenda is generated by the detectors and the gate rule is automatic, so the operator publishes and does not curate.

**L3, initiative owner.**

May: propose the acceptance criterion, the counter and the trajectory; declare a blocker on the initiative, which is a grant no one else holds; choose the outcome at review; request a change to the declared completion date.

May not: countersign its own proposal; set or change the counter's denominator, which comes from a system inventory; own the instrument behind its own counter; change the priority order; make outcomes that change the priority order effective without L1's countersignature.

**L4, discipline managers.**

May: assign people inside their own discipline; publish and hold the bound on work in progress for their own teams, which is the one mechanism in the method that needs no countersignature from anyone (METHODOLOGY.md mechanism 7); own the instrument for initiatives executed by another discipline; hold a delegated countersignature for initiatives their own teams do not execute; declare blockers on behalf of their teams.

May not: countersign an initiative their own teams execute; own the instrument for an initiative their own teams execute; settle contention for capacity between disciplines, which is L1's tiebreak.

**L5, teams.** Do the work, propose criteria and counters through L3, declare blockers, receive allocations. No individual score exists anywhere, by construction (METHODOLOGY.md metrics, tier 3).

---

## §4 Two constraints that pull against each other, and the resolution

The method requires **uniqueness** (exactly one decisive party per contended resource per period) and a **bounded span** (roughly ten initiatives per countersigner). With more than ten initiatives competing for the same teams, one party cannot satisfy both.

The resolution splits the two things that were bundled into "priority owner":

1. **The tiebreak is never delegated.** For each team in each period, exactly one party is decisive when two initiatives want the same people, and that is L1. Uniqueness is preserved because this is the only power that has to be unique.
2. **The countersignature is delegated per initiative** to an L4 manager whose discipline does not execute it. Span is preserved because countersignatures divide, and separation is preserved because the countersigner is outside the executing discipline.

3. **Assignment is not volunteered.** Which initiatives a countersigner holds follows a mapping stated in advance and recorded in the register, by discipline or by rotation. Left to choice, the selection itself is the loophole rather than the leniency: a countersigner measured on date movement and decision execution prefers short, safe, well-instrumented initiatives, and the multi-year migration ends up with whoever is least able to refuse. The list per countersigner is published together with the span count, so both the load and the composition are visible.

**The obvious attack on this, and its price.** Delegated countersignature between L4 peers invites reciprocal leniency: approve my weak criterion and I will approve yours. It is not forbidden, it is priced. Countersignature pairs are published, and the four priority-owner measures (coverage, decision latency, decision execution, date movement) are computed **per countersigner**, not only for L1. A pair trading weak bars produces two visibly bad columns rather than one invisible favour. This is the same move the method makes everywhere else: the compromise is made visible rather than prohibited.

---

## §5 Escalation, given that L1 is the top

Two mechanisms escalate above the priority owner: the repeated-blocker rule in the weekly review (CONTROL.md §9) and the countersignature deadline (ECONOMY.md R3a). With L1 at the top of the chain, both pointed at nobody, which is the quiet failure this assignment has to close.

**Escalation is widening the audience of an unresolved item, not moving it up a line.** A superior is only the cheapest audience. So the audience is named in advance, in the register, before it is needed:

- the heads of the projects consuming the initiative's outcome
- the teams that confirm cross-team benefit under ECONOMY.md R5
- whoever was promised the declared completion date

Publishing to that audience is what "escalated" means for an item that has reached L1 and stopped. It requires no new authority and no fictional superior, and it is the only pressure available on the party at the top of a chain.

**The same audience receives L1's own four measures.** In a vertical line, L1's result is the sum of the teams below, so L1 sets the bar and is measured on it being cleared, whatever the org chart shows. Nobody above can enforce the substitute measures, which means they are worthless unless published outside. This is the weakest point of the whole assignment and it belongs in the proposal, not in the post mortem.

---

## §6 Every authority-dependent mechanism, checked against this assignment

| Mechanism | Where | Who holds it here | Holds? |
|---|---|---|---|
| Telling a team to drop what it is doing | PROBLEM.md failure criterion | L1 | yes, and this is the strongest available answer in this shape |
| A published bound on concurrent work in progress | METHODOLOGY.md mechanism 7 | L4 for its own teams, L1 where an initiative spans disciplines | yes, and it is the only mechanism here needing no countersignature and no telemetry |
| One ordering across initiatives competing for the same teams | METHODOLOGY.md Roles | L1, per team per period | yes, for teams inside L1's span. §7 residual 3 otherwise |
| Countersigning criterion, counter, target, date | ECONOMY.md R3 | L1, or a delegated L4 outside the executing discipline | yes, §4 |
| Countersignature deadline of five working days | ECONOMY.md R3a | L2 detects, audience receives | yes, via §5 |
| Separation of defines, executes, instruments | METHODOLOGY.md Roles | L1 or L4, L3 with L5, a different L4 | yes, three distinct parties |
| Definer span limit of about ten | METHODOLOGY.md Roles | delegation in §4 | yes, and the count per countersigner is published |
| Priority owner measured on something other than delivery | METHODOLOGY.md Roles | the four measures, per countersigner, published to the §5 audience | partly. §7 residual 1 |
| Repeated blocker escalates | CONTROL.md §9 | L2 triggers, audience receives | yes, via §5 |
| Review outcomes that change the priority order | CONTROL.md §9 | L3 chooses, L1 countersigns within the R3a deadline | yes |
| Decisions are recorded and their execution verified | CONTROL.md §9 | L2 records and queries, actor named in the record | yes |
| Coverage gate withholds the report below threshold | CONTROL.md §4 | automatic, and L1 may not suspend it | yes |
| Counter definition changes are reviewed and flagged | CONTROL.md §7 | L1 reviews the commit, L2 cannot self-approve | yes |
| Denominators come from a system inventory | ECONOMY.md R2a, CONTROL.md §7 | instrument-owning L4, never the executing side | yes |
| Instrument outages are the instrument owner's blocker | CONTROL.md §6, ECONOMY.md R11 | the instrument-owning L4 | yes, and the executing team's allocation is held rather than forfeited |
| Blocker moves off the team within one review cycle | PROBLEM.md success criterion 5 | named clearer in the decision record, L4 or L1 | yes |
| Redemption against a pre-agreed catalogue | ECONOMY.md R12 | L1 as budget owner | permitted, and see §7 residual 5 |
| No ranking of people or teams | METHODOLOGY.md metrics tier 3 | nobody, by construction | yes, with the load-number hole stated in CONTROL.md §11 |

Fifteen of eighteen hold outright. The three that do not are below, and none of them is fixed by adding a level to the chain.

---

## §7 What this assignment does not fix

1. **L1 is measured on the sum of the teams below.** Check 3 is at its most severe in a vertical line, and no party above exists to enforce the substitute measures. Publishing them to the outside audience in §5 is the whole defence, and it is a weaker defence than an enforcing superior would be. State it when proposing the method rather than discovering it later.
2. **Reciprocal leniency between delegated countersigners** is priced in §4 and not removed.
3. **Contention that crosses outside L1's span** has no owner in this shape. The detector for a team with no named tiebreak, or with more than one, fires and the finding is published as contention for capacity. That is the honest output: a priority order nobody can enforce is the actual problem, and no instrument downstream of it will help.
4. **L2 operates the instrument and runs the review**, which would be a single point able to shape what gets discussed. Three things limit it: the detectors are queries in git rather than an agenda someone assembles, the coverage gate is automatic, and any change to a definition or a query is a commit L1 reviews. What remains is that L2 could be slow rather than selective, which shows up as its own detector findings ageing.
5. **L1 as both priority owner and budget owner** is permitted and concentrates two levers. ECONOMY.md R12 is the only thing standing between that and points being a promise, which is why stage 3 should not start until the catalogue is agreed in advance.

---

## §8 The minimum version of all this

Stage 0 needs **L2 and read access, and nothing else**. Coverage, the absence detectors and the stall list require no authority from anyone, and they are the part most likely to carry the effect. Everything in §3's permissions matters from stage 1 onward, when decisions have to follow the deviations.

So the assignment above is not a precondition for starting. It is what has to be true before the numbers can change anything, and it is worth agreeing while stage 0 is running rather than before it begins.

---

## Changelog

| Version | Date | What and why |
|---|---|---|
| 0.2 | 2026-09-07 | Fixes from the third analysis pass ([ANALYSIS.md](ANALYSIS.md) §13). §4 gained a third point: countersignature assignment follows a mapping stated in advance instead of being volunteered, because the previous version priced reciprocal leniency and left the prior question open, and a countersigner measured on date movement will choose short safe initiatives while the multi-year migration lands on whoever cannot refuse (F10, P33). The new bound on work in progress was placed with the discipline managers and added to the §6 check table, where it is the only mechanism requiring no countersignature and no telemetry from anyone (F1, P25). Contribution shares were added to what the priority owner countersigns (ECONOMY.md R5a). |
| 0.1 | 2026-09-07 | Written after the author stated the real authority chain, which is vertical and ends at the party with capacity authority. METHODOLOGY.md v0.8 states generically what the roles must satisfy, and the request was for the powers to be unambiguous inside the current model, so this document assigns them level by level, enumerates the prohibitions, and checks all seventeen authority-dependent mechanisms. Two findings came out of writing it. Uniqueness of the tiebreak and the bounded countersignature span conflict above ten competing initiatives, resolved in §4 by delegating the countersignature to a discipline manager outside the executing discipline while never delegating the tiebreak, with reciprocal leniency priced by computing the four priority-owner measures per countersigner. And two of the four review outcomes change the priority order, which the ownership grant in METHODOLOGY.md did not distinguish, so they now take effect only when the priority owner countersigns the record (CONTROL.md §9). |
