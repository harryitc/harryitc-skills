---
name: github-pull-request
description: Create or update a GitHub pull request the careful way — read-only pre-push checks (clean tree, sync with the base via a dry-run merge, real test evidence for the areas the diff touches, new migrations), a PR description that contains only the sections the diff actually triggers, and a draft shown to the user for approval before any push or `gh pr create`. Per-repo settings (base branch, test commands, extra checklist lines) come from `.agents/pr-config.md` when present. PR text defaults to English; write it in another language when the user asks. Use this skill whenever the user wants to create/open/push a PR, send a branch for review, says "merge request" or "push this up for review", or wants to update an existing PR's description — even if they never say "pull request".
---

# GitHub Pull Request

Goal: a PR that a reviewer (often someone who will not read every line) understands at a
glance — **what changed, how it behaves, what was removed or changed, how it was tested, and
what deployment needs** — with nothing pushed or published until the user agrees.

The body contains only what is relevant to this branch: a docs-only PR has no permissions
section, a backend fix has no UI checklist. Step 2 decides which parts apply before anything is written.

## Why ask before pushing

Pushing a branch and opening a PR are public actions: others see them immediately and they are
hard to take back. So the workflow has two halves: the first half is read-only (checks + draft),
the second half runs only after the user explicitly says to go ahead. Approval for one branch
does not carry over to the next one.

Never do these, even when convenient: merge the PR, force-push, push directly to the base or
default branch, rewrite already-pushed history, assign reviewers/labels/milestones unless asked.
Never include secrets, env files, local agent state, or caches in the PR (plus any paths the
project config lists under "Never include").

## Step 0 — Load the project config

Look for `.agents/pr-config.md`, then `.claude/pr-config.md`, in the repo root. If found, read it:
it overrides the defaults below (base branch, test commands per path, extra sections and checklist
lines, title modules, language notes). Format: `references/project-config.md`.

If there is none, use the defaults and infer what you can (base = `dev` if `origin/dev` exists,
else the remote default branch; test commands from `package.json` scripts, `Makefile`,
`pyproject.toml`/`pytest.ini`, `go.mod`, `Cargo.toml`). Tell the user what you inferred, and offer
once to write a `.agents/pr-config.md` for them — never commit it without their approval.

## Language

Write the PR title and body in **English by default**, or in the language the user (or the
project config) asks for. Keep code identifiers, paths, permission codes and API routes as-is.
Quote user-facing messages from the app verbatim; add a short English gloss if the PR is in
English and the message is not.

## Step 1 — Pre-push checks (read-only)

Run from the repo root.

1. **Branch state**
   - `git status -sb`: tracked files must be clean. List untracked files; never add them yourself.
   - Not on the base/default branch — if so, stop and suggest creating a branch.
   - `git ls-remote --heads origin <branch>`: whether the branch already exists on the remote.
   - `gh pr list --head <branch> --state open`: whether a PR is already open (if so, see "Updating an existing PR").
2. **Sync with the base**
   - `git fetch origin`
   - `git rev-list --count HEAD..origin/<base>`: how many new base commits the branch lacks.
   - If > 0, dry-run the merge without touching the branch:
     `git merge-tree --write-tree --name-only HEAD origin/<base>`. Report the commit count and any
     conflicting files (the project config may say how to resolve generated files).
   - Recommend merging the base and re-running tests, but **let the user choose**; never merge or
     rebase on your own.
3. **Scope of the change**
   - `git log --oneline origin/<base>..HEAD`, `git diff --stat origin/<base>...HEAD`
   - Changed paths: `git diff --name-only origin/<base>...HEAD` (used by Steps 1.4 and 2).
   - New migrations (any `migrations/`, `db/migrate/`, `*.sql` schema files).
   - Related spec/plan/issue, if the project config names where they live.
4. **Test evidence** — run only the suites for the areas the diff touches, using the project
   config's test matrix (or the inferred commands). Reuse results from this session only if they
   were produced on the current HEAD. A diff that only touches docs/markdown/agent files runs
   nothing, and the PR says "No tests run — docs only". A mixed diff runs every matching suite.
   - If anything is red, compare against the base commit (temporary worktree at
     `git merge-base HEAD origin/<base>`) to separate **new failures caused by the branch** from
     **pre-existing ones**. The PR may say "no new failures" only after that comparison was done.
   - New failures caused by the branch → stop and report; do not draft the PR as if it were green.

## Step 2 — Classify the change

Before writing, decide two things and keep them in your notes for the user:
1. **PR type** = the title's `<type>` (`feat`, `fix`, `refactor`, `perf`, `docs`, `test`, `chore`),
   judged from the commits and diff. It picks the shape of the Changes section.
2. **Triggered sections** — match the changed paths against the trigger tables in
   `references/pr-body-template.md` §2–§3 plus any extra triggers in the project config. Only
   triggered sections go into the body; never add a section just to write "None".

## Step 3 — Draft the PR

Read `references/pr-body-template.md`, then only the example that matches the PR
(`references/examples/feature.md` for a feature, `references/examples/small.md` for a fix, docs
or chore). Fill the core sections plus the sections triggered in Step 2.

- **Title:** `<type>(<module>): <short description>` — match the repo's existing commit style
  (`git log --oneline -20`); module is the main app/area. Same language as the body.
- **Sources:** spec/plan/issue, `git log`, the actual code. Do not invent anything; mark
  unverified claims as such. Test numbers must be numbers that were actually produced, noting if
  they predate syncing with the base. A field that does not apply is dropped, not filled with guesses.
- **The Changes section is the most important part.** For a `feat`, one subsection per feature
  so a reviewer understands the behavior without opening the code; "add form" is not enough.
- **"Removed / behavior changes"** is always present (write "None" if truly none) — it is what
  reviewers most often miss.
- Write the body to a temp file (outside the repo) for `--body-file`.

**Show the user:** base ← head, the title, the full body, the Step 1 findings (especially new
base commits and conflicts), and one line naming the PR type and which optional sections were
triggered (so a wrong classification is easy to spot). Ask one clear question: create now /
sync with base first / edit the content.

## Step 4 — After the user approves

1. `git push -u origin <branch>`
2. `gh pr create --base <base> --head <branch> --title "<title>" --body-file <file>`
3. Give the user the PR link; if the repo has CI, run `gh pr checks <number>` and report status.

## Updating an existing PR

If the branch already has an open PR, do not open a second one. Redraft the body as in Steps 2–3,
show it to the user, then `gh pr edit <number> --body-file <file>` (plus `--title` if needed).
New commits are pushed with a normal `git push` (never force).

## When something fails

- **Push rejected for permissions** (`403`, `permission denied`): stop, report the active `gh`
  account (`gh auth status`) and the repo owner; do not change remotes or fork on your own.
- **Push rejected as non-fast-forward:** the remote branch has other commits — report it, suggest
  `git pull --rebase` or a merge, and wait for the user's choice; never force.
- **`gh` not installed or not logged in:** ask the user to install it / run `gh auth login` themselves.
