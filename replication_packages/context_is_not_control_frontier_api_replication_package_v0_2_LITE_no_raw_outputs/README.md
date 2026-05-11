# Context Is Not Control — Frontier/API Replication Package v0.2

Created: 2026-05-11T15:23:37.924270+00:00

This package contains the cleaned frontier/API-model artifacts for the manuscript section on source-boundary failures in LLM evidence use.

It is a cleaned derivative package. It does not include messy exploratory Colab notebooks, API keys, hidden credentials, or private runtime state.

## Scope

This package covers the API-requested frontier model tests only.

Primary tested frontier models:

- `openai/gpt-5.1`
- `anthropic/claude-sonnet-4.6`
- `google/gemini-3.1-pro-preview`

## Core claim supported by these artifacts

The frontier/API tests examine whether explicit source-boundary representations reduce unsupported answer attempts when context contains non-admissible or control-like text.

The runs also test major alternative explanations:

1. The model merely lacked an `INSUFFICIENT` output channel.
2. The intervention merely caused blanket refusal.
3. The intervention only worked by directly handing the model the abstention decision.

## Contents

- `data/` — canonical attack rows CSV used to derive frontier subsets.
- `runs/` — cleaned run-specific artifacts for each canonical frontier run.
- `tables/` — location for regenerated aggregate tables.
- `scripts/` — no-API helper script for regenerating summary tables from packaged scored outputs.
- `RUN_INVENTORY.csv` — inventory of canonical run directories included or checked.
- `FILE_MANIFEST.csv` — file-level manifest with package-relative paths and SHA-256 hashes.
- `SHA256SUMS.txt` — checksum list for verification.

## Canonical frontier runs

- `sentinel_v0_1` — Initial small frontier sentinel run; exploratory bridge from open-model tests to frontier/API endpoints.
- `answer_pressure_ablation_v0_1` — Initial frontier answer-pressure ablation across prompt policies.
- `answer_pressure_replication_v0_2` — Scaled frontier answer-pressure replication across 120 base trials and three frontier/API models.
- `boundary_component_ablation_v0_3` — Unsupported-row boundary-component ablation testing which source-boundary components reduce answer attempts.
- `channel_control_ablation_v0_4` — Channel-control ablation testing whether an INSUFFICIENT output channel alone fixes the failure.
- `supported_preservation_v0_1` — Supported-row preservation test ruling out blanket refusal under boundary prompting.
- `metadata_only_status_ablation_v0_1` — Metadata-only / not-handed-status ablation testing whether models can infer inadmissibility without explicit selected-status handoff.

## Reproducing aggregate tables

From the package root:

```bash
python scripts/reproduce_frontier_summary_tables.py
```

This script does not call OpenRouter or any external model API. It only reads packaged CSV outputs.

## API keys

No API keys are included. Original OpenRouter credentials were stored separately in Colab Secrets and are not part of this package.

## Raw outputs

If present, `raw_outputs.jsonl` files contain raw model responses from OpenRouter calls. The lite ZIP excludes these raw-output files.

## Notes on notebooks

The original exploratory Colab notebooks were working lab notebooks. They are not included here. This package preserves the cleaned inputs, prompts, raw outputs, scored outputs, audits, summaries, and manifests needed to inspect the frontier/API results.

## Status

This is a replication/audit package for a working manuscript / public preprint draft. It is not a polished software library.
