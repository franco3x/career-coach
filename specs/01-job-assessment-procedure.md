# Spec 01 — Job Assessment Procedure

**Status:** Draft. The Fit Rubric (§5) is derived from the 28 assessments already logged and
needs Frank's explicit ratification before this spec is "active."

## 1. Purpose

Turn a pasted job description into a consistent, logged fit assessment inside
`Career_Pivot_Action_Tracker.md`. One posting in → one numbered Job Assessment entry out, plus the
tracker's rollup sections updated.

This spec **stops at the Action Tracker.** It never touches `Career_Activity_Log` or
`Job_Applications_Tracker` — those update only on an apply decision, under a later spec.

## 2. Inputs (from Frank, each time)

Required:

- **Full JD text**, pasted. Must include the "About the job" / full body, not just the summary —
  the relocation check (§4) depends on text that the location field alone doesn't show.
- **Posting URL** (for the link fields). If genuinely unavailable, log "Not provided".

Optional:

- Frank's own track call (BI or SWE), if he wants to override the routing in §3.
- Any context he wants weighed (e.g. "this came through a referral").

If the JD text is missing the "About the job" section, ask for it before assessing.

## 3. Track routing (do this first)

Every posting is assessed under exactly one track. Decide by job title against the lists below;
if the title isn't listed, decide by JD content.

### BI track — route here if the title is (or closely matches) one of:

Business Intelligence Analyst / Sr BI Analyst / BI Analyst II · Business Intelligence Developer ·
Business Intelligence Architect · Business Intelligence Engineer · Business Intelligence Manager /
Lead · Business Analyst / Sr Business Analyst · Business Analysis Manager · Business Analytics
Specialist / Sr Business Analytics Specialist · Data Analyst / Sr Data Analyst / Data Analyst Sr ·
Reporting Analyst / Reporting Developer · Analytics Consultant / BI Consultant · Power BI Developer
· Tableau Developer · Product Analyst / Product Analytics Analyst

### SWE track — route here if the title is (or closely matches) one of:

Software Engineer (I / II / III / Senior / Staff / Principal) · Software Developer / Sr Software
Developer · Associate Software Engineer · Full Stack Engineer / Developer · Backend Engineer /
Developer · Frontend Engineer / Developer · Application Developer · Platform Engineer · DevOps
Engineer · Site Reliability Engineer · Python Developer / Java Developer · Game Engineer / Graphics
Engineer

### Ambiguous titles — decide by JD content:

Data Engineer / Sr Data Engineer / Data Operations Engineer · Data Scientist / Sr Data Scientist ·
Machine Learning Engineer · AI Developer / AI Engineer · Analytics Engineer · Solutions Architect /
Solutions Engineer

Content-clue rule for the ambiguous set:

- Route to **BI** if the JD centers on dashboards/reports, semantic models, DAX / Power BI /
  Tableau, self-service enablement, metric definitions, data storytelling, stakeholder liaison.
- Route to **SWE** if the JD centers on production services/APIs, OOP depth / design patterns,
  CI/CD pipelines, containerization / IaC, distributed systems, cloud-native architecture,
  software on-call.
- If genuinely split, assess under the track whose **required** (not preferred) qualifications
  Frank is closer to, and add one sentence in the Verdict rationale noting the other lens.

Record the chosen track in the entry and in the snapshot table. (This is separate from the
existing descriptive "Role Category" column — keep both.)

## 4. Pre-filter checks & stamps (run before scoring)

These are checked first. **None of them change the Strong/Moderate/Weak/Not-competitive score** —
the verdict is always pure skills fit. They add a **stamp** to the entry and can stop the apply
path. Stamps in use: `Will not apply — out-of-state, non-remote` and `Low Compensation`.

### 4.1 Relocation outside Florida

- Read the full JD body for any requirement to be in, or relocate to, a specific non-FL location.
  A posting can display one city while the body requires another.
- If the role requires a non-FL location **and is not remote**: **pause and surface it to Frank**
  before finishing the assessment.
- If Frank confirms it is genuinely out-of-state and not remote: finish the full assessment anyway
  (it still has calibration value), but stamp the entry **"Will not apply — out-of-state,
  non-remote"** and do not generate apply-oriented action items. This holds even if the skills
  verdict is Strong.
- Fully-remote roles (any US state) sidestep this entirely — note "Remote — relocation constraint
  does not apply."

### 4.2 Security clearance

- Per standing rule (2026-08-14): a stated clearance requirement is **noted as a real
  qualification item** but is **never** a disqualifier and never an "unresolved blocker."
