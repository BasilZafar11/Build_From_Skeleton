# Week 2 backlog

Goal: publish one usable expense-tracker skeleton with milestone tests and a
verified reference. Follow the [specification](specs/expense-tracker.md).
These tasks do not imply a learner project is already available.

Track the initial implementation in the
[Week 2 milestone](https://github.com/BasilZafar11/Build_From_Skeleton/milestone/1).
The specification walkthrough is [#2](https://github.com/BasilZafar11/Build_From_Skeleton/issues/2),
package/stubs are [#3](https://github.com/BasilZafar11/Build_From_Skeleton/issues/3),
learner tests are [#4](https://github.com/BasilZafar11/Build_From_Skeleton/issues/4),
and the isolated reference is [#5](https://github.com/BasilZafar11/Build_From_Skeleton/issues/5).

| Order | Task | Dependencies | Acceptance criteria |
| --- | --- | --- | --- |
| 1 | Review the specification | None | Resolve contradictions with examples and update the contract before implementation |
| 2 | Create package and documented stubs | Agreed specification | Independent package, dataclass/parser wiring, precise exercise signatures, explicit NotImplementedError, clean imports/install |
| 3 | Add milestone tests | Agreed interfaces; coordinate with task 2 | Tests collect on stubs and cover the inventory with meaningful unfinished-behavior failures |
| 4 | Add isolated reference | Tasks 2 and 3 | Same interfaces and learner tests pass; no reference imports in learner code/tests |
| 5 | Write learner README and hints | Actual commands available | Verified setup, milestone order/commands, expected failures, progressive hints, spoiler links |
| 6 | Verify clean checkout | Tasks 2 through 5 | Independent environment, command transcript, passing reference tests, checked support claims |
| 7 | Arrange learner trial | Task 6 | Obtain authorization before contacting participants; record confusing steps and revise |
| 8 | Update project catalog | Task 6; preferably learner feedback | README links to the available project and accurately describes verified support |

Keep the first example cohesive. Agree on interfaces before splitting connected
code/tests across contributors. Record Python version, OS, commands, expected
stub failures, reference results, and limitations in implementation PRs. Include
malformed-file and alternate-data-path checks; failed commands must preserve data.

Once CI exists, separate structural skeleton checks from reference behavior tests.
Do not require a status check before the corresponding workflow has run.

Before broad promotion, add the private conduct contact, review contributor issue
scope, and verify live GitHub settings. Do not estimate completion times until
learners have tried the project.
