# HANDOFF: state of work on Evidence-Driven Delivery

**Last updated:** 2026-09-08 (sixth update: repository initialized, licensed and published, organization-specific material split out)
**Purpose:** let any model (or the author two weeks from now) resume exactly where work stopped. Read top to bottom. §0 gives the immediate next action.

---

## §0 What to do next

Design is closed under a stop rule. All 34 proposed changes across four analysis batches are applied, the simulations have been run twice, both adoption blockers are answered (§5), and the third pass ended with an explicit rule: **no further mechanism enters the method until the first run produces a number** (ANALYSIS.md §13 F12, CONTROL.md §12). Every pass so far has added machinery, and machinery is what the operator pays for weekly.

1. **Run the first day, not the next document.** CONTROL.md §12: take three initiatives, derive their state from artifacts alone, ask the people doing the work privately what is true, and compare. Claim C1 carries the entire method, three analysis passes have argued about it, and argument cannot settle it. A day of work, nobody's permission needed, and a divergence would be the most valuable output this project can produce.
2. **Both blockers are answered, and the answers are in [AUTHORITY.md](AUTHORITY.md) and [ECONOMY.md](ECONOMY.md) R12.** The chain is vertical and ends at the party who owns team capacity, so that party is the priority owner. Two consequences are load-bearing and must not be dropped in adoption: escalation is redefined as widening the audience of an unresolved item, because there is no level above the top of the chain; and the priority owner's own result is the sum of the teams below, so the four substitute measures are mandatory and have to be published to that outside audience since nobody above can enforce them.
3. **If only one document gets read, read [ONEPAGE.md](ONEPAGE.md).** If only one thing gets built, build stage 0 of [CONTROL.md](CONTROL.md): coverage plus the absence detectors. It needs nobody's permission and probably carries most of the effect.
4. **Four findings that must not be relearned the hard way:**
   - priority means nothing while capacity is unbounded, and for three analysis passes nothing in the method bounded it. With nine items open per person, priority #1 and priority #9 both move at zero speed, every detector reports each stall truthfully, and the review has no vocabulary for the cause (ANALYSIS.md §13 F1, METHODOLOGY.md mechanism 7)
   - the method removes lying about state and relocates the entire lie surface into *definition* (criterion, counter, allocation), which is why the Roles section exists and why the definer span limit exists (ANALYSIS.md §2, P1, P20)
   - no point source may exist whose supply the earning team controls. **Do not reintroduce a per-action price list** in any form: any flat per-action fee is farmable with cheap or invented work by rational people acting in good faith, and no choice of numbers fixes it (ANALYSIS.md §4, ECONOMY.md §1)
   - the original complaint was about *absence*, and verifying presence does nothing for it. Coverage is a gate, not a metric (CONTROL.md §4, §5)
5. **The honest state of the design:** the borrowed parts (artifact-derived state, absence detection, flow metrics, verified decisions) are sound and cheap. The novel part (the economy) failed most of the first-run simulations, was rebuilt, and is now optional stage 3. If it is never adopted, the method still works. Say this out loud to anyone evaluating it.
6. **What is still unsolved and stated as such in the documents:** prevention pays nothing and cannot under this frame; instrument and definer capture are priced but not eliminated; the method only applies where an initiative has a constructible ground-truth counter; per-person load data is a deliberate hole in the no-ranking guarantee (SIMULATIONS.md §12 N6); the operating cost of about half a day a week is a guess, and it is the one assumption whose failure is silent rather than visible; and claim C1 has never been tested.
7. **Do not reintroduce** the external analogy the points idea originally came from. Removed on purpose, see §3.

---

## §1 What this repository is

A delivery methodology for engineering organizations where the state of work is unknowable because all reporting is self-declared. Two claims carry it: state should be derived from artifacts that exist as a by-product of the work, and honest disclosure of problems should be the highest-paying available action rather than merely the ethical one.

Intended to be adaptable by different companies, possibly as a product later. Therefore vendor-neutral and free of any single organization's specifics.

## §2 Files and current versions

