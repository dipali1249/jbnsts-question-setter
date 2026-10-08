# JBNSTS Question Setter

Durable store for the daily **JBNSTS Junior Talent Search** practice-exam job, so its state
survives sandbox resets.

## What this is

A scheduled task ("Agent Question Setter") generates one interactive HTML practice exam each
day at 12:00 PM IST, targeted at the JBNSTS Junior Talent Search Test (Class 10 / Madhyamik
syllabus, all Indian boards). Each paper has three tests — Mathematics, Physical Science,
Life Science — 15 objective questions each, +2 correct / -0.5 wrong, 4 minutes per question,
English + Bengali, with a topic-tagged answer key and a "weaker portions" analysis.

## Files

- `question_history.json` — fingerprints of every question used so far, with a count.
  A question may appear **at most 3 times** across all sets. The job reads this before
  writing new questions and writes it back after.
- `sets/JBNSTS_Practice_Exam_Class_X_Set_<N>.html` — the generated exam papers (also the
  format template: start screen, per-question timer, overview grid, result screen with
  review + weak-topic analysis).

## How the daily job uses this repo

1. Read `question_history.json` (and the latest set file) to know what has been used and to
   reuse the exact HTML format.
2. Generate 45 fresh, bilingual, cross-checked questions.
3. Commit the new set file and the updated `question_history.json` back here.

Owner: dipali1249. Repository is private.
