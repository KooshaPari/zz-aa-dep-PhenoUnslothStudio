# Action Plan — `phenotype-unsloth-studio`

Phase H of the single-repo forensic-completion protocol. Concrete next steps, all reversible, none executed without explicit operator approval.

## Pre-flight (already complete)

- [x] Cloned `KooshaPari/phenotype-unsloth-studio` to `~/wt-phenotype-unsloth-studio-20260910`.
- [x] Verified `origin/main = upstream/main + 1 commit`; merge-base `6fd4e9a2a`.
- [x] Confirmed working tree clean and no untracked files.
- [x] Captured baseline, hypotheses, and role decision in `docs/audit/`.

## Step 1 — Pin upstream SHA (new file, no source mutation)

Create `UPSTREAM_PIN.md` at repo root with:

```markdown
# Upstream pin

This fork pins upstream at the merge-base from which it was branched.

- Upstream: `https://github.com/unslothai/unsloth`
- Upstream `main` tip at branch: <SHA captured at fork>
- Merge-base (fork-point): `6fd4e9a2af36653b25aa9456e836e6ba0b56a6fc`
- Local ahead of merge-base: 1 commit (`44bcd491d` — README badges)
- Upstream ahead of fork: 1494 commits (as of 2026-09-10)

To resync, run from a clone with the `upstream` remote:

```bash
git fetch upstream
git merge --ff-only 6fd4e9a2a  # or use a release tag if available
```

## Step 2 — Document the delta (new file, no source mutation)

Create `DELTA.md` listing every deliberate local change. Today that is:

```text
44bcd491d docs(readme): add AI slop inside + downloads badges
  README.md | 2 ++
  - adds "AI slop inside" badge
  - adds "GitHub Downloads" badge pointed at KooshaPari/phenotype-unsloth-studio
```

Both badges point at the fork (intentional rebrand). All other files at `origin/main` are inherited verbatim from upstream's `6fd4e9a2a`-era state.

## Step 3 — Consumer search (E3 evidence) — DONE

Searched the retained slice on 2026-09-10:

```bash
rg -l 'phenotype-unsloth-studio|KooshaPari/phenotype-unsloth-studio|unsloth_studio' \
  /Users/kooshapari/CodeProjects/Phenotype/repos \
  --glob '!node_modules' --glob '!.git' --glob '!target'
```

Result: zero hits in any code, `Cargo.toml`, `pyproject.toml`, `package.json`, or `.github/workflows/uses:` form. Hits only in operator-managed process docs (`state.md`, `chat2-*.md`, `audit-evidence/*.json`, `tgt/state/*.json`, `research/audit-system/...`).

H1 is fully supported — the fork has no code-level consumer; it is a display artifact.

## Step 4 — Choose terminal disposition (operator decision required)

Two options, both reversible:

| Option | Action | Cost | Reversibility |
|---|---|---|---|
| **A. Archive** | `gh repo edit KooshaPari/phenotype-unsloth-studio --enable-archive` | none | yes (un-archive) |
| **B. Active mirror** | add `sync.yml` workflow: `git fetch upstream && git push origin <pinned>` weekly | small ongoing CI cost | yes (delete workflow) |

The disposition register's `upstream_reference` decision is consistent with **A** if the operator treats the fork purely as a display artifact, or **B** if the operator wants fresh badges / download counts.

## Step 5 — Audit log + handoff

Append a provenance line to `~/.forge/audit/2026-09-10-batch-phenotype-studio-actions-utils.log` summarising what was decided and what is awaiting owner action.

## Blockers / risks

- **Risk**: a future contributor treats this fork as a shadow product and adds Studio-specific code. Mitigated by `DELTA.md` + `ROLE_DECISION.md` being visible at repo root.
- **Risk**: upstream renames the package or shifts to a different distribution model. Mitigated by an explicit `UPSTREAM_PIN.md` and the archive-vs-mirror decision logged.

## What this plan does NOT do

- Does not modify `pyproject.toml`, source code, or any non-audit file.
- Does not push, force-push, open PRs, or merge.
- Does not delete the local clone or the remote repo.
- Does not introduce any CI workflow.