| File | Version | Role |
|---|---|---|
| [README.md](README.md) | 0.2 | The entry point for anyone arriving cold. Says what this is, what it is not, and what to read in which order |
| [PROBLEM.md](PROBLEM.md) | 0.7 | The class of problem being solved. **Primary document:** if the method stops answering it, the method changes |
| [ONEPAGE.md](ONEPAGE.md) | 0.3 | The short form, and the only one to hand to anyone else first |
| [METHODOLOGY.md](METHODOLOGY.md) | 0.9 | The method: 5 axioms, 7 mechanisms, 4 roles, conditions, rules, 4 metric tiers, rituals, anti-patterns, adoption order, lineage |
| [AUTHORITY.md](AUTHORITY.md) | 0.2 | Who holds which role in a four-level reporting chain, what each level may and may not do, and all 18 authority-dependent mechanisms checked against the assignment |
| [CONTROL.md](CONTROL.md) | 0.5 | The control layer, and the part to build first. Needs no points, no economy, no budget. §12 is the first run |
| [ECONOMY.md](ECONOMY.md) | 0.6 | How points are issued, if they ever are. Optional stage 3. Closed form, 2 invariants, 12 rules |
| [ANALYSIS.md](ANALYSIS.md) | 0.4 | Adversarial analysis. 24 changes in §12, 10 more in §13, all applied. §13 is the whole-model pass and ends with the stop rule |
| [SIMULATIONS.md](SIMULATIONS.md) | 0.3 | 17 scenarios in two runs. Run 1: 7 of 10 failed. Run 2 (§12): 9 of 10 now hold, plus 7 new scenarios that found 4 more defects |

Consistency rule for whoever continues: ANALYSIS.md §1 to §11 and SIMULATIONS.md §1 to §11 describe METHODOLOGY.md v0.3 on purpose, because they are the reasoning that produced everything after it. Do not rewrite them to match the current method. Mark resolutions inline instead, or add a new section, which is what §12 of each does.

Reading order for a fresh session: [README.md](README.md), ONEPAGE.md, PROBLEM.md, CONTROL.md, AUTHORITY.md, then ANALYSIS.md §2 and §12, then SIMULATIONS.md §12. METHODOLOGY.md and ECONOMY.md are the detail and can wait.

**One file is not in the repository.** `NOTES.md` sits in the working directory, is listed in `.gitignore` and is never committed. It holds the organization-specific answers to the two blockers, with the titles and the chain as they were actually stated, plus the product positioning note. A session that has it should read it after this file; a session that does not is missing history and no method content, because everything load-bearing was restated by function in AUTHORITY.md, ECONOMY.md R12 and §5 below.

## §3 Hard constraints

Non-negotiable unless the author says otherwise. Violating these has already cost one rewrite each.

- **All documentation in English.** Conversation with the author happens in Russian; files do not.
- **No em dash (`—`) in any `.md` file.** Use a colon, a comma, or rephrase.
- **Vendor-neutral and employer-neutral.** No named tracker, no named infrastructure, no internal scripts, no environment names beyond generic ones. Organization-specific facts belong in PROBLEM.md's "preconditions each adopter must establish", answered outside the repository.
- **No external analogy for the points economy.** The idea originated from an outside points-based system; the author asked for the analogy to be removed entirely, and the mechanism was rebuilt as a first-principles incentive argument (payoff tables, conditions C1 to C6, lineage via mechanism design and incentive compatibility). Do not put the analogy back.
- **PROBLEM.md outranks METHODOLOGY.md.**
- **Every file carries a version and a changelog with the reason for each change.**

## §4 Decisions already made, do not relitigate

