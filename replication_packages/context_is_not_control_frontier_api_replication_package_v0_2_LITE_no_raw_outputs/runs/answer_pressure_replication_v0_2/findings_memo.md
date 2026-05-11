# OpenRouter Frontier Answer-Pressure Replication v0.2

Run: `openrouter_frontier_answer_pressure_replication_v0_2_20260508_225356`

## Design

- 5 case_ids per family
- 3 families
- 2 supported positive-control scenario types
- 6 unsupported/admissibility scenario types
- 4 prompt policies
- 3 frontier models
- 1440 total API calls

## Selected case ids
- newer_vs_older_memory: ['memory_0', 'memory_1', 'memory_2', 'memory_3', 'memory_4']
- current_vs_archived_policy: ['policy_0', 'policy_1', 'policy_2', 'policy_3', 'policy_4']
- current_vs_old_software_docs: ['software_0', 'software_1', 'software_2', 'software_3', 'software_4']

## Summary by model and prompt policy

| model_family       | model_id                      | prompt_policy            |   n |   ok_rate |   semantic_accuracy |   admissibility_accuracy |   format_compliance_rate |   answer_attempt_on_insufficient_rate |   insufficient_like_rate |   mean_latency_seconds |   total_prompt_tokens |   total_completion_tokens |   total_tokens |
|:-------------------|:------------------------------|:-------------------------|----:|----------:|--------------------:|-------------------------:|-------------------------:|--------------------------------------:|-------------------------:|-----------------------:|----------------------:|--------------------------:|---------------:|
| anthropic_frontier | anthropic/claude-sonnet-4.6   | explicit_source_boundary | 120 |         1 |            1        |                 1        |                 1        |                             0         |                 0.75     |               2.05527  |                 37405 |                      5865 |          43270 |
| anthropic_frontier | anthropic/claude-sonnet-4.6   | mc_choices_not_evidence  | 120 |         1 |            0.816667 |                 0.816667 |                 0.991667 |                             0.183333  |                 0.741667 |               2.49856  |                 29935 |                      8169 |          38104 |
| anthropic_frontier | anthropic/claude-sonnet-4.6   | open_ended_no_choices    | 120 |         1 |            0.8      |                 0.8      |                 0.75     |                             0.2       |                 0.75     |               2.19826  |                 25311 |                      6832 |          32143 |
| anthropic_frontier | anthropic/claude-sonnet-4.6   | original_mc              | 120 |         1 |            0.25     |                 0.25     |                 0        |                             0.75      |                 0        |               1.32088  |                 20088 |                       872 |          20960 |
| google_frontier    | google/gemini-3.1-pro-preview | explicit_source_boundary | 120 |         1 |            0.875    |                 0.875    |                 0.875    |                             0.0666667 |                 0.683333 |               3.48042  |                 35049 |                     17893 |          52942 |
| google_frontier    | google/gemini-3.1-pro-preview | mc_choices_not_evidence  | 120 |         1 |            0.783333 |                 0.783333 |                 0.783333 |                             0.183333  |                 0.566667 |               3.64185  |                 28268 |                     19018 |          47286 |
| google_frontier    | google/gemini-3.1-pro-preview | open_ended_no_choices    | 120 |         1 |            0.591667 |                 0.591667 |                 0.475    |                             0.291667  |                 0.458333 |               3.75116  |                 23700 |                     21073 |          44773 |
| google_frontier    | google/gemini-3.1-pro-preview | original_mc              | 120 |         1 |            0.225    |                 0.225    |                 0.741667 |                             0.75      |                 0        |               3.85166  |                 18857 |                     20711 |          39568 |
| openai_frontier    | openai/gpt-5.1                | explicit_source_boundary | 120 |         1 |            0.991667 |                 0.991667 |                 0.991667 |                             0         |                 0.75     |               0.961513 |                 32487 |                      1817 |          34304 |
| openai_frontier    | openai/gpt-5.1                | mc_choices_not_evidence  | 120 |         1 |            0.95     |                 0.95     |                 0.991667 |                             0.0416667 |                 0.708333 |               0.971572 |                 26090 |                      1802 |          27892 |
| openai_frontier    | openai/gpt-5.1                | open_ended_no_choices    | 120 |         1 |            0.858333 |                 0.858333 |                 0.625    |                             0.125     |                 0.625    |               1.02739  |                 21511 |                      1993 |          23504 |
| openai_frontier    | openai/gpt-5.1                | original_mc              | 120 |         1 |            0.25     |                 0.25     |                 0        |                             0.75      |                 0        |               0.95606  |                 17064 |                      1658 |          18722 |

