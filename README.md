---
language:
- en
license: other
license_name: tbd
pretty_name: English Practical Grammar (Instruction Dataset)
size_categories:
- 1K<n<10K
task_categories:
- text-generation
- question-answering
tags:
- grammar
- english
- education
- instruction-tuning
- sft
- chat
configs:
- config_name: all
  default: true
  data_files:
  - split: train
    path: data/*.jsonl
- config_name: ch01_the_sentence
  data_files:
  - split: train
    path: data/01_the_sentence.jsonl
- config_name: ch02_more_about_questions
  data_files:
  - split: train
    path: data/02_more_about_questions.jsonl
- config_name: ch03_nouns
  data_files:
  - split: train
    path: data/03_nouns.jsonl
- config_name: ch04_pronouns
  data_files:
  - split: train
    path: data/04_pronouns.jsonl
- config_name: ch05_articles
  data_files:
  - split: train
    path: data/05_articles.jsonl
- config_name: ch06_adjectives
  data_files:
  - split: train
    path: data/06_adjectives.jsonl
- config_name: ch07_adverbs
  data_files:
  - split: train
    path: data/07_adverbs.jsonl
- config_name: ch08_degrees_of_comparison
  data_files:
  - split: train
    path: data/08_degrees_of_comparison.jsonl
- config_name: ch09_verbs
  data_files:
  - split: train
    path: data/09_verbs.jsonl
- config_name: ch10_verbs_tenses
  data_files:
  - split: train
    path: data/10_verbs_tenses.jsonl
- config_name: ch11_active_and_passive_voice
  data_files:
  - split: train
    path: data/11_active_and_passive_voice.jsonl
- config_name: ch12_concord
  data_files:
  - split: train
    path: data/12_concord.jsonl
- config_name: ch13_prepositions
  data_files:
  - split: train
    path: data/13_prepositions.jsonl
- config_name: ch14_prepositional_phrases_and_phrasal_verbs
  data_files:
  - split: train
    path: data/14_prepositional_phrases_and_phrasal_verbs.jsonl
- config_name: ch15_direct_and_indirect_speech
  data_files:
  - split: train
    path: data/15_direct_and_indirect_speech.jsonl
- config_name: ch16_types_of_sentences
  data_files:
  - split: train
    path: data/16_types_of_sentences.jsonl
- config_name: ch17_clause_patterns
  data_files:
  - split: train
    path: data/17_clause_patterns.jsonl
- config_name: ch18_synthesis_of_sentences
  data_files:
  - split: train
    path: data/18_synthesis_of_sentences.jsonl
- config_name: ch19_transformation_of_sentences
  data_files:
  - split: train
    path: data/19_transformation_of_sentences.jsonl
- config_name: ch20_punctuation_and_capitals
  data_files:
  - split: train
    path: data/20_punctuation_and_capitals.jsonl
- config_name: ch21_expansion_of_proverbs
  data_files:
  - split: train
    path: data/21_expansion_of_proverbs.jsonl
---

# English Practical Grammar — Instruction Dataset

A chat-format (system / user / assistant) instruction dataset for teaching English grammar to LLMs.
It covers 21 chapters of a practical English grammar course: theory, worked examples, identification
drills and **every practice exercise, each with a correct answer and a short justification**.

- **4,233 records** in 21 JSONL files (one per chapter)
- Ready for supervised fine-tuning (SFT) with TRL, Axolotl, Unsloth, LLaMA-Factory, etc. — the `messages` column is in the standard OpenAI/HF chat format

## Quick start

```python
from datasets import load_dataset

ds = load_dataset("YOUR_HF_USERNAME/english-practical-grammar", split="train")          # all chapters
tenses = load_dataset("YOUR_HF_USERNAME/english-practical-grammar", "ch10_verbs_tenses", split="train")  # one chapter

print(ds[0]["messages"])
exercises = ds.filter(lambda r: r["type"] == "exercise")
```

## Record format

```json
{
  "id": "ch05-0001",
  "chapter": 5,
  "chapter_title": "Articles",
  "section": "5.1 The Definite Article (the): Uses",
  "type": "concept",
  "exercise": null,
  "messages": [
    {"role": "system", "content": "You are an expert English grammar tutor. Explain rules clearly and simply, give correct answers, and briefly justify each answer."},
    {"role": "user", "content": "What are articles? How many kinds of articles are there?"},
    {"role": "assistant", "content": "The **articles** of English (**the, a/an**) are ..."}
  ]
}
```

| Field | Type | Description |
|---|---|---|
| `id` | string | Unique id, `chNN-NNNN` |
| `chapter` | int | Chapter number (1–21) |
| `chapter_title` | string | Chapter name |
| `section` | string | Section heading, using the book's numbering |
| `type` | string | `concept`, `example`, `identification` or `exercise` |
| `exercise` | int / null | Exercise number within the chapter (only for `type == "exercise"`) |
| `messages` | list | Chat turns: `system`, `user`, `assistant` (assistant answers use Markdown) |

### Record types

| Type | What it is |
|---|---|
| `concept` | A rule, definition or explanation from the theory, asked as a natural student question |
| `example` | A worked example built from the book's own illustrations (form changes, usage, meanings) |
| `identification` | Drills: identify / classify / "is this correct?" questions on example sentences |
| `exercise` | One practice question from a book exercise (instruction + item), with the answer in bold and a brief reason |

## Contents

| Ch | Title | File | Records | Concept | Example | Identification | Exercise |
|---|---|---|---|---|---|---|---|
| 1 | The Sentence | `01_the_sentence.jsonl` | 132 | 18 | 0 | 10 | 104 |
| 2 | More About Questions | `02_more_about_questions.jsonl` | 86 | 30 | 1 | 10 | 45 |
| 3 | Nouns | `03_nouns.jsonl` | 353 | 51 | 188 | 40 | 74 |
| 4 | Pronouns | `04_pronouns.jsonl` | 141 | 36 | 30 | 51 | 24 |
| 5 | Articles | `05_articles.jsonl` | 138 | 33 | 24 | 56 | 25 |
| 6 | Adjectives | `06_adjectives.jsonl` | 211 | 44 | 9 | 58 | 100 |
| 7 | Adverbs | `07_adverbs.jsonl` | 212 | 38 | 45 | 52 | 77 |
| 8 | Degrees of Comparison | `08_degrees_of_comparison.jsonl` | 123 | 27 | 34 | 32 | 30 |
| 9 | Verbs | `09_verbs.jsonl` | 421 | 54 | 134 | 135 | 98 |
| 10 | Verbs: Tenses | `10_verbs_tenses.jsonl` | 288 | 52 | 9 | 92 | 135 |
| 11 | Voice: Active and Passive | `11_active_and_passive_voice.jsonl` | 152 | 27 | 35 | 15 | 75 |
| 12 | Concord | `12_concord.jsonl` | 102 | 18 | 41 | 18 | 25 |
| 13 | Prepositions | `13_prepositions.jsonl` | 654 | 37 | 367 | 115 | 135 |
| 14 | Prepositional Phrases and Phrasal Verbs | `14_prepositional_phrases_and_phrasal_verbs.jsonl` | 305 | 109 | 116 | 40 | 40 |
| 15 | Direct and Indirect Speech | `15_direct_and_indirect_speech.jsonl` | 193 | 32 | 67 | 42 | 52 |
| 16 | Types of Sentences | `16_types_of_sentences.jsonl` | 55 | 21 | 6 | 18 | 10 |
| 17 | Clause Patterns | `17_clause_patterns.jsonl` | 152 | 26 | 13 | 73 | 40 |
| 18 | Synthesis of Sentences | `18_synthesis_of_sentences.jsonl` | 157 | 21 | 45 | 51 | 40 |
| 19 | Transformation of Sentences | `19_transformation_of_sentences.jsonl` | 195 | 25 | 46 | 19 | 105 |
| 20 | Punctuation and Capitals | `20_punctuation_and_capitals.jsonl` | 120 | 38 | 7 | 65 | 10 |
| 21 | Expansion of Proverbs | `21_expansion_of_proverbs.jsonl` | 43 | 9 | 4 | 0 | 30 |
| | **Total** | | **4,233** | **746** | **1221** | **992** | **1,274** |

There is a single `train` split. Each chapter is also available as its own config (`ch01_the_sentence` … `ch21_expansion_of_proverbs`).

## How it was made

- Source: scanned pages of a printed English grammar textbook used in India. Pages were read chapter by chapter and converted into question–answer pairs.
- The book prints exercises **without answers**; every exercise answer in this dataset was written for it, with a short justification. Handwritten (often wrong) pen answers on the scanned pages were ignored.
- Obvious printing errors in the book were corrected, and a few dated or insensitive examples were reworded. Notes on modern usage (British vs American English, renamed cities such as Madras → Chennai, old-fashioned forms) were added where useful.
- "Expansion of Proverbs" is numbered 2 in the book's composition part; it is chapter 21 here.

## Limitations

- The grammar follows a traditional British/Indian-English school textbook. Some rules are prescriptive, and some vocabulary and examples are dated; notes flag the main differences from modern or American usage, but not exhaustively.
- Where an exercise blank admits more than one correct answer, the main answer is bold and alternatives are mentioned in the explanation, but not every possible alternative is listed.
- Answers were written with AI assistance and spot-checked, not fully reviewed by a grammar expert. Please report errors in the Community tab.

## License

TBD. The theory and example sentences are derived from a copyrighted textbook; confirm you have the right to redistribute this content before making the dataset public.
