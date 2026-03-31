# Project Grade & Feedback — Tic-tac-toe

**Grade: D-**
**Score: 55 / 100**
**Graded by:** Zoe Hartmann
**Date:** 2025-11-19
**Repository:** [janavaldezcw-cloud/project](https://github.com/janavaldezcw-cloud/project)

---

## Summary

Tic-tac-toe has a clear architectural vision — factory functions for `Gameboard`, `Cell`, and `GameController` — but the implementation is incomplete and contains critical JavaScript errors that prevent it from running at all. The HTML file is an empty shell with just a script tag, the CSS file is completely empty, there are no click handlers, no win condition checks, and no UI rendering. The README is blank. This is an early draft that needs significant work.

---

## Grading Rubric

| Category | Points Possible | Points Earned | Notes |
|---|---|---|---|
| Functionality & Completeness | 30 | 8 | Game does not run; no UI, no win detection, no interaction |
| Code Quality & Organization | 25 | 18 | Good factory function pattern; critical logic bugs present |
| Design & Styling | 20 | 8 | HTML shell only; CSS is empty |
| Documentation | 15 | 11 | README exists but is blank |
| Testing | 10 | 10 | No tests expected at this stage |

**Total: 55 / 100 → D-**

---

## What Was Done Well

### Factory Function Architecture (Good Instinct)
Using factory functions (`Gameboard()`, `Cell()`, `GameController()`) instead of classes or global variables shows awareness of encapsulation. This is the right pattern for a project like this.

### 2D Array for the Board
Representing the game board as a nested array is correct. Tracking `availableCells` alongside it is good thinking.

---

## Critical Bugs

### Bug 1: `switchPlayerTurn()` Comparison Is Broken
```js
// Line 65 — this always evaluates to true (object === itself)
if (activePlayer === activePlayer[0]) { ... }

// Fix — compare against one player
if (activePlayer === players[0]) {
  activePlayer = players[1];
} else {
  activePlayer = players[0];
}
```

### Bug 2: `activePlayer` Used Before `players` Is Defined
`activePlayer` is initialized to `players[0]` at function scope, but `players` is defined a few lines below — this causes a `ReferenceError` at runtime. Define `players` first, then `activePlayer`.

---

## What's Missing

To make this a working game, the following still needs to be built:

1. **HTML board** — 9 clickable cells rendered from the `Gameboard` array
2. **Click handlers** — each cell click should call `play(row, col)` and re-render
3. **Win condition check** — check all rows, columns, and two diagonals after each move
4. **Turn display** — show whose turn it is
5. **Game reset** — button to start a new game

---

## Final Notes

The foundation is architecturally sound — factory functions, encapsulated state, a `GameController` that manages flow. None of that needs to be thrown away. Fix the two bugs, add the HTML grid, wire up click events, and implement the win check. The hardest conceptual work (how to structure the code) is mostly done.

**Grade: D- (55/100)**
