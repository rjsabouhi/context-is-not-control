# OpenRouter Frontier Channel-Control Ablation v0.4

Run: `openrouter_frontier_channel_control_ablation_v0_4_20260509_055740`

## Design

- All unsupported raw-render rows
- 3 families
- 20 case_ids per family
- 6 unsupported scenario types
- 5 prompt policies
- 3 frontier models
- 5400 total planned API calls

## Prompt policies

- `original_mc`: original multiple-choice prompt.
- `insufficient_channel_only`: original prompt plus only an INSUFFICIENT output option.
- `insufficient_channel_choices_not_evidence`: adds INSUFFICIENT and says choices are not evidence.
- `insufficient_channel_admissibility_rule`: adds INSUFFICIENT and an admissibility/evidence rule.
- `full_boundary_wrapper`: explicit requested source, selected source status, selected source id, and boundary rules.

## Summary by model and prompt policy

| model_family       | model_id                      | prompt_policy                             |   n |   ok_rate |   admissibility_accuracy |   answer_attempt_on_insufficient_rate |   insufficient_like_rate |   format_compliance_rate |   mean_latency_seconds |   total_prompt_tokens |   total_completion_tokens |   total_tokens |
|:-------------------|:------------------------------|:------------------------------------------|----:|----------:|-------------------------:|--------------------------------------:|-------------------------:|-------------------------:|-----------------------:|----------------------:|--------------------------:|---------------:|
| anthropic_frontier | anthropic/claude-sonnet-4.6   | full_boundary_wrapper                     | 360 |         1 |                 0.958333 |                             0.0416667 |                 1        |                 1        |                2.81368 |                104356 |                     21471 |         125827 |
| anthropic_frontier | anthropic/claude-sonnet-4.6   | insufficient_channel_admissibility_rule   | 360 |         1 |                 0.744444 |                             0.255556  |                 0.994444 |                 0.994444 |                3.20308 |                 85276 |                     27516 |         112792 |
| anthropic_frontier | anthropic/claude-sonnet-4.6   | insufficient_channel_choices_not_evidence | 360 |         1 |                 0        |                             1         |                 0        |                 1        |                1.82758 |                 90408 |                      2520 |          92928 |
| anthropic_frontier | anthropic/claude-sonnet-4.6   | insufficient_channel_only                 | 360 |         1 |                 0        |                             1         |                 0        |                 1        |                1.85622 |                 78168 |                      2556 |          80724 |
| anthropic_frontier | anthropic/claude-sonnet-4.6   | original_mc                               | 360 |         1 |                 0        |                             1         |                 0        |                 0        |                1.82347 |                 60528 |                      2556 |          63084 |
| google_frontier    | google/gemini-3.1-pro-preview | full_boundary_wrapper                     | 360 |         1 |                 0.95     |                             0.05      |                 0.95     |                 0.95     |                4.21512 |                 97657 |                     52616 |         150273 |
| google_frontier    | google/gemini-3.1-pro-preview | insufficient_channel_admissibility_rule   | 360 |         1 |                 0.755556 |                             0.241667  |                 0.755556 |                 0.755556 |                4.23123 |                 78938 |                     60132 |         139070 |
| google_frontier    | google/gemini-3.1-pro-preview | insufficient_channel_choices_not_evidence | 360 |         1 |                 0        |                             1         |                 0        |                 0.972222 |                4.06983 |                 86142 |                     49434 |         135576 |
| google_frontier    | google/gemini-3.1-pro-preview | insufficient_channel_only                 | 360 |         1 |                 0        |                             1         |                 0        |                 1        |                3.97872 |                 74623 |                     44132 |         118755 |
| google_frontier    | google/gemini-3.1-pro-preview | original_mc                               | 360 |         1 |                 0        |                             1         |                 0        |                 0.680556 |                4.24801 |                 56622 |                     62223 |         118845 |
| openai_frontier    | openai/gpt-5.1                | full_boundary_wrapper                     | 360 |         1 |                 1        |                             0         |                 1        |                 1        |                1.1222  |                 90906 |                      5760 |          96666 |
| openai_frontier    | openai/gpt-5.1                | insufficient_channel_admissibility_rule   | 360 |         1 |                 0.880556 |                             0.119444  |                 0.880556 |                 1        |                1.06773 |                 74396 |                      5620 |          80016 |
| openai_frontier    | openai/gpt-5.1                | insufficient_channel_choices_not_evidence | 360 |         1 |                 0        |                             1         |                 0        |                 1        |                1.06817 |                 78354 |                      4680 |          83034 |
| openai_frontier    | openai/gpt-5.1                | insufficient_channel_only                 | 360 |         1 |                 0        |                             1         |                 0        |                 1        |                1.03721 |                 67914 |                      4680 |          72594 |
| openai_frontier    | openai/gpt-5.1                | original_mc                               | 360 |         1 |                 0        |                             1         |                 0        |                 0        |                1.08715 |                 51354 |                      4908 |          56262 |

## Channel-control lift table

