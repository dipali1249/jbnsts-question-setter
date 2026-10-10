# JOB INSTRUCTIONS — generate one JBNSTS practice set

**Run this only when the user has explicitly said "go".** The daily scheduled run does
*not* generate anything — it only reports that it is ready (see `README.md`).

## Target

The JAGADIS BOSE NATIONAL SCIENCE TALENT SEARCH (JBNSTS) — Junior Talent Search Test.
Audience: West Bengal students who passed Class 10 (Madhyamik) with 75%+ and joined Class 11
science.

## Durable state

GitHub — owner `dipali1249`, repo `jbnsts-question-setter`, branch `main`. Read and write it
**before** relying on any local `/scratch` files (the sandbox may be empty).

## STEP 1 — READ STATE

- Read `question_history.json` (fingerprints of every question used so far, with counts; a
  question may appear **at most 3 times** across all sets).
- Read the **permanent template** `template/JBNSTS_Exam_Template.html` — use this, never a
  set file, as the format.
- List `sets/` to find the highest existing N. **Today's Set number = highest N + 1** (or 1
  if none).

## STEP 2 — QUESTIONS (BILINGUAL)

Write 45 fresh objective questions: 15 Mathematics, 15 Physical Science, 15 Life Science.
Draw from the Class 10 syllabus of all Indian boards (CBSE, ICSE and state boards — WBBSE,
Maharashtra, Tamil Nadu, Karnataka, UP and others), mixing boards within the paper; tag each
question with its board. Concept- and reasoning-oriented, JBNSTS-level difficulty.

Every question must be in BOTH English and Bengali — stem, all four options and the one-line
explanation — Bengali first, English beneath. Use the exact question-object schema documented
in `template/README.md`.

Enforce the **no-repeat rule** using the fingerprints in `question_history.json`.

## STEP 3 — CROSS-CHECK EVERY ANSWER (mandatory)

Independently verify the correct answer to every one of the 45 questions before shipping:
re-derive numerical answers by calculation, re-check factual/science answers against the
Class 10 syllabus, and confirm the stored `answer` index points to the option you verified.
Confirm each question has exactly one unambiguously correct option and no duplicate options,
and that the Bengali and English versions state the same thing. If any answer cannot be
confirmed, rewrite or replace that question — never ship an unverified answer.

## STEP 4 — MARKING & TIMING

4 minutes per question → 180 minutes; each question 2 marks; +2 correct, −0.5 wrong,
0 unattempted; 90 marks total; pass 40%. These are baked into the template — do not change them.

## STEP 5 — BUILD, WRITE BACK, DELIVER

1. Build the paper by copying `template/JBNSTS_Exam_Template.html` and substituting
   `__SET_NO__` and `__QUESTIONS_JSON__`.
2. Commit to the repo: `sets/JBNSTS_Practice_Exam_Class_X_Set_<N>.html` and the updated
   `question_history.json` (new fingerprints added, counts incremented, `last_set` updated).
3. Save the paper to `/scratch/output/JBNSTS_Practice_Exam_Class_X_Set_<N>.html` so it is
   delivered to the user.
4. Give a short chat summary: set number, boards covered, questions per subject, and
   confirmation that every answer was cross-checked.
