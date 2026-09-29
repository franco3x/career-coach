---
name: skill-ontology
description: Paste one or more course/credential URLs to correct their rows in Skill Ontology.csv against the real curriculum, following specs/02-skill-ontology.md.
---

# Skill Ontology — course link update

Invoked with one or more course/credential URLs, either passed as `args` or given in the user's
next message if `args` is empty (they may be comma- or newline-separated).

## What to do

1. **Read `specs/02-skill-ontology.md` in full first.** It is the single source of truth for the
   CSV schema (§3), controlled vocabularies (§4), and the update procedure (§5) — including the
   Proficiency-verification step (§5 step 3) and the amendment log (§7a). Follow that procedure
   exactly; do not improvise a different one or restate its rules here.
2. For each URL:
   - Fetch the course/curriculum or "what you'll learn" page. If it's login-gated or blocks direct
     fetching, say so, then search for the course by name and reconstruct the real curriculum from
     search results or a syllabus aggregator — never from marketing copy alone.
   - Match it to the right existing row in `Skill Ontology.csv` by name. If no row plausibly
     matches, ask before adding a new one — don't guess a rename is a new row, or vice versa.
   - Correct `Skill Domain`, `Tools / Tech`, and `Techniques / Concepts` against what the course
     *actually* teaches (its real module/lecture list).
   - If `Proficiency` is being set or bumped upward on that row, run the §5 step-3 verification
     (one concrete probe question tied to the target level's own §4.3 definition, plus an Evidence
     cross-check) before recording it.
3. Show a before/after per row you touch — not just "updated" — so the change is checkable.
4. Do not commit or push anything without Frank's explicit go-ahead (standing instruction).
