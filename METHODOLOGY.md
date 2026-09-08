# Evidence-Driven Delivery (EDD)

**Version:** 0.9 (draft)
**Date:** 2026-09-07
**Status:** not deployed. No mechanism here has been tested in practice.

A living document. It changes based on results, not on discussion. Every change is recorded in the changelog at the bottom with its reason.

---

## In one sentence

Work counts as done only when an artifact that nobody produced for the sake of reporting confirms it; honesty is paid for, and lying is never punished, it simply does not convert into anything.

## Who this is for

Engineering organizations where:

- several critical initiatives run in parallel
- the people doing the work are spread across teams with different managers
- reporting is self-declared, and therefore unverifiable
- initiatives live for quarters and years, not sprints

Not for: product teams with fast user feedback (product metrics already give you objectivity there), or time-and-materials outsourcing.

**Explicit boundary.** The method requires that an initiative's progress be expressible as an observable change in system state. Work whose outcome is a decision or a change in judgment (research, design exploration, architecture choices) is **out of scope**, and the correct handling is to leave it outside the instrument with a named owner rather than to manufacture a number for it. A counter invented under pressure to be measurable becomes an activity count dressed as evidence, which is worse than an honest qualitative status because it is harder to argue with. Excluded work is still counted as excluded, so that coverage stays honest (CONTROL.md §4).

In practice this limits the method to infrastructure, platform, reliability, migration and decommissioning work. That is a real limitation, not a temporary one, and it is better discovered on day one than in month six.

---

## Five axioms

**1. Lying is the price of telling the truth.**
People lie where telling the truth costs more than staying quiet. There are no honest and dishonest teams, there are different prices attached to bad news. Lower the price instead of hunting for liars.

**2. "Laziness" is a placeholder diagnosis.**
Underneath it there is always one of four things: it is unclear what exactly needs doing; the person is blocked and gave up; the person is overloaded and picked the easier item; the person does not believe it matters to anyone. Four different remedies, and none of them is control. In this system the word "lazy" is banned as an explanation.

**3. A report is not data.**
Data is what appears as a side effect of the work itself: a commit, a deploy, a change in a production metric, an entry in the tracker's transition log. Anything a human types specifically for reporting purposes is a lie surface, and people will lie there not out of malice but because it is cheaper.

**4. What cannot be verified was not done.**
The verification criterion is fixed before work starts and does not change along the way. The main lie surface is not the status update, it is the task definition: while "done" is vague, any state is defensible and acceptance turns into negotiation.

**5. Experience scales through defaults, not through stories.**
A practice is adopted not when it is written down but when violating it takes effort. A template, a generator, a CI check, a changed default value: those scale. Verbal agreements and wiki pages die within a quarter.

---

## Seven mechanisms

One per axiom, plus two that no axiom implied and the original problem demanded. If a mechanism fails, fix the mechanism, not the axiom.

**1. Pre-registered acceptance criteria, in one of four admissible forms.**
A line `done = <verifiable fact>` is written before work starts and lives in git. Free text is not enough. `done = the migration is complete` satisfies every check that looks for a criterion being present, counts toward the coverage gate, and still leaves acceptance to a person reading prose, which is the negotiation the criterion exists to end. So the fact comes from a closed set of forms:

1. a named metric with a threshold, and the query that reads it
2. a named check that must pass
3. the absence of a named artifact from a named inventory
4. a state value holding for every row of a named inventory

Not "set up monitoring" but "an alert on 5xx > 1% fires in staging, and there is a record of it firing", which is form 1. Acceptance is then mechanical: either the fact exists or it does not, and there is nothing to argue about. Work whose acceptance cannot be written in one of the four forms does not get a prose criterion, it is registered as excluded with a named owner ([CONTROL.md](CONTROL.md) §11), which keeps the boundary of the method honest rather than decorated.

**Where an initiative replaces something, removal is part of the criterion.** Otherwise the counter completes while the outcome does not exist: the share of traffic on the new path reaches 100% while the old path is still deployed, still configured, still costing money and still able to take traffic. The criterion names the removal, and the counter is denominated against the inventory of the old state rather than the adoption of the new one.

**2. Blocked as a first-class status that pushes the problem upward.**
Declaring a blocker must pay better than staying silent (see the contribution economy: it earns points). Time to blocker resolution is a manager's metric, not an engineer's. As long as blockers hide inside "in progress", that is exactly where tasks disappear for years.

**3. Observability instead of status meetings.**
State is derived from the tracker's transition log, git, CI and production metrics. Nobody is asked anything. Control stops being an act of interrogating a person, and with that both the reason to lie and the reason to resent disappear.

**4. The unit of progress is a change in system behavior.**
Not a closed ticket. Progress on an initiative is the share of observed target behavior: share of requests served by the new path, share of hosts on the current version, share of releases that need no manual step, share of services meeting a required policy. One such chart outweighs a hundred tickets: if the line is flat for a week, no set of statuses can mask it.

