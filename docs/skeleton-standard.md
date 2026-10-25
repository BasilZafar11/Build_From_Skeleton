# Skeleton standard

This is the acceptance standard for projects contributed to Build From Skeleton.
The first project targets Python 3.11 or later. Support claims must be verified
before a learner project is published.

## Purpose and scope

Each project teaches a small, explicit set of skills by connecting functions into
a complete application. State prerequisites separately from learning objectives.
Core milestones must work locally without paid services, API credentials, or
personal data. Optional extensions must not be needed to finish the core project.

Provide working setup, imports, and framework registration where they are not
the subject of an exercise. Leave the behavior being taught unfinished. Do not
add decorators or abstractions just to make the skeleton appear more elaborate.

## Layout

```text
projects/<language>/<project>/
  README.md
  HINTS.md
  pyproject.toml                 # Python projects
  src/<package>/
  tests/
    test_milestone_1_*.py
    test_milestone_2_*.py

solutions/<language>/<project>/
  README.md                    # Spoiler warning and exact verification commands
  src/<package>/               # Complete reference using the same public interface
```

Use lowercase, hyphen-separated project directory names and language-appropriate
package names. Add files only when needed. Each project owns its dependencies;
there is no shared root installation containing all project dependencies.

Reference source must not be imported by the skeleton or its learner tests.
The reference README must document how to run the same tests against the
reference in a separate environment without copying completed code over stubs.
Duplicated interfaces must stay synchronized. A reference implementation is one
valid solution, not the only permitted design.

## Project README

Include overview, prerequisites, learning objectives, setup for Windows and
macOS/Linux, file responsibilities, milestone order, expected behavior, exact
test commands, completion checklist, and optional extensions. Explain expected
failures in the untouched skeleton and link to optional hints and spoiler-marked
reference material.

Do not claim completion times or supported environments without checking them.
Never imply a virtual environment is bundled with the repository.

## Exercise contracts

Every unfinished function or method must document:

1. Its responsibility and milestone.
2. Input types, accepted ranges, and normalization rules.
3. Return type and exact result shape.
4. Mutations and other side effects, including file writes.
5. Error types and the conditions that produce them.
6. Relevant empty, invalid, and boundary cases.
7. A short example when it clarifies the contract.

Use type annotations where they help. Python exercise bodies should raise
`NotImplementedError` with a useful milestone/function message. A comment alone
is not a valid Python function body. Avoid placeholder returns that could pass
tests accidentally.

Requirements should describe observable behavior. Do not supply a line-by-line
algorithm in the exercise contract. Place conceptual and then more specific
hints in `HINTS.md`, grouped by milestone.

## Tests and verification

Keep these responsibilities distinct:

| Layer | Expected outcome in an untouched skeleton |
| --- | --- |
| Syntax, imports, installation, and test discovery | Pass |
| Tests that exercise unfinished behavior | Fail with clear context |
| Same learner tests run against the completed reference | Pass |

Group tests by milestone and document commands that run each group. Later
milestones may depend on earlier ones. Cover normal behavior, specified errors,
meaningful boundaries, and integration. Test the contract rather than private
helpers or one exact algorithm. Use temporary directories for persistence and
fictional records. Do not write into a learner's real data file.

Do not skip or mark every learner test as expected failure to make CI green.
Repository checks must not require the untouched exercises to behave as completed
solutions. Once CI exists, run structural checks on the skeleton and behavior
tests against the reference separately. No required CI check is configured until
that workflow exists and has run successfully.

New exercises must include a reference that passes the same tests. For changes
to a contract, update instructions, stubs, tests, hints, and reference together.

## Dependencies and distribution

Use the standard library when practical. Justify each external dependency, keep
test dependencies separate, and document the supported runtime. Use released
packages from their normal registries. Do not require broad system privileges.
Keep credentials, real user data, environments, caches, and generated output out
of version control.

Original contributions use the repository's MIT license. Identify and review
third-party licensing before copying material. Preserve required attribution and
notices; do not assume everything in another public repository is reusable.

## Acceptance checklist

- [ ] Scope and prerequisites are clear and the project fits an agreed proposal.
- [ ] A clean checkout can be set up using only the documented steps.
- [ ] Every exercise has a precise contract and explicit unfinished body.
- [ ] Milestone tests collect without implementation or import errors.
- [ ] Untouched-skeleton failures are explained.
- [ ] The reference passes the same tests in isolation.
- [ ] Hints help without being required to discover missing requirements.
- [ ] Required sources and license notices are present.
- [ ] README catalog status matches actual project availability.
