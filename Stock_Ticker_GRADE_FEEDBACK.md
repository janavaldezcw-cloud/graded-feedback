# Project Grade & Feedback — Stock Ticker

**Grade: B**
**Score: 83 / 100**
**Graded by:** Aiden Tran
**Date:** 2025-07-30
**Repository:** [janavaldezcw-cloud/project](https://github.com/janavaldezcw-cloud/project)

---

## Summary

Stock Ticker is a real-time (simulated) stock price display that updates every second. It shows a price card for "QtechAI" (symbol QTA) with a directional indicator (▲/▼/▷) based on price movement. The code is cleanly modular — `fakeStockAPI.js` is separated from the rendering logic — and uses ES6 imports correctly. The mock data is fully random (0–100), which makes the ticker behave erratically, but the core architecture is solid.

---

## Grading Rubric

| Category | Points Possible | Points Earned | Notes |
|---|---|---|---|
| Functionality & Completeness | 30 | 25 | Works as described; limited to one hardcoded stock |
| Code Quality & Organization | 25 | 22 | Good module separation; minor unused CSS selector |
| Design & Styling | 20 | 17 | Clean card UI; could use more visual polish |
| Documentation | 15 | 11 | No README or comments |
| Testing | 10 | 8 | No tests; straightforward enough to not need many |

**Total: 83 / 100 → B**

---

## What Was Done Well

### Clean Module Separation
Splitting the mock API into its own file (`fakeStockAPI.js`) is the right instinct. If this were a real app, swapping in a real API would only require changing that one file.

### Directional Indicator Logic
Comparing `currentPrice` to `previousPrice` and displaying ▲/▼/▷ is a nice touch. The state tracking with a module-level `previousPrice` variable is simple and effective.

### ES6 Module Syntax
`import`/`export` used correctly across files. Clean dependency direction (main imports API, API doesn't import anything).

---

## Areas for Improvement

### 1. Mock Price Is Purely Random (Medium)
`Math.random() * 100` produces prices that jump wildly every second — $3.47 to $98.12 to $22.08. Real stock prices move in small increments. A more realistic simulation would be:

```js
// Simulate ±5% change per tick instead of pure random
export function getRandomPrice(previous) {
  const change = (Math.random() - 0.5) * 0.1; // ±5%
  return Math.max(0.01, previous * (1 + change));
}
```

### 2. Hardcoded to One Stock (Low)
The symbol, company name, and initial price are all hardcoded. Even a small array of a few fake stocks with a dropdown would make this much more interesting to demo.

### 3. Unused CSS Selector
`#price-icon` is in the stylesheet but doesn't appear in the HTML. Remove it.

### 4. No Error Handling or Loading State
The `setInterval` starts immediately with no initial load state. A brief "Fetching..." placeholder before the first tick would be a small improvement.

---

## Final Notes

This is a functional, cleanly architected project. The real-time update loop works, the modular split is correct, and the directional indicator adds genuine value. The main upgrade path is making the mock data more realistic and supporting multiple tickers.

**Grade: B (83/100)**