Finding this number is the hardest and most valuable part of setting up an initiative. An initiative for which no such number can be constructed cannot be tracked objectively by any method, and that is worth discovering on day one rather than in month six.

**5. Every improvement ends in a default.**
A retrospective that produces no new default did not happen. The output is not a decision, it is a commit: a CI check, a template, a script, a changed default value.

**6. Absence is detected, not noticed.**
Mechanisms 1 to 5 all verify that something claimed is real. The original symptom was the opposite: items never created, initiatives never decomposed, work happening entirely outside the system. Verifying presence does nothing about that, so absence gets its own detectors, each of them a query rather than a meeting: an initiative with no items, an item with no criterion, an initiative with no counter, a counter with no instrument, a merged change mapped to nothing, a decision that was never executed. The full set is in [CONTROL.md](CONTROL.md) §5.

This is the mechanism that addresses the complaint the method was built for. The others make reported work trustworthy; this one makes unreported work visible.

**7. Work in progress is bounded, and the bound is published.**
Priority means nothing while capacity is unbounded. With nine items open per person, priority #1 and priority #9 both move at zero speed, every detector reports each stall truthfully, and no artifact anywhere states the cause. The review then has no vocabulary for it either: outcome 1 gets chosen because there is no blocker to name, only attention divided nine ways, and the escalation machinery fires on a problem stated in the wrong terms.

So a bound on concurrent items exists per person and per team, it is published as a default rather than issued as an instruction, and breaching it is a detector finding like any other ([CONTROL.md](CONTROL.md) §5). Starting an item above the bound means finishing or explicitly parking another, and parking is a decision record with the same four mandatory fields as any other decision. This is the cheapest mechanism here: no telemetry, no countersignature, no authority beyond what a manager of a discipline already holds, and it acts directly on the oldest symptom in [PROBLEM.md](PROBLEM.md), which is teams working on whatever happens to be at hand.

---

## Roles

Four roles, and the integrity of everything else depends on them being different parties. This is the gap that mattered most: the method used to specify who executes and who verifies, and left unspecified **who defines**, which meant definition defaulted to the party being measured. Verification can be perfectly objective while the bar quietly drops.

| Role | Owns | Must not be |
|---|---|---|
| **Priority owner** | the priority order, the allocation, and the countersignature on each initiative's acceptance criterion, counter and trajectory | the executing team |
| **Executing team** | proposing the criterion, counter and trajectory, and doing the work | the definer of its own bar |
| **Instrument owner** | the telemetry that produces the counter | the executing team |
| **Verifier** | reading the artifact and deciding whether the fact exists | a person, in any case |

**The separation rule.** No two of {defines, executes, instruments} may be the same party. Where a collapse is unavoidable, the initiative is marked as such in every report about it (`self-instrumented`, `self-defined`) and is excluded from the economy. The compromise is made visible rather than forbidden, which is how this method handles every compromise: what cannot be verified is not punished, it is inert.

**The definer has a span limit, and it is published.** A priority owner holding thirty initiatives countersigns each one in a minute, on whatever the team proposed, and self-definition is restored with a formal approval on top, which is worse than the honest original because it looks like rigor. So the number of concurrent initiatives per priority owner is itself a published number, and beyond roughly ten the role must be split. A role whose capacity is not bounded is not a control, it is a formality.

**What the priority owner is judged on, and why it cannot be delivery.** This is the failure mode to design against, because the obvious candidates for the role are exactly the people already measured on shipping the same initiatives. If the party who countersigns the bar is judged on whether the bar is cleared, definition has not moved away from the measured party, it has been concentrated in one person holding all three levers: countersign a weak criterion, move the declared date, reallocate toward whatever looks best. One person with that incentive is worse than twenty engineers with it, because twenty cover for each other imperfectly and one covers everything.

The test: **is the party who countersigns judged on whether the countersigned thing succeeds?** If yes, the separation is nominal.

So the role gets its own measures, and all four already exist in the control layer:

| The priority owner is judged on | Why it is safe |
|---|---|
| coverage, both gate numbers | improves only if more real work is registered and instrumented |
| share of detected deviations that received a decision within one review cycle | cannot be improved by anything looking successful |
| share of those decisions executed by their stated date | measures follow-through, not outcomes |
| how often declared completion dates moved, per initiative-quarter | rises when reality is absorbed by resetting the date rather than by deciding |

None of these improves when an initiative appears to be going well, and every one of them degrades under silence. That is the property being bought.

**Why the fourth measure is normalized.** As a raw count it punishes long initiatives, and long initiatives are what an organization with this problem is failing at: a three-year decommissioning will legitimately re-declare more often than a one-quarter change, so the safest portfolio to hold becomes a portfolio of short work, and the preference for anything that finishes inside the current period comes back through the definer's incentives instead of the team's. So it is normalized per initiative-quarter, the first declaration is not counted as a move, and the size of each move is published beside the count: a date that slipped two weeks four times and a date that moved once by a year are different facts and should not score the same.