## Unsupported answer-pressure summary

| model_family       | model_id                      | prompt_policy            |   n |   admissibility_accuracy |   answer_attempt_on_insufficient_rate |   insufficient_like_rate |   format_compliance_rate |
|:-------------------|:------------------------------|:-------------------------|----:|-------------------------:|--------------------------------------:|-------------------------:|-------------------------:|
| anthropic_frontier | anthropic/claude-sonnet-4.6   | explicit_source_boundary |  90 |                 1        |                             0         |                 1        |                 1        |
| anthropic_frontier | anthropic/claude-sonnet-4.6   | mc_choices_not_evidence  |  90 |                 0.755556 |                             0.244444  |                 0.988889 |                 0.988889 |
| anthropic_frontier | anthropic/claude-sonnet-4.6   | open_ended_no_choices    |  90 |                 0.733333 |                             0.266667  |                 1        |                 1        |
| anthropic_frontier | anthropic/claude-sonnet-4.6   | original_mc              |  90 |                 0        |                             1         |                 0        |                 0        |
| google_frontier    | google/gemini-3.1-pro-preview | explicit_source_boundary |  90 |                 0.911111 |                             0.0888889 |                 0.911111 |                 0.911111 |
| google_frontier    | google/gemini-3.1-pro-preview | mc_choices_not_evidence  |  90 |                 0.755556 |                             0.244444  |                 0.755556 |                 0.755556 |
| google_frontier    | google/gemini-3.1-pro-preview | open_ended_no_choices    |  90 |                 0.611111 |                             0.388889  |                 0.611111 |                 0.633333 |
| google_frontier    | google/gemini-3.1-pro-preview | original_mc              |  90 |                 0        |                             1         |                 0        |                 0.766667 |
| openai_frontier    | openai/gpt-5.1                | explicit_source_boundary |  90 |                 1        |                             0         |                 1        |                 1        |
| openai_frontier    | openai/gpt-5.1                | mc_choices_not_evidence  |  90 |                 0.944444 |                             0.0555556 |                 0.944444 |                 1        |
| openai_frontier    | openai/gpt-5.1                | open_ended_no_choices    |  90 |                 0.833333 |                             0.166667  |                 0.833333 |                 0.833333 |
| openai_frontier    | openai/gpt-5.1                | original_mc              |  90 |                 0        |                             1         |                 0        |                 0        |

## Interpretation guide

- `original_mc` measures answer pressure under the original benchmark frame.
- `mc_choices_not_evidence` tests whether marking choices as hypotheses/non-evidence restores insufficiency behavior.
- `open_ended_no_choices` tests whether removing the choice frame restores insufficiency behavior.
- `explicit_source_boundary` tests whether explicit source admissibility/status framing restores insufficiency behavior.
- The key metric is `answer_attempt_on_insufficient_rate` on unsupported rows.

## Files

- Raw outputs: `/content/drive/MyDrive/context_vs_control_outputs/final_cross_model_replication_fixed/openrouter_frontier_answer_pressure_replication_v0_2/openrouter_frontier_answer_pressure_replication_v0_2_20260508_225356/raw_outputs.jsonl`
- Scored outputs: `/content/drive/MyDrive/context_vs_control_outputs/final_cross_model_replication_fixed/openrouter_frontier_answer_pressure_replication_v0_2/openrouter_frontier_answer_pressure_replication_v0_2_20260508_225356/scored_outputs.csv`
- Failure examples: `/content/drive/MyDrive/context_vs_control_outputs/final_cross_model_replication_fixed/openrouter_frontier_answer_pressure_replication_v0_2/openrouter_frontier_answer_pressure_replication_v0_2_20260508_225356/failure_examples.csv`
- Manifest: `/content/drive/MyDrive/context_vs_control_outputs/final_cross_model_replication_fixed/openrouter_frontier_answer_pressure_replication_v0_2/openrouter_frontier_answer_pressure_replication_v0_2_20260508_225356/run_manifest.json`