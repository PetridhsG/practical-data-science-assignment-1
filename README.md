# Assignment 1 — Do personas annotate like people, and does context change them?

Practical Data Science, MSc in Data Science, Athens University of Economics and Business (AUEB).

## Overview

Toxicity is subjective: different people rate the same comment differently. This assignment asks whether a
small LLM, prompted to play annotators with different identities (personas), can reproduce a human's
toxicity judgements, and whether giving it the surrounding conversation changes its ratings.

The pipeline, built with [SynDisco](https://pypi.org/project/syndisco/):

| Part | Step |
|---|---|
| A | Sample 20 comments with a fixed seed and rate each one myself on a 1-5 toxicity scale, marking the toxic words for ratings 3-5. These ratings are made before seeing any model output and are never changed. |
| B | Describe my ratings (tables, histogram, boxplot). |
| C | Generate one synthetic online conversation per comment, with the comment as the opening post. |
| D | LLM annotators (a persona grid plus a no-persona baseline) rate every comment **with** its conversation as context. |
| E | The same annotators rate every comment **without** context. Invalid answers are counted and reported, not fixed. |
| F | Compare ratings with simple agreement (exact rating and civil/toxic label): me vs. each annotator, with vs. without context, and persona vs. persona. |
| G | Justify the design choices, tell the story of the results, and discuss limitations. |

## Repository contents

- `test.ipynb` — the full analysis with all outputs; seed and repository link in the first cell, explanations in markdown cells.
- `llm_interactions.md` — the prompts and answers exchanged with LLMs while doing the assignment.

## Running

The notebook was run on a Google Colab T4 GPU (runtime 2026.10) with a 4-bit instruction-tuned model.
All outputs are saved in the notebook, so it can be read without being re-run.