**When this role is actually filled, and when it only looks filled.** Four checks, and the first is the one organizations fail:

1. **Can this person interrupt work already in progress**, across the projects competing for the same people, and do they in fact do it? Administrative rights are not this. Influence over another manager's team is not this either.
2. **Is there a level above them** to receive an escalation? The review escalates one level above the priority owner when the same blocker repeats, so a role at the top of the chain breaks that mechanism silently.
3. **Are they measured on something other than delivery of what they countersign?** See the table above.
4. **Do they hold few enough initiatives** to countersign meaningfully? See the span limit above.

**Which existing role to give it to.** The two natural candidates fail opposite checks, which is why organizations tend to appoint both and end up with neither.

| Candidate | Strong on | Weak on |
|---|---|---|
| A delivery or product role spanning several projects | check 1's breadth: they see the whole ordering | check 1's teeth: they usually influence capacity rather than command it |
| A manager who owns the capacity of several teams | check 1's teeth: they can genuinely interrupt work | breadth, if projects competing for those teams sit outside their span |
| The manager of the executing team | nothing here | this is the forbidden collapse: defines and executes are the same party |

Appointing both candidates does not add their strengths together, it recreates negotiation. So the requirement is not a title, it is a tiebreak: **if the two disagree about what a team does on Monday morning, whose word ends it?** That party is the priority owner and the other is an input to the decision. Where no tiebreak exists, the role is empty whatever the titles say.

The requirement is weaker than one person per organization, though, and the weaker form is usually achievable where the strong one is not. What is needed is **uniqueness per contended resource**: for a given team in a given period, exactly one party is decisive. Who that is may differ between teams and between periods. So the register records, per team per period, who holds the tiebreak, which makes the two failure states queryable rather than political: a team with no named tiebreak, and a team with more than one.

**When the chain ends at the priority owner, escalation has to be redefined.** Check 2 fails whenever the role lands at the top of a reporting line, and that is the common case, because the party with real authority over capacity is usually near the top. Two mechanisms depend on a level above: the repeated-blocker escalation in the weekly review, and the countersignature deadline. Rather than invent a fictional superior, escalation is defined as **widening the audience of an unresolved item, not moving it up a line.** A superior is simply the cheapest audience. Where none exists, the audience is the parties who depend on the outcome and sit outside the chain: the project heads consuming it, the teams confirming cross-team benefit, whoever was promised the declared date. Escalation is pressure through visibility to people with an interest, and going up is only the most convenient instance of that.

**The vertical case, and the residual it leaves.** Where the priority owner sits above the executing teams in a single reporting line, checks 1 and 4 become easy and check 3 becomes as hard as it can get: their own result is the sum of the teams below them, so they set the bar and are measured on it being cleared, even though the org chart shows two different parties. The four substitute measures are then not optional, and they cannot be enforced from above because there is nobody above. They have to be published to the same outside audience. This is the weakest point of any vertical adoption, and it belongs in the proposal rather than in the post mortem.

One thing the vertical case makes easier: instrument ownership. In a chain containing several disciplines, one discipline can own the counters for initiatives another executes, in both directions. The separation rule constrains the party, not the reporting line, so this is legitimate and costs nothing.

**Where a middle role goes.** A delivery or product role sitting between the decisive manager and the team managers is not the priority owner, and forcing it to be one produces exactly the negotiation described above. Its natural place is operating the instrument: maintaining the register, keeping the trajectory of record current, running the weekly review, and chasing the absence detectors to closure. That requires no authority over capacity, which is what the role lacks and why the fit is good.

A worked assignment of all four roles onto an ordinary four-level reporting chain, with the powers of each level enumerated and every authority-dependent mechanism checked against it, is in [AUTHORITY.md](AUTHORITY.md). This section states what the roles must satisfy; that document states who holds them.

Failing check 1 puts the organization in the worst available state: the role is formally occupied, the method assumes deviations are being received, and nothing arrives. That is strictly worse than an empty role, which at least is visible. Where check 1 fails, the honest response is not to appoint someone anyway, it is to run stage 0 and publish contention for capacity as the first finding, because a priority order that no one can enforce is the actual problem and no instrument downstream of it will help.

**What ownership means for the named owner.** Naming one owner per initiative used to be pure exposure: the name was visible and the reward was collective. Ownership is therefore defined as a grant of authority, not a target: the owner is the only party who can declare a blocker on that initiative, choose the outcome at review, and propose the trajectory. The owner's name never appears beside a score, a rating or a colour. What is coloured is the initiative.

---

## Adoption order

The parts have very different risk profiles and very different evidence behind them, so they are not adopted together.

| Stage | When | What | Needs |
|---|---|---|---|
| 0 | week 1 | derive state from artifacts, publish coverage and the stall list | nobody's consent |
| 1 | month 1 | one owner per initiative, countersigned criteria, the published bound on work in progress, the weekly review, verified decisions, monthly cancellation | escalation authority |
| 2 | quarter 2 | counters, trajectories of record, the forecast gap | independent instruments |
| 3 | quarter 3 at the earliest, and optional | the contribution economy | a real budget |

