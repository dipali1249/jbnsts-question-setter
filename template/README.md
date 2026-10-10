# JBNSTS Exam Template (permanent)

`JBNSTS_Exam_Template.html` is the **canonical, frozen format** for every daily practice
set — the exact format delivered and approved on 2026-10-10. It is a self-contained,
Bengali-first bilingual interactive exam page: a start screen, a per-question timer (4 min)
and a total timer (180 min), question cards with a Bengali-first stem and four bilingual
options, an "All questions" overview grid, and a result screen with negative marking, a
"Weaker portions to revise" list and a full per-question review with explanations.

Do **not** change the layout, CSS or JS per set. To produce a set, copy this file and
substitute the two placeholders only:

| Placeholder | Replace with |
|---|---|
| `__SET_NO__` | the set number, e.g. `3` |
| `__QUESTIONS_JSON__` | a JSON array of exactly 45 question objects (schema below) |

## Question object schema

```json
{
  "subject": { "en": "Mathematics", "bn": "গণিত" },
  "topic":   { "en": "Quadratic Equations", "bn": "দ্বিঘাত সমীকরণ" },
  "board": "CBSE",
  "q": { "en": "question stem in English", "bn": "প্রশ্ন বাংলায়" },
  "options": [
    { "en": "option A English", "bn": "বিকল্প A বাংলা" },
    { "en": "option B English", "bn": "বিকল্প B বাংলা" },
    { "en": "option C English", "bn": "বিকল্প C বাংলা" },
    { "en": "option D English", "bn": "বিকল্প D বাংলা" }
  ],
  "answer": 0,
  "exp": { "en": "one-line explanation in English", "bn": "এক লাইনের ব্যাখ্যা বাংলায়" }
}
```

Rules for the data:

- `answer` is the **0-based** index of the correct option.
- Exactly **4** options, all distinct, with exactly one unambiguously correct answer.
- Exactly **45** objects: 15 Mathematics, 15 Physical Science, 15 Life Science.
- Subject labels must be exactly `Mathematics`/`গণিত`, `Physical Science`/`ভৌতবিজ্ঞান`,
  `Life Science`/`জীবনবিজ্ঞান`.
- Every field must be present in **both** English and Bengali (Bengali in Bengali script).
- Vary the position of the correct answer across the paper (do not cluster on one letter).
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
