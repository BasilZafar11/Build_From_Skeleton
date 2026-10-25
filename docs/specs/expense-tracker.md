# CLI expense tracker specification

Status: specified for implementation review. This describes a future learner
project, not an application available to install. Follow the
[skeleton standard](../skeleton-standard.md).

## Audience and scope

Prerequisites: Python functions, lists, dictionaries, exceptions, and basic file
handling. Learning objectives: validate inputs, compose functions, represent money
without floating-point errors, persist JSON, and connect behavior to a CLI.

Target Python 3.11 or later. Application code and learner tests use the standard
library (`unittest` for tests). A conventional `pyproject.toml` may use a justified
build backend. Verify supported versions and OS claims before publication.

Core operations: add, list, category filtering, totals, and local persistence.
The first version uses INR with 100 paise per rupee. Editing, deletion, recurring
expenses, accounts, currency conversion, external services, and concurrent writers
are outside the core project. Use fictional data throughout.

## Layout and provided code

```text
projects/python/expense-tracker/
  README.md
  HINTS.md
  pyproject.toml
  src/expense_tracker/
    __init__.py
    __main__.py
    models.py
    validation.py
    tracker.py
    storage.py
    cli.py
  tests/
    test_milestone_1_validation.py
    test_milestone_2_records.py
    test_milestone_3_queries.py
    test_milestone_4_storage.py
    test_milestone_5_cli.py
```

Provide imports, package entry wiring, parser construction, test scaffolding,
and a frozen dataclass with this shape:

```python
@dataclass(frozen=True)
class Expense:
    id: int
    amount_minor: int
    category: str
    date: str
    description: str
```

Learner functions below begin with a useful `NotImplementedError`. Document their
milestone, inputs, results, errors, and side effects. No inheritance, service
containers, database layer, or custom exceptions are needed.

## Canonical data

| Field | Contract |
| --- | --- |
| `id` | Positive integer, unique in its collection; booleans invalid |
| `amount_minor` | Positive integer; booleans invalid |
| Amount text | Strip outer whitespace, then accept ASCII digits with an optional decimal point followed by one or two digits; amount must be positive |
| `category` | Strip outer whitespace, lowercase, then match `[a-z][a-z0-9-]{0,29}` |
| `date` | Exactly ASCII `YYYY-MM-DD` and a real calendar date; future dates allowed |
| `description` | String; strip outer whitespace; maximum 200 characters after stripping; empty allowed; reject tabs, CR, and LF anywhere in the original input |

Amount examples: `"12" -> 1200`, `"12.5" -> 1250`, `" 0.01 " -> 1`.
Reject zero, negatives, signs, commas, exponents, `.5`, `1.`, more than two
fractional digits, Unicode digits, and non-string inputs. Leading zeros are
accepted. Amounts have no arbitrary upper limit beyond Python's integer support.

Collection operations validate every existing record and ID uniqueness. Empty
collections are valid. Directly constructed records with noncanonical fields,
such as `category=" Food "`, are invalid; queries do not silently repair them.
Collection interfaces accept lists of `Expense` instances; invalid containers,
items, or field values raise `ValueError`. No function mutates a collection unless
its contract explicitly says so.

## Milestone 1: validation

Declare in `validation.py`:

| Signature | Behavior |
| --- | --- |
| `parse_amount(text: str) -> int` | Return positive minor units using no floating-point arithmetic |
| `validate_date(text: str) -> str` | Return an exact valid date unchanged; do not strip whitespace or accept relaxed formats |
| `normalize_category(text: str) -> str` | Normalize and enforce the category contract |
| `normalize_description(text: str) -> str` | Enforce the description contract and return stripped text |

Invalid inputs, including non-string inputs, raise `ValueError`. Functions have
no side effects. Date validity is independent of the current date.

## Milestone 2: records

Declare in `tracker.py`:

```python
def add_expense(
    expenses: list[Expense],
    amount: str,
    category: str,
    date: str,
    description: str = "",
) -> Expense: ...

def list_expenses(expenses: list[Expense]) -> list[Expense]: ...
```

`add_expense` validates the collection and all input before mutation. Choose ID
1 for an empty collection, otherwise the maximum ID plus one. Append exactly one
canonical record and return it. Existing IDs need not be contiguous or sorted.
Invalid input raises `ValueError` and leaves the original collection unchanged.

`list_expenses` validates and returns a new list sorted by ascending ID. It does
not reorder the original. Immutable records may be shared; the list must be new.

## Milestone 3: queries

Declare in `tracker.py`:

```python
def filter_expenses(expenses: list[Expense], category: str) -> list[Expense]: ...
def total_expenses(expenses: list[Expense], category: str | None = None) -> int: ...
```

Validate the complete collection and normalize supplied category filters. Invalid
categories raise `ValueError` even on empty input. Filtering returns a new list
sorted by ascending ID. Unknown valid categories return an empty list.

Totals return minor units as an integer. `None` selects every record. Empty or
unmatched totals are zero. Neither operation mutates input or formats currency.

## Milestone 4: persistence

Declare in `storage.py`:

```python
def load_expenses(path: Path) -> list[Expense]: ...
def save_expenses(path: Path, expenses: list[Expense]) -> None: ...
```

Accept `pathlib.Path` objects. Neither function creates missing parent directories.
File-system failures propagate as `OSError`. The format is UTF-8 JSON:

```json
{
  "version": 1,
  "currency": "INR",
  "expenses": [
    {
      "id": 1,
      "amount_minor": 1250,
      "category": "food",
      "date": "2026-01-15",
      "description": "Lunch"
    }
  ]
}
```

