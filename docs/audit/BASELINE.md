# Baseline — `phenotype-unsloth-studio`

Captured: 2026-09-10
Source repo: `KooshaPari/phenotype-unsloth-studio`
Upstream: `unslothai/unsloth`
Local clone: `~/wt-phenotype-unsloth-studio-20260910`
Branch: `main` = `origin/main` HEAD `44bcd491dc6595a5575483572dc642c0faeb2130`

## Repository identity

| Field | Value |
|---|---|
| Package name (`pyproject.toml`) | `unsloth` |
| Distribution channel | `unsloth-cli` / `unsloth-cli` console_script + `unsloth_cli:app` |
| License | Apache-2.0 |
| `requires-python` | `>=3.9,<3.15` |
| Description | `2-5X faster training, reinforcement learning & finetuning` |
| Mainline (PyPI) | `unsloth` on `https://unsloth.ai/install.sh` |
| Repo fork point | `6fd4e9a2af36653b25aa9456e836e6ba0b56a6fc` (`Studio: surface an MLX completion-masking miss as a warning, not a status line #8133`) |

## Working tree

- Clean (no untracked, no unstaged, no staged).
- `git status --porcelain` empty.
- No submodules.

## Branch and remote state

| Ref | State |
|---|---|
| `origin/main` HEAD | `44bcd491dc6595a5575483572dc642c0faeb2130` |
| `upstream/main` HEAD | diverged (1494 commits ahead of origin at capture) |
| Merge-base | `6fd4e9a2af36653b25aa9456e836e6ba0b56a6fc` (2026-08-08) |
| Local `main` ahead of merge-base | **1 commit** (`44bcd491d`) |
| `origin/main` ahead of `upstream/main` | **1 commit** (`44bcd491d`) |
| `upstream/main` ahead of `origin/main` | **1494 commits** |
| Branches | `main` only locally; `upstream` exposes dozens of feature/agent/ci branches |
| Tags | upstream-tagged; none added locally |
| Open PRs (GitHub) | none |
| Recent workflow runs | none |

## Provenance — local changes vs upstream

Only one commit is unique to `origin/main`:

```text
44bcd491d docs(readme): add AI slop inside + downloads badges
Author: Koosha Paridehpour, 2026-08-31T21:17:04-07:00
```

Stat against its parent (`6fd4e9a2a`):

```text
README.md | 2 ++
1 file changed, 2 insertions(+)
```

Two badge lines added under "Get started":

```markdown
[![AI slop inside](https://sladge.net/badge.svg)](https://sladge.net)
[![GitHub Downloads (all assets, all releases)](https://img.shields.io/github/downloads/KooshaPari/phenotype-unsloth-studio/total)](https://github.com/KooshaPari/phenotype-unsloth-studio/releases)
```

These reference the **fork** download counter (`KooshaPari/phenotype-unsloth-studio`), not upstream — confirming intentional rebrand target.

## Tree inventory (top level)

| Path | Role |
|---|---|
| `unsloth/` | Upstream Python package (kernels, models, registry, save, trainer) |
| `unsloth_cli/` | CLI sub-package and tests |
| `tests/` | Large pytest suite (studio, fast_inference, notebooks, python, qlora, saving, security, sh, version_compat, vllm_compat, utils) |
| `scripts/` | Lockfile audit, build, lint, install helpers |
| `docker/` | Dockerfile, Dockerfile.studio, jupyter branding assets, install scripts |
| `.github/workflows/` | ~60 workflows: cache-janitor, clean-machine-*, kaggle-*, lint-ci, mlx-ci, notebooks-ci, ossf, security-audit, studio-*-ci, version-compat-ci, wheel-smoke |
| `.github/actions/` | 7 local composite actions (frontend-dist-*, pip-cache-*, uv-cache-*, install-unsloth-local) |
| `.github/ci-preempt.json` | Local CI policy |
| `pyproject.toml`, `.pre-commit-config.yaml`, `.pre-commit-ci.yaml` | Build + lint config |
| `README.md`, `CHANGELOG.md`, `MANIFEST.in` | Docs |
| `install.sh`, `install.ps1`, `build.sh`, `cli.py`, `unsloth-cli.py` | Install + CLI entry |