Stage 0 is the whole of [CONTROL.md](CONTROL.md) that needs no cooperation, and it is the part most likely to carry the effect. Stage 3 is the part most likely to cause harm: it is the only novel part of the method, it failed most of the adversarial simulations, and it is the reason a separate document exists to close a loophole in it. **Do not start with stage 3.** Running stages 0 to 2 and never adding the economy is a legitimate end state.

---

## The contribution economy

Stage 3, and optional. This is the novel part of the method: a reward model designed so that dishonest reporting has no payoff, while nothing about it is punitive. It is also the fragile part, so read the failure modes at the end of this section before deciding to use any of it.

### Why dishonest reporting pays in a conventional system

Start from the payoffs rather than from character. Suppose your initiative is in trouble.

| What you do | Immediate cost | Immediate benefit | Chance of being caught |
|---|---|---|---|
| Report green | none | you are left alone | low, nobody verifies |
| Report the problem | scrutiny, blame, lost autonomy, a reputation for slipping | none | n/a |
| Report nothing | none | you are left alone | low, absence is not tracked |

Optimistic reporting and silence both strictly dominate honesty. No moral failing is required to produce systemic lying: the incentive structure produces it from ordinary rational people. Any attempt to fix this by tightening control raises the cost of honesty even further, so the observable result of more control is better-crafted reporting, not better information.

This yields the design constraint: **truthful disclosure has to be the highest-paying available action, not merely the ethical one.**

### Six conditions under which dishonesty stops paying

**C1. Claims do not convert; artifacts do.**
Reward attaches to a machine-checkable fact, never to a statement about one. An unbacked claim yields exactly zero. This removes the payoff for lying without adding any penalty, which is the whole trick: you never have to detect a lie, because an unverified claim is indistinguishable from no claim at all and is therefore inert.

**C2. Evidence is a by-product of the work.**
If producing evidence is extra work, it becomes a second reporting layer, and that layer gets faked or skipped like the first one. Admissible evidence is only what already exists because the work happened: the deploy, the metric, the passing check, the removed config.

**C3. Verification is done neither by the claimant nor by a human reading a report.**
A machine reads production. If a person verifies by reading a report, verification collapses back into trust; if a person verifies by hand, it becomes bureaucracy and dies within two iterations.

**C4. Zero is the worst possible outcome.**
No negative points, no sanctions, ever. The moment concealment is cheaper than disclosure, every confirmation mechanism above starts working against you, because people will optimize to avoid being measured rather than to be measured accurately.

**C5. The truth about problems carries a positive price.**
C1 to C4 make lying worthless, but that only makes it tie with silence at zero. Honesty has to strictly dominate, so declaring a blocker and documenting a failure must both pay. This asymmetry is the load-bearing element of the entire model.

**C6. Reward accrues to a group and buys capability, not cash.**
Group accrual removes the incentive to compete with the people you depend on. Capability-only purchases keep it from becoming a bonus scheme, which would re-import every incentive to inflate that C1 to C5 just removed.

### The payoff table under this model

Same situation: your initiative is in trouble.

| What you do | Points | What follows |
|---|---|---|
| Report green | 0, because no confirming artifact exists | the stall surfaces automatically within 14 days regardless |
| Report nothing | 0 | same as above, and you forfeited the disclosure payment |
| Declare the blocker | a share of the progress you will now fail to make | it becomes a manager's metric, not yours |
| Establish the approach does not work, and write down which default changes | a larger share of the same | the organization cannot repeat the mistake |
| Deliver the outcome | the whole allocation | strictly the largest payoff available |

Honest disclosure is the only branch other than delivery with a positive payoff, and the two dishonest branches are not punished, they are merely empty. Nobody has to be caught, confronted, or trusted. The exact shares, and the reason disclosure is priced as a fraction of forgone progress rather than as a flat fee, are in [ECONOMY.md](ECONOMY.md).

### Seven rules

Rules 1 to 6 are direct implementations of C1 to C6. Rule 7 is what closes the farming loophole those six left open.

**Rule 1. Points only for a confirmed change in system behavior.**
Sources of confirmation: a production metric, a green CI run, a deploy, infrastructure state. Never: number of commits, lines, closed tickets, story points, or hours.

**Rule 2. Points only for pre-registered work.**
If there was no `done` criterion before work started, there are no points. This blocks inventing work after the fact and makes mechanism 1 economically mandatory rather than merely declared.

**Rule 3. Negative points do not exist.**
Zero is the only punishment.

**Rule 4. Points accrue to a team and are spent by that team.**
Personal points do not exist in any form, including "just for my own understanding". The owner's name is always visible; no score is ever kept next to that name.

**Rule 5. Points buy the ability to work, never personal gain.**

