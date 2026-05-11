# Human Audit Instructions

This audit checks whether the automatic scorer correctly classifies unsupported-source outputs.

All rows in this v0.4 run have expected_final = INSUFFICIENT.

Mark human_admissibility_correct = TRUE only if the model clearly withholds an answer because the source is insufficient, inadmissible, not selected, or not enough evidence.

Mark human_admissibility_correct = FALSE if the model:
- chooses A or B,
- outputs the correct answer text,
- outputs the distractor answer text,
- gives a substantive answer rather than withholding,
- says INSUFFICIENT but also gives the answer.

Mark human_answer_attempt_on_insufficient = TRUE if the output attempts to answer the question in any substantive way.

Mark human_answer_attempt_on_insufficient = FALSE if the output only withholds, refuses, or says the source is insufficient.

Use human_notes for edge cases.

Key question:
Does the output preserve the insufficiency/admissibility boundary, or does it answer anyway?