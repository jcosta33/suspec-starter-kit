# Checks reference card

<!-- The review checklist for specs, tasks, and review packets. Levels:
     convention = expected practice · checklist = review inspects it ·
     toolable = `corpus check` (corpus-cli, shipped) can flag it. Nothing in this kit
     itself is machine-enforced; teams may treat any item as blocking by policy. -->

## Spec checks (both forms)

| #    | Check                                                                                                                                                                                                           | Severity   | Level    |
| ---- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------- | -------- |
| C001 | `unique-ids` — every requirement ID appears exactly once in the file                                                                                                                                            | hard error | toolable |
| C002 | `duplicate-id` — no other file claims the same frontmatter `id:` (requirement IDs are spec-scoped — a bare `AC-NNN` may recur across specs)                                                                     | hard error | toolable |
| C003 | `verify-with` — every requirement carries a `Verify with:` (SOL: `VERIFY BY`) line                                                                                                                              | hard error | toolable |
| C004 | `one-strength-word` — exactly one of must / must not / should / should not / may per requirement                                                                                                                | warning    | toolable |
| C005 | `non-goals-present` — a non-empty Non-goals section exists                                                                                                                                                      | warning    | toolable |
| C006 | `open-questions-present` — an Open questions section exists (even "none")                                                                                                                                       | warning    | toolable |
| C007 | `no-tbd-at-ready` — no `TBD`/`TODO`/unresolved question at `status: ready`                                                                                                                                      | hard error | toolable |
| C008 | `sources-named` — frontmatter `sources:` names at least one origin                                                                                                                                              | warning    | toolable |
| C009 | `broken-source-link` — every named source or cross-reference resolves                                                                                                                                           | hard error | toolable |
| C015 | `citation-resolves` — an inline `[[KEY]]` citation resolves to a matching `<a id="KEY">` anchor in the `sources.md` the frontmatter names (skips when no `sources.md` is resolvable; v0 = dangling-anchor only) | warning    | toolable |

Beyond the numbered checks, review also inspects (checklist level): an `owner:` is named;
no two requirements contradict each other on the same trigger; watchlist words carry a
same-line observable criterion.

Watchlist (advisory): robust, fast, graceful, handle, support, improve, optimize,
seamless, appropriate, significant, as needed, where possible — a vague word is fine
_if the same line_ gives a number, an actor+action, or a named test.

## Change-plan checks

| #    | Check                                                                                                                                                                                               | Severity   | Level    |
| ---- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------- | -------- |
| C010 | `preserves-refs-resolve` — every `preserves:` frontmatter entry and Behavioral-preservation-guarantees table id resolves to a real requirement ID (or is an explicit `PG-NNN` plan-local guarantee) | hard error | toolable |
| C011 | `waves-present` — a change plan whose `kind` is `migration`, `rewrite`, or `schema-change` carries a non-empty Transformation waves section, each wave naming its verify step                       | warning    | toolable |

## Task checks

- Scope ids all exist in the named spec/change plan (hard error, checklist).
- `Do not change` present (warning, checklist).
- Every Verify item maps to a scope id (warning, checklist).

## Review-packet checks

| #    | Check                                                                                                                                                                                                                                                                                                                                                 | Severity   | Level    |
| ---- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------- | -------- |
| C012 | `coverage` — every in-scope requirement id (keyed on the task's declared `scope`) has exactly one coverage row, and no row names an id absent from the source spec; non-draft source specs only                                                                                                                                                       | warning    | toolable |
| C013 | `verify-evidence-binding` — where a coverage row carries a structured `verify` block (`id=AC-NNN cmd="…" result=pass\|fail`), the recorded `cmd` matches the requirement's named `Verify with:` / `VERIFY BY` command and a Pass row reads `result=pass`; a Pass row with only a free-form Evidence cell stays a warning; non-draft source specs only | warning    | toolable |
| C014 | `do-not-change-touched` — a changed file matching a task's `## Do not change` entry is surfaced as a protected-path fact routed to Human attention (same matcher as Affected areas; distinct from out-of-scope drift)                                                                                                                                 | warning    | toolable |
| C016 | `pass-needs-evidence` — a Pass coverage row with an empty Evidence cell is a structural contradiction (a Pass needs pasted output, a CI link, or a named manual observation); the `corpus check <review>` gate **blocks** it, the `corpus review` reconcile surfaces it advisorily                                                                    | hard error | toolable |

Beyond the numbered checks, review also inspects:

- No merge recommendation with an open critical item (hard error, checklist).
- At least one green row spot-checked by the reviewer (convention).

## Workspace checks

| #    | Check                                                                                                                                                                                              | Severity | Level    |
| ---- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------- | -------- |
| C017 | `orphaned-reference` — a bundled `.agents/skills/<name>/references/<file>` named nowhere in its sibling `SKILL.md` (orphan direction only — a load-bearing reference the guide forgot to point at) | warning  | toolable |

## Findings / board

- A finding has evidence and a where-it-applies scope (warning, checklist).
- A board "done/verified" row links its review packet (convention).
