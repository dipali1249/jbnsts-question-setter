# JBNSTS Exam Template (permanent)

`JBNSTS_Exam_Template.html` is the **canonical, frozen format** for every daily practice
set. It is a self-contained interactive exam page containing: a start screen, a
per-question timer (4 min) and a total timer (180 min), question cards with a bilingual
stem and four bilingual options, an "All questions" overview grid, and a result screen
with negative marking, a "Weaker portions to revise" list and a full per-question review
with explanations.

Do **not** change the layout, CSS or JS per set. To produce a set, copy this file and
substitute the two placeholders only:

| Placeholder | Replace with |
|---|---|
| `__SET_NO__` | the set number, e.g. `3` |
| `__QUESTIONS_JSON__` | a JSON array of exactly 45 question objects (schema below) |

## Question object schema

```json
{
  "subject_en": "Mathematics",
  "subject_bn": "গণিত",
  "topic_en": "Quadratic Equations",
  "topic_bn": "দ্বিঘাত সমীকরণ",
  "board": "CBSE",
  "q_en": "question stem in English",
  "q_bn": "প্রশ্ন বাংলায়",
  "options": [
    {"en": "option A English", "bn": "বিকল্প A বাংলা"},
    {"en": "option B English", "bn": "বিকল্প B বাংলা"},
    {"en": "option C English", "bn": "বিকল্প C বাংলা"},
    {"en": "option D English", "bn": "বিকল্প D বাংলা"}
  ],
  "correct": 0,
  "exp_en": "one-line explanation in English",
  "exp_bn": "এক লাইনের ব্যাখ্যা বাংলায়"
}
```

Rules for the data:

- `correct` is the **0-based** index of the correct option.
- Exactly **4** options, all distinct, with exactly one unambiguously correct answer.
- Exactly **45** objects: 15 Mathematics, 15 Physical Science, 15 Life Science.
- Every field must be present in **both** English and Bengali (Bengali in Bengali script).
- Vary the position of the correct answer across the paper (do not let it cluster on one letter).
- `board` is the syllabus board the question aligns with — one of
  `CBSE`, `ICSE`, `WBBSE`, `Maharashtra`, `Tamil Nadu`, `Karnataka`, `UP` — mixed within a paper.

## Fixed marking / timing (baked into the template — do not change)

- 4 minutes per question → **180 minutes** total; each question carries **2 marks**.
- +2 correct, −0.5 wrong, 0 unattempted; maximum **90** marks; pass **40%** (36 marks).

## Example: producing a set

```python
import json
tpl = open("template/JBNSTS_Exam_Template.html", encoding="utf-8").read()
html = tpl.replace("__SET_NO__", "3").replace(
    "__QUESTIONS_JSON__", json.dumps(questions, ensure_ascii=False))
open("sets/JBNSTS_Practice_Exam_Class_X_Set_3.html", "w", encoding="utf-8").write(html)
```
