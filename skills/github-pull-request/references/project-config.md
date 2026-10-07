# Project config — `.agents/pr-config.md`

A plain markdown file in the target repo (committed, so the whole team and every agent shares it).
Every section is optional; anything missing falls back to the skill's defaults. Keep it short —
only what differs from the defaults or cannot be inferred.

## Sections the skill reads

| Heading | What it sets |
|---|---|
| `## Base branch` | Default PR base (e.g. `dev`). |
| `## Title modules` | Allowed `<module>` names for the title. |
| `## Test matrix` | Table: changed-path glob → command to run, with any flags and why. |
| `## Extra sections` | Table: section heading → trigger (path globs or condition) → what it must contain. |
| `## Extra checklist lines` | Table: checklist line → trigger. Added to the Review checklist only when triggered. |
| `## Never include` | Paths that must never be part of a PR. |
| `## Language` | PR language and tone rules (e.g. how app messages address users). |
| `## Notes` | Anything else: generated files and how to regenerate them on conflict, where specs/plans live, deploy caveats. |

## Example

````markdown
# PR config

## Base branch
dev

## Title modules
api, web, billing, auth, infra

## Test matrix
| Changed paths | Run |
|---|---|
| `api/**/*.py` | `docker compose run --rm api pytest <touched apps> -q` |
| `web/src/**` | `cd web && npx tsc --noEmit && npx eslint <changed files> && npx vitest run` |
| `web/e2e/**` or a changed UI flow | `cd web && npx playwright test <spec>` |

## Extra sections
| Section | Trigger | Contents |
|---|---|---|
| `## Permissions` | `api/auth/**`, `**/permissions.py`, new endpoint | permission codes, who holds them, hidden button ⇔ API blocks |

## Extra checklist lines
| Line | Trigger |
|---|---|
| `- [ ] Responsive at 1280 / 1024 / 768 px` | layout changes in `web/src/**/*.tsx` |
| `- [ ] Feature flag defaults to off` | new entry in `api/flags.py` |

## Never include
`.envs/`, `media/`, `.omc/`

## Notes
- Specs live in `docs/specs/`, plans in `docs/plans/`.
- `docs/INDEX.md` is generated: resolve conflicts with `python scripts/gen_index.py`.
````
