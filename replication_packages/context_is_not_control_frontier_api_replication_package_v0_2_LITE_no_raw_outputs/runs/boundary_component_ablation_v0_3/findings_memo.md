# OpenRouter Frontier Boundary-Component Ablation v0.3

Run: `openrouter_frontier_boundary_component_ablation_v0_3_20260509_000143`

## Design

- All unsupported raw-render rows
- 3 families
- 20 case_ids per family
- 6 unsupported scenario types
- 6 prompt policies
- 3 frontier models
- 6480 total planned API calls

## Prompt policies

- `original_mc`: original multiple-choice prompt.
- `choices_not_evidence_only`: answer choices marked as hypotheses/non-evidence.
- `source_id_only`: selected source id shown, without explicit admissibility explanation.
- `admissibility_rule_only`: evidence/admissibility rules stated, without explicit selected-source status.
- `selected_status_only`: selected source status states no admissible answer-bearing source is present.
- `full_boundary_wrapper`: requested source, selected source status, selected source id, non-evidence choices, and boundary rules.

## Summary by model and prompt policy

| model_family       | model_id                      | prompt_policy             |   n |   ok_rate |   admissibility_accuracy |   answer_attempt_on_insufficient_rate |   insufficient_like_rate |   format_compliance_rate |   mean_latency_seconds |   total_prompt_tokens |   total_completion_tokens |   total_tokens |
|:-------------------|:------------------------------|:--------------------------|----:|----------:|-------------------------:|--------------------------------------:|-------------------------:|-------------------------:|-----------------------:|----------------------:|--------------------------:|---------------:|
| anthropic_frontier | anthropic/claude-sonnet-4.6   | admissibility_rule_only   | 360 |         1 |                 0.766667 |                             0.233333  |                 1        |                 1        |               2.57617  |                 83116 |                     26495 |         109611 |
| anthropic_frontier | anthropic/claude-sonnet-4.6   | choices_not_evidence_only | 360 |         1 |                 0.633333 |                             0.366667  |                 1        |                 1        |               2.71881  |                 76276 |                     29284 |         105560 |
| anthropic_frontier | anthropic/claude-sonnet-4.6   | full_boundary_wrapper     | 360 |         1 |                 0.952778 |                             0.0472222 |                 1        |                 1        |               2.32544  |                104356 |                     21873 |         126229 |
| anthropic_frontier | anthropic/claude-sonnet-4.6   | original_mc               | 360 |         1 |                 0        |                             1         |                 0        |                 0        |               1.28486  |                 60528 |                      2556 |          63084 |
| anthropic_frontier | anthropic/claude-sonnet-4.6   | selected_status_only      | 360 |         1 |                 0.822222 |                             0.177778  |                 0.997222 |                 1        |               2.54299  |                 59356 |                     24465 |          83821 |
| anthropic_frontier | anthropic/claude-sonnet-4.6   | source_id_only            | 360 |         1 |                 0.766667 |                             0.233333  |                 0.955556 |                 1        |               2.51022  |                 55756 |                     25118 |          80874 |
| google_frontier    | google/gemini-3.1-pro-preview | admissibility_rule_only   | 360 |         1 |                 0.858333 |                             0.136111  |                 0.858333 |                 0.861111 |               3.51441  |                 77137 |                     56475 |         133612 |
| google_frontier    | google/gemini-3.1-pro-preview | choices_not_evidence_only | 360 |         1 |                 0.827778 |                             0.169444  |                 0.827778 |                 0.827778 |               4.15584  |                 72458 |                     55798 |         128256 |
| google_frontier    | google/gemini-3.1-pro-preview | full_boundary_wrapper     | 360 |         1 |                 0.936111 |                             0.0638889 |                 0.936111 |                 0.936111 |               3.63443  |                 97659 |                     52641 |         150300 |
| google_frontier    | google/gemini-3.1-pro-preview | original_mc               | 360 |         1 |                 0        |                             1         |                 0        |                 0.683333 |               3.58265  |                 56622 |                     62188 |         118810 |
| google_frontier    | google/gemini-3.1-pro-preview | selected_status_only      | 360 |         1 |                 0.95     |                             0.05      |                 0.95     |                 0.955556 |               3.46633  |                 54818 |                     47957 |         102775 |
| google_frontier    | google/gemini-3.1-pro-preview | source_id_only            | 360 |         1 |                 0.886111 |                             0.113889  |                 0.886111 |                 0.944444 |               3.55811  |                 51579 |                     51365 |         102944 |
| openai_frontier    | openai/gpt-5.1                | admissibility_rule_only   | 360 |         1 |                 0.941667 |                             0.0583333 |                 0.941667 |                 1        |               1.04127  |                 72186 |                      5697 |          77883 |
| openai_frontier    | openai/gpt-5.1                | choices_not_evidence_only | 360 |         1 |                 0.858333 |                             0.141667  |                 0.858333 |                 1        |               0.96324  |                 67506 |                      5607 |          73113 |
| openai_frontier    | openai/gpt-5.1                | full_boundary_wrapper     | 360 |         1 |                 1        |                             0         |                 1        |                 1        |               0.979732 |                 90906 |                      5760 |          96666 |
| openai_frontier    | openai/gpt-5.1                | original_mc               | 360 |         1 |                 0        |                             1         |                 0        |                 0        |               0.924897 |                 51354 |                      4896 |          56250 |
| openai_frontier    | openai/gpt-5.1                | selected_status_only      | 360 |         1 |                 0.830556 |                             0.169444  |                 0.830556 |                 1        |               0.912144 |                 50946 |                      5577 |          56523 |
| openai_frontier    | openai/gpt-5.1                | source_id_only            | 360 |         1 |                 0.738889 |                             0.261111  |                 0.738889 |                 1        |               0.924441 |                 48066 |                      5478 |          53544 |

