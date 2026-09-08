# Specs — claude-career-coach

## What this project is

A chat-driven career-coaching system. Its single objective is to **land Frank a role in his
career pivot**. The markdown/CSV files in this vault are scaffolding for that goal, not the goal.

Claude does the work each session by following the small, explicit specs in this folder, so that:

- every job posting is assessed the same way, with the same standing rules applied;
- every apply decision produces consistent tracker updates;
- the supporting documents (resume, LinkedIn, Skill Ontology, trackers) stay in sync.

Two parallel tracks are maintained — **BI** and **SWE** — each with its own fit rubric and its own
base resume. Every posting is routed to exactly one track at assessment time.

## Execution model

Claude, manually, per session. Specs are procedures/checklists Claude follows in a chat. No code,
no automation. A spec is "done" when a future session can execute it from the file alone.

## Conventions

- One spec per concern. Small and self-contained. Numbered by the order they were written.
- Each spec has: Purpose, Inputs, Procedure (numbered steps), Definitions/rubric, Out of scope.
- A spec change is a deliberate act — note the date and what changed at the bottom of the file.
- Source of truth for Frank's current skills is `Skill Ontology.csv` + the Confirmed Strengths
  section of `Career_Pivot_Action_Tracker.md` + `LinkedIn_Profile_Update.md`. The resume PDFs/docx
  are stale and are NOT authoritative until the resume-tailoring spec says otherwise.

## Specs

| # | File | Concern | Status |
|---|---|---|---|
| 01 | `01-job-assessment-procedure.md` | JD pasted → fit verdict → logged in `Career_Pivot_Action_Tracker.md` | **Active** (ratified 2026-09-08) |
| 02 | `02-skill-ontology.md` | Schema, vocabularies, and update rules for `Skill Ontology.csv` | **Active** (ratified 2026-09-08) |

## Backlog (not written yet)

- `resume-tailoring` — when to apply, which base resume per track, tailoring rules, file naming, save location.
- `tracker-updates` — exact rules for adding/updating rows in `Career_Activity_Log` and
  `Job_Applications_Tracker`, and keeping them consistent with the assessment log. Includes the
  `.xlsx` → CSV conversion (both trackers become canonical CSV; the Field Guide sheet becomes a
  markdown file).
- `doc-sync-source-of-truth` — canonical hierarchy across Skill Ontology, resume, LinkedIn,
  trackers; what a "sync pass" checks.
- `standing-rules-registry` — pull the scattered standing rules / notes into one referenced list.
- `session-start-checklist` — what Claude reads at the start of every session.
