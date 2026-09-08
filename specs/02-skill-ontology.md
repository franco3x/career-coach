# Spec 02 — Skill Ontology

**Status:** Active (schema + first re-encode applied 2026-09-08). Some cells need Frank's
confirmation — see §7.

## 1. Purpose

`Skill Ontology.csv` is Frank's **demand-matching skill inventory** — not a résumé, not a course
log. It is the source of truth (with the Confirmed Strengths section of
`Career_Pivot_Action_Tracker.md` and `LinkedIn_Profile_Update.md`) for:

- Spec 01 job assessments (classifying each required qualification Met / Partial / Absent).
- Résumé and LinkedIn tailoring (an evidence bank of provable claims).
- Seeing gaps, not just holdings.

## 2. File format

Single CSV, one row per **activity, credential, role, or distinct competency**. Edit in
Numbers/Excel; commit readable diffs. Columns in §3. Controlled vocabularies in §4. Do not add
columns without updating this spec.

## 3. Columns (11)

| # | Column | Notes |
|---|---|---|
| 1 | **Date** | `YYYY-MM-DD` (or `YYYY`, or `YYYY-MM`). When the skill/credential was earned or the activity started. For ongoing work use the start date. Several legacy rows still carry the 2026-03-10 bulk-log date — see §7. |
| 2 | **Activity / Credential** | The course, cert, project, role, task, or competency name. |
| 3 | **Skill Domain** | One or two values from the §4.1 list. Maps rows to JD requirement families. |
| 4 | **Tools / Tech** | Actual tools, platforms, languages, libraries only. `n/a` if none. |
| 5 | **Techniques / Concepts** | Granular competencies / keywords (the old Tier 3). |
| 6 | **Context Type** | One value from §4.2. |
| 7 | **Proficiency** | One value from §4.3. Honest self-rating of *current* ability. |
| 8 | **Last Used** | `Current`, or `YYYY` / `YYYY-MM` of last real use. Distinct from Date. |
| 9 | **Evidence** | The proof: repo path/URL, dashboard/report name, Credly/cert ID, quantified result, "course cert", assessment score. Keep short. Note caveats here ("AutoML-assisted", "training-only", "R = exposure"). |
| 10 | **Claim Strength** | One value from §4.4. Guards against overstatement. |
| 11 | **Track Relevance** | One value from §4.5. Lets a résumé pass filter by track. |

## 4. Controlled vocabularies

### 4.1 Skill Domain

`BI & Visualization` · `Data Modeling` · `ETL / Data Prep` · `SQL & Databases` · `Programming` ·
`SW Engineering Practices` · `Cloud & DevOps` · `Statistics & ML` · `Semantic / Ontology Modeling`
· `Web / Front-End` · `Low-Code / Automation` · `Process Improvement` · `Communication & Enablement`
· `Domain — Audit/GRC` · `Domain — Public Sector/Judicial` · `Domain — Program Finance/EVMS`

### 4.2 Context Type

`Production (Job)` · `Personal Project` · `Coursework` · `Certification` · `Academic Degree` ·
`Skill Assessment` · `Self-Study (in progress)`

### 4.3 Proficiency

| Value | Meaning |
|---|---|
| `1 Awareness` | Knows the concepts; little or no hands-on. |
| `2 Working` | Can do it with reference/help; limited reps. |
| `3 Proficient` | Independent, routine use on real work. |
| `4 Advanced` | Deep; handles edge cases; can guide others. |
| `5 Expert` | Authority; could set standards / teach it. |

### 4.4 Claim Strength

