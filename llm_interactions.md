# Interactions with LLMs

**Tools used:** Claude Code (Claude Opus 5.5)

The exchanges were long and many, so below is a faithful summary of each way I used the LLM, with example
prompts. My own annotation (part A) was done by me alone, before seeing any model output; the LLM was never
asked to rate the items or to change my ratings.

## 1. Writing the code

The LLM generated most of the code of the notebook: loading the data, the conversations with SynDisco (C), the annotation jobs (D, E), parsing and checking the model's answers, and the agreement tables
and plots (F). I gave it the assignment's requirements and the SynDisco examples of the lab, and asked for one
part at a time. I read and checked every piece of code before keeping it, ran it, and asked for changes when the
output was wrong or not what the assignment asked for.

## 2. Translating my reasoning into English

Some of my explanations and conclusions I first wrote in Greek. I gave them to the LLM to translate into English
for the markdown cells, and then checked that the translation kept my meaning.

> **Example prompt:** "Translate this into English for the notebook, keeping it simple and keeping my meaning:
> «Το context δεν φέρνει τα μοντέλα πιο κοντά σε μένα· όλοι οι annotators καταλήγουν να βαθμολογούν ίδια με το
> baseline.»"
>
> **Answer (summary):** "The context does not bring the models closer to me: every annotator ends up rating
> exactly like the baseline."

## 3. Improving how the results are printed

I asked the LLM to make the printouts easier to read: tables shown in full instead of cut by pandas, long texts
wrapped, and the civil/toxic labels coloured.

> **Example prompt:** "The tables of the items and my ratings are cut off and the comments are on one long line.
> Show them in full in a scrollable box, with the text column wrapped, no index, and the label coloured green for
> civil and red for toxic."
>
> **Answer (summary):** it wrote the `show_table()` helper, which uses a pandas `Styler` to hide the index, wrap
> the text and prompt columns, colour the labels, and display the table inside a scrollable HTML box. It later
> wrote `show_conversations()` in the same style for the 20 conversations of part C.

## 4. The annotation instructions for the model

For the instructions the model annotators follow in D and E (`RATING_INSTRUCTIONS`), I took the annotation
guidelines of the assignment (part A, the scale of `annotate.html`) and asked the LLM to summarise them into a
short prompt with the same 1-5 scale, plus a fixed answer format (`rating | evidence`) so the answers can be
parsed.

## 5. The Colab GPU quota

The model needs a GPU, and I ran out of my free GPU time on Google Colab. The LLM helped me understand why this
happened: the model was kept running on the GPU runtime the whole time I was working on the notebook, including
the parts that do not need it. With its help I changed the notebook so that the parts that need the model (C, D
and E) are run once, their results saved under `data/` and pushed to GitHub, and every later run loads these
files instead of running the model again. The model is only loaded when a GPU is found. I then generated the data
once on Colab with a second account, and did the rest of the assignment (F and the conclusions) locally, without
a GPU.
