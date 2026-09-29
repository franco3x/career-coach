# Career Pivot — Weekly Plan (Tier 1 close-out + Tier 2, through 2026-12-31)

*Companion to `Career_Pivot_Roadmap.md` — that file holds the full strategy, gap analysis, and Tier 1/2/3 definitions; this file is just the week-by-week execution checklist for closing Tier 1 and Tier 2 by end of 2026. Update it as weeks close; when Tier 2 is done, log the outcome in the main roadmap's Progress Tracking Log rather than here.*

**Assumption carried over from the roadmap:** pace is roughly evenings-and-weekends part-time, not full-time hours. If actual available time per week is meaningfully different, the task-to-week mapping should shift, but the dependency order (test suite → CI → AWS/Docker) shouldn't.

**How the hour estimates below work — read this before trusting the numbers.** These assume Claude does most of the actual typing (writing test code, YAML, Dockerfiles, deployment scripts) and explains it along the way, rather than Frank writing it solo — that's faster than learning from scratch out of a textbook. But it's not zero time: understanding well enough to survive an interview follow-up question — not just accepting what Claude outputs — is real time, especially for concepts that are entirely new (TypeScript, Docker, AWS networking/IAM). Estimates lean toward the higher end where the concept is brand new and toward the lower end where it's close to something already known (e.g., Snowflake, which is just SQL Frank already has from the Data Architect background). Treat every number here as a rough band, not a commitment — log the real time in Week-14's wrap-up so future estimates get more accurate.

**Priority if a week overruns and something has to slip:** (1) `bookshq` test suite/CI — protect first, it's the item actually closing the Stage 1 rubric gap. (2) AWS cert + deployment — protect second, it's clock-bound once the account's open. (3) Docker. (4) GitLab pass and Agile/Scrum course — these are the safe things to push into January; each is only a single confirmed-gap hit, not a recurring one.

**Heads up on load, before you start:** Weeks 8, 10, and 12 are estimated heavier than the rest (11–16 hrs, 9–16 hrs, and 9–14 hrs respectively) — auth/CORS hardening, the AWS deployment, and Docker are the three biggest single chunks of new-concept learning in the whole plan, and they land close together. If real available time is closer to 6–8 hrs/week, expect those three weeks specifically to run over into the Week 13 buffer — which is what that buffer is for, but it means there's realistically no slack left in December for anything else unexpected.

---

## Week 1 — Sun 9/27 – Sat 10/3 — *est. 7–10 hrs*

