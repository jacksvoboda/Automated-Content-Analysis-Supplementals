# **Methodological insights from an LLM-automated content analysis of free-text data from a digital mental health intervention**

> This repository accompanies the poster presentation and documents the methods used to classify spantaneous user messages in an SMS-based digital mental health intervention. It is intended as a resource for those without prior experience in executing an automated content analysis process for future projects.

---

## Overview

Participants in a text message-based mental health program occasionally sent messages outside of intended interaction points (i.e., not in response to a system prompt). We refer to these as *unsolicited* or *spontaneous* messages. This project used a large language model to classify those messages based on a codebook developed by human-led inductive qualitative analysis performed on a subsample of the full message set.

These materials focus on the iterative prompting methodology and approach to process refinement, rather than study findings or full data processing pipelines. We wish to highlight our approach to translating a human-authored codebook into an automated classification task, providing materials which demonstrate the simplicity and approachability of LLM-enabled content analysis.

## Repository Structure

```
├── prompts/
│   ├── v1_system_prompt.txt          # Initial prompt with theme definitions
│   └── final_system_prompt.txt       # Final prompt used in classification of the full dataset
├── data/
│   ├── synthetic_input_data.xlsx     # Synthetic input data for demonstration purposes (no real participant data)
│   └── example_input_output.md       # Annotated example: one input row and an expected model output with classifications
└── code/
    └── classification.ipynb          # Python notebook implementing a simplified demonstration of the classification pipeline
```

---

## Coding Scheme

Messages were coded across nine non-mutually-exclusive themes:

| Key             | Description                                                             |
| --------------- | ----------------------------------------------------------------------- |
| `polite`      | Brief responses following common conversational conventions             |
| `relational`  | Conveying positive affect or personifying the system                    |
| `provocative` | Intentional absurdity or expressions of frustration                     |
| `journaling`  | Reflecting on personal experiences or thoughts                          |
| `mistimed`    | User message intended as a prompt response                              |
| `commands`    | Attempts to control the system or giving broad feedback                 |
| `reaction`    | SMS "react" feature messages                                            |
| `automated`   | Auto-replies triggered by smartphone focus modes or automated responses |
| `na`          | Uninterpretable or erroneously included messages                        |

See `prompts/final_system_prompt.txt` for full operationalizations and output schema.

---

## Data Collection

Under a waiver of consent, we deployed an automated DMHI, Small Steps SMS, to 5,076 individuals who completed online mental health self-screeners on the website of Mental Health America. Of the 86,007 recorded user messages, we focus on 11,193 “unsolicited” messages, defined as unprompted user responses received outside prescribed interactive program content. To better understand intentions behind unsolicited interaction, we first conducted a human-only inductive content analysis on a random sample of 1,000 unsolicited user messages, developing a codebook through coding overlapping samples until we achieved substantial interrater reliability.

---

## Design and Development

We followed **"[A Practical Guide and Case Study on How to Instruct LLMs for Automated Coding During Content Analysis](https://doi.org/10.1177/08944393251349541)"** by Farjam et al., to focus our efforts while translating the codebook into a classification task prompt and data processing pipeline. We used our 1,000 human-coded messages to inform prompt iteration by first setting aside 200 messages as a validation holdout. The remaining 800 were used to observe model performance over the course of the development process.

``Farjam, M., Meyer, H., & Lohkamp, M. (2026). A practical guide and case study on how to instruct LLMs for automated coding during content analysis. Social Science Computer Review, 44(3), 488-502.``

Iteration rounds consisted of the following steps:

1. Draft instructions (system prompt) for classification task.
2. Execute classification on the 800 "training" messages.
3. Compare classification output to human coding, highlighting disagreements.
4. Meta-prompt, use a separate "review agent" to refine prompt format, while adding text to explicate assumptions in definitions of underperforming codes
5. Repeat steps 2-4 until desired agreement between human coders and LLM classifier is achieved.

You can observe the differences between our initial draft and final system prompt by comparing `v1_system_prompt.txt` and `final_system_prompt.txt`. Key changes from v1 include structured output format specification, an illustrative JSON example, clarified decision rules for edge cases, and added background information on the Small Steps program.

---

## Present Demonstration Data

`data/synthetic_input_data.xlsx` contains fabricated message data structured to match the format used as model input. No real participant data is included.

Each row contains:

- `days_transcript` — the full message history for a given day, formatted as `to-recipient` / `to-system` turns
- `Message` — the target unsolicited message to classify
- `previous_system_message` — the most recent system message before the target (used to disambiguate between multiple similar user messages)

`data/example_input_output.md` shows how one row is formatted as model input and what the classification output looks like.

---

## Code

`code/classification.ipynb` is a Python notebook that implements a simplified demonstration of the classification pipeline.

---

## Citation

> **Svoboda, J.,** Popowski, S., Moon, C., Krause, C., Karr, C., Mohr, D., Meyerhoff, J., & Kornfield, R. (2026). *Methodological insights from an LLM-automated content analysis of free-text data from a digital mental health intervention*. Poster to be presented at the annual meeting of the Society for Digital Mental Health, [Virtual].

---

## Contact

Jack Svoboda
*Research Study Assistant*
Northwestern University, Feinberg School of Medicine
[Center for Behavioral Intervention Technologies](https://cbits.northwestern.edu/)
jack.svoboda@northwestern.edu





---
---


