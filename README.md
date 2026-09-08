# Evidence-Driven Delivery

**Version:** 0.2
**Date:** 2026-09-08
**Status:** design complete, never run. No part of this has been tested in a real organization. Read it as a specification with an argument attached, not as a practice with results.

A delivery method for engineering organizations where the state of the work is not badly reported but genuinely unknowable, because every source of information about it is a person who will be judged on what they say.

The symptoms are ordinary: priorities are announced, work is distributed, and months later nobody can say what is true. Some items were never created. Some work never appeared in any system. Some tasks have been open for years. All the reports look fine. Asking harder produces better reports rather than better information.

## The claim

People do not conceal the state of work because they are dishonest. They conceal it because telling the truth costs more than staying quiet. So the method does three things instead of adding a reporting layer:

- **derive state from artifacts** that exist as a by-product of doing the work, so nobody is asked anything
- **make bad news the highest-paying available action**, so disclosure beats silence for a self-interested party and not only for an honest one
- **detect what is missing** by query, rather than verifying what was claimed, because the original problem is absence and presence checks say nothing about it

Three invariants carry the whole design. Every rule in it is machinery for these:

```
1.  deliver the outcome  >  disclose a blocker or a failed approach  >  silence = unverified claim = 0
2.  no point source exists whose supply the earning team controls
3.  measured and progressing  >  measured and stalled  >  unmeasured
```

## Where to start

| Read this | If you want |
|---|---|
| [ONEPAGE.md](ONEPAGE.md) | the whole method in five minutes. Start here |
| [PROBLEM.md](PROBLEM.md) | the problem, the hypotheses with checks you can run this week, and what success would look like. This document outranks the method: if the method stops answering it, the method changes |
| [CONTROL.md](CONTROL.md) | what to build first. Needs no points, no economy and no budget. §12 is the first run, day by day |
| [METHODOLOGY.md](METHODOLOGY.md) | the long form: axioms, seven mechanisms, four roles, metric tiers, rituals, anti-patterns |
| [AUTHORITY.md](AUTHORITY.md) | who may do what in an ordinary reporting chain, and why the method is unbuildable without answering that |
| [ECONOMY.md](ECONOMY.md) | how points would be issued, if they ever are. Optional, last, and skippable forever |
| [ANALYSIS.md](ANALYSIS.md), [SIMULATIONS.md](SIMULATIONS.md) | the case against the method. Three adversarial passes and seventeen scenarios, including the ones it failed |
| [HANDOFF.md](HANDOFF.md) | the state of the work, the decisions already settled, and every open question |

The first thing to do is not a build. Take three initiatives, derive their state from artifacts alone, then ask the people doing that work privately what is actually true, and compare the two. It costs a day, needs nobody's agreement, and it tests the one claim everything else rests on.

## What it deliberately does not do

- **It does not measure people.** No per-person or per-team ranking is produced anywhere, including in exports and intermediate outputs. The honest form of the guarantee: the system does not produce evaluation data, which is not the same as making evaluation impossible.
- **It does not replace your tracker.** A record must have exactly one write path, or "people forget to create items" simply migrates to the new tool.
- **It does not use estimates.** An estimate is a number produced by the party who will be judged on it. Forecasts come from historical throughput instead.
- **It does not apply everywhere.** It needs an initiative with an independently observable ground-truth number, which limits it to infrastructure, platform, reliability and migration work today and excludes most product, design and research work.
- **It does not reward prevention,** and cannot in this frame: an incident that did not happen leaves no change in system state.

## Editing conventions

If you send changes: documentation is in English, no em dash in any `.md` file, no named vendors or employers anywhere, every file carries a version and a changelog stating the reason for each change, and PROBLEM.md outranks METHODOLOGY.md. The full list is [HANDOFF.md](HANDOFF.md) §3, and the decisions that are settled and should not be relitigated are §4.

## License

[CC BY-SA 4.0](LICENSE). Use it, adapt it, instantiate it inside a company, sell services around it. Two conditions: credit the source, and publish adaptations under the same license. Attribute as *Evidence-Driven Delivery*, https://github.com/n0rm4l-me/evidence-driven-delivery.

The answers an adopting organization fills in are its own facts, not adaptations of this work, and nothing here asks for them back.

---

## Changelog

| Version | Date | What and why |
|---|---|---|
| 0.2 | 2026-09-08 | Licensed under CC BY-SA 4.0, replacing the placeholder that said no license was attached yet. A methodology with all rights reserved cannot be adopted by the organizations it is written for, because their legal review stops at the missing license, and share-alike keeps adaptations readable by everyone who adopts it. |
| 0.1 | 2026-09-08 | Written when the repository was prepared for publication. There was no entry point: a reader landing on nine documents of two hundred lines each reads none of them, and the two things they need first are where to start and the fact that none of this has been run yet. |