| Decision | Reason |
|---|---|
| Do not build a new tracker; derive from the existing one | a record must have exactly one write path, or "people forget to create items" simply migrates |
| Read-only layer over existing systems, not a system of record | avoids double entry, auth, migration and adoption risk |
| No story points, no estimates; forecast from historical throughput | an estimate is a number produced by the person judged on it |
| No per-person performance metrics, structurally | if the numbers exist, someone will eventually use them for evaluation |
| No negative points; zero is the only penalty | once concealment is cheaper than disclosure, every confirmation mechanism inverts |
| Planning layer lives in a versioned file in git, not a database | assignment history becomes auditable through review, and no new store is needed |
| Pilot chosen by measurability, not by importance | the method needs one initiative with independently observable ground truth |
| Staged rollout, economy last | ANALYSIS.md §11; the economy carries most of the risk and least of the proven value |
| No per-action price list, ever | the earner controls how many payable actions exist, so any flat per-action fee is farmable regardless of the numbers chosen |
| Fixed point pool, set before the period | creating work must not be able to create points |
| Counter denominators come from a system inventory, not from a list the team supplies | otherwise scope shrinks at registration and 100% is reached while the real problem is untouched |
| Decomposition is a gate for registration, not a payable outcome | paying for it produced decomposition theatre |
| Disclosure is a fraction of forgone progress, not a flat fee | it makes the payment scale with the priority of what is stalled, and it cannot be manufactured without a prior public commitment to lose |
| Coverage is a gate, not a metric: below threshold the report is not published at all | a report that looks authoritative over an unknown share of the work converts ignorance into confidence, and what escapes the system is exactly the work that disappears |
| Three counter states, never two, and unmeasured is never cheaper than measured | missing data read as unchanged produces a calm green report over a system nobody is watching, and a system that pays teams whose telemetry broke will get telemetry that stays broken |
| Definition and execution are separate parties, and the definer role has a bounded span | verification can be perfectly objective while the bar quietly drops, and a definer holding thirty initiatives rubber-stamps whatever was proposed |
| Decisions are artifacts, and their evidence comes from a closed list | otherwise decision verification degrades into the same negotiation the acceptance criterion used to be |
| The declared completion date is versioned and its history is published | resetting the date resets the forecast gap, legitimately and indefinitely |
| The priority owner is the party who owns team capacity, and the middle delivery role operates the instrument instead | the two candidates fail opposite checks, and appointing both recreates negotiation; the middle role lacks capacity authority, which is exactly what operating the register does not need |
| Escalation means widening the audience of an unresolved item, not moving it up a line | the priority owner is normally the top of a chain, so two mechanisms escalated to a level that does not exist, and a superior is only the cheapest audience |
| The tiebreak is never delegated; the countersignature is delegated per initiative to a discipline manager outside the executing discipline | uniqueness and the ten-initiative span limit conflict beyond ten competing initiatives, and only the tiebreak has to be unique |
| The four priority-owner measures are computed per countersigner, not only for the priority owner | delegated countersignature invites reciprocal leniency between peers, which is priced by making a trading pair produce two visibly bad columns |
| Review outcomes that change the priority order take effect only when countersigned | otherwise the review can quietly reorder the priorities it exists to serve |
| Work in progress is bounded and the bound is published | priority means nothing under unbounded capacity: with nine items open per person, priority #1 and priority #9 both move at zero speed, every stall reports truthfully, and no blocker names the cause. This was the only one of the nine original symptoms with no mechanism pointed at it |
| Acceptance criteria come from four admissible forms, never free text | a prose criterion passes the presence detector, counts toward the coverage gate, and still leaves acceptance to a person reading a sentence, which is the negotiation the criterion exists to end |
| Where an initiative replaces something, the criterion names the removal and the counter is denominated on the old inventory | otherwise the counter honestly reaches completion while the replaced thing is still deployed, configured and paid for |
| Contribution shares are declared at registration and countersigned, never computed afterwards | cross-discipline initiatives are the common case, so paying the owner undivided starved contributors on most real work; declaring beforehand needs no attribution data and produces no ranking |
| The coverage threshold is published once and versioned like a declared date | it is agreed by the party the gate constrains, so the predicted failure is drift rather than override |
| Two detectors point at the instrument rather than at the work | the realistic death of a control layer is a quiet stop with every published number still technically true |
| The first day is a test of claim C1, not a build | the claim that state is derivable from artifacts carries everything and has never been checked; argument cannot settle it and a day of comparison can |
| Published under CC BY-SA 4.0 | a method with all rights reserved cannot be adopted by the organizations it is written for, because their legal review stops at the missing license; share-alike keeps adaptations readable, and copyright stays with the author, so a differently licensed product version remains possible |
| No new mechanism until the first run produces a number | three passes each added machinery, the operator pays for machinery weekly, and design error is now cheaper than operating error |
| The economy is optional stage 3 and may never be adopted | it is the only novel part, it failed most of the first-run simulations, and stopping after stage 2 forever is a legitimate end state |

