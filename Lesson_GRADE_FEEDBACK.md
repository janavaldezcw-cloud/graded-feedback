# Project Grade & Feedback — Lesson (JS Fundamentals Notes)

**Grade: D+**
**Score: 67 / 100**
**Graded by:** Ethan Kowalski
**Date:** 2025-08-22
**Repository:** [janavaldezcw-cloud/project](https://github.com/janavaldezcw-cloud/project)

---

## Summary

The Lesson folder is a set of four JavaScript study files covering arrays, callbacks, Map/Set, and Promises. As learning notes they show genuine engagement with core JS concepts. As code, they won't run — three of the four files have syntax errors, typos, or fundamentally wrong API calls. Graded as working code this scores low, but graded as a study record the effort is real.

---

## Grading Rubric

| Category | Points Possible | Points Earned | Notes |
|---|---|---|---|
| Correctness (Code Runs) | 35 | 14 | Only callbacks.js is close to runnable; others have hard errors |
| Concept Understanding | 30 | 22 | Demonstrates awareness of core concepts even when syntax is wrong |
| Code Clarity | 20 | 18 | Notes-style code is readable; intent is clear |
| Completeness | 15 | 13 | All four major topics covered |

**Total: 67 / 100 → D+**

---

## File-by-File Breakdown

### `callbacks.js` — Best File (Good)
Uses `fs.readFile()` correctly with a callback, handles errors, parses JSON. The try-catch around `JSON.parse` is the right pattern. One typo: `"erroe"` in the error message. This file almost works.

### `promises.js` — Several Bugs (Needs Work)
- Line 4: parameter named `date` but used as `data` — will be `undefined`
- Lines 6 and 10: `consolo.log` → `console.log` (two occurrences)
- Line 19: `fsc.readFile` → `fs.readFile`
None of these are conceptual misunderstandings — they're all typos. Run the file, read the errors, fix them.

### `map&set.js` — API Confusion (Fix This)
- Maps use `.set(key, value)` — not `.add()`. `.add()` is a Set method.
- Line 20: `new Set = myArray [1, 2, 3]` is not valid JavaScript syntax.
The concept of what Maps and Sets are seems understood; the specific methods need review.

### `array.js` — Incomplete Notes (Neutral)
More of an outline than runnable code. Lists methods (`push`, `splice`, `filter`) without using them. Not broken, just not finished.

---

## Key Things to Fix

1. Run every file in Node.js. Read the error messages. Fix one at a time.
2. `Map.set(key, value)` vs `Set.add(value)` — these are different. Review both.
3. Consistent variable naming — `date` vs `data` is an easy bug to catch if you read the code out loud.

---

## Final Notes

These files exist because you were learning, and that's the right reason. The concepts being studied (Promises, callbacks, Map/Set) are real fundamentals. The next step is to run each file, fix the errors, and confirm it produces the expected output. Notes that don't execute aren't as useful as notes that do.

**Grade: D+ (67/100)**
