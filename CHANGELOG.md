# Changelog

All notable changes to the Suspec starter kit are recorded here. The format follows
[Keep a Changelog](https://keepachangelog.com/en/1.1.0/), and the kit is versioned with
[semantic versioning](https://semver.org/spec/v2.0.0.html): a **major** bump means a copy-whole
adopter would have to reconcile a breaking layout or format change, **minor** adds files or
guidance you can re-copy safely, **patch** is a fix or wording change.

You adopted this kit by copying it whole, so there is no automatic upgrade — watch the
[releases](https://github.com/jcosta33/suspec-starter-kit/releases) and re-copy the parts you have
not customized (see `docs/ADOPTING.md` → _Upgrading_ in the Suspec repo).

## [Unreleased]

### Added

- `.gitignore.additions` — ignore `*.suspec-bak` backups left by `suspec update --write` (suspec-cli),
  so they are not committed or flagged as out-of-scope changes by `suspec review`.
- **Implementation-depth skills** `write-feature`, `write-fix`, `write-refactor`, `write-rewrite`,
  `write-migration`, `write-performance`, `write-testing`, `write-documentation` — **relocated into the
  kit** from the suspec-skills catalog (suspec ADR-0112). They implement a Suspec task packet of a given
  kind, so they are Suspec-coupled and belong with the other Suspec skills; the catalog is now
  framework-free (universal stances + disciplines only). Opt-in depth — summon the kind your task needs.

### Removed

- `adversarial-review` skill — **relocated to the suspec-skills catalog** (suspec ADR-0111): a review
  *style* is not a Suspec concept (Suspec mandates the review artifact, not how you review). Install it
  with `npx skills add jcosta33/suspec-skills --skill adversarial-review`. `review-output` (which builds
  the review packet) stays in the kit.
- `advanced/` and `examples/` directories — **dropped** (suspec ADR-0105): the ADR shape moved into
  `templates/adr.md`, the reference cards were already single-sourced to the canonical
  `docs/reference/`, and the worked example chain lives in the Suspec repo's `docs/examples/`.

### Changed

- Spec template + `write-spec`: the `## Open questions` section is now filled with **options + a
  recommendation** (a decidable fork), not a bare question — the section name and C006 are unchanged
  (suspec ADR-0101).
- **Spec is the unit of work; the task is an on-demand split slice** (suspec ADR-0103). The spec
  template gains an append-only `## Execution` section the implementer fills for 1:1 work — no task
  file unless the spec splits into parallel slices. The task template, `split-work`, `implement-task`,
  and `review-output` are reworded to match. Additive: existing specs and tasks stay valid.

## [1.3.0] - 2026-06-22

### Added

- `LICENSE` — MIT, matching the rest of the family.
- `templates/review.md` — an optional `## Open decisions` section for routing a decision to the
  reviewer ([Suspec ADR-0089](https://github.com/jcosta33/suspec/blob/main/docs/adrs/0089-decision-handoff-open-decisions.md)).
- `templates/change-plan.md` — a prompt under **Affected surfaces** to enumerate _callers_ (the
  inventory's `Current interfaces → Callers` column), not only edit sites, when the surface is a
  shared signature or interface (single-sourced from the Suspec change-plan docs).
- `.gitignore.additions` — ignore `.worktrees/` and reinforce the co-located-workspace ignores.

### Changed

- `.agents/skills/adversarial-review/SKILL.md` — a Rule-0 load directive (a point-of-need 1-hop
  link) so the bundled `references/task-template.md` is actually loaded, not merely listed.
- `templates/task.md` — document the Do-not-change paths as a hard wall.
- `hooks/pre-commit` — narrower gate scope (excludes scaffold READMEs); still fail-open when
  suspec-cli is absent.
- `advanced/` — point at the [suspec-agents](https://github.com/jcosta33/suspec-agents) catalog as
  the single source for agent definitions and remove the in-kit probe; `advanced/checks-reference.md`
  now carries the full change-plan (C010/C011) and task (C012–C015) check tables, and
  `advanced/sol-reference.md` + the `review-output`/`spec-check` guides reword "future CLI" → the
  shipped [`suspec check`](https://github.com/jcosta33/suspec-cli).

## [1.2.0] - 2026-06-18

### Added

- `templates/review.md` — the optional structured-evidence `verify` block convention beside the
  coverage table: a fenced block whose info-string (`verify id=AC-NNN cmd="…" result=pass|fail`) is
  the machine-checkable form [`suspec check` / `suspec review`](https://github.com/jcosta33/suspec-cli)
  reconciles against the spec's named command (core check **C013**, [Suspec ADR-0083](https://github.com/jcosta33/suspec/blob/main/docs/adrs/0083-verify-evidence-reconcile.md)).
  Opt-in — a row may still use only the free-form Evidence cell; the check surfaces a consistency
  fact (the recorded evidence names the requirement's own command and a pass), never a review result.

## [1.1.0] - 2026-06-15

### Added

- `hooks/` — gate templates that run [`suspec check`](https://github.com/jcosta33/suspec-cli):
  a **fail-open** `pre-commit` hook (skips when suspec-cli is not installed, so it never blocks a
  teammate) and an **authoritative** `suspec-check.yml` GitHub Actions workflow (gates the merge).
  Exit `2` blocks, `1` warns, `0` passes. See `hooks/README.md`.
- A "wire the gate" step in the README and a `hooks/` entry in _What you copied_.
- This CHANGELOG.

## [1.0.0] - 2026-06-13

### Added

- The copy-whole workspace baseline ([Suspec ADR-0075](https://github.com/jcosta33/suspec/blob/main/docs/adrs/0075-starter-kit-template-repo.md)):
  `AGENTS.md` bootloader (with `CLAUDE.md` / `GEMINI.md` symlinks); the core loop guides and the
  workspace authoring guides under `.agents/skills/`; the eight core artifact templates under
  `templates/`; the flow folders (`specs/ intake/ tasks/ reviews/ findings/ inventory/
change-plans/`); `decisions/` seeded with `0001-adopt-suspec`; the hand-edited `status.md` board;
  one worked `examples/` chain; the optional `advanced/` templates and reference cards;
  `.gitignore.additions` for governed code repos.

Tagged releases live at
<https://github.com/jcosta33/suspec-starter-kit/releases> (tagging starts at v1.3.0; the earlier
versions above are documented here but were never tagged).
