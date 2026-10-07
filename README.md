# harryitc-skills

Agent skills by [harryitc](https://github.com/harryitc). Works with Claude Code, Codex, Cursor,
OpenCode and other agents that read `SKILL.md` skills.

| Skill | What it does |
|---|---|
| [`github-pull-request`](skills/github-pull-request/SKILL.md) | Opens or updates a GitHub PR carefully: read-only pre-push checks (sync with base via dry-run merge, tests only for the areas the diff touches), a PR body with only the sections the diff triggers, and a draft shown for approval before any push. |

## Install

### Any agent — `npx skills`

```bash
# into the current project (pick agents interactively)
npx skills add harryitc/harryitc-skills

# one skill, Claude Code only, global
npx skills add harryitc/harryitc-skills --skill github-pull-request -a claude-code -g

# update later
npx skills update
```

### Claude Code plugin

```text
/plugin marketplace add harryitc/harryitc-skills
/plugin install harryitc-skills@harryitc-skills
```

Skills from the plugin are namespaced: `/harryitc-skills:github-pull-request`.
Updates: `claude plugin update harryitc-skills@harryitc-skills`, or enable auto-update for this
marketplace in `/plugin` → Marketplaces.

## Per-repo settings (`github-pull-request`)

The skill works without configuration (it infers the base branch and test commands). To pin the
base branch, test commands per path, extra PR sections or checklist lines for a repo, add
`.agents/pr-config.md` to that repo — format and example in
[`references/project-config.md`](skills/github-pull-request/references/project-config.md).

## Requirements

`git` and the [GitHub CLI](https://cli.github.com/) (`gh auth login`).
