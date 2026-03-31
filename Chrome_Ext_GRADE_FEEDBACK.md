# Project Grade & Feedback — Chrome Ext (URL/Link Saver)

**Grade: C-**
**Score: 65 / 100**
**Graded by:** Priya Nair
**Date:** 2025-09-12
**Repository:** [janavaldezcw-cloud/project](https://github.com/janavaldezcw-cloud/project)

---

## Summary

Chrome Ext is an early-stage Chrome extension attempt that lets users type and save URLs to an in-memory array. The concept is sound, but the implementation is incomplete in several critical ways: it's missing the `manifest.json` file required to run as an actual Chrome extension, saved links only exist in memory (gone on refresh), there's no way to view saved links in the UI, and the JavaScript file ends with garbage data ("11 12 51"). This reads as a learning exercise that was abandoned partway through.

---

## Grading Rubric

| Category | Points Possible | Points Earned | Notes |
|---|---|---|---|
| Functionality & Completeness | 30 | 14 | Saves to array only; no display, no persistence, no manifest |
| Code Quality & Organization | 25 | 18 | Readable but redundant; garbage at end of JS file |
| Design & Styling | 20 | 16 | Clean green/white theme; functional enough for a simple popup |
| Documentation | 15 | 10 | No README, no comments |
| Testing | 10 | 7 | No tests |

**Total: 65 / 100 → C-**

---

## What Was Done Well

### Clean HTML Structure
The HTML is minimal and readable. The input + button layout is appropriate for a browser extension popup.

### Basic Event Handling
Wiring a button click to push to an array shows correct understanding of DOM event listeners and basic JavaScript data structures.

### Styling
The green accent color and clean layout are appropriate for an extension popup. It doesn't look bad.

---

## Areas for Improvement

### 1. Missing `manifest.json` — This Isn't a Chrome Extension Yet
The single most critical omission. Chrome extensions require a `manifest.json` to declare the extension name, version, permissions, and entry point. Without it, this folder is just an HTML page — you cannot load it as an extension in Chrome.

Minimum `manifest.json` needed:
```json
{
  "manifest_version": 3,
  "name": "Link Saver",
  "version": "1.0",
  "action": {
    "default_popup": "index.html"
  }
}
```

### 2. No Persistence — All Saved Links Are Lost on Close
The `myLeads` array lives in memory. When the popup closes (which happens every time you click away), all saved links vanish. Use `chrome.storage.local` or `localStorage`:

```js
// Save
localStorage.setItem('myLeads', JSON.stringify(myLeads));

// Load on startup
const saved = localStorage.getItem('myLeads');
if (saved) myLeads = JSON.parse(saved);
```

### 3. No Display — Users Can't See What They Saved
Saved links are only logged to the console. There should be a `<ul>` or `<ol>` that renders each saved link as a clickable `<a>` tag below the input.

### 4. Garbage Data at End of JS File
The file ends with `11 12 51` — stray text that will throw a syntax error. Delete it.

### 5. Redundant Loop
`console.log(myLeads)` already prints the full array. The `for` loop after it that logs each item individually is redundant.

---

## Final Notes

This is a reasonable starting point for a first extension project. The core idea is good and the basic event wiring is correct. Finish it: add `manifest.json`, persist with `localStorage`, and render the saved links as a list. Those three changes would move this from a broken demo to a genuinely usable tool.

**Grade: C- (65/100)**
