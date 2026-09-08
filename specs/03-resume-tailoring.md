# Spec 03 — Resume Tailoring

**Status:** Active (ratified by Frank 2026-09-08). The Verification Layer (§7) is the part Frank
asked for by name — it is run in full every time.

## 1. Purpose

Turn a **logged Spec 01 assessment** into a decision to apply-or-not and, when the answer is apply,
a **tailored résumé draft** that is provably consistent with Frank's real evidence and aligned to
the specific posting — with a standing **Verification Layer** run before anything is handed back.

One assessed posting in → an apply / stretch / skip call out, and (if apply) one tailored résumé
draft plus its filled verification checklist and change table.

This spec **runs after Spec 01 and off its logged entry.** It never re-scores fit. It never touches
`Career_Activity_Log` or `Job_Applications_Tracker` (those update under Spec `tracker-updates`), and
it does not edit `Skill Ontology.csv`, the Master résumé, or LinkedIn.

## 2. Inputs (each time)

Required:

- **The logged Spec 01 Job Assessment entry** for this exact posting — its Track, Verdict, Flags,
  Matched Skills, and Key Gaps. If no entry exists, stop and run Spec 01 first. Résumé tailoring is
  never done from a raw JD.
- **The full JD text**, for exact keyword phrasing (the assessment entry paraphrases; tailoring
  needs the posting's own words).
- **Source-of-truth documents**, in this precedence order:
  1. `Skill Ontology.csv` (the evidence bank — every claim must trace here).
  2. Confirmed Strengths section of `Career_Pivot_Action_Tracker.md`.
  3. `LinkedIn_Profile_Update.md`.
  4. `Resumes/Frank_Coleman_Master_Resume.docx` (the bullet superset — wording source, not an
     authority on what is true; the résumé PDFs/docx are otherwise stale per `specs/README.md`).

Optional:

- Frank's instruction to apply as a stretch on a Weak-fit posting (see §4).
- Any framing he wants foregrounded (referral, a specific differentiator).

## 3. Résumé classes (definitions)

| Class | Files | Role |
|---|---|---|
| **Master** | `Resumes/Frank_Coleman_Master_Resume.docx` | Superset of every true bullet, in full wording. Never sent to an employer. Source for bullet text. |
| **Base (per track)** | BI: `Resumes/Frank_Coleman_Resume_Business_Intelligence.docx` · SWE: `Resumes/Frank_Coleman_Resume_Software_Engineering.docx` | The starting point for a tailored draft. One per track. Changed only by a deliberate decision, noted in §9. |
| **Tailored instance** | `Resumes/Tailored/…` (see §6) | One posting's résumé. Produced by this spec. The Disney / Zillow / KPMG files currently in `Resumes/` are legacy tailored instances from before this spec. |

## 4. Apply decision  *(NEEDS FRANK'S RATIFICATION)*

Read the Spec 01 entry's **Verdict** and **Flags**. Map:

| Spec 01 verdict | Flags | Call | Tailoring effort |
|---|---|---|---|
| **Strong fit** | no blocking stamp | **Apply** | Full tailored draft. |
| **Moderate fit** | no blocking stamp | **Apply** | Full tailored draft. |
| **Weak fit** | no blocking stamp | **Stretch — Frank's call** | No draft until Frank explicitly opts in. If he does, tailor and add one honest framing line for the core gap (per the Spec 01 "honest talking point" clause). |
| **Not competitive yet** | — | **Skip** | No draft. The Spec 01 Action Items already name the milestones that would change this. |
| any | **"Will not apply — out-of-state, non-remote"** | **Skip** | No draft, regardless of verdict. The stamp is decisive (Spec 01 §4.1). |
| any | **"Low Compensation"** only | as per verdict row above | The comp stamp does **not** block applying — surface it to Frank, proceed on his confirmation. |

Always state the call and the reason back to Frank and **get his go before spending tailoring
effort.** A Strong/Moderate "Apply" still waits for his confirmation — he may be deprioritizing that
employer or vertical for reasons outside the rubric.

## 5. Tailoring rules

### 5.1 What a tailored draft MAY change

- **Professional summary** — rewrite to the posting's track and title, using the JD's own framing
  words. Keep it truthful; it is a reframing of the Master summary, not a new claim.
- **Skills section** — reorder and regroup so the skills the JD names (and Frank actually has) are
  first. Drop groupings irrelevant to this posting. Add no skill absent from `Skill Ontology.csv`.
- **Bullet selection and emphasis** — choose which Master bullets appear, and tighten their wording
  toward the JD's vocabulary. Reframing real work in role-specific language is expected
  (`Career_Pivot_Action_Tracker.md` Cross-Cutting Action Plan item 23). Inventing scope is not.
- **Certifications / Relevant Technical Training** — order and select for pivot-relevance to this
  posting. Nothing invented; nothing true is deleted from the record (LinkedIn keeps the full list).
- **One framing line** for a Weak-fit stretch (see §4) — an honest talking point, not a claim of
  experience.

### 5.2 What a tailored draft MUST NOT change

- Employers, titles, employment dates, degrees, the contact block — byte-identical to Master.
- Quantified facts: **295** pytest tests, **$350M** program value, **80%** efficiency, **50+**
  agencies, **$40M** interim-lead program, **~3,000-page** LBR. Never inflate, never round up.
  (The 282 / ~225 test counts in legacy files are superseded — Spec 02 §7.3.)
- No project, tool, employer, or responsibility that is not in `Skill Ontology.csv` and the Master.

### 5.3 Claim-strength floor  *(NEEDS FRANK'S RATIFICATION)*

Cross-check every skill line and bullet keyword against the matching `Skill Ontology.csv` row's
**Claim Strength** (Spec 02 §4.4):

- `Verified` / `Asserted` — may appear anywhere, including the summary.
- `In Progress` — may appear only as "currently developing / in progress", never as a held skill.
- `Exposure Only` — must **not** be led with; may appear only in a low-emphasis list if the JD
  names it directly, and only with the ontology's caveat wording.
- **Never claim, per Spec 02 §5.5 (as of 2026-09-08):** CI/CD (GitHub Actions), an ADR / design
  doc, macro-logic refactoring. These are not done. Not on a résumé until the ontology says so.

### 5.4 Track → base

Route by the **Track already recorded in the Spec 01 entry** (do not re-decide it). BI → BI base.
SWE → SWE base. A posting Spec 01 assessed under one track but noted "with the other lens" still
uses the recorded track's base; the other-lens note can inform one summary sentence.

### 5.5 Length and format

- One page is the target. Two pages allowed only if the Spec 01 entry shows a genuinely deep match
  across two full roles' worth of relevant bullets.
- The draft deliverable is **markdown** (same as `LinkedIn_Profile_Update.md`). Formatting the
  final employer-ready `.docx` / `.pdf` is a manual step Frank does (or a later spec) — see §8.

## 6. File conventions  *(NEEDS FRANK'S RATIFICATION)*

- **Draft location:** `Resumes/Tailored/_drafts/{filename}.md`
- **Ratified location:** `Resumes/Tailored/{filename}.md` (moved here only after §7 passes and Frank
  signs off).
- **Filename:** `Frank_Coleman_Resume_{Company}_{RoleShort}.md` — `{Company}` and `{RoleShort}` in
  PascalCase, no spaces. Matches the legacy pattern
  (`Frank_Coleman_Resume_KPMG_Associate_SWE`, `…_Disney_Senior_BI_Analyst`,
  `…_Zillow_BI_Manager`). Add `_v2`, `_v3` for re-tailors of the same posting.
- The `Resumes/` base and Master files stay where they are. Only tailored instances move under
  `Resumes/Tailored/`.

## 7. Verification Layer  — run in full, every time

Frank asked for this explicitly: **a check that the output is what we want.** Claude runs all eight
gates against the drafted markdown, records the result table **inside the draft file**, and may not
describe the résumé as "ready" while any gate is `FAIL` or `UNRESOLVED`. A `FAIL` sends the draft
back to §5; it does not get shown to Frank as a candidate until it clears.

| Gate | Question | How to check | Pass condition | On fail |
|---|---|---|---|---|
| **G1 Truthfulness** | Is every bullet and skill line traceable to a real source? | For each line, name the `Skill Ontology.csv` row / Master bullet / Confirmed-Strengths line that licenses it. | Every line has a named source. Zero invented scope. | Cut or rewrite the line. |
| **G2 Claim-strength floor** | Any overclaim vs §5.3? | Match each skill keyword to its ontology Claim Strength. Scan for CI/CD, ADR/design-doc, refactor claims. | No `Exposure Only` led with; none of the three banned items present; `In Progress` phrased as in-progress. | Downgrade wording or remove. |
| **G3 JD coverage** | Is each **Matched Skill** from the Spec 01 entry actually present in the résumé? | Walk the Spec 01 entry's Matched Skills list against the draft. | Every Matched Skill appears somewhere, in wording close to the JD's. | Add it (it is already evidenced — G1 is safe). |
| **G4 Gap honesty** | Does the draft imply experience in a Spec 01 **Key Gap**? | Walk the Key Gaps list against the draft. | No wording claims a gap area as held experience. A stretch framing line (§4) is allowed and labelled. | Rewrite to the honest framing. |
| **G5 Consistency** | Do the fixed facts match Master exactly? | Diff contact block, employers, titles, dates, degrees, and every quantified figure against Master. Test count must read **295**. | Byte-identical fixed facts; no stale 282 / 225. | Correct to Master. |
| **G6 Track fit** | Right base, right framing? | Confirm base matches the Spec 01 Track; summary and skills order match that track. | Correct base; summary names the posting's track/title. | Rebase / rewrite summary. |
| **G7 Format** | One page? No leftovers? | Length estimate; search for another company's name, another role's summary, `TODO`, `{…}` placeholders. | ≤ 1 page (or §5.5 two-page exception justified); zero cross-contamination from a prior tailor. | Trim / clean. |
| **G8 Change log** | Can Frank see exactly what changed? | Produce the §7.1 change table. | Every delta from the base is one row with its licensing source. | Complete the table. |

### 7.1 Change table (G8 output)

```markdown
| # | Section | Base wording | Tailored wording | Licensed by |
|---|---|---|---|---|
| 1 | Summary | … | … | JD line "…"; Ontology row "…" |
| 2 | Skills → order | … | … | JD required list |
| … | | | | |
```

### 7.2 Verification result block (goes in the draft file)

```markdown
## Verification Layer — {YYYY-MM-DD}
Posting: JA #{N} — {title} — {company}   Track: {BI|SWE}   Base: {file}
G1 Truthfulness ...... PASS
G2 Claim strength .... PASS
G3 JD coverage ....... PASS   (n/n Matched Skills represented)
G4 Gap honesty ....... PASS
G5 Consistency ....... PASS
G6 Track fit ......... PASS
G7 Format ............ PASS
G8 Change log ........ PASS   (see change table above)
Residual Key Gaps Frank should be ready to speak to: …
Verifier note: {anything Frank should weigh}
```

## 8. Procedure

1. **Precondition.** Confirm a logged Spec 01 entry exists for this posting. If not → run Spec 01,
   stop here.
2. **Apply decision (§4).** State the call (apply / stretch / skip) and why. Get Frank's go. Skip →
   done; note the skip on the Spec 01 entry's Action Items.
3. **Select base (§5.4)** by the recorded Track.
4. **Draft** `Resumes/Tailored/_drafts/{filename}.md` from the base, applying only §5 changes,
   pulling bullet wording from Master, keywords from the JD, and checking every claim against
   `Skill Ontology.csv` + Confirmed Strengths as you go.
5. **Build the change table (§7.1).**
6. **Run the Verification Layer (§7).** Any `FAIL` → back to step 4. Write the §7.2 result block
   into the draft file.
7. **Hand back to Frank:** the draft, the change table, the verification block, and the residual
   Key Gaps from the Spec 01 entry he should be ready to discuss. Say plainly whether it passed
   clean or with a verifier note.
8. **On Frank's ratification:** move the file to `Resumes/Tailored/{filename}.md`. On the Spec 01
   Job Assessment entry, tick the "tailor résumé" Action Item and add a line
   `**Résumé:** Resumes/Tailored/{filename}.md (tailored {YYYY-MM-DD}, verification PASS)`.
   Add a row to §10. Formatting the `.docx`/`.pdf` is Frank's step.
9. **Do not** write to `Career_Activity_Log` or `Job_Applications_Tracker` — that is the
   `tracker-updates` spec.

## 9. Base-résumé change log

*(When a Base per-track résumé itself is changed — new confirmed strength, corrected figure — note
the date and what changed here. Tailored instances do not go here; they go in §10.)*

- *(none yet — bases as of 2026-09-08 are `Resumes/Frank_Coleman_Resume_Business_Intelligence.docx`
  and `Resumes/Frank_Coleman_Resume_Software_Engineering.docx`. Both already read the ratified
  **295** test count. The legacy tailored instances still in `Resumes/` are stale — Disney and
  Zillow show 282, KPMG shows ~225 — and are not bases; do not tailor from them.)*

## 10. Résumé Tailoring Log

| Date | JA # | Posting | Company | Track | Base | Output file | Verification | Ratified by Frank |
|---|---|---|---|---|---|---|---|---|
| — | — | — | — | — | — | — | — | — |

## 11. Out of scope (deferred to other specs)

- Writing rows to `Career_Activity_Log` or `Job_Applications_Tracker` (`tracker-updates`).
- Producing the final formatted `.docx` / `.pdf` from the markdown draft.
- The cover letter.
- Editing `Skill Ontology.csv`, the Master résumé, or `LinkedIn_Profile_Update.md`.
- Re-scoring fit or re-routing the track (that is fixed by the Spec 01 entry).
- Full document-sync across all source-of-truth files (`doc-sync-source-of-truth`).

## 12. Ratification status

Ratified by Frank 2026-09-08:

- §4 apply-decision mapping — **accepted as written.**
- §5.3 claim-strength floor — **accepted;** carries the Spec 02 §5.5 "never claim" list forward.
- §6 `Resumes/Tailored/` folder + `_drafts/` + filename pattern — **accepted.**
- §5.5 mechanism — **accepted:** markdown draft here, Frank formats the employer-ready file.

Spec 03 is **active.**

---

*Written 2026-09-08. Follows Spec 01 (assessment) and Spec 02 (skill ontology). The Verification
Layer (§7) was requested by Frank as a required, every-time check that the tailored output matches
his real evidence and the posting.*