Require exactly the three top-level keys and exactly the five keys in each
expense object. Validate types, canonical field values, and unique expense IDs.
Reject unsupported version/currency, extra/missing keys, and boolean integer
fields, including `version`. `expenses` must be a JSON array. Special detection
of repeated JSON object member names is outside scope; normal JSON parsing applies.

Loading a missing file returns `[]` without creating it. Empty files, malformed
JSON, invalid UTF-8, and invalid schema raise `ValueError`. Do not normalize
invalid persisted records or modify any file while loading. Return records in
ascending ID order.

Saving validates everything before touching the destination. Serialize records
in ascending ID order; JSON whitespace and object-key order are unspecified.
Write a temporary file in the destination directory, close it, then atomically
replace the destination after writing succeeds. On ordinary write/replace
failure, preserve the old destination and attempt temporary-file cleanup without
hiding the original exception. Process crashes and concurrent writers are outside
scope. Saving an empty collection creates a valid empty document.

A round trip preserves all field values and IDs. Adding after loading uses the
maximum loaded ID plus one.

## Milestone 5: CLI

Provide parser construction in `cli.py`; leave orchestration unfinished:

```python
def main(argv: list[str] | None = None) -> int: ...
```

`None` uses normal process arguments. Provide `__main__.py` that exits with the
return value. `argparse` may raise `SystemExit` for help and syntax errors.

Planned usage after installation:

```bash
python -m expense_tracker --file expenses.json add --amount 12.50 --category Food --date 2026-01-15 --description Lunch
python -m expense_tracker --file expenses.json list
python -m expense_tracker --file expenses.json list --category food
python -m expense_tracker --file expenses.json total
python -m expense_tracker --file expenses.json total --category food
```

The global optional `--file` appears before the required subcommand. It defaults
to `expenses.json` in the current directory. `add` requires amount, category, and
date. Description defaults to empty. No date defaults to today.

| Situation | stdout | stderr | Exit status |
| --- | --- | --- | --- |
| Added ID 1 | `Added expense 1.` | Empty | 0 |
| Nonempty list | Header and rows below | Empty | 0 |
| Empty or unmatched list | `No expenses found.` | Empty | 0 |
| Total | For example `INR 12.50`, including `INR 0.00` for empty results | Empty | 0 |
| Invalid domain input or stored data | Empty | Useful message prefixed `Error: ` | 1 |
| File-system error | Empty | Useful message prefixed `Error: ` | 1 |
| Syntax error | Standard argparse behavior | Standard argparse error/usage | 2 |
| Help | Standard argparse help | Empty | 0 |

Output lines end in newline characters. Nonempty lists have tab-separated columns
and rows sorted by ascending ID:

```text
ID\tDATE\tCATEGORY\tAMOUNT\tDESCRIPTION
1\t2026-01-15\tfood\tINR 12.50\tLunch
```

Here `\t` represents an actual tab. Empty descriptions leave the last column
empty. Format money with integer arithmetic and exactly two fractional digits,
without grouping separators or locale formatting.

Each valid command loads the file. Only successful `add` saves it; print success
after saving. Queries and failed commands never create or change the data file.
Expected user errors produce no traceback. Do not catch programming errors or
`NotImplementedError` and disguise them as normal user errors.

## Test inventory

| Milestone | Required cases |
| --- | --- |
| 1 | Valid amounts and leading zeros; minimum positive; signed/zero/malformed/Unicode/non-string failures; leap and invalid dates; exact date format; category boundaries; description length and forbidden characters |
| 2 | Empty/nonempty adds; unsorted/noncontiguous IDs; normalization; duplicate/boolean IDs; malformed collections; validation before mutation; sorted independent result lists |
| 3 | All/category totals; category normalization; empty/unmatched inputs; invalid filter on empty input; source immutability; large integer values; invalid source records |
| 4 | Missing/empty/malformed/invalid-UTF-8 files; exact schema and types; invalid version/currency; duplicate IDs; noncanonical values; round trips; next ID after reload; invalid save preserves data; simulated write/replace errors preserve data and clean up |
| 5 | Add/list/total sequence; alternate/default paths; category filters; exact successful output; empty state; syntax/domain/storage errors; no writes on queries or failed adds; success only after save |

Use `tempfile.TemporaryDirectory`, `unittest.mock`, and captured output. Never
require real records or network access. Simulate file-system failures portably;
do not assume permissions behave the same under every OS/account. Tests must
assert observable contracts rather than helper names or JSON indentation.

## Setup and reference acceptance

The implementation PR must document and check environment creation, installation,
imports, collection without test execution, and each milestone command. Standard
`unittest` discovery executes tests, so provide a collection-only snippet or
command as well. Group milestone runs using the planned test filenames.

The stub's `main` initially raises `NotImplementedError`; executable CLI help
becomes functional in milestone 5. Parser construction must be importable from
the start. Explain this instead of claiming the untouched CLI already works.

Reference code lives at `solutions/python/expense-tracker/` with a spoiler warning
and separate setup. Run exactly the same learner tests against it in a second
environment; never import reference code in learner source/tests. Finalize exact
commands with the actual package and verify them before publishing.

- [ ] Untouched skeleton installs, imports, and collects every test.
- [ ] Exercise functions remain explicitly unfinished.
- [ ] Reference passes all milestones and integration checks.
- [ ] README/hints/docstrings agree with the specification.
- [ ] Claimed runtime/OS support has been checked.
- [ ] A clean checkout follows the documented path without extra steps.

## Optional extensions

Learners may explore editing, deletion, monthly summaries, CSV export, or a
database backend in their forks after finishing core milestones. Extensions
must not change the baseline requirements or become necessary for core tests.
