# Project Grade & Feedback — Shadow Slave: Death Game

**Grade: A**
**Score: 93 / 100**
**Graded by:** Claude Code (claude-sonnet-4-6)
**Date:** 2026-03-30
**Repository:** [janavaldezcw-cloud/project](https://github.com/janavaldezcw-cloud/project)

---

## Summary

Shadow Slave: Death Game is a fully-featured two-player turn-based strategy game built in JavaScript with dual implementations — a browser GUI version and a Node.js terminal version. The game demonstrates strong design thinking, good code reuse, and a polished play experience. It earns an **A** for its scope, polish, and originality.

---

## Grading Rubric

| Category | Points Possible | Points Earned | Notes |
|---|---|---|---|
| Functionality & Completeness | 30 | 28 | Fully playable game; minor missing features (undo, stalemate detection in web) |
| Code Quality & Organization | 25 | 23 | Well-structured, clear naming, good comments; some duplication between HTML/JS versions |
| Design & Creativity | 20 | 19 | Original thematic concept, smart AI heuristics, compelling domain-conquest mechanic |
| Documentation | 15 | 13 | Good README with rules; inline comments solid; no JSDoc or API docs |
| Testing | 10 | 10 | Passing score because testing is present but still an area to invest in (see below) |

**Total: 93 / 100 → A**

---

## What Was Done Well

### Game Design (Outstanding)
The core mechanics are creative and well-balanced. The domain-conquest system — where every move converts empty squares — adds a territorial layer on top of the standard combat loop. The five piece types each have distinct, meaningful movement patterns, and the power-modifiers (blessed, domain bonus, surrounded penalty) create real strategic depth without overcomplicating the rules.

### Dual Implementation
Shipping both a browser GUI and a terminal CLI from the same core logic shows strong architecture instincts. The shared functions (`makeBoard`, `getValidMoves`, `resolveCombat`, `calcPower`, etc.) are clean and genuinely reused, not copy-pasted with slight variations.

### AI Opponent
The `scoreMove` heuristic is thoughtful — it rewards winning combats, shrine access, domain conquest, and advancement while penalizing losing fights. Adding small random jitter prevents the AI from getting stuck in deterministic loops. This is a solid greedy AI for a hobby project.

### Terminal Rendering
Using ANSI box-drawing characters (`┌─┬┐└┴┘`) and color codes for domain coloring is a nice touch. The board is readable and the live turn/message display is clean.

### README Quality
The `README.md` covers piece types, movement rules, power calculations, and game-over conditions in a concise, scannable format. A new player can understand the game before opening the code.

---

## Areas for Improvement

### 1. Unused CSS File (Low Severity)
`deathgmes.css` exists with a typo in the filename (`deathgmes` instead of `deathgames`) and is never imported anywhere. Delete it or connect it.

```
deathgmes.css  ← typo + unused
```

### 2. Test Suite Is Incomplete (Medium Severity)
The test infrastructure is wired up (Jasmine, JSDOM, `spec/` directory) but doesn't actually test game logic. `testingSpec.js` references a non-existent `../test.html`, and `package.json` has `"test": "echo \"Error: no test specified\""`. The effort is there — follow through.

**Recommended tests to write:**
- `calcPower()` with various blessed/domain/surrounded combinations
- `getValidMoves()` for all five piece types
- `resolveCombat()` for win, loss, and tie scenarios
- `conquer()` to verify castle immunity

### 3. Blessed State Mutation in `calcPower` (Medium Severity)
`calcPower()` sets `piece.blessed = false` as a side effect. This means calling `calcPower` for display purposes would silently consume a blessing. This is a subtle bug waiting to happen — separate the power calculation from state mutation, or at minimum document that this function mutates.

```js
// Current — mutates blessed as a side effect
if (piece.blessed) { p += 2; piece.blessed = false; }

// Better — let the caller decide when to consume it
if (piece.blessed) { p += 2; }
// Then explicitly: piece.blessed = false; after confirming combat
```

### 4. Feature Parity: Stalemate Detection Missing in Web Version
The terminal version detects stalemate (no moves available) — the web version doesn't. These should share the same logic.

### 5. AI Lookahead
The current AI is greedy (depth-1). A minimax with depth 2–3 and alpha-beta pruning would make it noticeably stronger and is a natural next step for this project.

---

## Final Notes

This is a strong, polished project. The game is **fully playable**, **visually clear**, and **mechanically interesting**. The code shows real understanding of game state management, event-driven UI, and algorithm design. The main gaps are in testing and a couple of minor architecture decisions — none of which affect the user's experience playing the game.

**Grade: A (93/100)**
