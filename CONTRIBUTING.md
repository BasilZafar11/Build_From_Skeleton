# Contributing

Build From Skeleton is a collection of unfinished educational projects. Help us
make those projects understandable, correct, and practical to complete.

## What to contribute

- New skeletons with documented exercises, milestone tests, hints, and a verified
  reference implementation.
- Corrections to setup, requirements, tests, and examples.
- Clearer explanations and optional hints.

Functions marked as learner exercises are intentionally unfinished. Complete
your own implementation in your fork. Do not replace exercise stubs with working
solutions in a skeleton PR. Reference implementations live separately under
`solutions/<language>/<project>/`, with a spoiler warning.

## Before starting

Read the [code of conduct](CODE_OF_CONDUCT.md) and
[skeleton standard](docs/skeleton-standard.md).

For a substantial new project, open a new skeleton proposal and wait for a
maintainer to agree on its scope before implementing it. Python is the initial
language. Proposals for other languages should identify someone able to review
and maintain them.

Small, clear corrections can go directly into a PR. Comment on an existing issue
before starting larger work to reduce duplicate effort. An issue comment is not
a permanent reservation.

## Make a contribution

1. Fork the repository on GitHub.
2. Clone your fork and create a descriptive branch:

   ```bash
   git clone https://github.com/YOUR-USERNAME/Build_From_Skeleton.git
   cd Build_From_Skeleton
   git switch -c improve-expense-tracker-instructions
   ```

3. Make one focused change. Follow the affected project's documented commands.
4. Verify the change and record the commands and results in your PR.
5. Commit and push your branch, then open a PR against `main`.
6. Link the relevant issue and explain the resulting behavior. Include screenshots
   only when the change benefits from them.

Never include credentials, real personal expenses, local virtual environments,
or generated build output. Use fictional data in examples and fixtures.

## Verification expectations

| Change | Expected verification |
| --- | --- |
| Documentation | Check examples, spelling, relative links, and agreement with the specification |
| Setup or dependency change | Install in a new environment and run the documented commands |
| Learner tests | Show they collect on the untouched skeleton and pass against the reference implementation |
| New skeleton | Verify clean setup, every milestone, hints, and reference behavior |

Learner tests may fail on an untouched skeleton because its exercises are
unfinished. Collection errors, missing imports, and broken installation are not
expected failures. Explain expected failures in the project README.

There are no root-level install or learner-test commands yet. Do not claim that
planned CI or unpublished projects have passed. Repository automation, when
introduced, will distinguish structural checks from learner implementation tests.

## Dependencies and ownership

Prefer the standard library. Explain added dependencies and keep them specific to
the project that needs them. No learner project should require paid services or
credentials for its core milestones.

Submit work you have the right to contribute under this repository's
[MIT license](LICENSE). You retain your copyright. Identify third-party code,
text, fixtures, and their licenses; retain required notices. Do not copy material
from a tutorial or repository simply because it is publicly accessible. Flag
licensing uncertainty before including the material.

Tools, including AI tools, may assist a contribution. You remain responsible for
understanding the result, checking its sources, and verifying its behavior. Do
not send other people's private information to external services.

## Review and maintenance

Maintainers review scope, teaching value, correctness, dependencies, and clarity.
A maintainer may request changes, narrow a proposal, or decline work that does
not fit the collection. Submitting a PR does not guarantee acceptance.

Keep discussion in the relevant issue or PR. Respond to review comments or state
when you need more time. Before closing apparently abandoned work, a maintainer
should leave a follow-up and give the contributor an opportunity to respond.
Closed work can be revisited later.

Contributors use forks and PRs; write access is not required. Maintainer access
is granted separately based on sustained participation and judgment.