**Rule 6. Allocations are public, set before the quarter, and set by whoever owns priorities.**
Allocating the pool is the mechanism for steering priorities: a priority expressed as a standing allocation acts continuously, unlike a priority expressed as an instruction issued once. Allocations are never changed retroactively for work already registered.

**Rule 7. No point source may exist whose supply the earning team controls.**
Points are released only by movement of a bounded counter that someone else defined, instrumented and owns. This is the rule that makes fake and low-importance work unprofitable arithmetically rather than by prohibition, and it is the reason there is no price list of action types in this method.

### How points are actually issued

The full mechanism is in [ECONOMY.md](ECONOMY.md). It replaced an earlier flat price list, which paid a fixed amount per completed action and could therefore be farmed with cheap or invented work by rational people acting in good faith. The shape had to change, not the numbers.

In short:

- the pool is fixed before the quarter and does not grow with the number of items created or closed, so creating work cannot create points
- the priority owner allocates the pool across registered initiatives in priority order, before work starts
- each initiative has exactly one counter with a start value, a completion value, an inventory-derived denominator, and an owner who is not the earning team
- release is proportional to how far the counter moved, with no milestone lumps
- disclosure of a blocker or of a failed approach is paid as a fraction of the progress that will now not be made, drawn from that initiative's own allocation

What is deliberately absent: any measure of volume and any measure of effort, and any payment for producing an artifact as such. In 2026, volume of output has stopped being evidence of work; generated text and code have devalued every proxy metric the old control systems rested on.

### What points can be spent on

This list must be real. Fake currency destroys trust worse than having no system at all.

- hardware, compute and GPU quota
- training, conferences, certifications
- licenses and tooling
- **protected time for the team's own technical debt** (for example, one team-week per N points): the cheapest line item for the company and the most valuable one for engineers
- hiring priority, contractor hours, an intern
- the right to decline one incoming request per quarter without explanation

### Known failure modes

Required reading before deployment. Ignoring this section is the primary way to fail this project.

**1. Prevention produces no artifact.**
The model rewards what leaves a machine-checkable trace, and the most valuable engineering work often leaves none: an incident that never happened, a bad idea talked out of existence, a colleague unstuck in a corridor conversation, a refactor that makes the next ten changes cheap. A points system rewards the visible and starves the invisible. Partial remedy: the "default", "removal" and "unblocking another team" rows. The problem is not fully solved, and what remains is closed only by hand and on purpose.

**2. Goodhart's law is unavoidable.**
Once a metric is paid for, people optimize it directly. The dangerous version is not misconduct, it is a competent team reading a published incentive and responding rationally: splitting work to farm points, producing cheap qualifying artifacts, avoiding hard thankless items. The structural answer is Rule 7 and the two invariants in ECONOMY.md: if a team cannot increase its points without moving a bounded counter that someone else owns, then farming has a ceiling equal to the real work remaining. What survives that is measured once a quarter (ECONOMY.md R8) and treated as a defect in the design rather than misconduct by a person. The rule stands: if a team found a way to farm points, the design is at fault.

**3. Extrinsic reward can crowd out intrinsic motivation.**
This is a well-studied effect, and it is the deepest risk in the whole model: a team that used to care about the system starts caring about the score. Mitigations, all structural: purchases are capability only, never cash; points are never used in performance evaluation; the score is never the goal of a quarter. If people start asking "how many points is this worth" before asking "is this the right thing to do", the model is failing and should be paused.

**4. Teams share systems, so attribution is contested.**
Awarding points for a shared result creates arguments about who contributed what, and where teams are organized by discipline the shared result is the common case rather than the edge one. Paying the owning team in full and undivided, which is what this said before, therefore starves contributing teams on most of the work they actually do, and the rational response to that is to prefer initiatives your own team owns, which is the fragmentation the method exists to remove.

Mitigation: shares are **declared at registration and countersigned** with the criterion, the counter and the trajectory ([ECONOMY.md](ECONOMY.md) R5a), never computed afterwards. Computing them afterwards needs attribution data that does not exist and produces a comparison between teams, which tier 3 forbids; declaring them beforehand needs neither. Where no shares are declared the initiative pays its owner alone, and that is stated at registration, so the choice is visible rather than discovered at settlement. A disagreement about shares then surfaces before the work starts, where the tiebreak already applies.

**5. Verification must be automated from day one.**
C3 is the condition most likely to be quietly violated, because manual verification always looks like a reasonable temporary compromise. It is not: as soon as a human confirms results by reading reports, the model has no independent evidence and reverts to conventional self-declared reporting with extra ceremony.

---

## Metrics

Four tiers. The tier a number sits in decides who may see it, and the boundary between tier 2 and tier 3 is the entire "no punishment" mechanism.

**Tier 0. The gate. Published above everything else.**

- **mapping coverage**: share of merged changes that map to a registered item
- **instrument coverage**: share of registered initiatives whose counter produced fresh data within its stated latency

