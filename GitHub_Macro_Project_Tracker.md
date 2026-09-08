# GitHub Macro Migration Project — Action Tracker
**Owner:** Frank Coleman III
**Purpose:** Track upgrades to the Excel/MS Project macro version-control project, since it's the primary current vehicle for building real software engineering signal. Cross-referenced in the main Career Pivot Action Tracker — this file is the detailed working log for this one project specifically.

---

## Project Snapshot (as of 2026-07-05)
- Migrated Excel and MS Project macros into a version-controlled GitHub repo
- Built a Python script that tracks/inventories the macros
- Built a second Python script that auto-generates README files from a metadata.yml file per macro
- Not yet doing: refactoring macro logic itself (still version-control stage, not modernization stage)

---

## Why This Project Matters
This is your single best current source of real, referenceable software engineering evidence — it shows you building tools, not just applying them. Testing and CI/CD have already been flagged twice across job postings (Orlando Magic Data Operations Engineer, plus the original project-scoping discussion) as a recurring, real gap. Leveling this project up directly closes that gap with something you already own, rather than requiring a brand-new project.

---

## Action Items (ordered by impact)

- [x] **1. Add tests (pytest)** — Write unit tests for both scripts (the tracker and the README generator). Cover basics: correct parsing of metadata.yml, handling of malformed/missing fields. This is the single biggest jump from "scripts" to "engineered software." *(Completed 2026-07-28 — see Progress Log for full detail.)*
- [ ] **2. Add CI (GitHub Actions)** — Set up a workflow that automatically runs the pytest suite on every push. Gives real, current, hands-on CI/CD experience — not just the definition.
- [x] **3. Schema validation for metadata.yml** — Use `pydantic` or `jsonschema` so the script rejects malformed metadata instead of silently failing. Real data engineering / software engineering skill; adjacent to schema enforcement work already in the Skill Ontology (Alteryx Data Prep). *(Completed — see Progress Log for full detail.)*
- [x] **4. Package it properly** — Structure both scripts as an installable Python package (proper folder layout, `pyproject.toml` or `setup.py`, `requirements.txt` or `poetry`). Small effort, disproportionate resume value. *(Completed — see Progress Log for full detail.)*
- [x] **5. Add a CLI interface** — Use `argparse` or `click` so scripts run as proper command-line tools (e.g., `macro-doc generate --file metadata.yml`) instead of being run by editing/calling directly. *(Completed 2026-08-05 — see Progress Log for full detail.)*
- [ ] **6. Write an architecture decision record (ADR) / design doc** — Explain why GitHub over alternatives, how the metadata schema is structured, tradeoffs made. Demonstrates architectural thinking, not just execution.
- [ ] **7. (Stretch, later) Refactor one macro end-to-end** — Pick one low-risk Excel macro and port its logic into Python, with tests. This is the piece that lets you legitimately claim "legacy modernization" experience — don't start here; get the tooling around it solid first.
- [ ] **8. End-user README visibility on SharePoint** — End users only ever access macros via SharePoint; they have no GitHub access. So "let end users view READMEs, read-only" is NOT a standalone small feature — it requires publishing/syncing the generated README content from GitHub to SharePoint (there is no version of this that stays inside GitHub). Scope depends on a sync mechanism, SharePoint's API/permissions, and likely auth handling. Not yet sized — revisit once items 1–3 (tests/CI/schema) are done and the README generator's output is reliable, since publishing unreliable docs is worse than not publishing at all. (Corrected 2026-07-08 — originally logged as a small read-only-viewer item, but that assumed end users had some GitHub access, which they don't.)

---

## Progress Log
*(Update as items are completed — include date and a one-line note on what changed)*

- 2026-07-05: Tracker created. No items started yet.
- 2026-07-08: Completed a full line-by-line understanding pass on
  `query_macros.py` (all 25 queries + helpers), followed by a full
  strengthen/fix pass: added 4 shared helper functions (`classify_application`,
  `make_relative_link`, `parse_version`, `criticality_rank`), fixed several
  real bugs (a missing print block, a missing `.get()` default causing a
  crash risk, and 6 menu options that silently did nothing due to missing
  parentheses), and redesigned 8 queries to support both filtering and
  grouped-overview modes. Verified changes directly against the real
  uploaded file (not just conversational confirmation) — caught and
  corrected several additional gaps in that verification pass, including
  one finding (a suspected `export_to_csv` key-name bug) that was later
  confirmed 2026-07-09 to be a false positive, not a real issue. Not itself
  one of the 7 numbered action items, but sets up item #1 (tests) well: the
  code being tested is now understood in depth and meaningfully more
  correct, so upcoming tests will validate real, intentional behavior
  rather than encode existing bugs as "expected" results. Also added item
  #8 (README visibility on SharePoint) to the action items list, corrected
  mid-discussion once it became clear end users have no GitHub access at
  all. Full detail in `changes_log.md`, `deferred_notes.md`, and
  `concepts_glossary.md` (all in the same project folder).
- 2026-07-09: **Action item #1 (tests) started.** Wrote and successfully ran
  the first 4 real pytest tests, covering `load_all_metadata()` in
  `query_macros.py` — valid-file loading, correct bookkeeping fields
  (`_folder`, `_file_path`), graceful handling of malformed YAML (one bad
  file doesn't take down the whole load), and empty-folder edge case. Set
  up as `scripts/tests/test_query_macros.py`, run via
  `python -m pytest tests/test_query_macros.py -v` from inside `scripts/`.
  Debugged and fixed real setup issues along the way (a missing colon, an
  import-path/working-directory mismatch, and a test assertion that didn't
  match the real code's actual field names and Windows path separators) —
  all 4 tests passing now. Remaining scope of item #1: extend the same
  process to the other 24 query functions and to
  `generate_readme_from_metadata.py` (not yet started).
- 2026-07-09 (cont'd): Wrote and passed 11 more tests, covering the 4 shared
  helper functions (`classify_application`, `parse_version`,
  `criticality_rank`, `make_relative_link`) added during the earlier
  strengthen pass. Caught two real setup issues along the way: the helper
  function definitions themselves had never actually been copied into the
  real `query_macros.py` (only the query functions calling them had been
  updated), and a test docstring/assertion mismatch (`'1.0'` vs. intended
  `'1.10'`) — both found and fixed correctly without direct hand-holding.
  15 tests passing total across `test_query_macros.py` and
  `test_helpers.py`. Remaining scope of item #1 unchanged: 24 query
  functions + `generate_readme_from_metadata.py` still to go.
- 2026-07-22: Wrote and passed 4 tests for `find_by_status()` (filter
  branch, group-all branch, no-match message, case-insensitivity) —
  19 tests passing total now. This session focused on debugging practice:
  worked through 4 real failures largely independently, reading pytest's
  traceback output rather than being handed fixes directly. Root causes
  included: the redesigned `find_by_status` (from the earlier strengthen
  pass) had never actually been copied into the real file, an incorrect
  `if`/`else` indentation causing an `UnboundLocalError`, incomplete fake
  test YAML missing an `ownership` field two tests depended on, and a
  simple string mismatch (`'archive'` vs `'archived'`) between a test's
  function call and its assertion. Good demonstrated progress reading and
  interpreting pytest failure output unassisted. Remaining scope of item #1
  unchanged: ~23 query functions + `generate_readme_from_metadata.py`
  still to go.
- 2026-07-22 (cont'd): Wrote and passed 5 tests for `find_by_criticality()`
  (filter branch, group-all branch with a dedicated regression test for
  High→Medium→Low ordering via `criticality_rank()`, no-match message,
  case-insensitivity, criticality_notes display), then uploaded the full
  real `query_macros.py` file for the first time to validate tests against
  actual current code rather than reconstructed assumptions. Used that to
  write 5 tests for `find_by_owner()`, catching two real, non-obvious
  behaviors directly from the real source: it uses a SUBSTRING match for
  owner names (not exact match) and neither of its branches sorts results
  (unlike `find_by_status`/`find_by_criticality`, which both do) — both
  correctly reflected in the tests rather than assumed. One test-copying
  slip (an extraneous "not" in an assertion) found and fixed independently.
  29 tests passing total now. Remaining scope of item #1 unchanged: ~22
  query functions + `generate_readme_from_metadata.py` still to go.
- 2026-07-22 through 2026-07-24: Wrote and passed tests for 5 more query
  functions: `find_by_usage_frequency()` (6 tests, including a dedicated
  regression test confirming the real missing-`.get()`-default crash bug
  found earlier can't recur), `find_by_tag()` (5 tests, including a test
  specifically confirming a macro with multiple tags appears under EVERY
  matching tag group since tags are list-valued, unlike status/criticality),
  `find_by_category()` (6 tests, covering all three OR'd match fields —
  primary/secondary/workflow_category — plus confirming group mode
  intentionally only groups by primary), `find_by_skill_level()` (5 tests,
  simplest of the batch), and `find_by_application()` (5 tests). **Found and
  fixed a real, previously-undiscovered production bug** while testing
  `find_by_application()`: its group-mode `return` statement was incorrectly
  indented inside the grouping `for` loop, causing "group all by
  application" to silently show ONLY Excel macros every time — MS Project
  and any other macros were completely missing from that view with no error.
  This is the first bug in the whole project caught purely by running a
  test, not by manual code review. Logged in `changes_log.md`. Also wrote
  6 tests for `find_macros_with_external_systems()`.
  56 tests passing total across `query_macros.py` now — 9 of 25 numbered
  queries covered, plus `load_all_metadata` and the 4 shared helpers.
- 2026-07-26 through 2026-07-27: Continued testing in query order.
  `find_macros_with_dependencies()` (6 tests, including a regression test
  for the `network_resources` print-block fix from the original strengthen
  pass) — caught one test-writing mistake of my own (used a wrong field
  name, `system_name` instead of the real `system` key, confirmed against
  actual source before fixing). `find_by_version_requirement()` (6 tests,
  with a dedicated regression test using '9' vs '10' to confirm numeric,
  not alphabetical, version comparison). `generate_summary_report()`
  (9 tests covering all 6 mini-reports, with regressions for criticality
  ordering, numeric version min/max, and the invalid-date/never-tested
  distinction) — discovered the real function's exact wording (capitalization,
  emoji icons, section headers) had drifted from what was read earlier in
  the project, resolved by Frank editing the real file to match rather than
  vice versa. `list_all_macros()` (3 tests, straightforward, no bugs).
  **Found and fixed a second real, previously-undiscovered bug** in
  `find_untested_macros()`: sorting was done on the display STRING
  (e.g. "120 days ago"), which alphabetically misorders anything over 99
  days (a bug flagged all the way back in the original walkthrough but
  never actually fixed until now). Fixed by adding a real numeric
  days-overdue sort key, with "Never tested"/"Invalid date" macros treated
  as maximally overdue. 6 regression-focused tests written against the
  corrected version. Logged in `changes_log.md`.
  80 tests passing total across `query_macros.py` now — 13 of 25 numbered
  queries covered (1, 2, 3, 4, 5, 6, 7, 8, 12, 13, 15, 17, 19, 21), plus
  `load_all_metadata` and the 4 shared helpers. Remaining: queries 9, 10,
  11, 14, 16, 18, 20, 22, 23, 24, 25, then `generate_readme_from_metadata.py`
  in full.
- 2026-07-28: **Finished testing every remaining query in `query_macros.py`
  — all 25 numbered queries now have real, verified test coverage,** plus
  `load_all_metadata` and the 4 shared helpers. Covered in this final push:
  `find_macros_with_issues()` (6, including the `[:3]` limitations-slice
  vs. full-count distinction), `find_deprecated_macros()` (7, relative-date
  math for future/past/malformed end-of-life dates), `export_to_csv()`
  (5 — first tests to check a REAL exported file's contents via the `csv`
  module rather than just captured print output),
  `find_macros_needing_review()` (6, confirmed already-correct numeric
  sort), `check_version_consistency()` (5 — first tests reading BOTH
  metadata.yml and a fake README.md from the same folder),
  `generate_markdown_catalog()` (7 — real file+folder creation, caught a
  filename mismatch: real default is `docs/macro-catalog.md`, hyphenated,
  not the underscored version assumed from memory), `find_large_macros()`
  (8 — first tests writing real dummy `.xlsm`/`.mpp` files with controlled
  byte sizes to exercise the disk-fallback path),
  `show_application_distribution()` (3, already correct),
  `find_excel_with_power_query()` (6, already correct),
  `find_macros_with_com_references()` (5, already correct), and
  `check_metadata_completeness()` (7 — the most sophisticated function in
  the file, with a dedicated test for the subtle "missing required field →
  Missing bucket, but missing OPTIONAL field → Unknown/TBD bucket, never
  Missing" design distinction). Total across `query_macros.py`: roughly
  150+ tests across 20 test files. Every test validated against the real
  function logic (via a local copy) before being handed over, and every
  fake YAML block checked with a real YAML parser, before Frank ever typed
  a single one in — a discipline that held up well: nearly every real
  failure along the way traced back to either a genuine hand-retyping slip
  (confirmed against the real source before "fixing" anything) or, twice,
  the real file having drifted from what was read earlier in the project.
  **`query_macros.py`'s portion of action item #1 is now fully complete.**
  Item #1's checkbox stays unchecked, since the item covers BOTH scripts,
  and `generate_readme_from_metadata.py` hasn't been read or tested at all
  yet — that's the entire remaining scope of item #1 now.
- 2026-07-28 (cont'd): **A real crash surfaced from actually running the
  tool**, right after declaring test coverage complete — a good, honest
  reminder that full test coverage reduces risk but doesn't guarantee zero
  bugs, especially for edge cases no one thought to write a test for yet.
  Two issues found: (1) ~6 menu entries in `main()` had lost their `lambda:`
  wrapper entirely, causing those query functions to execute immediately on
  script startup instead of waiting for menu selection — found and fixed by
  Frank independently. (2) A real crash in `generate_summary_report()`:
  `AttributeError: 'NoneType' object has no attribute 'capitalize'`, caused
  by a YAML field being present but explicitly null (e.g. `status:` with
  nothing after the colon) rather than missing entirely — a subtly
  different failure mode than the bracket-access risk deferred back at
  query 1, since `.get(field, 'unknown')`'s default only applies when the
  key is absent, not when it exists with a null value. Fixed the 2 specific
  spots causing the live crash (`status` and `business_criticality`) using
  `.get(field) or 'unknown'` instead of `.get(field, 'unknown')`. **Decision
  made**: the same "present but null" risk likely exists in several other
  functions, but rather than patch it everywhere now, it's being deferred to
  action item #3 (schema validation) — consistent with the original
  bracket-access deferral decision from query 1's walkthrough. Logged in
  `changes_log.md`. Regression tests for this specific fix were considered
  but deliberately skipped for now.
- 2026-07-24: **Important workflow constraint surfaced and addressed.**
  Confirmed Frank has no way to transfer files between the two computers
  used for this project (one running the Claude chat, one running
  VS Code/the real repo) other than hand-retyping code across screens —
  no shared drive, USB, or email transfer available. This explains most of
  the transcription-error debugging sessions throughout this project
  (dropped characters, mismatched whitespace, typos). Decision made:
  going forward, any NEW test involving multi-line YAML will use
  triple-quoted strings with real line breaks (matches how an actual
  `metadata.yml` file looks) instead of single-line `\n`-escaped strings,
  since real line breaks are much easier to hand-retype correctly than
  invisible escape sequences. The 40+ existing tests are NOT being
  retroactively rewritten — this applies only to new tests from this point
  forward. Worth remembering this constraint for any future file-based work
  on this project.
- 2026-07-28 (cont'd): **`generate_readme_from_metadata.py` fully understood
  and fully tested — action item #1 is now COMPLETE across both scripts.**
  Read through the whole file and found 4 real issues before testing:
  (1) a `freq_ok` checklist bug — a missing comma turned a tuple-membership
  check into a substring check, incorrectly marking legitimate
  `usage_frequency` values (Daily/Weekly/Monthly/As needed) as unconfirmed,
  since those words are substrings of the placeholder text itself; confirmed
  live against a real generated README before fixing; (2) an `.xlsm`
  extension mismatch for `.xlam`/`.xls` file types — reviewed, deliberately
  left as-is; (3) a `last_modified`/Version-History date inconsistency —
  reviewed, resolved as intentional once actual usage was clarified
  (the field represents when the macro itself was updated, not the README);
  (4) a duplicated "User type not specified" x3 placeholder — confirmed
  intentional (matches the template's 3 user-type slots). Then wrote 10
  test files (~74 tests) covering every function: the 2 pure helpers
  (`safe_get`, `is_set`), all sections of `build_readme_content()` (header,
  description, macros-included/who-should-use-this, prerequisites/how-to-use,
  version history, and the Metadata Status checklist), a static-sections
  smoke test, `process_macro_folder()`, and `main()`. **Found and fixed 2
  more real bugs while writing the checklist tests** — genuinely caught by
  the act of testing, not by reading: `status_ok` was computed but never
  actually referenced in the output (the "Version, status, and owner set"
  line only ever checked `version_ok`), and even after wiring it in,
  `status_ok`'s own maintainer check was contaminated by a display-friendly
  placeholder ("Maintainer Name") that gets substituted in before the
  completeness check runs, making a genuinely missing owner look "set."
  Both fixed and regression-tested. Full detail in `changes_log.md`.
  **Total test coverage across both scripts: ~225 tests across 30 test
  files.** Action item #1 checkbox now checked.
- 2026-07-30: **Action item #2 (CI) started, then shelved due to a real
  infrastructure blocker.** Built and explained a working GitHub Actions
  workflow (`.github/workflows/tests.yml`) that runs the full pytest suite
  on every push/PR to `main`. Pushed successfully, but the workflow got
  stuck "queued" indefinitely. Root cause identified: the repo lives on
  **GitHub Enterprise Server** (`github.l3harris.com`), not public
  `github.com` — Enterprise Server has no access to GitHub's cloud-hosted
  `ubuntu-latest` runners at all; it requires self-hosted runners
  (company-provided machines registered to the instance) that don't appear
  to exist or be accessible here. Confirmed no "Actions → Runners" option
  exists in repo settings, and no admin contact/access is available to
  request one. Also confirmed moving this repo (or its data) to a personal
  GitHub.com account is not viable, since it contains real company data
  that can't be transferred to a personal machine. **Decision: shelve item
  #2 for now.** Two real workarounds were identified and explained for
  later, if useful: (a) a local Git pre-push hook — runs tests
  automatically before every push, blocks the push on failure, but only
  protects this one machine's pushes and isn't visible to others (not
  "real" CI, just local automation); (b) a small, separate, from-scratch
  demo repo with fake/sanitized data on a personal GitHub.com account,
  purely to demonstrate real working Actions CI for interview purposes,
  independent of this company repo. Neither pursued yet — revisit if
  circumstances change (e.g., runner access becomes available, or the demo
  repo path becomes worth the separate effort).
- 2026-08-04 (approximate — reported after work happened elsewhere):
  **Action item #3 (schema validation) is COMPLETE.** Built `schema.py`
  using `pydantic`, modeling the fields actually read by both scripts today
  (not the full metadata template) — `Ownership`, `Dates`, `Users`,
  `Technical`, `Categories`, and the top-level `MacroMetadata`, with
  required vs. optional fields deliberately matching real usage (e.g.
  `business_criticality` required, `last_tested` optional). Wired into
  `load_all_metadata()` at the loading boundary only: raw YAML is now
  validated against the schema immediately after parsing, then converted
  back to a plain dict via `.model_dump()` before being handed to the rest
  of the codebase — meaning all 25 query functions and all existing tests
  needed zero changes, since the function's external return shape never
  changed. A validation failure is treated the same as a YAML parse
  failure already was: print a clear error, skip that one macro, keep
  going with the rest.

  Real issues found and fixed while validating against all 25 real macro
  files: (1) `tags` and `typical_users` — YAML fields present but null
  (`tags:` with nothing after the colon) failed validation, since the
  `List[str] = []` default only applies when a field is missing entirely,
  not when it's explicitly null; fixed with `@field_validator(...,
  mode='before')` methods that convert `None` to `[]` before Pydantic's
  normal type-check runs — first real use of Pydantic validators in this
  project. (2) `ms_project_version_required` (and similar version fields)
  — real metadata had unquoted numbers (`2016` instead of `"2016"`), which
  YAML parses as an actual integer, not a string; rather than hand-editing
  every affected file (found in ~10 macros, likely to recur with any future
  macro), fixed with a coercion validator that converts numeric input to a
  string before validation — the more durable fix, matching the same
  validator pattern already established for the null-list issue. Frank
  diagnosed and fixed both independently after the pattern was demonstrated
  once. (3) Confirmed and fixed a real `usage_freuency` (missing 'q') typo
  in the schema field name itself, caught via a screenshot during
  debugging.

  **Separate genuine refactor**: `safe_get()` was originally written only
  in `generate_readme_from_metadata.py`, but turned out to be needed in
  `query_macros.py` too. Rather than duplicate it, both scripts' shared
  helpers were consolidated into a new `utils.py`, imported by both — a
  real DRY improvement, done independently. Some existing test files
  needed minor adjustment to match (import paths, etc.).

  **Verification note**: full test suite was rerun after these changes as
  a safety check (good instinct — confirming a refactor didn't silently
  break existing coverage) and some tests did fail; the specific failures
  weren't reviewed together in this chat, since Frank moved active
  debugging to a different chat/session to solve the cross-computer
  copy-paste constraint documented below. Confirm with Frank next session
  whether those failures are already resolved.

  **Workflow note**: Frank has started using a separate chat/computer
  setup to work around the file-transfer constraint described in "Known
  Constraint" below — worth checking next session whether that constraint
  has actually been resolved (e.g. a real file-transfer method was found)
  or whether work is still being manually relayed between sessions.
- 2026-08-04 (cont'd): **Follow-up reported via screenshots from the
  separate session/computer — the open test-failure item is resolved.**
  231 tests, all passing. Full technical detail logged in `changes_log.md`;
  summary here: (1) `schema.py` was substantially expanded beyond the
  original agreed scope to cover nearly the entire metadata template
  (Dependencies, Issues, Documentation, VersionControl, ChangeEntry,
  Migration, and more) — noted factually as a real scope change from the
  "Option 3, actively-used-fields-only" plan agreed on in this chat, not
  treated as either automatically right or wrong. (2) **A real, notable bug
  was found in `safe_get()` itself**, caused by adding schema validation:
  `MacroMetadata.model_dump()` turns a missing `Optional` field into an
  explicit `None` value in the dict rather than an absent key, and the
  original `safe_get` only checked for absence — so it started silently
  returning `None` instead of intended defaults everywhere, project-wide,
  the moment schema validation went live. Fixed with a one-line change
  (`return cur if cur is not None else default`). Good concrete example of
  why rerunning the full suite after any change matters, even one that
  seems unrelated. (3) `main()` was redesigned for better UX — menu prints
  once, auto-returns after each query instead of requiring a manual
  re-menu option — and a real "missing parens on lambda" bug (the same
  category found and fixed project-wide much earlier) was found freshly
  reintroduced in menu options 22–25 and fixed again. (4) Test files
  refactored to use a shared `_BASE_YAML` template + small YAML-building
  helpers instead of each test hand-writing full YAML blocks, reducing
  duplication across the ~30 test files. (5) One test file
  (`test_find_excel_with_power_query.py`) was found to contain the wrong
  test's content entirely and was replaced.

  **Total project test count: 231, all passing**, across both scripts.
- 2026-08-04 (cont'd): Confirmed the newly-expanded `schema.py` sections
  (Dependencies, Issues, Documentation, VersionControl, ChangeEntry,
  Migration, Description, MacroEntry, OriginalAuthor, InputOutput) have
  **no dedicated test coverage yet** — the 231 passing tests don't include
  anything specifically exercising these newer models or their validators.
  **Decision: have the other chat/computer session write `test_schema.py`**
  to close this gap, rather than doing it here. When that comes back,
  worth specifically checking: (1) does it cover the required-vs-optional
  distinction for each new section, the way the original core schema tests
  would have; (2) does it include the same "present but null" edge case
  tests as `tags`/`typical_users` for every new list field, given that's
  been a recurring real bug pattern in this project (found 3 times now:
  `generate_summary_report`, the original `tags` schema issue, and
  `safe_get` itself); (3) does it verify `coerce_versions_list` on the two
  version-list fields specifically, since that validator does real
  normalization work (bare values, filtering nulls) worth confirming
  directly.
- 2026-08-04 (cont'd): **`test_schema.py` completed — 51 new tests, all
  passing.** Closes the coverage gap flagged above for the expanded schema
  sections. **Total project test count: 282, all passing**, across both
  scripts plus the schema module. Worth confirming next session whether
  the three specific checks noted above (required-vs-optional per new
  section, "present but null" edge cases on new list fields, and
  `coerce_versions_list` behavior) actually got covered, or just general
  happy-path validation — not yet reviewed in this chat.
- 2026-08-05 (cont'd): **Action item #5 (CLI interface) reviewed in full —
  genuinely thorough, well-reasoned work.** Full technical detail in
  `changes_log.md`; summary here. Used `click` (deliberately chosen over
  `argparse` for cleaner syntax and better `--help` output). Deliberately
  scoped as a **partial** CLI, not a full flag-based overhaul of all 25
  queries — a considered, well-justified decision (the interactive menu
  already suits the real use case; 25 flags would be a lot of new surface
  area for a small team that's always at a terminal), not a shortcut.
  `macro-query` gained real `--help` support around its existing menu.
  `macro-generate-readme` gained a proper optional `FOLDER` argument, plus
  a genuinely good safety feature: a new **three-prompt confirmation flow**
  when run with no argument, specifically added because the original
  script silently overwrote every README in the repo with zero
  confirmation — a real risk this closes. `click>=8.0` added as a declared
  dependency; a new 10-test CLI test file was added using `click.testing.
  CliRunner` (the correct, click-specific way to test CLI commands — not
  calling `main()` directly). **A real bug was found and fixed as a direct
  consequence of this change**: the existing `test_readme_main.py` broke
  in two distinct ways once `click` was introduced (an uncaught
  `SystemExit` from click's default `sys.exit(0)` behavior, and a stdin-
  read conflict with pytest's output capture) — both fixed by rewriting
  those 5 tests to also use `CliRunner`. Good, concrete example of a
  click-specific testing gotcha, worth remembering for any future CLI work.

  **Reported test total: 295, all passing — confirmed directly via
  `pytest --collect-only` (2026-08-11), not just taken on report.** The
  earlier expected total of 292 was simply an arithmetic miscount
  somewhere, not a real issue with the work.
- 2026-08-05: **Action item #4 (packaging) reported complete** —
  work done in the separate session/computer, not directly reviewed here.
  Package named `macro_tools`, built with `pyproject.toml`, using the
  `src/` layout (package code under `src/macro_tools/`, separated from
  tests/config at the repo root — the more modern convention). Reported as
  "successfully tested and complete." **Confirmed**: `pip install -e .`
  was actually run (editable install). **Confirmed**: `[project.scripts]`
  console-script entry points exist for both scripts:
  ```toml
  [project.scripts]
  macro-query = "macro_tools.query_macros:main"
  macro-generate-readme = "macro_tools.generate_readme_from_metadata:main"
  ```
  This means both tools can already be run as real terminal commands
  (`macro-query`, `macro-generate-readme`) after install, instead of
  `python query_macros.py`. **Important distinction for scoping item #5**:
  this is NOT the same thing as item #5's flag-based CLI goal — the entry
  points just give the existing `main()` functions memorable command
  names; `macro-query`'s `main()` still drives the same interactive numbered
  menu, and `macro-generate-readme`'s `main()` still takes one positional
  macro-folder argument. Item #5 (structured flags, e.g.
  `macro-query find-by-status --status active`, real `--help` text,
  argument validation via `argparse`/`click`) is still fully open — but the
  console-script foundation it would build on top of is already in place,
  which should make item #5 somewhat smaller than starting from scratch.
- 2026-08-11: **Action item #5 (CLI interface) reported complete**
  — work done in the separate session/computer, not directly reviewed
  here. Built using `click` (not `argparse`). A dedicated test file for
  the CLI layer was created, and all its tests passed. Some "minor
  refactoring of other files" was needed to support it — specifics not yet
  reviewed in this chat. **Not yet confirmed**: the actual command
  structure now available (e.g. whether it's genuinely flag-based like
  `macro-query find-by-status --status active`, or something else), how
  many CLI-layer tests were added and what they cover, which existing
  files were refactored and why, and whether `click` was added as a
  declared dependency in `pyproject.toml`. Worth reviewing the actual CLI
  test file and command definitions together next session, both to verify
  the work and to fold a firsthand understanding of `click` into the
  project the way every other tool introduced here has been walked
  through directly (pytest, pydantic, GitHub Actions) — this is the first
  action item completed entirely off-session without any of that shared
  walkthrough happening yet.

---

## Known Constraint
Frank works across two separate computers for this project (Claude chat on
one, VS Code + the real repo on the other) with no file-transfer method
between them — all code has to be hand-retyped from one screen to the
other. This is a real, ongoing source of transcription bugs (not a
carelessness issue) and should be kept in mind: prefer code patterns that
are easier to retype correctly by hand (e.g., real line breaks over escaped
`\n` sequences in multi-line strings) when it doesn't cost much else.

---

## Resume Bullet Draft (update as project matures)
> Current draft (pre-tests/CI): "Built a Python-based documentation generator that auto-creates README files from structured YAML metadata, standardizing documentation across [N] legacy macros."
>
> Upgrade once items 1–2 are done: add "...with automated test coverage and CI validation via GitHub Actions" or similar, once true.
