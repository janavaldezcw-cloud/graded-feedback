# Project Grade & Feedback — Unit Converter

**Grade: B+**
**Score: 86 / 100**
**Graded by:** Leo Mbeki
**Date:** 2026-02-04
**Repository:** [janavaldezcw-cloud/project](https://github.com/janavaldezcw-cloud/project)

---

## Summary

Unit Converter is a clean, functional metric-to-imperial converter covering length (m ↔ ft), volume (L ↔ gal), and mass (kg ↔ lb). It displays all three conversions simultaneously on button click, with values formatted to 3 decimal places. The CSS is well-crafted — CSS variables for theming, responsive layout, proper input validation, accessibility labels. The main weakness is consistent misspelling of "convert" in variable and function names throughout the codebase.

---

## Grading Rubric

| Category | Points Possible | Points Earned | Notes |
|---|---|---|---|
| Functionality & Completeness | 30 | 27 | Works correctly for all three unit types; no real-time update |
| Code Quality & Organization | 25 | 20 | Clean logic; naming typos appear ~6 times |
| Design & Styling | 20 | 19 | Strong CSS — variables, responsive, professional purple header |
| Documentation | 15 | 12 | No README; inline comments are adequate |
| Testing | 10 | 8 | No tests; simple logic, low risk |

**Total: 86 / 100 → B+**

---

## What Was Done Well

### CSS Variables for Theming
Defining colors and spacing as custom properties (`--primary`, `--shadow`, etc.) makes the stylesheet easy to maintain and restyle. Good habit.

### Three Conversions Rendered at Once
Showing length, volume, and mass side by side from a single input is good UX — users get everything in one click without switching modes.

### Accessibility
`aria-label` on the input and proper `<label>` elements are present. The purple header has sufficient contrast. These are easy to skip and you didn't.

### Conversion Precision
Formatting to 3 decimal places is the right call — enough precision to be useful, not so many digits it looks noisy.

### Bidirectional Results
Showing both directions (e.g., "5 meters = 16.404 feet" AND "5 feet = 1.524 meters") in the same card is a smart design choice.

---

## Areas for Improvement

### 1. Naming Typos — Fix These (Easy)
The word "convert" is misspelled across multiple identifiers:

| Current | Should Be |
|---|---|
| `numberCoverter` | `numberConverter` |
| `covertNumber` | `convertNumber` |
| `renderHmtl` | `renderHtml` |
| `covertbtn` | `convertBtn` |

A find-and-replace across `index.js` and `index.html` would fix all of them. This is the single biggest thing holding back an otherwise clean codebase.

### 2. No Real-Time Conversion (Low)
Converting only on button click is functional, but adding an `input` event listener so results update as the user types would feel more modern:

```js
numberInput.addEventListener('input', () => renderHtml(numberInput.value));
```

### 3. NaN Silently Displays (Low)
If the user enters a letter, `parseFloat()` returns `NaN` and `NaN × 3.281 = NaN` renders in the output. Add a guard:

```js
if (isNaN(value)) { /* show "Please enter a valid number" */ return; }
```

### 4. Accidental `er.name` File in Directory
There's a file named `er.name` in the project folder that appears to be a stray git config artifact. Delete it.

---

## Final Notes

This is a complete, working project with solid CSS and correct math. The typos are disproportionately damaging to readability for how easy they are to fix. Clean those up and add a NaN guard and this is a solid A.

**Grade: B+ (86/100)**