## Component lift vs original

| model_family       | model_id                      | prompt_policy             |   n |   admissibility_accuracy |   admissibility_lift_vs_original |   answer_attempt_on_insufficient_rate |   answer_attempt_reduction_vs_original |
|:-------------------|:------------------------------|:--------------------------|----:|-------------------------:|---------------------------------:|--------------------------------------:|---------------------------------------:|
| anthropic_frontier | anthropic/claude-sonnet-4.6   | admissibility_rule_only   | 360 |                 0.766667 |                         0.766667 |                             0.233333  |                               0.766667 |
| anthropic_frontier | anthropic/claude-sonnet-4.6   | choices_not_evidence_only | 360 |                 0.633333 |                         0.633333 |                             0.366667  |                               0.633333 |
| anthropic_frontier | anthropic/claude-sonnet-4.6   | full_boundary_wrapper     | 360 |                 0.952778 |                         0.952778 |                             0.0472222 |                               0.952778 |
| anthropic_frontier | anthropic/claude-sonnet-4.6   | original_mc               | 360 |                 0        |                         0        |                             1         |                               0        |
| anthropic_frontier | anthropic/claude-sonnet-4.6   | selected_status_only      | 360 |                 0.822222 |                         0.822222 |                             0.177778  |                               0.822222 |
| anthropic_frontier | anthropic/claude-sonnet-4.6   | source_id_only            | 360 |                 0.766667 |                         0.766667 |                             0.233333  |                               0.766667 |
| google_frontier    | google/gemini-3.1-pro-preview | admissibility_rule_only   | 360 |                 0.858333 |                         0.858333 |                             0.136111  |                               0.863889 |
| google_frontier    | google/gemini-3.1-pro-preview | choices_not_evidence_only | 360 |                 0.827778 |                         0.827778 |                             0.169444  |                               0.830556 |
| google_frontier    | google/gemini-3.1-pro-preview | full_boundary_wrapper     | 360 |                 0.936111 |                         0.936111 |                             0.0638889 |                               0.936111 |
| google_frontier    | google/gemini-3.1-pro-preview | original_mc               | 360 |                 0        |                         0        |                             1         |                               0        |
| google_frontier    | google/gemini-3.1-pro-preview | selected_status_only      | 360 |                 0.95     |                         0.95     |                             0.05      |                               0.95     |
| google_frontier    | google/gemini-3.1-pro-preview | source_id_only            | 360 |                 0.886111 |                         0.886111 |                             0.113889  |                               0.886111 |
| openai_frontier    | openai/gpt-5.1                | admissibility_rule_only   | 360 |                 0.941667 |                         0.941667 |                             0.0583333 |                               0.941667 |
| openai_frontier    | openai/gpt-5.1                | choices_not_evidence_only | 360 |                 0.858333 |                         0.858333 |                             0.141667  |                               0.858333 |
| openai_frontier    | openai/gpt-5.1                | full_boundary_wrapper     | 360 |                 1        |                         1        |                             0         |                               1        |
| openai_frontier    | openai/gpt-5.1                | original_mc               | 360 |                 0        |                         0        |                             1         |                               0        |
| openai_frontier    | openai/gpt-5.1                | selected_status_only      | 360 |                 0.830556 |                         0.830556 |                             0.169444  |                               0.830556 |
| openai_frontier    | openai/gpt-5.1                | source_id_only            | 360 |                 0.738889 |                         0.738889 |                             0.261111  |                               0.738889 |

## Interpretation guide

- If `selected_status_only` nearly matches `full_boundary_wrapper`, the key intervention is explicit admissibility status.
- If `admissibility_rule_only` works without selected status, general rule framing is sufficient.
- If `source_id_only` fails, simply exposing source id is insufficient.
- If `choices_not_evidence_only` helps but does not fully solve, answer-choice pressure is part of the failure but not the whole boundary representation.

## Files

- Raw outputs: `/content/drive/MyDrive/context_vs_control_outputs/final_cross_model_replication_fixed/openrouter_frontier_boundary_component_ablation_v0_3/openrouter_frontier_boundary_component_ablation_v0_3_20260509_000143/raw_outputs.jsonl`
- Scored outputs: `/content/drive/MyDrive/context_vs_control_outputs/final_cross_model_replication_fixed/openrouter_frontier_boundary_component_ablation_v0_3/openrouter_frontier_boundary_component_ablation_v0_3_20260509_000143/scored_outputs.csv`
- Failure examples: `/content/drive/MyDrive/context_vs_control_outputs/final_cross_model_replication_fixed/openrouter_frontier_boundary_component_ablation_v0_3/openrouter_frontier_boundary_component_ablation_v0_3_20260509_000143/failure_examples.csv`
- Manifest: `/content/drive/MyDrive/context_vs_control_outputs/final_cross_model_replication_fixed/openrouter_frontier_boundary_component_ablation_v0_3/openrouter_frontier_boundary_component_ablation_v0_3_20260509_000143/run_manifest.json`