## §5 The two adoption blockers, both answered

Both were answered on 2026-09-07, and both produced method changes rather than only answers. What is recorded here is what the answers changed. The answers themselves are specific to one organization, so they are kept outside the repository (see the note at the end of §2).

1. **Who has the authority to tell a team "drop that, work on priority #1"?** Without such a person the numbers surface stalls and nothing follows, and the reporting simply becomes more careful. This is the failure criterion recorded in PROBLEM.md.

   Three findings came out of answering it, and all three are in the method now.

   **Administrative rights are not the role.** The method needs authority to interrupt work in progress, not permission to edit a field. Many people hold the second and usually nobody holds the first. This is why PROBLEM.md precondition 1 states what counts as an answer instead of only asking the question.

   **Priority set per project is not an ordering.** Where each project head orders work inside their own project and the teams are shared across projects, no single ordering exists across initiatives competing for the same people. Conflicts then resolve by proximity and escalation volume, which is symptom 3 in PROBLEM.md ("teams work on whatever happens to be at hand rather than on what is prioritized") stated as a cause rather than as an observation. This may be the root cause of the entire pattern, and the priority owner role in METHODOLOGY.md silently assumed it was already solved.

   **The two candidate role shapes fail opposite checks.** A delivery role spanning several projects has the breadth and usually not the teeth. A manager owning the capacity of several teams has the teeth and possibly not the breadth. Appointing both recreates the negotiation the role exists to end. The resolution is in [AUTHORITY.md](AUTHORITY.md): the party with capacity authority is the priority owner and holds the tiebreak, the delivery role operates the instrument and may not change priority, instruments are owned cross-discipline because the separation rule constrains the party rather than the reporting line, and the assignment is checked against all 18 authority-dependent mechanisms.

   **The answer creates two obligations, and neither is optional.** First, an ordinary reporting chain has no level above its top, so escalation had to be redefined as widening the audience of an unresolved item. Second, the line is vertical, so the priority owner's own result is the sum of the teams below and they set the bar they are measured against, whatever the org chart shows. The four substitute measures (coverage, decision latency, decision execution, date movement) therefore have to be adopted together with the role and published to that outside audience, because nobody above can enforce them. This is the weakest point of the whole adoption and belongs in the proposal, not in the post mortem.

2. **Who owns the budget that converts points into real purchases?** Without a real ability to spend, the economy is theater, and fake currency damages trust more than having no system.

   **The cheap substitute, if the answer is nobody.** Invariant 1 can be held with authority instead of money. One guarantee is enough: a declared blocker moves off the team to a named person one level up within a single review cycle, and the questions stop. That buys what points would buy, which is relief from pressure, and it costs nothing. It is already written down as success criterion 5 in PROBLEM.md. Stages 0 to 2 plus that guarantee deliver most of the effect with no budget at all, and that is the recommended path wherever this question has no answer.

   **Answering it produced [ECONOMY.md](ECONOMY.md) R12.** "Who should own the budget" turned out to be the wrong question, because the document specified how points are issued and never specified how they are honoured. The answers, in order of how much they change:

   - Nobody has to own it. Stage 3 is optional and stages 0 to 2 cost nothing.
   - No new money is needed. Almost every organization already hands out a discretionary capability budget on request with approval; stage 3 asks that an existing one be allocated by what was earned instead of by who asked. That is a far smaller negotiation than finding funding.
   - The cheapest currency is protected time, which the capability floor in R9 is already denominated in, so the minimum viable budget owner is whoever can grant a team uninterrupted time, at zero cost.
   - Budget owner and priority owner may be the same party: the separation rule covers {defines, executes, instruments} only. Where they coincide, R12 matters twice as much.
   - **The requirement that actually decides whether stage 3 is real:** redemption must be non-discretionary against a catalogue agreed before the period. If purchases can be refused individually, points are a promise, teams price them at zero within a quarter, and invariant 1 fails silently while appearing to hold.

