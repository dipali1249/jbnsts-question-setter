# JBNSTS Question Setter

Durable store for the daily **JBNSTS Junior Talent Search** practice-exam job, so its state
survives sandbox resets.

## What this is

A scheduled task ("Agent Question Setter") prepares one interactive HTML practice exam,
targeted at the JBNSTS Junior Talent Search Test (Class 10 / Madhyamik syllabus, all Indian
boards). Each paper has three tests — Mathematics, Physical Science, Life Science — 15
objective questions each, +2 correct / -0.5 wrong, 4 minutes per question, English + Bengali,
with a topic-tagged answer key and a "weaker portions" analysis.

**Standby mode:** the job does **not** generate a paper on its own. Each day it confirms it
is ready and waits; a paper is produced only when the user explicitly says **"go"**.

## Files

- `JOB_INSTRUCTIONS.md` — the full generation procedure. Run it only when the user says "go".
- `template/JBNSTS_Exam_Template.html` — **the permanent format template.** The single,
  frozen source of the page layout, CSS and JavaScript. Every set is produced by copying
  this file and filling in `__SET_NO__` and `__QUESTIONS_JSON__` only. See
  `template/README.md` for the question schema and usage.
- `sets/JBNSTS_Practice_Exam_Class_X_Set_<N>.html` — the generated exam papers.
- `question_history.json` — fingerprints of every question used so far, with a count.
  A question may appear **at most 3 times** across all sets.

## How the job uses this repo

1. **Daily scheduled run:** confirm readiness (repo reachable, permanent template present,
   history readable), report the next set number, and **stop**. Do not generate anything.
2. **When the user says "go":** follow `JOB_INSTRUCTIONS.md` — read the history, generate 45
   fresh bilingual cross-checked questions, fill the permanent template, commit the set and
   the updated history, and deliver the paper.

> Never treat the latest set file as the template — always use
> `template/JBNSTS_Exam_Template.html`.

Owner: dipali1249. Repository is private.
