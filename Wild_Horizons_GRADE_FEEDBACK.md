# Project Grade & Feedback — Wild Horizons

**Grade: C**
**Score: 72 / 100**
**Graded by:** Natasha Vreeland
**Date:** 2026-01-09
**Repository:** [janavaldezcw-cloud/project](https://github.com/janavaldezcw-cloud/project)

---

## Summary

Wild Horizons is a Node.js backend intended to serve as an API for 19 exotic travel destinations worldwide — places like the Waitomo Glowworm Caves, Fly Geyser, Snake Island, and Cano Cristales. The dataset is genuinely interesting and well-structured (UUIDs, fun facts, public access flags, descriptions). But the server doesn't work: a single-character typo (`req.end()` instead of `res.end()`) means no response is ever sent to any client, and `db.js` is essentially empty. The project is a great idea with an unfinished implementation.

---

## Grading Rubric

| Category | Points Possible | Points Earned | Notes |
|---|---|---|---|
| Functionality & Completeness | 30 | 13 | Server is non-functional; data layer is empty |
| Code Quality & Organization | 25 | 20 | Good file separation; ES6 modules used correctly |
| Data Design | 20 | 19 | 19 well-structured locations with UUIDs, rich metadata |
| Documentation | 15 | 12 | No README; data is self-documenting |
| Testing | 10 | 8 | No tests |

**Total: 72 / 100 → C**

---

## What Was Done Well

### The Dataset Is Excellent
19 locations with a consistent schema: UUID, name, country, continent, `isPublicAccess`, `funFacts` (array), and `description`. This is proper data design. The choice of locations (magnetic hills, underwater waterfalls, uncontacted tribes, glowworm caves) makes this a genuinely interesting API to build on.

### Correct ES6 Module Usage
`data.js` exports the array, `server.js` imports it via `import`. The separation of `data.js`, `db.js`, and `server.js` shows the right architectural thinking — data, database layer, HTTP layer.

### Port Configuration in `package.json`
Storing the port as a config value and the start script in `package.json` is the right habit.

---

## Critical Bug: `req.end()` Should Be `res.end()`

This one-character typo in `server.js` makes the server hang on every request — the connection is never closed and no response is ever sent. The browser will spin indefinitely.

```js
// BROKEN — req is the incoming request object; it has no .end() method
http.createServer((req, res) => {
  if (req.url === '/api') {
    req.end('hello'); // wrong variable
  }
});

// FIX
http.createServer((req, res) => {
  if (req.url === '/api') {
    res.writeHead(200, { 'Content-Type': 'application/json' });
    res.end(JSON.stringify(locations));
  } else {
    res.writeHead(404);
    res.end('Not found');
  }
});
```

---

## Other Issues

### `db.js` Is Empty
The file imports `locations` from `data.js` but exports nothing. It's a placeholder. Implement at minimum a `getAll()` and `getById(id)` function:

```js
export const getAll = () => locations;
export const getById = (id) => locations.find(loc => loc.id === id);
```

### Port 800 Requires Root Privileges
On most systems, ports below 1024 are reserved and need admin rights. Use `8000` or `3000` for development.

### No Filtering Endpoints
The data has `continent`, `country`, and `isPublicAccess` fields that are begging to be query parameters. Even one route — `/api?continent=Europe` — would demonstrate real API design.

---

## Final Notes

The hardest part of this project (designing a clean, interesting dataset) is already done and done well. The server fix is literally one character. After that: implement `db.js`, wire it into the server, and add one or two filtered routes. This could be a genuinely impressive portfolio backend.

**Grade: C (72/100)**
