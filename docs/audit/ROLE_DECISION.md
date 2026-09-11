# Role Decision — `phenotype-unsloth-studio`

Decision status: **accepted** (operator ratified 2026-09-11; register entry remains `provisional` until next register sync)
Discipline: single-repo forensic completion (Phase C.3)
Date: 2026-09-10 (ratified 2026-09-11)

## Decision

Adopt the disposition register's recommended role:

> **Role**: `upstream_reference` — a downstream reference fork of `unslothai/unsloth` carrying only deliberate, narrow rebrand changes. Maintain a pinned upstream reference, a documented delta inventory, and do not let the fork acquire a shadow product identity.

**Target upstream**: `unslothai/unsloth` (`upstream/main`).
**First-task (per register)**: *Add exact upstream pin and delta inventory; maintain only deliberate local changes, not a shadow product identity.*

## Rationale

The baseline (see `BASELINE.md`) and competing hypotheses (see `HYPOTHESES.md`) converge on H1:

- The fork has exactly 1 commit of local divergence from its fork-point (`44bcd491d`, README badge lines).
- The package identity (`pyproject.toml [project].name = "unsloth"`) is identical to upstream.
- No second package namespace, no local-only module, no wrapper code.
- The fork is 1494 commits behind `upstream/main` and has zero CI runs of its own.

This is exactly the situation the register's `upstream_reference` decision is designed for: a fork that should remain a *reference*, not a divergence. The 1494-commit drift is not "local work" — it is *absent* local work plus accumulated upstream advance.

## Evidence tier

`E1-root-docs` for the repo itself. `E2` for the upstream identity (well-known public package). `E3` for downstream consumers: not yet searched across the phenotype portfolio — required before final acceptance.

## Boundaries

- **In scope (post-acceptance)**:
  - Add `UPSTREAM_PIN` and `DELTA.md` documenting the 2-line badge rebrand.
  - Decide whether the fork's purpose is *display only* (archive) or *active mirror* (sync strategy).
- **Out of scope**:
  - Cherry-picking upstream features into a forked identity.
  - Renaming the package.
  - Building local kernels.
  - Running a separate release channel.
- **Reversibility**: full — archive (read-only) and active mirror are both reachable.

## Required follow-up evidence (E3, before acceptance) — DONE

Searched the phenotype slice on 2026-09-10 for `phenotype-unsloth-studio|KooshaPari/phenotype-unsloth-studio|unsloth_studio`. **Zero hits** in any code, `Cargo.toml`, `pyproject.toml`, `package.json`, or `.github/workflows/uses:` form. Hits only in operator-managed process docs (`state.md`, `chat2-*.md`, `audit-evidence/*.json`, `tgt/state/*.json`, `research/audit-system/...`).

H1 is fully supported. Decision can move from `proposed` to `accepted` pending operator ratification.

## Mutation footprint for Phase H

| Action | File(s) | Reversible? |
|---|---|---|
| Write `UPSTREAM_PIN.md` (new) | new file | yes |
| Write `DELTA.md` listing the 2-line badge change | new file | yes |
| Update `docs/audit/` baseline/hypothesis/role/plan docs (already done) | docs/audit/*.md | yes |
| Archive repo (set GitHub repo to `isArchived: true`) | GitHub UI only | yes |
| Delete local clone | shell | yes |

No source tree mutations until owner accepts the role decision.

## Open questions for operator

1. Archive (`isArchived`) or active mirror (sync script + cron)?
2. Keep the 2-line README rebrand, or revert README to upstream verbatim and drop the fork?
3. Search the portfolio slice for `phenotype-unsloth-studio` references before finalising.