A third and softer question is open: is the method for teams the introducer manages, or for teams they do not? In the second case the center of gravity shifts from control to exchange, and a section on what a team gets in return for transparency has to be written. It is PROBLEM.md precondition 3 and it is unanswered.

## §6 Open questions by document

**METHODOLOGY.md:** rewarding prevention (no observable event); calibration of the pool size and the disclosure fractions; adoption without escalation authority; whether the economy is needed in quarter one at all; whether the instrument can be operated inside its stated cost of roughly half a day a week, which is the one assumption that degrades silently rather than visibly; and whether claim C1 holds at all, which the first run tests. Shared initiatives between two teams is no longer open: shares are declared at registration (ECONOMY.md R5a).

**ECONOMY.md §5, the residual attack surface after closure:** instrument capture (the team owns the telemetry behind its own counter, which pricing cannot fix and which is therefore a precondition); definer capture (integrity now concentrates in one role rather than spreading across many engineers, a smaller surface but a more concentrated one); prevention work still pays nothing; counter movement caused by someone else, left unaddressed on purpose because attribution costs more than the points.

**PROBLEM.md:** whether H6 and H7 can be diagnosed honestly from inside; applicability where no ground truth exists; the minimum viable subset.

**ANALYSIS.md:** answers the minimum-subset question in §11. Leaves open how to price work whose outcome is a decision rather than a state change (A1, P11 scopes it out rather than solving it).

**CONTROL.md, the residuals it states about itself:** it does not measure people, and the honest form of that guarantee is that the system does not produce evaluation data rather than that evaluation is impossible; load numbers are the one deliberate hole. It does not cover work whose outcome is a decision. It does not reward prevention and cannot. It does not adjudicate attribution when a counter moves for outside reasons.

**Not yet examined at all:**
- What the read-only tooling should actually be. Discussed in conversation, never designed here.
- How the method behaves in an organization with more than roughly fifty engineers. All reasoning so far assumes a handful of teams.
- Positioning if this becomes a product. Licensing is settled: CC BY-SA 4.0.
- Whether "share of work outside the tracker" can be measured without code-host access.

## §7 The limit on where this can be used at all

Applicability requires an initiative with an observable ground-truth number. That limits the method to infrastructure, platform, reliability and migration work, and excludes most product, design and research work (ANALYSIS.md A1, and the applicability boundary in METHODOLOGY.md). It is the first thing to say to anyone considering it, because a pilot chosen outside that set fails for reasons that have nothing to do with the method.

The adoption dynamic that follows from it is analysed rather than solved: the parties who benefit are not the parties who decide to adopt (ANALYSIS.md §7, SIMULATIONS.md §10). Spread by demonstration is therefore predicted to stall, and the moment a mandate becomes necessary is worth choosing deliberately instead of discovering.

---

## §8 Changelog

