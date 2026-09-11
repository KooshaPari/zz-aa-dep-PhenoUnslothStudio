# Hypotheses — `phenotype-unsloth-studio`

Roster of competing hypotheses about the role and intended disposition of this repo. Each is scored against the baseline evidence. Winner is promoted to `ROLE_DECISION.md`.

## H1 — Reference fork of upstream `unsloth` (no product identity)

**Claim**: this repo exists only to mirror `unslothai/unsloth` with a `KooshaPari`-branded README so that `KooshaPari/phenotype-unsloth-studio` shows the AI-slop badge and downloads counter. Local code state should match upstream modulo a small rebrand.

**Evidence for**:
- Package name is `unsloth` (same as upstream) — no shadow product.
- Only 1 local commit on `main` ahead of fork-point.
- That commit adds 2 README badge lines and nothing else.
- Working tree clean, no untracked files, no local-only source.

**Evidence against**:
- 1494-commit upstream drift — fork is far behind.
- README diff at `origin/main` vs `upstream/main` is dramatic; fork's README header promotes "Studio" instead of upstream's "first desktop app" framing.
- Some `pyproject.toml` deltas (setuptools bump, `huggingface-hub>=0.34.0`, dropped `_changelog_build.build_py`) suggest the fork was created from an upstream snapshot a bit older than the merge-base.

**Score**: high — register's `upstream_reference` tag fits this hypothesis verbatim.

## H2 — Independent product ("phenotype-unsloth-studio") that wraps upstream

**Claim**: this repo is its own product; it depends on upstream `unsloth` at runtime but has its own value (Studio UI bundle, branding, downloads).

**Evidence for**:
- Repo name embeds "phenotype" — non-trivial identity signal.
- README devotes a section to "Unsloth Studio (web UI)" with multi-platform install table.
- The `_changelog_build.build_py` cmdclass keeps `CHANGELOG.md` shipped with the Studio package data.

**Evidence against**:
- `pyproject.toml` `name = "unsloth"` — same package name as upstream.
- No second `phenotype_unsloth_studio` package or importable namespace.
- Only 2 lines of structural code change vs fork-point; no wrapper module.
- The 1494-commit drift isn't evidence of independent work — it's evidence of upstream outpacing the fork.

**Score**: low — fits the register's "shadow product identity" anti-pattern, not its intended pattern.

## H3 — Offline mirror / cached snapshot

**Claim**: the fork exists so users without internet access to `github.com/unslothai/unsloth` can fetch from `KooshaPari`.

**Evidence for**:
- GitHub Releases badge counts downloads against the fork's URL.
- `install.sh` / `install.ps1` in repo are upstream's (no fork-specific install logic).

**Evidence against**:
- README still points downloads at upstream's release page (the `latest/download/...` URLs in upstream's README remain).
- No offline-cache directory; no docs page advertising offline usage.
- Studio-only emphasis would not need a full fork.

**Score**: very low.

## H4 — Hold / abandon

**Claim**: this repo was created as an experiment and is no longer intended to be active.

**Evidence for**:
- No CI runs at all.
- No open or merged PRs.
- Single author (KooshaPari), single commit on top of fork-point.
- 1494 commits of upstream drift unintegrated.

**Evidence against**:
- The fork is public, so abandonment is non-zero cost.
- It shows up in the retained slice — operator has not yet archived it.

**Score**: medium as a *terminal* option if H1 is rejected.

## Winning hypothesis: **H1 (reference fork)**

Register's `upstream_reference` decision matches H1 exactly. Action: pin to a known upstream SHA, document the deliberate rebrand delta in `REBRAND_DELTA.md`, archive the local clone as read-only, and update the README to point downloads at upstream unless the operator wants the fork-distributed counts.