Below the agreed threshold on either, **the rest of the report is not published at all**. Not with a caveat, not in grey. A confident-looking report over unknown coverage converts ignorance into confidence, which is worse than having no report. Coverage is not one metric among several, it is the precondition for the others meaning anything.

**Tier 1. System metrics. Public, discussed out loud:**

- per initiative: state (progressing, stalled, unmeasured), counter value against trajectory, and the forecast gap against the declared completion date
- throughput: items closed per week (items, not points)
- lead time p50 and p85, from creation to closure
- flow efficiency: time working versus time waiting (typically 15..25%, and the most sobering chart you can show leadership)
- time to blocker resolution
- share of detected deviations that received a decision within one review cycle
- share of decisions that executed by their date
- number of initiatives with no owner
- number of deliberately cancelled initiatives

The last two lines of the middle group are the ones that say whether control exists at all. If either is near zero, the problem is authority, not instrumentation, and more measurement will not help.

**Tier 2. Load. Restricted, and it is not performance.**

Items in progress per person exists, because without it every case of overload presents as a case of poor discipline, and misreading the first as the second is one of the failures this method was built to prevent. It is constrained: current state only, no history, no aggregation, no comparison, visible only to whoever owns that person's capacity, and it is read as a capacity signal about the system rather than a judgment about the person.

**Tier 3. Numbers that must not exist.**

Not "are not used": do not exist, in any output, including intermediate files, ad hoc queries and exports.

- any per-person performance number
- any table that places people or teams side by side in a comparable order, including point totals

Allocations are public, because they express priority. Earnings are visible to the owning team and the priority owner only, and are never rendered in one table across teams. The invariant check in ECONOMY.md R8 is computed as a single organization-wide number, not per team.

The reason is not sensitivity, it is causality: if a rankable number exists, someone above you will eventually rank with it regardless of anyone's intentions, and every honest-disclosure incentive in this method inverts the day that happens. The only defense that has ever worked is that the number is not there to be found.

**Forecasts instead of estimates.** Dates come from Monte Carlo simulation over observed throughput and counter movement. An estimate is a number produced by the party that will be judged on it, and those do not exist here. A trajectory of record does exist and belongs to the priority owner (CONTROL.md §8), so there is a baseline to deviate from without anyone having been asked for a promise.

**Health check:** if a whole quarter passes with no critical initiative cancelled and no blocker escalated, you do not have order, you have silence.

---

## Rituals

Three. That is both the minimum and the maximum.

**Weekly, 20 minutes.** It **opens** with last week's decisions that did not execute, before any new item is discussed. Then red items only. Four possible outcomes, there is no fifth:

1. continue, with a named blocker and a named person who will clear it
2. change the owner
3. explicitly defer, and drop the critical flag
4. close as "will not do"

Every outcome becomes a decision record with four mandatory fields: what was decided, who acts, by when, and what observable fact will show it happened. A decision without those fields is not a decision, and the review has not produced an outcome.

If an item goes through two consecutive reviews without landing on one of the four, it automatically becomes the fourth. If outcome 1 is chosen twice in a row on the same blocker, it escalates one level above the priority owner: repeating a decision is not a decision.

Verifying that decisions execute is the other half of the method. Verified work and unverified decisions produce exactly the failure the problem statement predicted, which is a report that generates no consequences. See [CONTROL.md](CONTROL.md) §9.

**Monthly.** Kill or defer. Cancellation is a normal outcome; "still open after two years" is not.

**Quarterly.** A retrospective on the system, not on people. Plus the next quarter's allocation of the pool, and the invariant check in ECONOMY.md R8. Mandatory output: at least one new default.

---

## How experience accumulates

A system log: one entry per cleared blocker and per failure. One mandatory field: **which default we are changing so this does not recur.** The entry is not closed while that field is empty.

Without that field any log becomes an archive nobody reads. With it the organization physically cannot step on the same rake twice, because the rake is removed from the default rather than from people's memory.

Practices spread by demonstration, not by announcement: another team copies the approach because it removes work for them (their reporting is already computed), not because they were told to. That is axiom 5 applied to the method itself.

---

## Anti-patterns

Each of these kills the method entirely, not partially.

- **Personal metrics.** Even "just for myself", even "just to understand".
- **A metric used as a KPI.** Metrics here are diagnostic, not target. A target set on a metric destroys the metric.
- **Fake currency.** Points that cannot actually be spent are worse than no points.
- **Manual verification.** The moment a human confirms things by reading a report, you are back where you started.
- **Publishing over unknown coverage.** A report whose denominator is unknown is not a weak report, it is a confident wrong one.
- **Treating missing data as unchanged.** A null that inherits the previous value, or becomes a zero, hides the exact case you most need to see.
- **Letting the definer, the doer and the instrument owner be the same party** without marking it. Marking it is acceptable; silence about it is not.
- **Adding process without removing process.**
- **A document longer than two pages.** A method that does not fit on two pages does not get applied. This file is already over that limit: before deployment, distill it to one page and move the rest into an appendix.
- **Deployment by top-down mandate.** A methodology announced as an order reads as surveillance, which takes you back to axiom 1.