- Assume Frank is eligible to obtain a clearance and that the employer will sponsor/support it,
  **unless** the posting explicitly says otherwise (e.g. "must currently hold active TS/SCI, no
  sponsorship available"). If it does say otherwise, note that plainly and factor it into the
  verdict discussion only when paired with other hard gates.

### 4.3 Citizenship / work authorization

- Note if present. Not a blocker for Frank. Only call it out if the wording is unusual.

### 4.4 Compensation (Florida)

- **Floor: $120,000 base (FL).**
- Find the FL-applicable base range:
  - Explicit FL / Orlando / "Florida" range given → compare to floor.
  - Single national range with no location breakout → **neutral**, no stamp. Record the range.
  - Location-tiered ranges where FL is not named → **neutral**, no stamp. Record "not specified
    for FL".
- If an explicit FL range is **entirely below $120k**, stamp the entry **"Low Compensation"** and
  add the `**Comp flag:**` line (§7). This does **not** move the verdict — a role can be
  "Strong fit · Low Compensation."

## 5. Fit rubric  *(NEEDS FRANK'S RATIFICATION)*

Two scored dimensions, plus the §4 checks as context. The verdict is a **skills-fit verdict** on
a four-point scale: **Strong fit / Moderate fit / Weak fit / Not competitive yet.** Compensation
and relocation are stamps (§4), never inputs to the score.

### 5.1 Dimension A — Required-skills match

Score the JD's **Required / Basic / "must have"** qualifications only (not the "preferred"
section) against Frank's current evidence (`Skill Ontology.csv` + Confirmed Strengths +
`LinkedIn_Profile_Update.md`). For each required item classify:

- **Met** — real, demonstrable evidence (a project, a cert, sustained job experience).
- **Partial** — adjacent evidence, coursework-level, or an "or similar" clause Frank clears via a
  neighbouring skill (e.g. Python satisfying "Python or C#").
- **Absent** — no transferable evidence; blank slate.

Then judge the *shape*: are the Absent items the **core** of the role, or peripheral tools?

### 5.2 Dimension B — Degree-field risk

None of Frank's degrees (BS Business Admin, MBA, MS Data Analytics) are in an engineering
discipline. Grade the posting's degree wording:

| Grade | Wording pattern | Examples seen |
|---|---|---|
| **None** | No field restriction, or names Analytics/Data Science/Business directly | Lockheed Data Analyst Sr #19; Disney BI Analyst #13; Schneider #25; Microsoft #28 |
| **Low** | "or equivalent practical experience" / "or related field" catch-all | Deloitte Cyber #10; Disney SDE #11 |
| **Moderate** | "or equivalent field" (MS Data Analytics arguable, BBA alone not) | KPMG #9; Disney SWE II #12 |
| **High** | Strict "engineering / technical discipline", required not preferred | Lockheed SWE #8, #16, #17, #20 |

### 5.3 Verdict definitions

The two tracks share the scale but calibrate differently, because Frank's baseline differs.

**BI track**

| Verdict | Condition |
|---|---|
| **Strong fit** | All / nearly all Required quals **Met**; Absent items only in "preferred" or narrow tools (Snowflake, Fabric, Databricks, GitLab); degree risk None or Low. Bonus: a named differentiator present (mentoring, audit/GRC, judicial domain, Lean Six Sigma). |
| **Moderate fit** | Required quals mostly Met, but one **distinctive required** ask is a genuine domain or tenure gap (e.g. product-analytics domain, deep-learning frameworks); **or** degree risk Moderate. |
| **Weak fit** | Multiple Required quals Absent, **or** a core tool/skill of the role is a blank slate, **or** degree risk High. |
| **Not competitive yet** | Core BI bar itself not credibly Met **and** stacked multi-year tenure walls or a structural gate self-study can't touch **and** no differentiator that clears a screen. Applying is noise. |

**SWE track** (expect few or no Strong; the real output is apply-as-stretch vs skip)

