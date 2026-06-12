# Annotated Input/Output Example

This file shows one complete example of how a message is passed to the classifier and what the model returns.

---

## Input

The model receives three components formatted as plain text:

**Context (messages for the day):**

```
to-recipient: Good morning!
to-recipient: Today we'll be sending some messages about Valued Living.
to-recipient: Valued Living means living life guided by the principles that matter most to you.
to-recipient: The first step is thinking about what matters to you.
to-system: Good morning
to-recipient: Some common areas that people often have values about include: relationships, work or school, social life, family life, spirituality, health, community life, leisure/fun.
to-recipient: ✍ Text back with one value you hold ✍
to-recipient: Writing it down in a text might help you think through things.
to-system: Honesty
to-recipient: ✍ Did you get a chance to think about what you value? Reply with "yes" or "no" ✍
to-recipient: ✍ Do you want to see more content like this in the future? Reply with "yes" or "no". ✍
```

**Target message:**

```
Honesty
```

**Previous message:**

```
Writing it down in a text might help you think through things.
```

---

## Output

The model returns a JSON array of exactly nine objects, one per theme, in fixed order:

```json
[
  {"key": "polite",      "score": 0.05, "present": false, "evidence": "Single-word reply, but content is substantive rather than perfunctory."},
  {"key": "relational",  "score": 0.05, "present": false, "evidence": "No affective content or personification of the system."},
  {"key": "provocative", "score": 0.02, "present": false, "evidence": "No signs of provocation, frustration, or program inquiry."},
  {"key": "journaling",  "score": 0.10, "present": false, "evidence": "Too brief to constitute personal reflection; no elaboration on experience."},
  {"key": "mistimed",    "score": 0.88, "present": true,  "evidence": "Target directly answers the ✍ response-elicitation prompt ('Text back with one value you hold ✍'), but two subsequent system messages appear before the Target, indicating a belated reply."},
  {"key": "commands",    "score": 0.02, "present": false, "evidence": "No attempt to control or query the program."},
  {"key": "reaction",    "score": 0.01, "present": false, "evidence": "Not formatted as an SMS reaction."},
  {"key": "automated",   "score": 0.01, "present": false, "evidence": "No indicators of an automated focus-mode reply."},
  {"key": "na",          "score": 0.02, "present": false, "evidence": "Message is coherent and interpretable."}
]
```

---

## Notes

- `key` is the name of the label as defined in prior human-only inductive coding of a smaller sample. 
- `score` reflects model confidence that the theme is present (0.0–1.0). This value is not necessarily instructive but can be useful for human review. Understanding the model's confidence can help a human reviewer align prompting with codebook theme concepts. 
- `present` is `true` when `score ≥ 0.5`.
- The `evidence` field contains the model's one-sentence rationale, citing specifics from the message or context. Similar to `score`, this information is intended for use in the iteration process, allowing human reviewers to refine prompting. A rationale out of line with theme concepts calls for further explication of those concepts in the prompting. 