---

## Two requests you will receive, and what to say

Both arrive from above, both sound reasonable, both are fatal, and both will be made by someone who means no harm. Deciding the answer in advance is cheaper than improvising it in the moment.

**"Let us align this with the existing goal-setting process."**
Answer: these numbers are diagnostic, and the moment a target is set on one of them it stops describing reality and starts describing what people believe is expected. Offer the substitute rather than only refusing: the goal process can take the initiative's declared completion date, which is an outcome, and leave the flow numbers as instrumentation. What is being protected is the ability to see, not anyone's comfort.

**"Can we see this broken down per person?"**
Answer: that number is not produced anywhere, on purpose, and there is nothing to enable. Explain the mechanism rather than declining: if a rankable number exists, it eventually gets used for evaluation, and on that day every incentive to declare a blocker early inverts, because declaring one becomes an admission of weakness in a comparison. Then answer the question actually being asked, which is usually "who needs help": that is a capacity question, it is answered by the load view with the person's own manager, and it does not require a ranking.

The reason this section exists at all: the method's threat model was an engineer who misreports, but the parties who lose from objective measurement are the ones whose position depends on ambiguity, and they are almost never engineers.

---

## Lineage

The method is assembled almost entirely from existing work. That is deliberate: 95% of adoption failures come not from a shortage of ideas but from taking a ready-made framework wholesale.

| Element | Source |
|---|---|
| The problem is in the system, not the people; "drive out fear" | Deming, 14 points |
| Flow metrics, aging WIP, forecasting instead of estimating | Kanban, Actionable Agile (Vacanti) |
| Blameless failure analysis | Google SRE |
| Psychological safety as a precondition for truthfulness | Edmondson |
| Improvement through a continuous cycle of small changes | Toyota improvement kata (Rother) |
| The constraint as the place to apply effort | Goldratt, Theory of Constraints |
| Effect of practices on organizational outcomes | DORA, "Accelerate" |
| Truthful reporting engineered to be the dominant strategy | mechanism design and incentive compatibility (Hurwicz, Myerson) |
| Metric-as-target degradation | Goodhart, Campbell |
| Extrinsic motivation crowding out intrinsic | Deci, Ryan |

Two things here are not borrowed: applying incentive-compatible reward design to engineering delivery, where the verifying artifact is production itself; and accepting that in 2026 volume of output is no longer evidence of work, which leaves observed change in system behavior as the only durable unit of progress.

---

## Open questions

The unsolved parts. This is the most important section in the file, and it shrinks as things get tested in practice.

1. How to reward prevention and problems that never happened, where there is no observable event. Not solved, and probably not solvable inside this frame: prevention leaves no change in system state, which is the only unit this method can see. Currently handled outside the instrument, by hand.
2. Who owns the budget that converts points into real purchases. Without it stage 3 does not work (see the "fake currency" anti-pattern).
3. How to account for an initiative pulled by two teams. Answered in v0.9: shares are declared at registration and countersigned, never computed afterwards ([ECONOMY.md](ECONOMY.md) R5a). What is untested is whether declaring them is cheap in practice, or whether it becomes one more negotiation standing between a priority and the start of work.
4. Calibration of the pool size and of the disclosure fractions in ECONOMY.md. The shape is the claim; every number in it is arbitrary until a quarter has run.
5. What to do in an environment where whoever introduces the method has no escalation authority. Stage 0 still works there and is worth running alone, but stages 1 and up do not, and this is the single most common reason the method will not be adoptable in an outside organization.
6. Whether the priority owner becomes a bottleneck once every registration needs a countersignature. The provisional-registration rule is a guess, not a result.
7. Whether the coverage gate survives contact with reality, or whether the threshold simply gets lowered until the report can be published. Partly answered in v0.9: the threshold is fixed and published before the first report, and any change to it is versioned exactly like a declared completion date ([CONTROL.md](CONTROL.md) §4), so lowering it stays legitimate and stops being invisible. What remains unknown is whether a visibly lowered threshold costs anything in an organization where nobody above the priority owner is watching.
8. Whether the instrument can be operated inside its stated cost. CONTROL.md §12 publishes an estimate of the operator's weekly hours, and it is a guess. If the real number is materially higher, the instrument gets maintained for one quarter and then quietly stops, and no other assumption in this method is load-bearing in the same way, because everything else degrades visibly and this degrades silently.
9. Whether claim C1 holds at all, which has never been tested. The whole method rests on the true state of work being derivable from artifacts, three analysis passes have argued about it, and argument cannot settle it. The test is in CONTROL.md §12 and costs about a day.

---

## Changelog