| Verdict | Condition |
|---|---|
| **Strong fit** | Rare. Required language + testing + version control + CI/CD all Met/Partial, experience bar ≤ 2 yrs, degree risk not High. |
| **Moderate fit** | Language bar Met (incl. via "or similar"); testing is a **matched strength** (the macro project); remaining gaps are already on the Cross-Cutting Action Plan (CI/CD, Docker, cloud) rather than new specialized domains; experience bar low (≤ 1–2 yrs); degree risk ≤ Moderate. *(= KPMG #9.)* |
| **Weak fit** | The role's core stack is a blank slate (Java/JS/C++/React/Unreal/Angular required outright), **or** degree risk High, **or** stacked 5-yr tenure walls — but an honest talking point exists (SDLC discipline via the macro project, AI-assisted development, testing rigor). |
| **Not competitive yet** | Blank slate on the core stack **and** a structural/tenure wall **and** no transferable talking point. Applying is pure noise; revisit only after named milestones. |

**Weak vs Not competitive yet** — the line: *Weak* keeps at least one of (a) partial credit on the
role's core, (b) gaps already on the action plan, (c) an arguable degree/tenure position — so
applying is a defensible stretch or a calibration probe. *Not competitive yet* has none of those.

## 6. Procedure

1. **Route** the posting to BI or SWE (§3). Note the track.
2. **Run the pre-filter checks** (§4). If relocation trips 4.1, pause and ask Frank before
   continuing. Determine the relocation and comp stamps.
3. **Assess** against the rubric (§5): classify each Required qual (Dimension A), grade degree
   risk (Dimension B). Land a verdict on the four-point scale using the track's definitions.
4. **Write the Job Assessment entry** — append to the `## Job Assessment Log` section of
   `Career_Pivot_Action_Tracker.md`, using the template in §7. Use the next Log # (current max + 1).
5. **Update the snapshot table** (`## Job Assessment Snapshot`): add a row with Log #, Job Title,
   Company, Role Category, **Track**, Fit, Salary (FL or as listed), Posting Link, Log Link.
   *(The "Track" column was added and all rows backfilled on 2026-09-08 — see §10.)*
6. **Update the verdict-count table** and the "Total job assessments logged" number.
7. **Update the Recurring Gap Tracker**: for each Key Gap in the new entry, either increment the
   matching row's JD count and append this posting to its Notes, or add a new row.
8. **Update Confirmed Strengths** only if the assessment surfaced a strength worth leading with
   that isn't already captured.
9. **Update Structural (non-skill) eligibility gates** only if a genuinely new gate type appeared.
10. **Cross-Cutting Action Plan** — do not rewrite it every time. Only add/re-order items if this
    posting actually shifts priorities; otherwise leave it and note the date it was last synthesized.
11. **Report back to Frank** in the chat: track, hard-gate result, verdict, top 3 gaps, and a
    one-line "worth applying / stretch / skip" call. If it's an apply candidate, say so — the
    apply steps themselves are a separate spec.

## 7. Entry template

```markdown
<a id="ja-N"></a>
### N. {Job Title} — {Company} ({Location / Org})
**Date assessed:** {YYYY-MM-DD}
**Track:** {BI | SWE}
**Posting link:** {URL | Not provided}
**Salary:** {range as listed, with FL note | Not listed in posting}
**Flags:** {Relocation: none / remote / "Will not apply — out-of-state, non-remote"} ·
{Comp: none / "Low Compensation"} · {Clearance: none / noted, not scored per standing rule} ·
{Citizenship: n/a unless unusual}
**Verdict:** {Strong fit | Moderate fit | Weak fit | Not competitive yet} — {one- to two-sentence rationale}

**Matched Skills:**
- ...

**Key Gaps:**
- ...

**Action Items Generated:**
- [ ] ...
```

Notes:

- If comp is confirmed sub-floor (explicit FL range entirely below $120k), add
  `**Comp flag:** FL range ${x}–${y}, below the $120k target.` right under **Salary**, and set the
  "Low Compensation" stamp on the **Flags** line. This does not change the verdict.
- Keep the existing prose style of the log: gaps and matches are full sentences with specific
  evidence named, not bare keywords.
- If the verdict is "Not competitive yet", the Action Items should name the concrete milestones
  that would change it, not generic study suggestions.

## 8. Out of scope (deferred to other specs)

- Writing rows to `Career_Activity_Log` or `Job_Applications_Tracker`.
- The apply / don't-apply decision workflow and JD-specific resume creation.
- Converting the `.xlsx` trackers to CSV.
- Editing `Skill Ontology.csv`, the resume, or LinkedIn.
- Re-synthesizing the whole Cross-Cutting Action Plan.

## 9. Ratification status

Ratified by Frank 2026-09-08:

- §5 rubric and per-track verdict definitions — **accepted.**
- §3 track routing title lists — **accepted as written.**
- Compensation — **not a verdict input.** Sub-floor FL comp adds a "Low Compensation" stamp only,
  parallel to the out-of-state stamp. A role can be "Strong fit · Low Compensation."
- Snapshot "Track" column — **added and all 28 existing rows backfilled** (§10).

Spec 01 is **active.**

## 10. Backfill log

- **2026-09-08** — Added a "Track" column to the `## Job Assessment Snapshot` table in
  `Career_Pivot_Action_Tracker.md` and classified all 28 existing assessments:
  - **BI (15):** #1, #3, #5, #6, #13, #14, #18, #19, #22, #23, #24, #25, #26, #27, #28
  - **SWE (13):** #2, #4, #7, #8, #9, #10, #11, #12, #15, #16, #17, #20, #21
  - Judgment calls: Data Scientist / Data Analyst / analytics-flavoured roles (#1, #18) → BI;
    "true production data engineering" roles (#2, #4, #10, #11) and production AI/ML engineering
    (#21) → SWE; BI-adjacent data engineering (#6 DFS) → BI.
  - The individual Job Assessment Log entries (#1–#28) were **not** retrofitted with the new
    `**Track:**` / `**Flags:**` fields — those apply from assessment #29 onward.

---

*Written 2026-09-08 from an interview + a read of all 28 logged assessments. No prior spec.
Ratified and activated same day.*
