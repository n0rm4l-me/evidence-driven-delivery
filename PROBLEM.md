# The problem

**Version:** 0.7
**Date:** 2026-09-08

This file takes precedence over [METHODOLOGY.md](METHODOLOGY.md). If the method stops answering the problem, the method changes. If the understanding of the problem changes, that change is recorded here with a date rather than silently rewritten.

This is a description of a recurring pattern, not of one company. It is written to be instantiated: an adopting organization answers the diagnostic checks and the preconditions below with its own facts, and keeps those answers outside this document.

---

## The symptom pattern

Observed directly in an engineering organization, 2026. Stated as observations, not interpretations.

1. There are several critical initiatives and a task list with explicitly assigned priorities.
2. After tasks are distributed they go nowhere: there is no observable movement.
3. Teams work on whatever happens to be at hand rather than on what is prioritized.
4. There is no tracking and no reporting.
5. Individual tasks sit untouched for years.
6. A tracker exists, but everyone manages their own items in it: a person can do nothing for weeks and it will not be noticed.
7. Some work never enters the tracker at all, because people forget to create items.
8. Rolling anything up is impossible: the question "how much has been done" cannot be answered for any initiative.
9. There is no objective control of any kind. Everything known about the state of the work is known from what the people doing it say.

The consequence of 6 to 9 is the actual problem: **the state of work in the organization is unknowable.** Not badly reported, not slowly reported. Unknowable, because no source of data exists that is independent of the people being asked.

Everything else on the list follows from that. Priorities evaporate because nothing observes whether they were followed. Tasks live for years because nothing marks the difference between a task being worked on and a task existing.

---

## Why the usual answers fail here

Each of these is the first thing organizations try, and each fails for a structural reason worth naming.

**More reporting.** Adds a second self-declared layer on top of the first. Self-declared data cannot verify self-declared data.

**More frequent status meetings.** Increases the cost of admitting a problem, so it improves the quality of the reporting rather than the quality of the information.

**A new tracking tool.** If items are not created in the current tool, they will not be created in the next one. Forgetting is not a property of a tool. A second tool also splits the record, so instead of one incomplete picture there are two.

**Tightening accountability.** Raises the price of bad news, which is the direct cause of the misreporting it is meant to fix.

**Estimates and commitments.** Creates a number produced by the person who will be judged on it. That is not a measurement, it is a negotiation with a number attached.

The common failure: all five collect information from people who have an incentive to shape it, and none of them creates a source of evidence that exists independently of the report.

---

## Hypotheses about causes

Not a diagnosis. Each hypothesis comes with a check that can be run before deploying anything.

**H1. Accountability is assigned to teams rather than to people.**
A team cannot be accountable; a person is.
Check: take 10 critical items and count how many have a single concrete owner who did not assign themselves.

**H2. There is no limit on work in progress.**
Priority only means something when capacity is bounded. With 15 concurrent items, priority #1 and priority #9 move at the same (zero) speed.
Check: count in-progress items per person. More than three means the problem is overload, not discipline.

**H3. There is no forcing function.**
Nobody regularly asks out loud about stalled work. Reporting with no audience is paperwork.
Check: does a person exist who can tell a team "drop that, work on priority #1", and do they actually do it?

**H4. There is no verifiable definition of done.**
While "done" is vague, any state is defensible and acceptance turns into negotiation. That is where a year-long "90% complete" comes from.
Check: of 10 items, how many state a verifiable fact rather than an intention?

**H5. Items are too large to be reportable.**
A six-month item physically cannot signal progress, so its stalling cannot be detected, and nobody is lying while that happens.
Check: distribution of items by expected size. How many are larger than two weeks?

**H6. A tracker item gives its creator nothing.**
If the only function of the record is oversight, the record will be sabotaged, and that is rational behavior rather than laziness.
Check: ask five engineers what they get from an item existing in the tracker. If the answer is "nothing" or "so people stop chasing me", the hypothesis holds, and no tool will fix it.

**H7. Bad news is expensive.**
If reporting a blocker means getting into trouble, everyone shows green under any amount of control.
Check: find the last three times someone said work would miss its date. What happened to that person afterwards?

