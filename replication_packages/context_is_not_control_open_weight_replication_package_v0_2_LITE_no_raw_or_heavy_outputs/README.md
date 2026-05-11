# Context Is Not Control — Open-Weight Replication Package v0.2

Created: 2026-05-11T15:43:15.014521+00:00

This package contains the cleaned open-weight model artifacts for the manuscript on source-boundary failures in LLM evidence use.

It is a cleaned derivative package. It does not include messy exploratory Colab notebooks, API keys, hidden credentials, or private runtime state.

## Scope

This package covers the open-weight / local-or-notebook model experiments, including the canonical multiple-choice replication package and the open-ended generation ablations.

Primary open-weight models represented in the canonical v0.4.1 evidence package include:

- Qwen2.5-7B
- Qwen2.5-14B
- Qwen2.5-32B
- Mistral-Small-24B
- Mistral-Nemo-12B
- DeepSeek-R1-Distill-Qwen-32B
- Gemma-2-27B-it

## Core role in the paper

The open-weight experiments establish the main empirical lineage: raw source renderings produce source-control failures; sanitized and fact-only renderings generally improve reliability; open-ended generation tests show the phenomenon is not merely a multiple-choice artifact; and wording/boundary-wrapper ablations show that explicit source-boundary representation matters.

The frontier/API package should be treated as the companion package that validates and isolates the mechanism across API-requested frontier models.

## Contents

- `data/` — canonical attack rows CSV.
- `top_level_artifacts/` — top-level open-weight result CSVs and plots from the project root.
- `runs/` — cleaned canonical open-weight evidence directories.
- `tables/` — location for regenerated inventory tables.
- `scripts/` — no-API helper script for scanning packaged summary/result tables.
- `RUN_INVENTORY.csv` — inventory of canonical open-weight directories included or checked.
- `TOP_LEVEL_FILE_INVENTORY.csv` — inventory of copied top-level open-weight files.
- `FILE_MANIFEST.csv` — file-level manifest with package-relative paths and SHA-256 hashes.
- `SHA256SUMS.txt` — checksum list for verification.

## Canonical open-weight directories

- `evidence_package_v0_4_1_preserved_scoring` — Canonical seven-model multiple-choice cross-model evidence package preserving original scoring.
- `open_ended_generation_v0_1` — Initial open-ended generation test; establishes transition beyond multiple choice.
- `open_ended_generation_v0_2_role_aware_fact_only` — Role-aware fact-only open-ended test; documents early over-refusal behavior.
- `open_ended_generation_v0_3_cross_model_package` — Canonical open-ended cross-model package using naturalized fact-only rendering.
- `open_ended_generation_v0_3_naturalized_fact_only` — Naturalized fact-only open-ended generation artifacts.
- `open_ended_generation_v0_4_qwen_wording_ablation` — Qwen wording ablation testing whether failures depend on boundary wording.
- `open_ended_generation_v0_5_boundary_wrapper_ablation` — Qwen boundary-wrapper ablation isolating source-boundary components.
- `open_ended_generation_v0_5_boundary_wrapper_ablation_mistral_nemo` — Mistral-Nemo boundary-wrapper follow-up artifacts, copied if present.
- `source_attribution_fidelity_v0_1` — Supplementary source-attribution fidelity artifacts, copied if present.

## Reproducing inventory tables

From the package root:

```bash
python scripts/reproduce_open_weight_summary_inventory.py
```

This script does not call model APIs. It scans the packaged CSV files and regenerates a compact inventory of available summary/result tables.

## Notes on notebooks

The original exploratory Colab notebooks were working lab notebooks and are not included here. This package preserves the cleaned inputs, outputs, summaries, figures, audits, and evidence directories needed to inspect the open-weight results.

## Status

This is a replication/audit package for a working manuscript / public preprint draft. It is not a polished software library.
