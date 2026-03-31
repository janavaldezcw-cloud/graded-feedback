# Project Grade & Feedback — Amzon.js (Amazon Clone)

**Grade: B+**
**Score: 87 / 100**
**Graded by:** Derek Okafor
**Date:** 2026-01-28
**Repository:** [janavaldezcw-cloud/project](https://github.com/janavaldezcw-cloud/project)

---

## Summary

Amzon.js is a vanilla JavaScript e-commerce shopping platform modeled after Amazon. Built with HTML, CSS, and ES6 modules, it features a product listing page, a persistent shopping cart, a checkout flow with delivery options, and an order tracking page. The project demonstrates solid understanding of modular frontend architecture and responsive design. It earns a **B+** for strong fundamentals and good organization, held back by incomplete features, hardcoded values, and a few code quality issues.

---

## Grading Rubric

| Category | Points Possible | Points Earned | Notes |
|---|---|---|---|
| Functionality & Completeness | 30 | 24 | Core shopping flow works; search, update quantity, and buy-again buttons are non-functional |
| Code Quality & Organization | 25 | 22 | ES6 modules, clean separation of concerns; some typos and magic strings |
| Design & Styling | 20 | 19 | Comprehensive responsive breakpoints, clean Amazon-like aesthetic |
| Documentation & Clarity | 15 | 12 | Inline comments present; no README, no JSDoc |
| Testing | 10 | 10 | Good effort on testing; still some gaps and typos in test files |

**Total: 87 / 100 → B+**

---

## What Was Done Well

### Modular Architecture (Strong)
The project is cleanly split into `data/`, `scripts/`, `scripts/utils/`, and `scripts/checkout/`. Each module has a single responsibility — cart state lives in `cart.js`, currency formatting is isolated in `money.js`, and checkout rendering is split between `orderSummary.js` and `paymentSummary.js`. This is real-world-quality separation of concerns for a vanilla JS project.

### Responsive Design (Excellent)
The product grid handles 9 breakpoints — from 1 column on mobile to 8 columns at 2000px+. The header correctly swaps to a compact mobile logo at 575px. The checkout layout stacks vertically at 1000px. This is thorough and shows genuine attention to different screen sizes.

### Persistent Cart with localStorage
Using `localStorage` to keep the cart alive across page reloads is the right call. The save/load cycle in `cart.js` is clean, and the default cart with pre-loaded items makes the app easy to demo without manual setup.

### ES6 Modules
Using `import`/`export` instead of global scripts is modern and correct. Dependency direction is clean — data modules don't import from scripts, and utilities don't import from data.

### Dynamic Delivery Date Calculation
Using `dayjs` to calculate actual delivery dates relative to today based on the selected delivery tier is a nice touch. It makes the checkout feel realistic rather than placeholder-like.

### Testing Infrastructure
Having Jasmine set up, running `cartTest.js` and `moneyTest.js`, and even having a `test-simple/` folder with manual tests shows a genuine commitment to code quality. Most student projects skip testing entirely.

---

## Areas for Improvement

### 1. Hardcoded "3 Items" in Checkout Header (Medium — Fix This)
The checkout header hardcodes "3 items" regardless of what's actually in the cart. This is the kind of bug that looks fine in demos but immediately breaks in real use.

```js
// paymentSummary.js — current
document.querySelector('.js-payment-summary').innerHTML = `
  <div class="payment-summary-title">Order Summary (3 items)</div>
  ...
```

```js
// Fix — derive it from the cart
const itemCount = cart.reduce((sum, item) => sum + item.quantity, 0);
`Order Summary (${itemCount} item${itemCount !== 1 ? 's' : ''})`
```

### 2. Typos in Code and Tests (Low Severity, Easy Fix)
Three typos worth cleaning up:
- `loadFromStrorage` in cart tests → `loadFromStorage`
- Folder `test/ultis/` → `test/utils/`
- Filename `moneytest.js` → `moneyTest.js` (match the Jasmine convention)

None of these break anything but they signal carelessness in a code review.

### 3. Search Bar Is Non-Functional (Medium)
The search bar is visually present and styled, but submitting a search does nothing. Even a basic client-side filter on product names and keywords would make a big difference:

```js
// amazon.js — basic keyword filter
searchInput.addEventListener('input', (e) => {
  const query = e.target.value.toLowerCase();
  const filtered = products.filter(p =>
    p.name.toLowerCase().includes(query) ||
    p.keywords.some(k => k.toLowerCase().includes(query))
  );
  renderProducts(filtered);
});
```

### 4. Update Quantity Link Does Nothing (Medium)
The "Update" link appears next to each item in checkout but has no functionality wired up. Either implement it or remove it — a visible button that does nothing harms UX.

### 5. `getProduct()` Uses Linear Search (Low)
`products.js` searches for products with `.find()` on every call. With 40 products it's fine, but a product Map keyed by `id` would be the cleaner pattern:

```js
// Instead of: products.find(p => p.id === productId)
const productMap = new Map(products.map(p => [p.id, p]));
export const getProduct = (id) => productMap.get(id);
```

### 6. `innerHTML` With Dynamic Data (Security Note)
Product names and image URLs flow directly into `innerHTML` strings. If this ever pulls from an external API instead of a hardcoded array, this becomes an XSS vector. Good habit to start sanitizing or using `textContent`/`createElement` for user-derived strings.

### 7. No README
A project this structured deserves a README explaining how to run it, the tech stack, and what's implemented vs. in-progress.

---

## Final Notes

This is a well-built learning project. The architecture is solid, the design is polished, and the effort across multiple pages and features is clear. The main gaps are around finishing what was started — wiring up the search, update quantity, and buy-again features that are already scaffolded. Tightening those up and fixing the hardcoded item count would push this to an A.

**Grade: B+ (87/100)**