Order matters. **H6 and H7 are primary.** If they hold, starting with tooling and metrics is pointless, because better control in that environment does not produce truth, it produces more careful reporting. H1 to H5 are mechanical and can be fixed with rules. H6 and H7 are economic and have to be fixed with incentives, which is what the method's contribution economy is for.

---

## What success looks like

Verifiable criteria, not intentions. Horizon: one quarter on a single pilot initiative.

1. The question "how much has been done on initiative X" is answered by a machine, in seconds, without asking anyone.
2. Work that has not moved for 14 days becomes visible automatically, and within a week one of four decisions is made about it.
3. The share of work outside the tracker (changes with no linked item) is measured and declining.
4. At least one critical item is deliberately cancelled during the quarter. Zero cancellations means silence, not order.
5. At least one declared blocker is escalated and cleared by someone other than the person who declared it.
6. By the end of the quarter at least one new default exists (a CI check, a template, a script) that did not exist at the start.
7. Not a single personal metric has appeared. Not one.
8. Coverage is known and above its threshold: the share of merged changes mapping to a registered item with an acceptance criterion, and the share of initiatives whose counter reported fresh data on time. Until both exist, nothing else on this list can be trusted, because a number computed over an unknown share of the work is not a measurement.
9. Of the deviations detected, most received one of the four decisions within a review cycle, and most of those decisions were executed by their stated date.
10. At least one initiative was excluded from the instrument on purpose, with a named owner, and still appears in the coverage denominator as excluded. Zero exclusions means the boundary is being ignored rather than respected.
11. Work in progress is bounded, the bound is published, and the count per person on the pilot teams is at or below it by the end of the quarter. This is the criterion that was missing: every other item on this list can be satisfied while nothing moves faster, because with nine items open per person priority #1 and priority #9 both proceed at zero speed, each stall is reported truthfully, and no blocker anywhere names the cause. H2 said this and the success list did not measure it.

Criteria 4, 5 and 9 matter more than they look. They are the only ones that cannot be satisfied by tooling alone, so they are what distinguishes a working method from a working dashboard. Criterion 9 is the direct inverse of the failure criterion below, and it is the number to watch first.

Failure criterion, recorded in advance: if after a quarter the report is being generated but no decision has been made on any flagged item, the method does not work in that environment, and the cause is missing authority, not the tooling.

---

## Boundaries: what this does not try to solve

- **Not replacing the tracker.** Work items stay where they are, because a record must have exactly one write path. The moment there are two, "people forget to create items" simply migrates to the new tool.
- **Not measuring time or effort.** No timesheets, no activity tracking.
- **Not evaluating people.** A method capable of evaluating people will eventually be used for that, regardless of its author's intentions. The only defense is to never produce the numbers.
- **Not a company-wide framework rollout.** One pilot initiative, chosen because it has independently observable ground truth.

---

## Risks

| Risk | Why it is dangerous | Mitigation |
|---|---|---|
| No escalation authority | the report becomes one more ignored channel | establish before starting, it is a blocker |
| Points cannot actually be spent | fake currency destroys trust worse than having no system | secure budget confirmation before announcing the economy |
| Metrics leak into people evaluation | the method dies that day | per-person numbers are never produced at all |
| Teams farm the reward system with cheap or invented work | the reward gets optimized instead of the outcome | structural: no point source may exist whose supply the earning team controls (ECONOMY.md). What survives that is measured quarterly and treated as a design defect, never as misconduct |
| Prevention goes unrewarded | the most valuable invisible work gets squeezed out | not solved. Prevention leaves no change in system state, so it has to be recognized outside the economy, deliberately and by hand |
| Deployment reads as surveillance | reproduces exactly the behavior it is meant to catch | pilot on an initiative the introducer owns, spread by demonstration |
| No initiative has observable ground truth | the central mechanism has nothing to stand on | find one before starting; if none exists, the method is not applicable yet |

---

## Preconditions each adopter must establish

Answered with the organization's own facts, outside this document. The first two are blockers: without them, do not start.

