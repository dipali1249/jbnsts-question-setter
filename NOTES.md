# Job notes (durable)

Operational memory for the JBNSTS Question Setter job, so a fresh (stateless) run
picks up correctly.

## Last run
- 2026-10-30 — generated **Set 16** (45 bilingual questions: 15 Mathematics, 15 Physical
  Science, 15 Life Science); every answer independently re-derived/cross-checked by script;
  committed to `main` through the GitHub contents API.
- `question_history.json`: `last_set` = 16, 720 fingerprints (675 before + 45 new), all count 1.
- Next set to produce = **17** (highest existing N + 1).

## Pushing to this repo (important)
- The sandbox has **no credentials by default**: an anonymous `git clone` works, but
  `git push` fails with `could not read Username for 'https://github.com'`.
- A push needs a token supplied by the user for that run:
  - Fine-grained PAT with **Repository access → dipali1249/jbnsts-question-setter** and
    **Permissions → Contents: Read and write**; or
  - Classic PAT with the **`repo`** scope.
- A read-only token fails with `403 ... denied to dipali1249` / `Resource not accessible
  by personal access token`. If that happens, ask the user to grant Contents: write.
- Never store the token value in the repo or in any file — it is a secret and must be
  supplied fresh each run.

## Format rules
- Build every set by copying `template/JBNSTS_Exam_Template.html` and substituting only
  `__SET_NO__` and `__QUESTIONS_JSON__`. Do not change layout, CSS or JS.
- Question-object schema and marking/timing are in `template/README.md`.
