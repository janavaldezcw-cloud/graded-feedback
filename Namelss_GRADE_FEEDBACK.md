# Project Grade & Feedback — Namelss (Employee Info CLI)

**Grade: D**
**Score: 62 / 100**
**Graded by:** Camille Osei
**Date:** 2025-10-07
**Repository:** [janavaldezcw-cloud/project](https://github.com/janavaldezcw-cloud/project)

---

## Summary

Namelss is a Node.js CLI tool intended to collect employee information (first name, last name, start date) and save it to a JSON file. The setup is reasonable — it uses `prompt-sync` for input, has a separate `createUserJson.js` module, and attempts input validation. But the core function, `employeeData()`, collects user input into local variables and then does nothing with them. The data is never returned, never stored, and never used. The `Employee` constructor is defined but never called. There's also a persistent typo (`fistName` instead of `firstName`) throughout the file.

---

## Grading Rubric

| Category | Points Possible | Points Earned | Notes |
|---|---|---|---|
| Functionality & Completeness | 30 | 12 | Core data collection logic never produces output |
| Code Quality & Organization | 25 | 18 | Decent structure; typo repeated 4 times; unused variable |
| Design & Architecture | 20 | 16 | Good intent to separate concerns; `createUserJson.js` is solid |
| Documentation | 15 | 10 | No README, no comments |
| Testing | 10 | 6 | No tests |

**Total: 62 / 100 → D**

---

## What Was Done Well

### `createUserJson.js` Is the Better File
The JSON file creation utility is well-written and functional. It uses the Node.js `fs` module correctly and shows cleaner thinking than the main file. This suggests real improvement between writing the two files.

### Input Validation Loop
Requiring non-empty strings before accepting input is the right instinct. The while loops that re-prompt on empty input are a good pattern.

### Module Setup
Using `prompt-sync` as a dependency and setting up `package.json` properly is a good habit even for a small project.

---

## Critical Issue: `employeeData()` Never Returns Its Data

This is the main problem. The function collects `firstName`, `lastName`, and `startDate` into local variables, then the function ends. Those values are gone. The `Employee` constructor below it is defined but never instantiated with the collected data.

```js
// Current — data collected but lost
function employeeData() {
  let firstName = prompt('...');
  let lastName = prompt('...');
  let startDate = prompt('...');
  // nothing returned, nothing saved
}

// Fix — return an Employee instance
function employeeData() {
  const firstName = prompt('...');
  const lastName = prompt('...');
  const startDate = prompt('...');
  return new Employee(firstName, lastName, startDate);
}

const emp = employeeData();
createUserJson(emp); // then save it
```

---

## Other Issues

### Typo: `fistName` (4 occurrences)
`fistName` → `firstName`. It appears four times. A find-and-replace fixes all of them in one shot.

### Unused Variable
`let employee = {}` at the top is declared but never assigned or used. Delete it.

---

## Final Notes

The architecture is pointed in the right direction — separate files for concerns, a constructor for the data shape, a utility for file output. The missing piece is the glue: make `employeeData()` return the result, pass it to `createUserJson`, and write it to disk. That's 5 lines of code that would make this actually work.

**Grade: D (62/100)**