1. **Who can tell a team "drop that, work on priority #1"?** The numbers will expose stalls within a week. If nobody with authority then asks questions out loud, the reporting just gets more careful. The answer has to be a single party per contended team per period, not a title: [AUTHORITY.md](AUTHORITY.md) states the shape a workable answer takes and what it obliges that party to publish in return.
2. **Who owns the budget that converts points into real purchases?** Without a real ability to spend, the contribution economy is theater. Note that this precondition blocks stage 3 only, and that redemption must be non-discretionary against a catalogue agreed in advance ([ECONOMY.md](ECONOMY.md) R12), or the currency is priced at zero within a quarter.
3. **Is this for a team the introducer manages, or for teams they do not?** In the second case the center of gravity shifts from control to exchange: what does a team get in return for transparency? Without an answer, the method will not survive a month.
4. **Which initiative has independently observable ground truth?** That is the pilot. Not the most important initiative, the most measurable one.
5. **Does the tracker expose a transition history through an API?** Flow metrics are computed from it. Without API access, none of the observability mechanisms are available.
6. **Is there API access to the code host?** Required to detect work happening outside the tracker.
7. **How is critical work currently grouped** (labels, epics, components, or not at all)? Without grouping there is nothing to roll up.

---

## Open questions

1. Whether H6 and H7 can be diagnosed honestly by someone inside the organization. Both checks require people to describe an incentive they are subject to, to a person who may be part of it.
2. Whether the method is applicable at all where no initiative has observable ground truth. Currently the answer is no, which limits it to infrastructure and platform work and excludes most of everything else.
3. What the minimum viable subset is. The full method has five mechanisms, seven metrics, three rituals and an economy. That is very likely more than any organization will adopt at once, and it is not yet known which part carries the effect. A staged answer is proposed in ANALYSIS.md §11, with the economy last, but it is a prediction and not a result.

---

## Changelog

| Version | Date | What and why |
|---|---|---|
| 0.7 | 2026-09-08 | One wording change in the 0.5 row below, made when the repository was prepared for publication: the insufficient answer to precondition 1 is now stated as a form the question attracts rather than as an answer that was received from a specific organization. The reasoning it illustrates is unchanged and is the useful part. |
| 0.6 | 2026-09-07 | Added success criterion 11, bounded work in progress. The third analysis pass ([ANALYSIS.md](ANALYSIS.md) §13) audited the mechanisms against the nine symptoms above for the first time and found symptom 3 only half addressed: everything in the method ordered what should be worked on and nothing bounded how much is open at once, although H2 in this document already said priority means nothing under unbounded capacity. The success list had the same hole, so all ten criteria could be met while nothing moved faster. |
| 0.5 | 2026-09-07 | Preconditions 1 and 2 now point to where a workable answer is specified, and precondition 2 is marked as blocking stage 3 only rather than the whole method. Both were written as questions with no statement of what counts as an answer, which is how precondition 1 attracts answers of the form "the administrator, or the head of each project": true, and not an answer, since administrative rights are not authority and per-project ordering means no ordering exists across shared teams. |
| 0.4 | 2026-09-07 | Added success criteria 8, 9 and 10. Coverage was missing from the list entirely, which meant every other criterion could be satisfied over an unknown share of the work. Decision execution was missing too, even though this document already recorded its absence as the failure criterion, so success and failure were being measured against different things. The exclusion criterion is there because a boundary nobody ever uses is a boundary nobody is respecting. |
| 0.3 | 2026-09-06 | Updated two rows of the risk table to match [ECONOMY.md](ECONOMY.md): reward farming is now mitigated structurally rather than by quarterly repricing, and the prevention row now states plainly that it is unsolved instead of claiming partial coverage by price list rows that no longer exist. |
| 0.2 | 2026-09-06 | Removed all organization-specific and tooling-specific detail so the document describes a class of problem rather than one company. Added "Why the usual answers fail here", turned the environment specifics into adopter preconditions, and dropped the internal-inventory section, which belonged to one instance rather than to the method. |
| 0.1 | 2026-09-06 | First statement of the problem. Symptoms observed, causes still hypotheses, none verified. |
