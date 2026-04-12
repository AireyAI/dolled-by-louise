# Dolled by Louise — Full Site Update Design

**Date:** 2026-04-12  
**Scope:** All three pages — `index.html`, `marketplace.html`, `welcome.html`  
**Approach:** Page by page. Design + features on each page, Lighthouse tested before each push. Chatbot/Railway deployment is out of scope.

---

## Design Direction

Keep existing direction unchanged:
- Dark plum hero (`#130a10`) + blush/rose body (`#fdf8f5`)
- Fonts: Playfair Display + Cormorant Garamond + DM Sans
- Design tokens: `--rose: #c2688e`, `--base: #fdf8f5`, `--plum: #2d1423`, `--gold: #c9956a`
- Alternating dark/light page rhythm maintained

---

## Skills In Use

| Skill | Purpose |
|-------|---------|
| `ui-ux-pro-max` | Design quality pass — spacing, shadows, hover states |
| `awesome-claude-skills:world-class-web-design` | Production craft standards |
| `awesome-claude-skills:website-features` | SEO, PWA, accessibility, analytics |
| `awesome-claude-skills:webapp-testing` | Playwright + Lighthouse audit |
| Nano Banana 2 MCP | Generate real images (hero, gallery, products) |
| Veo2 MCP | Hero video background on index.html |
| context7 MCP | Live library docs for Tailwind, GSAP etc. |
| Obsidian vault | Brand notes and client briefs |

---

## Step 0 — Housekeeping

Commit the unstaged `index.html` (body sections redesign: stats bar, services cards, asymmetric gallery, testimonials, dark CTA banner, dark footer) as a clean baseline before any new work.

---

## Step 1 — index.html

### Design Pass

- **ui-ux-pro-max + world-class-web-design** review: tighten spacing tokens, shadow layering system, and hover/focus states across all sections
- Move social proof (star rating + review count) directly under hero CTAs — currently too far from the action
- Generate new hero background image with Nano Banana 2: dark plum, bokeh lash close-up, cinematic mood
- Generate gallery section images with Nano Banana 2: styled lash work photos with rose tint treatment
- Veo2: generate hero video background — dark cinematic lash close-up, deep plum tones, slow motion. Fallback: if Veo2 generation fails, use the Nano Banana 2 static hero image instead; hero must never be empty

### Features Pass

- `og:image` meta tag — fixes missing previews on WhatsApp/Instagram shares
- `theme-color` meta — matches browser chrome to brand on mobile
- `sitemap.xml` — all three pages listed so Google can crawl them
- `FAQPage` JSON-LD schema — add a collapsible FAQ section to `index.html` (e.g. "How long do lashes last?", "What's included in the Lash Club?", "How do I book?") then apply the schema; this unlocks rich search results
- Exit intent modal — triggers on cursor-to-chrome: "Wait — grab 10% off your first booking" with email field
- Email capture strip — lead magnet: "Get our free lash aftercare guide"
- PWA `manifest.json` + service worker — enables Add to Home Screen on mobile; offline fallback page

### Audit + Push

Playwright: golden path test (hero CTAs, lash quiz, booking panel, Lash Club section, shop link)  
Lighthouse: performance, SEO, accessibility, PWA — fix all flags before push  
Commit + push to GitHub Pages

---

## Step 2 — marketplace.html

### Design Pass

- Product card hover: image scale (`transform: scale(1.04)`) + rose overlay + shadow lift
- Generate product images with Nano Banana 2: lash aftercare kit, foam cleanser, lash serum, spoolie set, lash pillow — styled to match brand palette
- "Only X left" scarcity label on 2–3 selected cards (e.g. Luxury Bundle, Lash Serum)
- Free shipping progress bar inside checkout modal: "Add £X more for free delivery"

### Features Pass

- Wishlist / save button on every product card — heart icon, toggled state persisted in `localStorage`
- Quick View modal — clicking product image opens detail panel without leaving the grid
- "You might also like" row inside checkout modal — 2–3 products from same category
- `og:image` + `theme-color` for the marketplace page

### Audit + Push

Playwright: product grid, quick view modal, checkout modal (Stripe/PayPal/WhatsApp), wishlist toggle  
Lighthouse: performance, SEO, accessibility — fix all flags before push  
Commit + push to GitHub Pages

---

## Step 3 — welcome.html

### Design Pass

- **ui-ux-pro-max** refinement: tighten lash eye SVG animation timing, smooth particle drift, ease the staggered text reveal
- Generate new atmospheric background with Nano Banana 2: deep plum, bokeh lashes, moody editorial

### Features Pass

- `og:image` + `theme-color` for the splash page
- Confirm sessionStorage welcome gate still works after any changes

### Audit + Push

Playwright: welcome gate loads, Enter button triggers curtain, redirects correctly to `index.html`  
Lighthouse: performance, accessibility — fix flags before push  
Commit + push to GitHub Pages

---

## Constraints

- Single `index.html` / `marketplace.html` / `welcome.html` files — all styles inline, no build step
- Tailwind CSS via CDN
- No backend changes (chatbot/Railway is separate)
- No colour or font changes — existing brand tokens only
- `node server.mjs` for local dev; screenshot via `node screenshot.mjs http://localhost:3000`