- [ ] Set up Vitest in `bookshq` and write the first batch of tests: the Google Books → Open Library cover-fetch fallback chain. *(~5–7 hrs — includes learning what Vitest is, what a test/assertion/mock actually is; the concept overhead is front-loaded here, later test-writing weeks should go faster.)*
- [ ] Filler: sign up for Snowflake free tier, run a few basic queries. *(~2–3 hrs — this is just SQL, which is already a strength, so it's genuinely cheap.)* *(Tier 1 #5)*

## Week 2 — Sun 10/4 – Sat 10/10 — *est. 7–10 hrs*

- [ ] Continue the Vitest suite: merge/dedup logic, gamification XP/leveling math. *(~4–6 hrs — should be faster than Week 1 now that the Vitest basics are down.)*
- [ ] Filler: Microsoft Fabric self-study via free trial. *(~3–4 hrs)* *(Tier 1 #4)*

## Week 3 — Sun 10/11 – Sat 10/17 — *est. 5–8 hrs*

- [ ] Finish the Vitest suite: CSV import parsers (Goodreads + Readwise). *(~2–3 hrs)*
- [ ] Start the GitHub Actions CI workflow. *(~3–5 hrs — new concept: YAML syntax, what a "workflow" and a "runner" are, why it needs to trigger on push/PR.)*

## Week 4 — Sun 10/18 – Sat 10/24 — *est. 5–7 hrs*

- [ ] Verify the CI workflow actually works end to end (a real PR that fails on a broken test, a real one that passes). *(~2–3 hrs)* **This closes Tier 1 #1**, the last Tier 1 item blocking Stage 1 rubric fit.
- [ ] Chip at CS50P. *(~3–4 hrs — ongoing every week from here, no fixed finish week; adjust this estimate once you tell me roughly how much is actually left.)* *(Tier 1 #6)*

## Week 5 — Sun 10/25 – Sat 10/31 — *est. 5–9 hrs*

- [ ] Buffer for any Week 1–4 spillover. *(~2–4 hrs if needed)*
- [ ] Checkpoint: confirm Tier 1 is fully closed before the AWS clock starts in November. *(~0.5–1 hr)*
- [ ] CS50P. *(~3–4 hrs)*

---

## Week 6 — Sun 11/1 – Sat 11/7 — *est. 7–9 hrs*

- [ ] Open the AWS account, set a Budget alert immediately, and start the AWS Cloud Practitioner course. *(~3.5–5 hrs — account/billing setup is quick; the course itself starts slow while cloud vocabulary is new.)*
- [ ] CS50P. *(~3–4 hrs)*

## Week 7 — Sun 11/8 – Sat 11/14 — *est. 7–10 hrs*

- [ ] Continue AWS Cloud Practitioner coursework. *(~4–5 hrs)*
- [ ] Filler: GitLab familiarity pass. *(~2–3 hrs)* *(Tier 2 #10)*
- [ ] Background, ~1–2 hrs this week: push `bookshq`'s TypeScript conversion past week 4 of the curriculum. *(Tier 2 #12 — repeats every week from here through December at roughly this pace, not re-estimated below. TypeScript is the one item on this whole list where "zero fluency" hits hardest — consider a short, dedicated 2–3 hr TypeScript-basics primer with Claude before diving back into the conversion, rather than trying to pick up types purely by osmosis while converting files.)*

## Week 8 — Sun 11/15 – Sat 11/21 — *est. 11–16 hrs (heaviest week in the plan)*

- [ ] Finish AWS Cloud Practitioner coursework; start Agile/Scrum fundamentals course. *(~4–5 hrs AWS + ~2–3 hrs Agile/Scrum)* *(Tier 2 #11)*
- [ ] Add basic auth to `bookshq` and lock down its CORS policy. *(~4–6 hrs — this is new-concept-heavy: what auth actually does, sessions vs. tokens, why CORS matters, all before the deployment can safely go public. Budget the higher end here rather than the lower.)*
- [ ] Background: TypeScript conversion. *(~1–2 hrs)*

## Week 9 — Sun 11/22 – Sat 11/28 — *est. 4–8 hrs — Thanksgiving week, deliberately light*

- [ ] Sit the AWS Cloud Practitioner exam if ready. *(~2–4 hrs including last review)* If Thanksgiving eats the week, this is the one place in the whole plan safe to push without cascading — move it to Week 10.
- [ ] Continue Agile/Scrum course. *(~2–3 hrs)*
- [ ] Background: TypeScript conversion. *(~0–1 hr — fine to skip entirely this week.)*

## Week 10 — Sun 11/29 – Sat 12/5 — *est. 9–16 hrs*

- [ ] AWS Cloud Practitioner exam, if not already done in Week 9. *(~2–4 hrs)*
- [ ] Begin the actual AWS deployment of `bookshq`'s backend + Postgres. *(~6–10 hrs — the single biggest unknown-unknown in the plan: first time standing up EC2/RDS, security groups, environment variables, DNS/networking. Claude can walk through each step, but expect real debugging time here, not just setup time.)*
- [ ] Background: TypeScript conversion. *(~1–2 hrs)*

---

## Week 11 — Sun 12/6 – Sat 12/12 — *est. 6–10 hrs*

- [ ] Continue/finish the AWS deployment: confirm it's reachable from outside, confirm the Budget alert threshold, confirm resources are tagged. *(~5–8 hrs)*
- [ ] Background: TypeScript conversion. *(~1–2 hrs)*

## Week 12 — Sun 12/13 – Sat 12/19 — *est. 9–14 hrs — last full working week before the holidays*

- [ ] Docker + docker-compose for `bookshq` (backend + Postgres). *(~8–12 hrs — a new concept end to end: images, containers, volumes, and the classic first-timer snag of getting the backend container to actually talk to the Postgres container. Realistically the second-biggest single item in the whole plan after the AWS deployment.)* *(Tier 2 #8)*
- [ ] Background: TypeScript conversion. *(~1–2 hrs)*

## Week 13 — Sun 12/20 – Sat 12/26 — *holiday week, buffer only*

- [ ] No new work scheduled. Use any spare time only to close out anything still open from Weeks 6–12 (most likely candidate: Docker, or the tail end of the AWS deployment). *(~0–3 hrs, spillover-dependent)*
- [ ] Do **not** let AWS Budget-alert monitoring lapse just because it's the holidays — a runaway EC2/RDS resource doesn't pause for Christmas.

## Week 14 — Sun 12/27 – Sat 1/2/27 — *New Year's week, buffer only*

- [ ] Final check: is Tier 2 actually done? (AWS cert ✓, AWS deployment ✓, Docker ✓, GitLab ✓, Agile/Scrum ✓, TypeScript conversion meaningfully further along ✓.) *(~1–2 hrs)*
- [ ] Whatever's still open carries into the roadmap's Q1 2027 plan — don't quietly drop it, log it.
- [ ] Update `Career_Pivot_Roadmap.md`'s Progress Tracking Log with the real outcome: what actually closed by 12/31, what slipped, why, and how the actual hours compared to these estimates — that comparison is what makes the *next* set of estimates better.

---

**Rough total across all 14 weeks: ~90–125 hours**, averaging roughly 6.5–9 hrs/week but unevenly distributed — October is the lightest stretch, Weeks 8/10/12 are the load-bearing crunch, and the holiday weeks are intentionally near-zero. If that total doesn't match the time actually available between now and 12/31, say so now rather than after Week 8 — the honest fallback is trimming GitLab and Agile/Scrum first (§3 of the roadmap already flags them as the lowest-cost items to lose).

*Newest status goes at the top of whichever week is current — check boxes off as items close, and add a one-line note if something slips or moves, so this stays an honest record of what happened rather than just what was planned.*
