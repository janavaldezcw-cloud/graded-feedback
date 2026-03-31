# Project Grade & Feedback — Leetcode Practice

**Grade: B**
**Score: 82 / 100**
**Graded by:** Sofia Delgado
**Date:** 2026-01-15
**Repository:** [janavaldezcw-cloud/project](https://github.com/janavaldezcw-cloud/project)

---

## Summary

This folder contains 10 LeetCode solutions (9 Easy, 1 Medium) written in JavaScript. The standout feature is that most problems include multiple solutions showing an evolution from brute-force to optimized — that's exactly the right way to practice algorithms. Code quality is generally solid, with a few typos and one legitimately buggy solution. Overall this is a healthy, consistent practice record.

---

## Grading Rubric

| Category | Points Possible | Points Earned | Notes |
|---|---|---|---|
| Correctness | 35 | 28 | Most solutions correct; Remove Element has a real bug; twoSums missing optimal |
| Optimization & Complexity | 25 | 20 | Good awareness of trade-offs; not all problems show optimal final solution |
| Code Clarity | 20 | 18 | Readable; a few typos and stray comments ("Help solution") |
| Problem Coverage | 10 | 9 | Good spread of problem types; only one Medium |
| Consistency | 10 | 7 | Files don't follow a consistent structure |

**Total: 82 / 100 → B**

---

## What Was Done Well

### Multiple Solutions Per Problem (Excellent Habit)
Several files (Contains Duplicate, Roman to Integer, Palindrome Number, Running Sum) show two or three approaches with increasing efficiency. This is exactly the right way to practice — solve it first, then ask "can I do better?" The progression from O(n²) to O(n) using a Set in Contains Duplicate is a perfect example.

### Valid Parentheses — Best Solution in the Set
The stack-based approach is correct, clean, and efficient. `push` on open brackets, check `pop` on close brackets — no unnecessary complexity.

### Roman to Integer — HashMap Approach
The second solution using a `Map` for O(1) lookups is elegant. Handling subtractive notation (IV, IX) by checking the next character is the right algorithm.

---

## Areas for Improvement

### 1. Remove Element — First Solution Has a Bug (Medium)
Using `splice()` inside a `for` loop that iterates by index is a classic mistake. Splicing shifts all subsequent elements left, so the loop skips elements. The second solution (two-pointer) is correct — but the first one shouldn't be left in as a "try" without a comment noting it's broken.

```js
// BUGGY — splice shifts indices, elements get skipped
for (let i = 0; i < nums.length; i++) {
  if (nums[i] === val) nums.splice(i, 1);
}
```

### 2. Two Sum — Only O(n²) Solution, Missing Hash Map
`twoSums.js` only has the nested-loop brute force. For a problem this famous, the HashMap solution (O(n) time) is the one interviewers expect. Add it:

```js
function twoSum(nums, target) {
  const map = new Map();
  for (let i = 0; i < nums.length; i++) {
    const complement = target - nums[i];
    if (map.has(complement)) return [map.get(complement), i];
    map.set(nums[i], i);
  }
}
```

### 3. Typos Worth Fixing
- `nums.legnth` → `nums.length` in Running Sum
- `"soultion"` → `"solution"` in multiple comments
- Integer to Roman file appears cut off mid-solution

### 4. Progress to More Medium Problems
9 out of 10 problems are Easy. Sliding Window, Dynamic Programming, and Tree traversal problems would round this out. Aim for a 60/40 Easy/Medium split.

---

## Final Notes

This is a solid practice folder. The habit of writing multiple solutions and thinking about optimization is more valuable than raw problem count. Fix the Remove Element bug, add the Two Sum hash map solution, and keep grinding Mediums.

**Grade: B (82/100)**
