# Merge Patient Records

A small utility for merging two SSN-sorted linked lists of patient records into a single SSN-sorted linked list — the classic "merge two sorted lists" algorithm applied to patient data (e.g. combining records from two source systems).

## Files

- [merge-sorted-list.js](merge-sorted-list.js) — implementation, list helpers, and a self-contained test runner

## How it works

Each patient record is a `patientNode`:

```js
{
  (ssn, age, fullName, next);
}
```

`mergePatientList(l1, l2)` walks both linked lists using a dummy head node and a tail pointer, always attaching whichever node has the smaller `ssn`, until one list is exhausted — then appends the remainder of the other list. Duplicate SSNs (e.g. the same patient present in both source systems) are preserved rather than deduplicated.

Two helpers convert between plain arrays and linked lists for testing:

- `arrayToList(records)` — builds a linked list from an array of `{ ssn, age, fullName }` objects
- `listToArray(head)` — flattens a linked list back to an array of SSNs

## Usage

```bash
node merge-sorted-list.js
```

Running the file executes `runTest` against six built-in cases (three normal, three edge) and prints a `✅ PASS` / `❌ FAIL` report for each, comparing the merged SSN order against the expected result.

### Cases covered

| Case                      | Description                                        |
| ------------------------- | -------------------------------------------------- |
| normal                    | Two interleaved lists of equal length              |
| different lengths         | One list longer than the other                     |
| one list before the other | Lists with non-overlapping SSN ranges              |
| first list empty          | Merging against an empty list                      |
| both lists empty          | Merging two empty lists                            |
| duplicate SSNs            | Same SSN in both lists — both records must be kept |

## Notes

- Records must already be sorted by `ssn` ascending in each input list; the merge does not sort.
- This is a plain Node.js script with no external dependencies.
