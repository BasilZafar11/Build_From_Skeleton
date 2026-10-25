# Week 1 foundation checklist

Started 2026-10-25. This records actual completion, not a future schedule.

## Local foundation

- [x] Define audience, Python-first scope, and contribution boundaries.
- [x] Explain current availability honestly in the README.
- [x] Add MIT license using Basil Zafar's copyright name.
- [x] Document fork/PR contribution and review expectations.
- [x] Add conduct standards and truthful interim reporting guidance.
- [x] Add bug, documentation, and new-skeleton issue forms and a PR template.
- [x] Define contracts, layout, hints, test layers, and reference isolation.
- [x] Specify expense-tracker milestones, schema, CLI, and test inventory.
- [x] Prepare Week 2 tasks and maintainer guidance.
- [x] Verify local links, issue forms, and whitespace.

## GitHub configuration and publication

- [x] Apply and read back repository merge/feature settings.
- [x] Apply and verify active default-branch ruleset.
- [x] Verify Actions permissions and outside-contributor approval policy.
- [x] Enable and verify available secret protection and Dependabot alerts.
- [x] Create/update contributor labels.
- [ ] Publish the foundation through a reviewable PR.
- [ ] Create initial scoped contributor issues.

## User-owned follow-up

- [ ] Basil adds a monitored private conduct-reporting contact before broad promotion.

The maintainer explicitly chose to add that contact later. GitHub's abuse route
is documented as a platform reporting option, not a private inbox for Basil.

## Verification boundaries

Verified on 2026-10-25 through authenticated GitHub API readback:

- Public repository, default branch `main`, issues on, wiki off; Discussions left off.
- Squash merges only, automatic merged-branch cleanup on, auto-merge off.
- Active ruleset `25829255`: PR required, one approval, stale approvals dismissed,
  resolved review threads, blocked deletion/non-fast-forward pushes, PR-only admin bypass.
- Actions token read-only, Actions PR approvals disabled, approval required for
  all outside-contributor workflows.
- Secret scanning, push protection, and Dependabot alerts enabled.
- All six contributor labels present with documented descriptions.

Local verification parses the three issue forms as YAML, checks required fields
and unique field IDs, resolves relative Markdown links, and checks whitespace.
GitHub's own rendered issue-form interface remains a post-merge check.

No learner implementation or automated workflow is part of Week 1. Runtime
behavior, reference test success, and clean learner installation belong to Week
2. No required CI status check is configured before its workflow exists.
