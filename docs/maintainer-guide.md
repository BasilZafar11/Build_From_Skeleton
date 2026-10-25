# Maintainer guide

Basil Zafar is the initial maintainer. Contributors use forks and PRs; write
access is not required. Grant maintainer access separately based on sustained
participation and judgment.

## Triage

| Label | Meaning |
| --- | --- |
| `bug` | Incorrect requirements, setup, behavior, or tests |
| `documentation` | Instructions need improvement |
| `new skeleton` | New educational project proposal or implementation |
| `good first issue` | Small task with explicit instructions and limited scope |
| `help wanted` | Defined work ready for an outside contributor |
| `needs discussion` | Scope or behavior is unsettled |

Open issues for real work, not a daily quota. Describe the problem, relevant
files, expected outcome, dependencies, and completion criteria. Do not label a
whole new project as a good first issue or blocked work as ready to start.

## Review

1. Confirm fit with the agreed scope and skeleton standard.
2. Read instructions, stubs, tests, hints, and reference together.
3. Verify checks appropriate to the change and require clean-setup evidence for
   new packages or setup changes.
4. Review dependency changes, sources, licenses, generated files, and secrets.
5. Resolve review conversations, approve contributor work, and squash merge.
6. Explain requested revisions or declined contributions with concrete reasons.

Use PRs for maintainer changes too. A PR-only admin bypass lets a solo maintainer
merge their own work without inventing independent approval. Keep force pushes
blocked and revisit the exception when a second trusted maintainer is available.

## GitHub configuration target

- Public repository, `main` default, issues enabled, wiki disabled.
- Squash merging enabled, merge commits/rebase merging disabled, auto-merge off,
  merged branches automatically deleted.
- Active default-branch ruleset: block deletions/non-fast-forward pushes, require
  a PR with one approval, dismiss stale approvals, resolve review conversations;
  admin bypass limited to PRs.
- No required status checks until an actual workflow has run successfully.
- Actions token defaults to read-only, Actions cannot approve PRs, and all
  outside-contributor workflows require approval.
- Available secret scanning and push protection enabled; Dependabot alerts on.
  Add dependency-update configuration when actual manifests exist.

Inspect the full PR, scripts, dependency installation, and workflow changes before
approving an outside workflow run. Prefer GitHub-hosted runners. Never execute
untrusted checked-out PR code with secrets through `pull_request_target`.

Read back live settings after changing them; the checklist records actual state.

- [Rulesets](https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/managing-rulesets/available-rules-for-rulesets)
- [Actions settings](https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/enabling-features-for-your-repository/managing-github-actions-settings-for-a-repository)
- [Security quickstart](https://docs.github.com/en/code-security/getting-started/quickstart-for-securing-your-repository)

## Community readiness

A monitored private conduct contact remains pending. Keep that limitation visible;
do not invent an address or response-time promise. Delay broad promotion until
the contact is added and at least one project has clean-setup evidence.

Review proposed work weekly. Follow up on inactive contributions before closing
them, and allow contributors to return later. Keep project availability accurate.