| model_family       | model_id                      | prompt_policy                             |   n |   admissibility_accuracy |   admissibility_lift_vs_original |   admissibility_lift_vs_channel_only |   answer_attempt_on_insufficient_rate |   answer_attempt_reduction_vs_original |   answer_attempt_reduction_vs_channel_only |
|:-------------------|:------------------------------|:------------------------------------------|----:|-------------------------:|---------------------------------:|-------------------------------------:|--------------------------------------:|---------------------------------------:|-------------------------------------------:|
| anthropic_frontier | anthropic/claude-sonnet-4.6   | full_boundary_wrapper                     | 360 |                 0.958333 |                         0.958333 |                             0.958333 |                             0.0416667 |                               0.958333 |                                   0.958333 |
| anthropic_frontier | anthropic/claude-sonnet-4.6   | insufficient_channel_admissibility_rule   | 360 |                 0.744444 |                         0.744444 |                             0.744444 |                             0.255556  |                               0.744444 |                                   0.744444 |
| anthropic_frontier | anthropic/claude-sonnet-4.6   | insufficient_channel_choices_not_evidence | 360 |                 0        |                         0        |                             0        |                             1         |                               0        |                                   0        |
| anthropic_frontier | anthropic/claude-sonnet-4.6   | insufficient_channel_only                 | 360 |                 0        |                         0        |                             0        |                             1         |                               0        |                                   0        |
| anthropic_frontier | anthropic/claude-sonnet-4.6   | original_mc                               | 360 |                 0        |                         0        |                             0        |                             1         |                               0        |                                   0        |
| google_frontier    | google/gemini-3.1-pro-preview | full_boundary_wrapper                     | 360 |                 0.95     |                         0.95     |                             0.95     |                             0.05      |                               0.95     |                                   0.95     |
| google_frontier    | google/gemini-3.1-pro-preview | insufficient_channel_admissibility_rule   | 360 |                 0.755556 |                         0.755556 |                             0.755556 |                             0.241667  |                               0.758333 |                                   0.758333 |
| google_frontier    | google/gemini-3.1-pro-preview | insufficient_channel_choices_not_evidence | 360 |                 0        |                         0        |                             0        |                             1         |                               0        |                                   0        |
| google_frontier    | google/gemini-3.1-pro-preview | insufficient_channel_only                 | 360 |                 0        |                         0        |                             0        |                             1         |                               0        |                                   0        |
| google_frontier    | google/gemini-3.1-pro-preview | original_mc                               | 360 |                 0        |                         0        |                             0        |                             1         |                               0        |                                   0        |
| openai_frontier    | openai/gpt-5.1                | full_boundary_wrapper                     | 360 |                 1        |                         1        |                             1        |                             0         |                               1        |                                   1        |
| openai_frontier    | openai/gpt-5.1                | insufficient_channel_admissibility_rule   | 360 |                 0.880556 |                         0.880556 |                             0.880556 |                             0.119444  |                               0.880556 |                                   0.880556 |
| openai_frontier    | openai/gpt-5.1                | insufficient_channel_choices_not_evidence | 360 |                 0        |                         0        |                             0        |                             1         |                               0        |                                   0        |
| openai_frontier    | openai/gpt-5.1                | insufficient_channel_only                 | 360 |                 0        |                         0        |                             0        |                             1         |                               0        |                                   0        |
| openai_frontier    | openai/gpt-5.1                | original_mc                               | 360 |                 0        |                         0        |                             0        |                             1         |                               0        |                                   0        |

## Interpretation guide

- If `insufficient_channel_only` performs poorly, merely adding an INSUFFICIENT output channel is not enough.
- If `insufficient_channel_choices_not_evidence` improves, answer-choice pressure is a causal contributor.
- If `insufficient_channel_admissibility_rule` improves further, admissibility semantics add value beyond the output channel.
- If `full_boundary_wrapper` remains strongest, explicit source-boundary representation adds value beyond output-channel availability.

## Files

- Raw outputs: `/content/drive/MyDrive/context_vs_control_outputs/final_cross_model_replication_fixed/openrouter_frontier_channel_control_ablation_v0_4/openrouter_frontier_channel_control_ablation_v0_4_20260509_055740/raw_outputs.jsonl`
- Scored outputs: `/content/drive/MyDrive/context_vs_control_outputs/final_cross_model_replication_fixed/openrouter_frontier_channel_control_ablation_v0_4/openrouter_frontier_channel_control_ablation_v0_4_20260509_055740/scored_outputs.csv`
- Failure examples: `/content/drive/MyDrive/context_vs_control_outputs/final_cross_model_replication_fixed/openrouter_frontier_channel_control_ablation_v0_4/openrouter_frontier_channel_control_ablation_v0_4_20260509_055740/failure_examples.csv`
- Manifest: `/content/drive/MyDrive/context_vs_control_outputs/final_cross_model_replication_fixed/openrouter_frontier_channel_control_ablation_v0_4/openrouter_frontier_channel_control_ablation_v0_4_20260509_055740/run_manifest.json`