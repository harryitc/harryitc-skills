# Examples — small PRs

These show how short a correct PR body can be when few triggers fire. A fictional project.

## A. Backend `fix` (no UI, no migration, no permission change)

Title: `fix(search): product search matches names regardless of letter case`

Triggers fired: none of the optional sections. Checklist: only the "always" line → section dropped.

```markdown
## Summary
Searching the catalog for "lamp" returned nothing for products stored as "Lamp".
Search is now case-insensitive.

## Fix
- **Symptom:** `GET /api/v1/products/?search=lamp` → 0 results while "Desk Lamp" exists.
- **Root cause:** `ProductFilter.filter_search` used `contains` instead of `icontains` (`catalog/filters.py`).
- **Fix:** switch to `icontains`; whole-phrase matching is unchanged.
- **Regression guard:** `test_product_search_is_case_insensitive`.

### Removed / behavior changes
- None.

## Testing
- Backend: `pytest catalog -q` — 88 passed
```

## B. `docs` / `chore` PR

Title: `docs(contributing): document the release checklist`

Triggers fired: none. No tests run, and the body says so.

```markdown
## Summary
Adds the release checklist to `CONTRIBUTING.md` so releases no longer depend on one person's memory.

## Changes
- New "Releasing" section in `CONTRIBUTING.md`.
- Linked it from `README.md`.

### Removed / behavior changes
- None.

## Testing
- No tests run — docs only.
```
