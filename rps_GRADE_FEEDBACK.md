# Project Grade & Feedback — RPS (Rock-Paper-Scissors)

**Grade: A-**
**Score: 90 / 100**
**Graded by:** Darius Cheng
**Date:** 2025-10-28
**Repository:** [janavaldezcw-cloud/project](https://github.com/janavaldezcw-cloud/project)

---

## Summary

RPS is a pure-logic Rock-Paper-Scissors engine with no UI — just a single `rps.js` file. What makes it stand out is the quality of the JavaScript design: a factory function that encapsulates game state, immutable score objects returned via spread, case-insensitive input handling, input validation with proper error throwing, and a clean data-driven beat relationship map. This is well beyond what most beginners produce for this problem.

---

## Grading Rubric

| Category | Points Possible | Points Earned | Notes |
|---|---|---|---|
| Functionality & Completeness | 30 | 25 | Game logic complete and correct; no UI layer |
| Code Quality & Organization | 25 | 24 | Factory pattern, immutability, clean encapsulation; one typo |
| Design & Architecture | 25 | 24 | Excellent — data-driven beat map, pure functions, factory pattern |
| Documentation | 10 | 10 | Logic is self-documenting; clean naming |
| Testing | 10 | 7 | No tests; structure is highly testable |

**Total: 90 / 100 → A-**

---

## What Was Done Well

### Factory Function Pattern
`createGame()` returns an object with a `play()` method and a `getScore()` method. Game state (score, history) is fully encapsulated — nothing leaks to global scope. This is clean, professional JavaScript.

### Immutable Score Returns
```js
return { ...score }; // returns a copy, not a reference
```
Returning a copy of the score object prevents the caller from accidentally mutating internal state. Small detail, big difference.

### Data-Driven Beat Map
```js
const beats = { rock: 'scissors', scissors: 'paper', paper: 'rock' };
```
Instead of a chain of if-else statements, using an object as a lookup table is elegant and easy to extend (if you ever wanted to add lizard/Spock).

### Input Validation with Error Throwing
```js
if (!['rock', 'paper', 'scissors'].includes(move)) {
  throw new Error('Invalid move');
}
```
Throwing on invalid input is the correct approach for a library-style module. The caller can decide how to handle it.

### Case-Insensitive Input
`move.toLowerCase()` before comparison means `'Rock'`, `'ROCK'`, and `'rock'` all work. Always the right choice for user-facing input.

---

## Areas for Improvement

### 1. No UI (Most Impactful Gap)
The game logic is complete — what's missing is a way to actually play it. Even a minimal HTML page with three buttons and a result display would let someone actually experience the game. The `play()` method is already perfectly shaped to hook into DOM click events.

### 2. Typo: `computerVaule` → `computerValue`
One variable name. Quick fix.

### 3. Redundant `playRound()` Function
There are two ways to play: the module-level `playRound()` function and `createGame().play()`. They do the same thing but `playRound()` creates a new score object each time (no persistence). Pick one and remove the other.

### 4. High Value of Testing This Code
The factory pattern makes this extremely testable — `createGame()` creates fresh isolated state. Writing Jasmine or Jest tests for win/loss/draw outcomes, score accumulation, and invalid input handling would take 20 minutes and significantly increase confidence in the logic.

---

## Final Notes

This is the best pure-JavaScript logic file in the portfolio. The architecture choices — factory function, immutable returns, data-driven lookup — are things developers learn from reading good code or getting code-reviewed. Build the UI and add tests and this is a complete, impressive project.

**Grade: A- (90/100)**