`Verified` (shareable artifact or credential exists) · `Asserted` (true, no shareable artifact) ·
`In Progress` · `Exposure Only` (touched it — don't lead with it on a résumé).

### 4.5 Track Relevance

`BI` · `SWE` · `Both` · `Foundational` (helps either track — Git, SQL, comms) · `Legacy-Domain`
(finance / audit / government — a differentiator, not a core pivot skill).

## 5. Update procedure

When Frank completes a course/cert/project, lands a new task, or a proficiency changes:

1. Add one row (or update the existing row if it's the same competency maturing — bump
   Proficiency / Last Used / Evidence rather than duplicating).
2. Fill all 11 columns. Use only §4 vocabulary for columns 3, 6, 7, 10, 11.
3. Keep grain consistent: a multi-module cert path may have child rows, but name them so they
   read as children (`Alteryx Core: Data Prep`), and keep one parent row for the credential.
4. If the row closes a gap in the `Recurring Gap Tracker`, note it in Evidence (`closes: CI/CD`).
5. Do **not** claim skills not yet real: CI/CD (GitHub Actions), an ADR/design doc, and macro
   logic refactoring are **not** done as of 2026-09-08 — do not add rows for them until they are.
6. Cross-check new Confirmed Strengths / gaps back into `Career_Pivot_Action_Tracker.md` if the
   change is material (full doc-sync is a later spec).

## 6. Accuracy fixes applied in the 2026-09-08 re-encode

**Overclaims dialed back:**

- *Computer Science 101 (Udemy)* — was "Software Engineering, Systems Architecture"; now
  `Programming`, `1 Awareness`, `Exposure Only`.
- *Alteryx ML Fundamentals* — was "Predictive Modeling, Data Science"; now `Statistics & ML`,
  `1 Awareness`, `Exposure Only`, Evidence notes "AutoML-assisted, not framework-level".
- *"Python, SQL, & Tableau Integration"* — was "Full-Stack Data Science, Pipeline Automation";
  now `Programming` / `2 Working`. Real course name still to confirm (§7).
- *1 Hour HTML* — was "Web Development, Front-End Markup"; now `Web / Front-End`, `1 Awareness`,
  `Exposure Only`, Depth "1 hr".
- *R* (in Google cert + MS Data Analytics rows) — kept, tagged "R = exposure only" in Evidence.
- *LSS Advanced Yellow Belt* — Evidence notes "entry tier; below Green/Black".

**Stale — GitHub macro project brought current:** added rows for Pydantic schema validation,
Python packaging (`pyproject.toml`, installable), and the partial Click CLI with safety-confirm
flow — all completed per `GitHub_Macro_Project_Tracker.md`. Test-count cell flags the 225-vs-295
discrepancy (§7). CI/CD deliberately **not** added.

**Missing high-value entries added:**

- Audit / Compliance / Governance — JAC (14+ yrs), `Domain — Audit/GRC` + `Domain — Public
  Sector/Judicial`, `4 Advanced`.
- Government / Judicial-System Domain — JAC, as a distinct row from the audit angle.
- Program Finance / Earned Value Management — L3Harris (Cobra, MPM, EVMS, BOE, ~$350M).
- Training & Mentoring / Analyst Enablement.
- Stakeholder & Executive Communication (promoted to a first-class row).
- AI-Assisted Development Practice (Claude as coding/testing partner).
- Data Architect role — L3Harris (Sept 2025–present) as a tenure anchor.
- CS50P (in progress); freeCodeCamp Python logged as superseded.

**Data hygiene:**

- All dates normalized to ISO.
- ~20 rows previously carried the `2026-03-10` bulk-log date. Where the true year was
  inferable I set a best-effort approximate acquisition year — **SAS suite → 2021** (MS Data
  Analytics era), **Google Data Analytics → 2023**, **Alteryx suite → 2024**, **LSS / CPM →
  2020** (JAC era). These are estimates flagged for Frank's correction (§7.1). Rows with no
  reasonable anchor (Computer Science 101, Tableau Consumer, the Python/SQL/Tableau course, SQL
  Bootcamp) kept `2026-03-10`.
- *Total Cost File Automation* and *Weekly Cost & Hours Reporting* re-dated from 2026-03-26 to
  `2021-2025` (Program Finance work; that role ended Sept 2025).
- "62% Time Savings" moved into the Evidence column; noted as formula-based, not VBA.
- Context Type values normalized to the §4.2 list ("Professional Strategy",
  "Professional Development (Palantir)" etc. removed).

## 7. Confirmation status (Frank, 2026-09-08)

Resolved:

1. **Acquisition dates** — the approximate estimates (SAS `2021`, Google `2023`, Alteryx `2024`,
   LSS + CPM `2020`; the rest left on `2026-03-10`) are **accepted as sufficient**.
2. **"Python, SQL, & Tableau Integration"** — that **is** the real Udemy course name. Row updated
   (`(Udemy)`, Evidence "Udemy course completion").
3. **pytest test count** — **295** is correct. Ontology row and the Confirmed Strengths line in
   `Career_Pivot_Action_Tracker.md` updated. Historical Job Assessment Log entries keep their
   point-in-time `~225` figure (a note on the Confirmed Strengths line says so); full reconciliation
   is left to the `doc-sync-source-of-truth` spec.
4. **Proficiency ratings** — first-pass values **accepted, no changes**.
6. **New domain rows** — wording **approved**.

Still to fill in (no blocker; do opportunistically):

5. **Evidence pointers** — in progress. Course-source URLs added for SQLBI DAX, Basic Git &
   GitHub, Power BI Desktop (Maven), Computer Science 101, Python+SQL+Tableau, The Complete SQL
   Bootcamp, 1 Hour HTML, and all 5 Palantir tracks (2026-09-08, via course-page verification —
   several row names, tool lists, and technique lists corrected in the process). Still missing:
   Credly links, the GitHub repo URL + visibility, SAS/Alteryx certificate numbers, specific
   dashboard/report names, and course links for the Alteryx suite, SAS suite, Google Data
   Analytics, LSS/CPM, Percipio, and the Udemy skill assessments.

---

*Written 2026-09-08. Schema chosen with Frank: structural fixes + Core columns, single CSV.*