| Version | Date | What and why |
|---|---|---|
| 0.9 | 2026-09-07 | Fixes from the third analysis pass ([ANALYSIS.md](ANALYSIS.md) §13), which audited the mechanisms against the original symptom list for the first time. Mechanism 7 added, a published bound on work in progress: symptom 3 was only half addressed, since everything in the method ordered what should be worked on and nothing limited how much is open at once, while PROBLEM.md H2 already stated that priority means nothing under unbounded capacity (F1, P25). Mechanism 1 now draws the criterion from four admissible forms instead of free text, because the fix applied to decision evidence was never applied one level down, and a prose criterion passes the detector, counts toward the coverage gate and still leaves acceptance to a person reading a sentence (F2, P26). Mechanism 1 also gained the removal clause: where an initiative replaces something, a counter can reach completion with the replaced state still deployed (F7, P31). Failure mode 4 rewritten, because cross-discipline initiatives are the common case in a discipline-organized chain, so paying the owner undivided starved contributors on most real work: shares are now declared at registration and countersigned (F3, P27). The fourth priority-owner measure is normalized per initiative-quarter, since as a raw count it punished exactly the long initiatives the organization is failing at (F4, P28). Open question 3 answered, 7 partly answered, and 8 and 9 added, which are the operating cost and the untested central claim. |
| 0.8 | 2026-09-07 | The author stated the real authority chain, which runs from a decisive manager through a senior delivery role and a per-project delivery role to the discipline team managers. Three consequences were written into Roles. Check 2 fails, because the priority owner is the top of that chain and two mechanisms escalated to a level that does not exist, so escalation is redefined as widening the audience of an unresolved item rather than moving it up a line, with a superior treated as the cheapest audience. Check 3 becomes maximally severe in a vertical line, because the decisive manager's own result is the sum of the teams below, which makes the four substitute measures mandatory and publishable only to an outside audience since nobody above can enforce them. Cross-discipline instrument ownership becomes the natural arrangement, since the separation rule constrains the party and not the reporting line. Added a pointer to [AUTHORITY.md](AUTHORITY.md), which assigns the roles concretely and checks every authority-dependent mechanism against the assignment. |
| 0.7 | 2026-09-07 | Specified what the priority owner is measured on, four checks for whether the role is actually filled, and which existing roles can hold it. Written after the role was discussed against a real organization, where the answer exposed that the method named the role and left three things unstated: that the obvious candidates are already measured on delivering what they countersign, which concentrates definer capture in one person holding all three levers instead of moving it away from the measured party; that a role at the top of the chain silently breaks the escalation mechanism, which escalates one level above the priority owner; and that appointing both natural candidates recreates negotiation rather than adding their strengths, so the requirement is a tiebreak and not a title. Also stated what to do when the role cannot be filled, which is to publish contention for capacity as the first finding rather than to appoint someone nominally. |
| 0.6 | 2026-09-07 | Added the definer span limit after the second simulation run ([SIMULATIONS.md](SIMULATIONS.md) §12 N2) found that the Roles section fixed the structural gap and left the attention limit open: a priority owner holding thirty initiatives countersigns whatever was proposed, which restores self-definition with a formal approval on top. The number of initiatives per priority owner is now published and the role must be split beyond roughly ten. |
| 0.5 | 2026-09-07 | Turned the method into a control instrument rather than only an incentive model, after the observation that it verified presence of artifacts well while the original problem was absence. Added mechanism 6 (absence is detected, not noticed) and [CONTROL.md](CONTROL.md). Added the Roles section, which closes the largest structural gap: the method specified who executes and who verifies and left unspecified who defines, so definition defaulted to the party being measured. Rebuilt metrics into four tiers with coverage as a gate, load explicitly permitted as tier 2, and rankable numbers explicitly non-existent as tier 3. Made decisions verifiable artifacts. Stated the applicability boundary and the adoption order, with the economy demoted to an optional stage 3. Added the two prepared answers to the requests that predictably arrive from above. Redefined ownership as a grant of authority rather than exposure. |
| 0.4 | 2026-09-06 | Removed the flat per-action price list and moved point issuance to [ECONOMY.md](ECONOMY.md). Reason: any scheme paying a fixed amount per completed action can be farmed with cheap or invented work, because the earning team controls how many payable units exist, and no choice of numbers fixes that. Added Rule 7 (no point source whose supply the earner controls) and rebuilt the payoff table so that delivering the outcome pays strictly more than disclosure, which the old list violated. |
| 0.3 | 2026-09-06 | Made every example vendor-neutral and environment-neutral, so nothing points at a specific organization's stack. Added the note under mechanism 4 that an initiative with no constructible ground-truth number cannot be tracked objectively by any method, which is a precondition worth failing fast on. |
| 0.2 | 2026-09-06 | Rebuilt the contribution economy as a first-principles incentive model: payoff analysis, six conditions, before-and-after payoff tables. Dropped the external analogy the idea originally came from, because a mechanism intended to be portable to other organizations has to stand on its own logic. Added open question 6 on whether the economy is needed in the first quarter at all. |
| 0.1 | 2026-09-06 | First draft. Nothing verified in practice. |
