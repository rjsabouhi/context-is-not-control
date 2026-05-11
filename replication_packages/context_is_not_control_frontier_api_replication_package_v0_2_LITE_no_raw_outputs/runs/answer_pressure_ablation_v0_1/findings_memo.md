# OpenRouter Frontier Answer-Pressure Ablation v0.1

Run: `openrouter_frontier_answer_pressure_ablation_v0_1_20260508_223131`

## Design

- 3 families
- 2 supported positive-control scenario types
- 6 unsupported/admissibility scenario types
- 4 prompt policies
- 3 frontier models
- 288 total API calls

## Prompt policies

- `original_mc`: original multiple-choice benchmark prompt.
- `mc_choices_not_evidence`: choices remain visible, but explicitly marked as non-evidence.
- `open_ended_no_choices`: removes A/B choice pressure.
- `explicit_source_boundary`: explicitly states selected/admissible source status and source-boundary rules.

## Summary by model and prompt policy

| model_family       | model_id                      | prompt_policy            |   n |   ok_rate |   semantic_accuracy |   admissibility_accuracy |   format_compliance_rate |   answer_attempt_on_insufficient_rate |   insufficient_like_rate |   mean_latency_seconds |
|:-------------------|:------------------------------|:-------------------------|----:|----------:|--------------------:|-------------------------:|-------------------------:|--------------------------------------:|-------------------------:|-----------------------:|
| anthropic_frontier | anthropic/claude-sonnet-4.6   | explicit_source_boundary |  24 |         1 |            1        |                 1        |                 1        |                             0         |                 0.75     |               2.16852  |
| anthropic_frontier | anthropic/claude-sonnet-4.6   | mc_choices_not_evidence  |  24 |         1 |            0.791667 |                 0.791667 |                 0.958333 |                             0.208333  |                 0.708333 |               2.52763  |
| anthropic_frontier | anthropic/claude-sonnet-4.6   | open_ended_no_choices    |  24 |         1 |            0.916667 |                 0.916667 |                 0.75     |                             0.0833333 |                 0.708333 |               2.25567  |
| anthropic_frontier | anthropic/claude-sonnet-4.6   | original_mc              |  24 |         1 |            0.25     |                 0.25     |                 0        |                             0.75      |                 0        |               1.26728  |
| google_frontier    | google/gemini-3.1-pro-preview | explicit_source_boundary |  24 |         1 |            0.708333 |                 0.708333 |                 0.708333 |                             0.25      |                 0.5      |               3.40958  |
| google_frontier    | google/gemini-3.1-pro-preview | mc_choices_not_evidence  |  24 |         1 |            0.583333 |                 0.583333 |                 0.583333 |                             0.375     |                 0.375    |               4.02458  |
| google_frontier    | google/gemini-3.1-pro-preview | open_ended_no_choices    |  24 |         1 |            0.416667 |                 0.416667 |                 0.291667 |                             0.416667  |                 0.291667 |               4.01463  |
| google_frontier    | google/gemini-3.1-pro-preview | original_mc              |  24 |         1 |            0.25     |                 0.25     |                 0.958333 |                             0.75      |                 0        |               3.38228  |
| openai_frontier    | openai/gpt-5.1                | explicit_source_boundary |  24 |         1 |            1        |                 1        |                 1        |                             0         |                 0.75     |               1.01433  |
| openai_frontier    | openai/gpt-5.1                | mc_choices_not_evidence  |  24 |         1 |            0.958333 |                 0.958333 |                 1        |                             0.0416667 |                 0.708333 |               0.975637 |
| openai_frontier    | openai/gpt-5.1                | open_ended_no_choices    |  24 |         1 |            0.875    |                 0.875    |                 0.625    |                             0.125     |                 0.625    |               0.922437 |
| openai_frontier    | openai/gpt-5.1                | original_mc              |  24 |         1 |            0.25     |                 0.25     |                 0        |                             0.75      |                 0        |               1.01234  |

## Unsupported answer-pressure summary

| model_family       | model_id                      | prompt_policy            |   n |   admissibility_accuracy |   answer_attempt_on_insufficient_rate |   insufficient_like_rate |
|:-------------------|:------------------------------|:-------------------------|----:|-------------------------:|--------------------------------------:|-------------------------:|
| anthropic_frontier | anthropic/claude-sonnet-4.6   | explicit_source_boundary |  18 |                 1        |                             0         |                 1        |
| anthropic_frontier | anthropic/claude-sonnet-4.6   | mc_choices_not_evidence  |  18 |                 0.722222 |                             0.277778  |                 0.944444 |
| anthropic_frontier | anthropic/claude-sonnet-4.6   | open_ended_no_choices    |  18 |                 0.888889 |                             0.111111  |                 0.944444 |
| anthropic_frontier | anthropic/claude-sonnet-4.6   | original_mc              |  18 |                 0        |                             1         |                 0        |
| google_frontier    | google/gemini-3.1-pro-preview | explicit_source_boundary |  18 |                 0.666667 |                             0.333333  |                 0.666667 |
| google_frontier    | google/gemini-3.1-pro-preview | mc_choices_not_evidence  |  18 |                 0.5      |                             0.5       |                 0.5      |
| google_frontier    | google/gemini-3.1-pro-preview | open_ended_no_choices    |  18 |                 0.388889 |                             0.555556  |                 0.388889 |
| google_frontier    | google/gemini-3.1-pro-preview | original_mc              |  18 |                 0        |                             1         |                 0        |
| openai_frontier    | openai/gpt-5.1                | explicit_source_boundary |  18 |                 1        |                             0         |                 1        |
| openai_frontier    | openai/gpt-5.1                | mc_choices_not_evidence  |  18 |                 0.944444 |                             0.0555556 |                 0.944444 |
| openai_frontier    | openai/gpt-5.1                | open_ended_no_choices    |  18 |                 0.833333 |                             0.166667  |                 0.833333 |
| openai_frontier    | openai/gpt-5.1                | original_mc              |  18 |                 0        |                             1         |                 0        |

## Interpretation guide

- If `original_mc` fails unsupported rows but `open_ended_no_choices` improves, answer-choice pressure is a major driver.
- If `mc_choices_not_evidence` improves over `original_mc`, choices-as-non-evidence language helps.
- If `explicit_source_boundary` improves most, the source-boundary representation is the controlling intervention.
- If unsupported rows fail across all policies, the insufficiency/admissibility boundary is deeply unstable under this task family.

## Files

- Raw outputs: `/content/drive/MyDrive/context_vs_control_outputs/final_cross_model_replication_fixed/openrouter_frontier_answer_pressure_ablation_v0_1/openrouter_frontier_answer_pressure_ablation_v0_1_20260508_223131/raw_outputs.jsonl`
- Scored outputs: `/content/drive/MyDrive/context_vs_control_outputs/final_cross_model_replication_fixed/openrouter_frontier_answer_pressure_ablation_v0_1/openrouter_frontier_answer_pressure_ablation_v0_1_20260508_223131/scored_outputs.csv`
- Failure examples: `/content/drive/MyDrive/context_vs_control_outputs/final_cross_model_replication_fixed/openrouter_frontier_answer_pressure_ablation_v0_1/openrouter_frontier_answer_pressure_ablation_v0_1_20260508_223131/failure_examples.csv`
- Manifest: `/content/drive/MyDrive/context_vs_control_outputs/final_cross_model_replication_fixed/openrouter_frontier_answer_pressure_ablation_v0_1/openrouter_frontier_answer_pressure_ablation_v0_1_20260508_223131/run_manifest.json`