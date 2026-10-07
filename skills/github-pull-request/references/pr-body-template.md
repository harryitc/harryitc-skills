# PR body template

The body = **core sections** (always) + **optional sections** (only when their trigger fired in
the Step 2 classification, including extra triggers from the project config). Do not add an
optional section just to write "None" — an absent section means its trigger did not fire.
Keep the order below.

## Contents
1. Core sections
2. Optional sections and their triggers
3. Review checklist (assembled from triggers)
4. Examples

## 1. Core sections (every PR)

```markdown
## Summary
<2–4 lines: what it was before → what it does now, and why>

## <Changes heading — see the shape for the PR type below>

### Removed / behavior changes
- <what was removed or now works differently, and why — or "None">

## Testing
- <only the suites that match what the diff touched; real numbers from this HEAD>
- <for a docs/config-only PR: "No tests run — docs only" is a valid line>
```

### Changes — shape per PR type

Pick the one shape that matches the title's `<type>`. Only fill fields that are true for this
change; drop a field rather than invent content for it.

**`feat`** — heading `## Feature details`, one `### N. <Feature name>` per feature:
- **Who:** permission/role and scope *(only if access control is involved)*
- **How:** what the user clicks, where *(only if there is UI)*
- **Behavior:** what the system does step by step; rules; data changed; edge cases
- **Messages:** exact user-facing text, verbatim *(only if the change adds/changes messages)*
- **API:** method + route *(only if endpoints were added/changed)*

A reviewer should understand the behavior without opening the code; "add form" is not enough.

**`fix`** — heading `## Fix`:
- **Symptom:** what the user/system saw (error text, wrong value, steps to reproduce)
- **Root cause:** the exact place and reason (`file:line` or function)
- **Fix:** what changed and why it is the minimal correct change
- **Regression guard:** the test that now covers it

**`refactor` / `perf`** — heading `## Changes`:
- **Before → after:** structure or hot path, briefly
- **Behavior unchanged because:** tests / evidence
- **Numbers** *(perf only)*: measured before/after (query count, ms), with how it was measured

**`docs` / `test` / `chore`** — heading `## Changes`: a short bullet list of what changed and why.

A mixed branch (e.g. one feature + one fix) uses `## Feature details` with a subsection per item,
each in its own type's shape.

## 2. Optional sections and their triggers

Add a section **only** when its trigger matches the diff (`git diff --name-only origin/<base>...HEAD`).
The project config can add more rows (`## Extra sections`).

| Section | Trigger |
|---|---|
| `## Docs` | the branch has a spec, plan, design doc or issue worth linking |
| `## Migrations & deployment` | a migration/schema file, new env var, new CLI/management command, new scheduled job, or a deploy step (sync, backfill, cache flush) |
| `## Permissions` | touches auth/permission/role code or config, or adds/changes an API endpoint |
| `## Known limitations / follow-ups` | there is something real to say (not done, known risk, deferred decision) |
| `## Review checklist` | at least one checklist line in §3 beyond the "always" line is triggered |

```markdown
## Docs
- Spec: <path or link> (<decision ids>)
- Plan: <path or link> (<deviations, if any>)

## Migrations & deployment
- <migration name> — <effect; reversible or not>
- ⚠ <what deploy needs / affects: commands, syncs, data>
- New environment variables: <names, or "none">

## Permissions
- <permission codes/roles used or added; who holds them>
- <hidden in UI ⇔ blocked by the API; out of scope returns 403/404>

## Known limitations / follow-ups
- <…>
```

## 3. Review checklist (assembled from triggers)

Always include the first line; add the others only when their trigger matches, then append the
triggered lines from the project config (`## Extra checklist lines`).

| Line | Include when |
|---|---|
| `- [ ] Matches the spec / issue, no scope creep` | always |
| `- [ ] Access checks enforced server-side; hidden in UI ⇔ blocked by the API` | Permissions section is present |
| `- [ ] Migrations run cleanly forward (and backward if reversible); deploy notes complete` | Migrations section is present |
| `- [ ] New/changed user-facing text reviewed` | the diff adds or changes user-visible text |

If only the first line applies, drop the whole checklist section.

## 4. Examples

Read only the one that matches the PR — do not copy sections from an example whose triggers
did not fire for this branch.
- `examples/feature.md` — a `feat` touching UI + API + migration + permissions (all sections fire).
- `examples/small.md` — a `fix` and a `docs` PR (core sections only).
