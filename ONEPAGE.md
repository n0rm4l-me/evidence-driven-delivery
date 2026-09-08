# Evidence-Driven Delivery, on one page

**Version:** 0.3
**Date:** 2026-09-07
**Status:** the short form. [METHODOLOGY.md](METHODOLOGY.md) is the long form and [CONTROL.md](CONTROL.md) is what you actually build first. If the two ever disagree with this page, they win.

---

## The problem

Priorities are announced and ordered. Work is distributed. Months later nobody can say what is true: some items were never created, some work never appeared in any system, some tasks have been open for years, and the reports all look fine. This is not a discipline problem and it will not be fixed by asking harder.

## The claim

People do not lie about state because they are dishonest. They lie because telling the truth costs more than staying quiet. So: derive state from artifacts nobody produced for reporting, make bad news the cheapest thing to say, and detect what is missing rather than checking what was claimed.

## Three invariants

Everything else is machinery for these. If a rule conflicts with an invariant, the rule is wrong.

```
1.  deliver the outcome  >  disclose a blocker or a failed approach  >  silence = unverified claim = 0
2.  no point source exists whose supply the earning team controls
3.  measured and progressing  >  measured and stalled  >  unmeasured
```

## Seven mechanisms

1. **Pre-registered criteria.** `done = <verifiable fact>` in git, before work starts, unchanged afterwards. Not prose: a metric with a threshold and its query, a named check that must pass, the absence of a named artifact from an inventory, or a state value holding for every row of an inventory. Where the work replaces something, the criterion names the removal. Acceptance stops being a negotiation.
2. **Blocked is a status that travels upward,** and saying so pays better than silence. Time to resolution is a manager's number, never an engineer's.
3. **State comes from artifacts,** not from people: transition log, git, CI, production metrics. Nobody is asked anything.
4. **Progress is a change in system behavior,** expressed as one bounded counter per initiative, with the denominator taken from an inventory rather than from a list the team supplied.
5. **Every improvement ends in a commit,** not a decision: a check, a template, a changed default.
6. **Absence is detected by query, not noticed.** An initiative with no items, an item with no criterion, a counter with no instrument, a merged change mapped to nothing, a decision never executed.
7. **Work in progress is bounded, and the bound is published.** Priority means nothing under unbounded capacity: with nine items open per person, priority #1 and priority #9 both move at zero speed and no blocker anywhere explains why. Cheapest mechanism here, and the one that acts directly on teams working on whatever is at hand.

## Four roles, and they must be different parties

| Role | Owns |
|---|---|
| Priority owner | the order, the allocation, the countersignature on each criterion, counter and date |
| Executing team | proposing all three, and doing the work |
| Instrument owner | the telemetry that produces the counter |
| Verifier | a query, never a person |

No two of {defines, executes, instruments} may be the same party. Where the collapse is unavoidable, the initiative is marked `self-defined` or `self-instrumented` in every report and is excluded from the economy. One priority owner holds about ten initiatives; past that the countersignature is a formality and the number is published so that shows.

**The priority owner is not measured on delivery of what they countersign.** Otherwise definition never left the measured party, it just concentrated in one person holding all three levers. They are measured on coverage, on the share of deviations that got a decision within one cycle, on the share of those decisions executed, and on how often declared dates moved. The role is only genuinely filled if that person can interrupt work already in progress across the competing projects. Where they are the top of the chain, escalation means widening the audience of an unresolved item rather than moving it up a line. Who holds which role in an ordinary reporting chain, and what each level may and may not do, is in [AUTHORITY.md](AUTHORITY.md).

## Two numbers that gate everything else

Coverage first, published above all else, and below threshold **the rest of the report is not published at all**:

- share of merged changes mapping to a registered item that has a criterion
- share of registered initiatives whose counter reported fresh data on time

A dashboard over 40% of the work is not control, it is a biased sample, because what escapes the system is exactly the work that disappears. The threshold is fixed before the first report and every change to it is published with its history, or the softest number in the instrument is the one deciding whether the instrument speaks.

## The weekly review, 20 minutes

Opens with last week's decisions that did not execute. Then red items only. Four outcomes, no fifth: continue with a named blocker and a named clearer; change the owner; defer and drop the flag; close as will-not-do. Each becomes a record with what, who, by when, and which of the four enumerated observable facts will show it happened. Twice the same outcome 1 escalates above the priority owner, because repeating a decision is not a decision. The last two outcomes change the priority order, so they take effect only once the priority owner countersigns the record.

Then monthly: kill or defer. Quarterly: a retrospective on the system, producing at least one new default.

## What it never does

No ranking of people or teams exists in any output, including exports. Load numbers exist for capacity decisions, current state only, no history, visible only to whoever owns that capacity. The honest form of the guarantee: the system does not produce evaluation data, which is not the same as making evaluation impossible.

## Adopt in this order

| Stage | What | Needs |
|---|---|---|
| 0, week 1 | artifact-derived state, coverage, the stall list | nobody's consent |
| 1, month 1 | one owner per initiative, countersigned criteria, the published bound on work in progress, the review, verified decisions | escalation authority |
| 2, quarter 2 | counters, trajectories of record, the forecast gap | independent instruments |
| 3, optional | the contribution economy ([ECONOMY.md](ECONOMY.md)) | a real budget |

Stage 0 needs no permission and probably carries most of the effect. Stage 3 is the only novel part, it failed most of the adversarial simulations, and stopping after stage 2 forever is a legitimate end state. **Do not start with stage 3.**

Week one is a test before it is a build: derive the state of three initiatives from artifacts, then ask the people doing that work privately what is actually true, and compare. It costs a day, needs nobody's agreement, and it is the only check that can fail early enough to save the effort ([CONTROL.md](CONTROL.md) §12).

## What it does not do, stated up front

It does not cover work whose output is a decision or a change in judgement: research, design, architecture. Such work is listed as excluded with a named owner and counted in the coverage denominator, so coverage stays honest.

It does not reward prevention, and cannot: an incident that did not happen leaves no change in system state.

It needs two things this document cannot supply. Someone with the authority to tell a team to drop what it is doing, and, for stage 3 only, someone who owns a real budget. Without the first, none of this starts.

---

## Changelog

| Version | Date | What and why |
|---|---|---|
| 0.3 | 2026-09-07 | Carried the third analysis pass into the short form ([ANALYSIS.md](ANALYSIS.md) §13): mechanism 7, the published bound on work in progress, which is the only mechanism acting directly on teams working on whatever is at hand; the four admissible criterion forms and the removal clause, since prose criteria pass every check and still have to be argued with a person; the versioned coverage threshold; the countersignature on the two review outcomes that change the priority order, which had landed in CONTROL.md v0.4 and never reached this page; and the week-one test of the claim the whole method rests on. |
| 0.2 | 2026-09-07 | Added the audience form of escalation and a pointer to [AUTHORITY.md](AUTHORITY.md), because the check that used to read "is there a level above them" fails whenever the priority owner is the top of the chain, which is the common case. |
| 0.1 | 2026-09-07 | Written per ANALYSIS.md change P10: the method had no short form, and a methodology nobody can read in five minutes is not adopted whatever its quality. |
