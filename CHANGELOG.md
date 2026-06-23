# Changelog

All notable changes to the Corpus starter kit are recorded here. The format follows
[Keep a Changelog](https://keepachangelog.com/en/1.1.0/), and the kit is versioned with
[semantic versioning](https://semver.org/spec/v2.0.0.html): a **major** bump means a copy-whole
adopter would have to reconcile a breaking layout or format change, **minor** adds files or
guidance you can re-copy safely, **patch** is a fix or wording change.

You adopted this kit by copying it whole, so there is no automatic upgrade — watch the
[releases](https://github.com/jcosta33/swarm-starter-kit/releases) and re-copy the parts you have
not customized (see `docs/ADOPTING.md` → *Upgrading* in the Corpus repo).

## [Unreleased]

### Added
- `.gitignore.additions` — ignore `*.swarm-bak` backups left by `swarm update --write` (swarm-cli),
  so they are not committed or flagged as out-of-scope changes by `swarm review`.

## [1.3.0] - 2026-06-22

### Added
- `LICENSE` — MIT, matching the rest of the family.
- `templates/review.md` — an optional `## Open decisions` section for routing a decision to the
  reviewer ([Corpus ADR-0089](https://github.com/jcosta33/swarm/blob/main/docs/adrs/0089-decision-handoff-open-decisions.md)).
- `templates/change-plan.md` — a prompt under **Affected surfaces** to enumerate *callers* (the
  inventory's `Current interfaces → Callers` column), not only edit sites, when the surface is a
  shared signature or interface (single-sourced from the Corpus change-plan docs).
- `.gitignore.additions` — ignore `.worktrees/` and reinforce the co-located-workspace ignores.

### Changed
- `.agents/skills/adversarial-review/SKILL.md` — a Rule-0 load directive (a point-of-need 1-hop
  link) so the bundled `references/task-template.md` is actually loaded, not merely listed.
- `templates/task.md` — document the Do-not-change paths as a hard wall.
- `hooks/pre-commit` — narrower gate scope (excludes scaffold READMEs); still fail-open when
  swarm-cli is absent.
- `advanced/` — point at the [swarm-agents](https://github.com/jcosta33/swarm-agents) catalog as
  the single source for agent definitions and remove the in-kit probe; `advanced/checks-reference.md`
  now carries the full change-plan (C010/C011) and task (C012–C015) check tables, and
  `advanced/sol-reference.md` + the `review-output`/`spec-check` guides reword "future CLI" → the
  shipped [`swarm check`](https://github.com/jcosta33/swarm-cli).

## [1.2.0] - 2026-06-18

### Added
- `templates/review.md` — the optional structured-evidence `verify` block convention beside the
  coverage table: a fenced block whose info-string (`verify id=AC-NNN cmd="…" result=pass|fail`) is
  the machine-checkable form [`swarm check` / `swarm review`](https://github.com/jcosta33/swarm-cli)
  reconciles against the spec's named command (core check **C013**, [Corpus ADR-0083](https://github.com/jcosta33/swarm/blob/main/docs/adrs/0083-verify-evidence-reconcile.md)).
  Opt-in — a row may still use only the free-form Evidence cell; the check surfaces a consistency
  fact (the recorded evidence names the requirement's own command and a pass), never a review result.

## [1.1.0] - 2026-06-15

### Added
- `hooks/` — gate templates that run [`swarm check`](https://github.com/jcosta33/swarm-cli):
  a **fail-open** `pre-commit` hook (skips when swarm-cli is not installed, so it never blocks a
  teammate) and an **authoritative** `swarm-check.yml` GitHub Actions workflow (gates the merge).
  Exit `2` blocks, `1` warns, `0` passes. See `hooks/README.md`.
- A "wire the gate" step in the README and a `hooks/` entry in *What you copied*.
- This CHANGELOG.

## [1.0.0] - 2026-06-13

### Added
- The copy-whole workspace baseline ([Corpus ADR-0075](https://github.com/jcosta33/swarm/blob/main/docs/adrs/0075-starter-kit-template-repo.md)):
  `AGENTS.md` bootloader (with `CLAUDE.md` / `GEMINI.md` symlinks); the core loop guides and the
  workspace authoring guides under `.agents/skills/`; the eight core artifact templates under
  `templates/`; the flow folders (`specs/ intake/ tasks/ reviews/ findings/ inventory/
  change-plans/`); `decisions/` seeded with `0001-adopt-swarm`; the hand-edited `status.md` board;
  one worked `examples/` chain; the optional `advanced/` templates and reference cards;
  `.gitignore.additions` for governed code repos.

Tagged releases live at
<https://github.com/jcosta33/swarm-starter-kit/releases> (tagging starts at v1.3.0; the earlier
versions above are documented here but were never tagged).