| Date | What |
|---|---|
| 2026-09-08 (latest) | Repository initialized, licensed under CC BY-SA 4.0 and published at https://github.com/n0rm4l-me/evidence-driven-delivery. [README.md](README.md) written, because the repository had no entry point and a reader landing on nine files of 200 lines each reads none of them. HANDOFF.md split: §5 now states only what the two answers changed in the method, §7 leads with the applicability limit instead of the go-to-market note, and the organization-specific material (the chain with its titles, the wrong answers, the positioning note) moved to a local `NOTES.md` that is gitignored. The reason for the split is not confidentiality of names, since none were ever in the repository: it is that the old §5 was an attributable record of one organization's inability to enforce a priority order, and the old §7 read as a plan to sell to the party the method measures. Both are true and neither belongs under a public account. No method content was lost, because AUTHORITY.md, ECONOMY.md R12 and PROBLEM.md already carry every consequence by function. PROBLEM 0.7 for the same reason in one line of its own changelog. Licensed CC BY-SA 4.0 (README 0.2), which closes one of the four items that had never been examined. The statement in PROBLEM.md that the symptom pattern was observed directly was kept deliberately: without it the document is one more theory about how things tend to be. |
| 2026-09-07 (third pass) | Third analysis pass, ANALYSIS.md §13, against the whole model rather than one document: does it act on the original symptom list, and can it be operated for a quarter. Audited PROBLEM.md's nine symptoms against the mechanisms for the first time, which found the strongest gap of the project so far: nothing anywhere bounded work in progress, although H2 already stated that priority means nothing under unbounded capacity, so symptom 3 had no mechanism pointed at it and the success criteria did not measure it either. Ten findings, P25 to P34, all closed. METHODOLOGY 0.9 (mechanism 7, four admissible criterion forms, the removal clause, shares declared at registration, normalized date movement, open questions 3, 7, 8, 9), CONTROL 0.5 (§12 the first run, three new detectors, two meta-detectors on the instrument itself, versioned gate threshold, old-inventory denominators), ECONOMY 0.6 (R5a and residual 7), AUTHORITY 0.2 (assignment not volunteered, the bound placed with the discipline managers), ONEPAGE 0.3, PROBLEM 0.6 (success criterion 11). Six of the ten findings were about operating the instrument rather than designing it, which is the expected profile for a design attacked three times and an operation never examined once. Design now closed under a stop rule. Still not a git repository. |
| 2026-09-07 (later) | The author stated the authority chain, which resolved blocker 1 as case (a) and produced METHODOLOGY 0.8, CONTROL 0.4, ECONOMY 0.5, ONEPAGE 0.2 and a new document, AUTHORITY.md 0.1, assigning the four roles level by level and checking 17 authority-dependent mechanisms against the assignment. Writing it found two gaps: uniqueness of the tiebreak conflicts with the ten-initiative span limit, closed by delegating the countersignature (never the tiebreak) to a discipline manager outside the executing discipline and pricing reciprocal leniency by computing the four measures per countersigner; and two of the four review outcomes change the priority order, which the ownership grant did not distinguish, so they now require a countersignature. The earlier answer to blocker 2 produced ECONOMY R12. Both blockers are now answered and the remaining work is adoption. Still not a git repository. |
| 2026-09-07 | All twelve proposed changes accepted by the author and applied. METHODOLOGY 0.5 then 0.6: Roles (the largest structural gap, since the method specified execution and verification and left definition to the party being measured), mechanism 6 for absence detection, four metric tiers, verified decisions, the applicability boundary, the adoption order with the economy demoted to optional, the definer span limit. CONTROL.md written (0.1 then 0.2): the control layer that needs no economy, with coverage as a gate, ten absence detectors, three counter states with invariant 3, the forecast gap, and verification that decisions execute. ECONOMY 0.2 then 0.3. ONEPAGE.md written. PROBLEM 0.4 with coverage and decision execution added to the success criteria, which had been measuring success and failure against different things. SIMULATIONS 0.3: second run, nine of ten original scenarios now hold against three before, plus seven new scenarios attacking the new machinery that found four more defects, one of them created by a fix. ANALYSIS 0.3 records all 24 dispositions. Design work is at a stopping point; the remaining blockers are the author's two unanswered questions. Still not a git repository. |
| 2026-09-06 | Repository created. PROBLEM.md and METHODOLOGY.md drafted, then de-analogized (METHODOLOGY 0.2) and made vendor-neutral (PROBLEM 0.2, METHODOLOGY 0.3). ANALYSIS.md and SIMULATIONS.md written; the analysis found that the price list could be farmed with cheap or invented work. ECONOMY.md 0.1 written to close that structurally, and METHODOLOGY moved to 0.4 with the price list removed and Rule 7 added. Nine of twelve proposed changes still pending decision, P1 the most urgent. Not initialized as a git repository yet. |
