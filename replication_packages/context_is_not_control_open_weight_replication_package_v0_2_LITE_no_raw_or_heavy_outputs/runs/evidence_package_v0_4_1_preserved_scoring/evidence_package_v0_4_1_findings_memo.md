# Evidence Package v0.4.1 Findings Memo

Generated output directory: `/content/drive/MyDrive/context_vs_control_outputs/final_cross_model_replication_fixed/evidence_package_v0_4_1_preserved_scoring`

## Purpose

v0.4.1 repairs the v0.4 scoring pass by preserving each original per-model run's parsed `final_prediction` and `parse_ok` values where available. This avoids penalizing reasoning-style outputs, especially DeepSeek-style outputs, with a stricter common parser that was not used during the original model runs.

## Included models

- DeepSeek-R1-Distill-Qwen-32B
- Gemma-2-27B-it
- Mistral-Nemo-12B
- Mistral-Small-24B
- Qwen2.5-14B
- Qwen2.5-32B
- Qwen2.5-7B

## Main empirical pattern

Across seven completed model runs spanning Qwen, Mistral, Gemma, and DeepSeek-derived architectures, source rendering materially changes benchmark behavior. Sanitized rendering usually reduces supported source-injection failure while preserving or improving supported answer accuracy. Fact-only rendering acts as an oracle-style upper bound and typically eliminates unsupported hallucination in this benchmark.

## Raw to sanitized deltas

- **DeepSeek-R1-Distill-Qwen-32B / direct_answer**: final accuracy 0.6970 → 0.8015 (+0.1045); injection failure 0.0625 → 0.0000 (-0.0625); unsupported hallucination 0.5139 → 0.3639 (-0.1500).
- **DeepSeek-R1-Distill-Qwen-32B / quarantined_answer**: final accuracy 0.7167 → 0.8136 (+0.0969); injection failure 0.0958 → 0.0042 (-0.0916); unsupported hallucination 0.4556 → 0.3389 (-0.1167).
- **Gemma-2-27B-it / direct_answer**: final accuracy 0.6682 → 0.8061 (+0.1379); injection failure 0.3083 → 0.0667 (-0.2416); unsupported hallucination 0.3972 → 0.3056 (-0.0916).
- **Gemma-2-27B-it / quarantined_answer**: final accuracy 0.7000 → 0.7682 (+0.0682); injection failure 0.2167 → 0.0292 (-0.1875); unsupported hallucination 0.4028 → 0.4028 (+0.0000).
- **Mistral-Nemo-12B / direct_answer**: final accuracy 0.5515 → 0.8773 (+0.3258); injection failure 0.5125 → 0.0208 (-0.4917); unsupported hallucination 0.4722 → 0.2083 (-0.2639).
- **Mistral-Nemo-12B / quarantined_answer**: final accuracy 0.3727 → 0.6364 (+0.2637); injection failure 0.4250 → 0.0000 (-0.4250); unsupported hallucination 0.6833 → 0.2833 (-0.4000).
- **Mistral-Small-24B / direct_answer**: final accuracy 0.9212 → 0.8758 (-0.0454); injection failure 0.0000 → 0.0000 (+0.0000); unsupported hallucination 0.1444 → 0.2278 (+0.0834).
- **Mistral-Small-24B / quarantined_answer**: final accuracy 0.9879 → 0.9530 (-0.0349); injection failure 0.0000 → 0.0000 (+0.0000); unsupported hallucination 0.0222 → 0.0861 (+0.0639).
- **Qwen2.5-14B / direct_answer**: final accuracy 0.8924 → 0.9879 (+0.0955); injection failure 0.2667 → 0.0000 (-0.2667); unsupported hallucination 0.0194 → 0.0222 (+0.0028).
- **Qwen2.5-14B / quarantined_answer**: final accuracy 0.9303 → 0.9652 (+0.0349); injection failure 0.1625 → 0.0000 (-0.1625); unsupported hallucination 0.0194 → 0.0639 (+0.0445).
- **Qwen2.5-32B / direct_answer**: final accuracy 0.8136 → 0.9061 (+0.0925); injection failure 0.2458 → 0.0000 (-0.2458); unsupported hallucination 0.1778 → 0.1722 (-0.0056).
- **Qwen2.5-32B / quarantined_answer**: final accuracy 0.8697 → 0.9121 (+0.0424); injection failure 0.2583 → 0.0000 (-0.2583); unsupported hallucination 0.0667 → 0.1611 (+0.0944).
- **Qwen2.5-7B / direct_answer**: final accuracy 0.6818 → 0.7894 (+0.1076); injection failure 0.2500 → 0.0833 (-0.1667); unsupported hallucination 0.4056 → 0.3194 (-0.0862).
- **Qwen2.5-7B / quarantined_answer**: final accuracy 0.6121 → 0.7697 (+0.1576); injection failure 0.1708 → 0.0667 (-0.1041); unsupported hallucination 0.5861 → 0.3667 (-0.2194).

## Caveats

- This remains a controlled, synthetic, forced-choice benchmark.
- Fact-only rendering is an oracle-style upper bound, not a complete production RAG design.
- Sanitization is the deployable intervention of interest, but it does not monotonically reduce every failure mode in every model.
- Non-monotonic cases support separating trace exclusion, evidence compression, and abstention calibration.

## Files

- Combined preserved-scoring results: `/content/drive/MyDrive/context_vs_control_outputs/final_cross_model_replication_fixed/evidence_package_v0_4_1_preserved_scoring/combined_all_models_results_preserved_scoring.csv`
- Master table: `/content/drive/MyDrive/context_vs_control_outputs/final_cross_model_replication_fixed/evidence_package_v0_4_1_preserved_scoring/paper_ready_master_results_table_all_models_v0_4_1.csv`
- Headline deltas: `/content/drive/MyDrive/context_vs_control_outputs/final_cross_model_replication_fixed/evidence_package_v0_4_1_preserved_scoring/paper_ready_headline_deltas_all_models_v0_4_1.csv`
- Wilson CIs: `/content/drive/MyDrive/context_vs_control_outputs/final_cross_model_replication_fixed/evidence_package_v0_4_1_preserved_scoring/wilson_95ci_by_condition_all_models_v0_4_1.csv`
- Paired McNemar tests: `/content/drive/MyDrive/context_vs_control_outputs/final_cross_model_replication_fixed/evidence_package_v0_4_1_preserved_scoring/paired_mcnemar_tests_holm_all_models_v0_4_1.csv`
- Figures directory: `/content/drive/MyDrive/context_vs_control_outputs/final_cross_model_replication_fixed/evidence_package_v0_4_1_preserved_scoring/figures`
- Parser audit: `/content/drive/MyDrive/context_vs_control_outputs/final_cross_model_replication_fixed/evidence_package_v0_4_1_preserved_scoring/parser_audit_v04_common_vs_preserved.csv`
- Parser row differences: `/content/drive/MyDrive/context_vs_control_outputs/final_cross_model_replication_fixed/evidence_package_v0_4_1_preserved_scoring/parser_audit_row_differences.csv`