## Build / lint tooling

- `pyproject.toml` (`setuptools==82.0.1` vs upstream `80.9.0`) — local is newer.
- `setuptools-scm` reads `unsloth._version.__version__` (vs upstream legacy `unsloth.models._utils.__version__`).
- `setuptools.cmdclass.build_py = "_changelog_build.build_py"` removed in upstream tip (still in fork).
- Added dependency: `huggingface-hub>=0.34.0`.

## Drift summary

The 1494-commit drift is concentrated in:

- `unsloth/kernels/` — MoE grouped GEMM, FP8, autotuning cache.
- `unsloth/models/` — Granite, GLM-4 MoE, Gemma 4, Llama 4, Qwen 2/3/MoE, diffusion, sentence-transformer, vision.
- `unsloth/optimizers/` — q-GaLore projector / AdamW.
- `unsloth/dataprep/` — synthetic configs, raw_text, synthetic.
- `unsloth/utils/attention_dispatch.py`, `prefix_grouper*.py`, `packing.py`.
- `unsloth_cli/` — `claude_subagent_mcp.py`, `codex_subagent_mcp.py`, `commands/{chat,export,inference,start,studio,train}.py`, tests for studio run / refresh shortcuts / runtime gate powershell.
- `tests/utils/` — many new compat probes (attention_dispatch, attn_mask, packing, rope_scaling_drift, q_galore, qat, xformers_capability_gate).
- `scripts/` — many probes (compare_engines, fp8_overflow_check, nvfp4_probe, prequant_probe, sdpa_mask_backend_probe, etc.).
- `.github/workflows/` — many studio CI workflows and `lint-ci.yml`, `startup-profile-ci.yml`, `consolidated-tests-ci.yml`.

The fork has none of these — its `tests/` and `scripts/` directories look like upstream's pre-2026-08 state.

## Cross-repo references found in this repo

- `unsloth_cli/codex_subagent_mcp.py` — Codex subagent integration.
- `unsloth_cli/claude_subagent_mcp.py` — Claude subagent integration.
- `unsloth_cli/codex_fallback_prompt.md` — Codex prompt fallback.
- `unsloth_cli/pi_subagent.ts` — Pi subagent (TS).
- `docker/unsloth_studio_update.sh`, `docker/studio_*.sh` — Studio entry scripts.

## E3 — consumer search across portfolio (2026-09-10)

`rg -l 'phenotype-unsloth-studio|KooshaPari/phenotype-unsloth-studio|unsloth_studio'` returned hits only in:

- `audit-evidence/account-scrape-2026-09-09/all-repos.json` — repo census metadata.
- `chat2-remote-ref-census.md`, `chat2-repo.md`, `state.md` — operator-managed process docs.
- `phenotype-registry/ecosystem-consolidation/pheno-master-audit.md` — portfolio inventory.
- `tgt/state/full_process_inventory_*.json` — operator process snapshots.
- `research/audit-system/structured-stores/forge/audit/badge-campaign-2026-08-31.md` — operator's own campaign notes.

**Zero hits** in any code, Cargo.toml, pyproject.toml, package.json, or `.github/workflows/uses:` form. The fork has no code-level downstream consumer in the portfolio — confirming H1 (reference fork, no shadow product).

## Evidence tier

`E3-root-docs`. Inspected: README, CHANGELOG, pyproject.toml, MANIFEST.in, .github/, pyproject, consumer search across the portfolio. Not yet independently verified: actual build/run, full kernels/ diff vs upstream, runtime behavior.

## Open questions for owner

1. Is the fork intended as a `KooshaPari`-branded re-distribution of upstream `unsloth` for Studio focus?
2. Should the fork sync from upstream before any new local change?
3. Are the `_changelog_build.build_py` cmdclass and the `huggingface-hub>=0.34.0` dep intentional retention of an older fork state, or accidental staleness?
