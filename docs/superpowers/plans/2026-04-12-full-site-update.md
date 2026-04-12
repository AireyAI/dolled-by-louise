# Dolled by Louise — Full Site Update Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Update all three pages (index.html, marketplace.html, welcome.html) using ui-ux-pro-max, world-class-web-design, website-features, and webapp-testing skills — replacing placeholder images, adding missing SEO/PWA/conversion features, and tightening the design — shipping each page independently.

**Architecture:** Single-file pages, all styles inline, Tailwind CDN. New files: `sitemap.xml`, `manifest.json`, `sw.js`, `offline.html`. Page-by-page approach: full update + Lighthouse audit before each push.

**Tech Stack:** HTML/CSS/JS (vanilla), Tailwind CSS CDN, Nano Banana 2 MCP (images), Veo2 MCP (video), Lighthouse MCP, Playwright MCP, Context7 MCP

**Design tokens (do not change):** `--rose:#c2688e`, `--base:#fdf8f5`, `--plum:#2d1423`, `--gold:#c9956a`. Fonts: Playfair Display + Cormorant Garamond + DM Sans.

**Local dev:** `node server.mjs` → `http://localhost:3000`. Screenshots: `node screenshot.mjs http://localhost:3000`.

---

## PHASE 0 — Baseline Commit

### Task 1: Commit unstaged index.html body redesign

**Files:**
- Modify: `index.html` (already modified, unstaged)

- [ ] **Step 1: Stage and commit the existing body redesign**

```bash
cd /Users/kyleairey/Desktop/dolled-by-louise
git add index.html
git commit -m "Redesign index.html body sections — stats, services, gallery, testimonials, CTA, footer"
```

- [ ] **Step 2: Verify clean working tree**

```bash
git status
```
Expected: `nothing to commit, working tree clean`

---

## PHASE 1 — index.html

### Task 2: Invoke design skills for index.html

**Files:**
- Reference: `docs/superpowers/specs/2026-04-12-full-site-update-design.md`

- [ ] **Step 1: Invoke ui-ux-pro-max skill**

Use the `Skill` tool with `skill: "ui-ux-pro-max"`. Run the palette search for dark plum / blush rose lash salon. Apply recommendations to index.html — spacing tokens, shadow system, hover state audit.

- [ ] **Step 2: Invoke world-class-web-design skill**

Use the `Skill` tool with `skill: "awesome-claude-skills:world-class-web-design"`. Apply its production craft checklist to index.html.

---

### Task 3: Generate hero background image

**Files:**
- Output image URL from Nano Banana 2 → used in Task 5

- [ ] **Step 1: Generate image via Nano Banana 2 MCP**

Call `mcp__nano-banana-2__generate_image` with prompt:
```
Dark cinematic lash close-up. Deep plum and midnight purple background. Extreme macro shot of perfectly applied lash extensions — individual lashes sharp against bokeh lights. Rose-gold light glints. Editorial fashion photography. Ultra-high resolution. No text, no person, just lashes and mood.
```

- [ ] **Step 2: Save the returned image URL**

Record the URL — it will be used as the hero video fallback `poster` attribute and as the static `img` fallback in Task 5.

---

### Task 4: Generate gallery images

**Files:**
- Output 3 image URLs from Nano Banana 2 → used in Task 6

- [ ] **Step 1: Generate gallery image 1 — close-up lash work**

Call `mcp__nano-banana-2__generate_image` with prompt:
```
Extreme close-up of a woman's eye with perfect Russian Volume lash extensions. Rose-gold bokeh background. Deep plum colour grade. Editorial beauty photography. Ultra sharp lashes, no text.
```

- [ ] **Step 2: Generate gallery image 2 — lifestyle**

Call `mcp__nano-banana-2__generate_image` with prompt:
```
Elegant woman looking down, wearing flawless lash extensions. Blush and cream tones. Soft window light. High-end beauty salon aesthetic. Rose tint colour grade. No text.
```

- [ ] **Step 3: Generate gallery image 3 — product/tools**

Call `mcp__nano-banana-2__generate_image` with prompt:
```
Luxury lash salon flat lay. Rose gold tweezers, lash trays, cream and blush palette, delicate lash strips arranged artfully on a white marble surface. Soft pink and gold tones. No text.
```

- [ ] **Step 4: Save all three image URLs** for use in Task 6.

---

### Task 5: Generate and implement hero video background

**Files:**
- Modify: `index.html` (hero section ~line 1453)

- [ ] **Step 1: Generate hero video via Veo2 MCP**

Call `mcp__veo2__generateVideoFromText` with prompt:
```
Slow motion extreme macro of individual lash extensions. Deep plum and midnight purple background. Rose-gold light particles drift. Cinematic, dreamlike, luxury beauty. No person, no face, just lashes and bokeh lights. Ultra slow motion.
```

- [ ] **Step 2: Check if video generation succeeded**

If video URL returned → proceed to Step 3.
If generation fails → skip to Step 5 (use static image only).

- [ ] **Step 3: Add hero video background to index.html**

Inside the `<section id="hero">` block, directly after `<div class="hero-bg" aria-hidden="true"></div>` (~line 1454), add:

```html
<video
  class="hero-video-bg"
  src="VIDEO_URL_FROM_VEO2"
  poster="HERO_IMAGE_URL_FROM_TASK_3"
  autoplay muted loop playsinline
  aria-hidden="true"
></video>
```

Replace `VIDEO_URL_FROM_VEO2` and `HERO_IMAGE_URL_FROM_TASK_3` with actual URLs from Tasks 3 and 5 Step 1.

- [ ] **Step 4: Add hero video styles**

Inside the `<style>` block, after the `.hero-bg` rule, add:

```css
.hero-video-bg {
  position: absolute; inset: 0; width: 100%; height: 100%;
  object-fit: cover; z-index: 0; opacity: 0.18;
  pointer-events: none;
}
```

- [ ] **Step 5: (Fallback only — skip if video succeeded) Add static hero image**

If Veo2 failed, update `.hero-bg` in the `<style>` block to reference the Nano Banana 2 image from Task 3:

```css
.hero-bg {
  /* existing rules... */
  background-image: url('HERO_IMAGE_URL_FROM_TASK_3');
  background-size: cover;
  background-position: center;
  opacity: 0.15;
}
```

---

### Task 6: Replace gallery placeholder images

**Files:**
- Modify: `index.html` (gallery section ~line 1835)

- [ ] **Step 1: Find the three gallery `<img>` or placeholder tags**

In the `<section id="gallery">` block (~line 1842), locate the three image cells.

- [ ] **Step 2: Replace each placeholder with Nano Banana 2 URLs**

For each gallery cell image, update the `src` attribute to the URLs saved in Task 4 Steps 1–3. Maintain existing `alt` text and `loading="lazy"`.

---

### Task 7: Improve social proof display under hero CTAs

**Files:**
- Modify: `index.html` (~lines 1583–1596)

- [ ] **Step 1: Update the `.hero-meta` strip**

The current strip shows dots + text. Replace `.hero-meta` HTML (~line 1592) with a more prominent star-forward version:

```html
<div class="hero-meta">
  <span class="hero-meta-item">
    <span class="hero-meta-stars" aria-label="5 stars">★★★★★</span>
    <span class="hero-meta-label">5.0 · 100+ clients</span>
  </span>
  <span class="hero-meta-sep" aria-hidden="true">·</span>
  <span class="hero-meta-item">Fully Insured</span>
  <span class="hero-meta-sep" aria-hidden="true">·</span>
  <span class="hero-meta-item">Longtown, Cumbria</span>
</div>
```

- [ ] **Step 2: Update `.hero-meta` styles**

Replace the existing `.hero-meta-item` and `.hero-meta-dot` rules with:

```css
.hero-meta {
  display: flex; align-items: center; gap: 12px; flex-wrap: wrap;
  margin-top: 20px;
}
.hero-meta-item {
  display: flex; align-items: center; gap: 6px;
  font-size: 12px; font-weight: 400; color: rgba(252,232,240,0.7);
  letter-spacing: 0.04em;
}
.hero-meta-stars { color: var(--gold); font-size: 13px; letter-spacing: 2px; }
.hero-meta-label { color: rgba(252,232,240,0.85); font-weight: 500; }
.hero-meta-sep { color: rgba(252,232,240,0.3); font-size: 10px; }
```

---

### Task 8: Add og:image, theme-color, and canonical meta tags

**Files:**
- Modify: `index.html` (head section ~line 7)

- [ ] **Step 1: Add missing meta tags to `<head>`**

After the existing `<meta property="og:type" content="website">` line, add:

```html
<meta property="og:image" content="HERO_IMAGE_URL_FROM_TASK_3">
<meta property="og:url" content="https://dolledbylouise.co.uk">
<meta name="theme-color" content="#130a10">
<link rel="canonical" href="https://dolledbylouise.co.uk">
```

Replace `HERO_IMAGE_URL_FROM_TASK_3` with the Nano Banana 2 URL from Task 3.

---

### Task 9: Add FAQPage JSON-LD schema

**Files:**
- Modify: `index.html` (head section, existing `<script type="application/ld+json">` block ~line 16)

The FAQ section already exists at `#faq` with 5+ questions. Add a second JSON-LD block for it.

- [ ] **Step 1: Add FAQPage schema after the existing BeautySalon schema block**

After the closing `</script>` of the BeautySalon schema, add:

```html
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "FAQPage",
  "mainEntity": [
    {
      "@type": "Question",
      "name": "How long do lash extensions last?",
      "acceptedAnswer": {
        "@type": "Answer",
        "text": "Most clients come back for infills every 2–3 weeks. Your natural lash cycle means individual extensions shed gradually — infills top them back up."
      }
    },
    {
      "@type": "Question",
      "name": "Will extensions damage my natural lashes?",
      "acceptedAnswer": {
        "@type": "Answer",
        "text": "When applied correctly and maintained properly, no. Louise uses lightweight extensions matched to your natural lash strength and trains in safe application techniques."
      }
    },
    {
      "@type": "Question",
      "name": "How long does a lash lift last?",
      "acceptedAnswer": {
        "@type": "Answer",
        "text": "A lash lift typically lasts 6–8 weeks, depending on your natural lash growth cycle. A tint added at the same time darkens lashes for a mascara-free look."
      }
    },
    {
      "@type": "Question",
      "name": "What's the difference between Hybrid and Russian Volume?",
      "acceptedAnswer": {
        "@type": "Answer",
        "text": "Hybrid mixes classic (one extension per lash) and volume (fan of 2–6 lashes) for a textured, full look. Russian Volume is all fans — resulting in softer, fluffier, more dramatic fullness."
      }
    },
    {
      "@type": "Question",
      "name": "How do I book an appointment?",
      "acceptedAnswer": {
        "@type": "Answer",
        "text": "The easiest way is via WhatsApp — tap the button on this page to message Louise directly. You can also call or use the booking form on this page."
      }
    }
  ]
}
</script>
```

---

### Task 10: Add exit intent modal

**Files:**
- Modify: `index.html` (add styles + HTML + JS)

- [ ] **Step 1: Add exit intent modal styles**

In the `<style>` block, before the closing `</style>`, add:

```css
/* ── Exit Intent Modal ── */
#exit-modal {
  display: none; position: fixed; inset: 0; z-index: 10000;
  background: rgba(19,10,16,0.7); backdrop-filter: blur(6px);
  align-items: center; justify-content: center; padding: 24px;
}
#exit-modal.open { display: flex; }
.exit-modal-box {
  background: var(--surface); border: 1px solid var(--border);
  border-radius: 16px; padding: 48px 40px; max-width: 440px; width: 100%;
  text-align: center; position: relative;
  box-shadow: 0 8px 64px rgba(194,104,142,0.18), 0 2px 16px rgba(19,10,16,0.3);
}
.exit-modal-close {
  position: absolute; top: 16px; right: 16px; background: none; border: none;
  cursor: pointer; color: var(--muted); font-size: 20px; line-height: 1;
  padding: 4px 8px;
}
.exit-modal-close:hover { color: var(--rose); }
.exit-modal-offer {
  display: inline-block; background: var(--floating); color: var(--rose);
  font-size: 11px; font-weight: 600; letter-spacing: 0.1em; text-transform: uppercase;
  padding: 6px 16px; border-radius: 100px; margin-bottom: 20px;
}
.exit-modal-title {
  font-family: 'Playfair Display', serif; font-size: 28px; font-weight: 700;
  color: var(--plum); line-height: 1.2; margin-bottom: 12px;
}
.exit-modal-sub {
  font-size: 14px; color: var(--muted); line-height: 1.7; margin-bottom: 28px;
}
.exit-modal-form { display: flex; gap: 8px; }
.exit-modal-input {
  flex: 1; padding: 12px 16px; border: 1px solid var(--border); border-radius: 8px;
  font-size: 14px; font-family: 'DM Sans', sans-serif; background: #fff;
  color: var(--text);
}
.exit-modal-input:focus { outline: 2px solid var(--rose); outline-offset: 0; }
.exit-modal-btn {
  padding: 12px 20px; background: var(--rose); color: #fff; border: none;
  border-radius: 8px; font-size: 14px; font-weight: 500; cursor: pointer;
  white-space: nowrap;
  transition: background 0.2s var(--ease), transform 0.15s var(--spring);
}
.exit-modal-btn:hover { background: #a8567a; transform: translateY(-1px); }
.exit-modal-dismiss {
  display: block; margin-top: 16px; font-size: 12px; color: var(--muted);
  cursor: pointer; background: none; border: none; text-decoration: underline;
}
```

- [ ] **Step 2: Add exit intent modal HTML**

Directly before the closing `</body>` tag, add:

```html
<!-- ── Exit Intent Modal ── -->
<div id="exit-modal" role="dialog" aria-modal="true" aria-labelledby="exit-modal-title">
  <div class="exit-modal-box">
    <button class="exit-modal-close" onclick="closeExitModal()" aria-label="Close">✕</button>
    <span class="exit-modal-offer">✦ Before you go</span>
    <h2 class="exit-modal-title" id="exit-modal-title">Grab 10% off<br>your first booking</h2>
    <p class="exit-modal-sub">Drop your email and Louise will send your discount code. No spam — just lashes.</p>
    <form class="exit-modal-form" onsubmit="submitExitForm(event)">
      <input class="exit-modal-input" type="email" placeholder="your@email.com" required aria-label="Email address">
      <button class="exit-modal-btn" type="submit">Claim it</button>
    </form>
    <button class="exit-modal-dismiss" onclick="closeExitModal()">No thanks, I'll pay full price</button>
  </div>
</div>
```

- [ ] **Step 3: Add exit intent JavaScript**

In the `<script>` block, add:

```js
// Exit intent
(function() {
  let shown = false;
  function showExitModal() {
    if (shown || sessionStorage.getItem('exitDismissed')) return;
    shown = true;
    document.getElementById('exit-modal').classList.add('open');
  }
  function closeExitModal() {
    document.getElementById('exit-modal').classList.remove('open');
    sessionStorage.setItem('exitDismissed', '1');
  }
  function submitExitForm(e) {
    e.preventDefault();
    closeExitModal();
    // Louise can hook this to her email provider — for now just closes
  }
  document.addEventListener('mouseleave', function(e) {
    if (e.clientY <= 0) showExitModal();
  });
  window.closeExitModal = closeExitModal;
  window.submitExitForm = submitExitForm;
})();
```

---

### Task 11: Add email capture strip

**Files:**
- Modify: `index.html` (add section before `<section id="cta-banner">` ~line 2062)

- [ ] **Step 1: Add email capture styles**

In the `<style>` block, before `</style>`, add:

```css
/* ── Email Capture ── */
#email-capture {
  padding: 80px 40px; background: var(--elevated);
  border-top: 1px solid var(--border);
}
.ec-inner {
  max-width: 560px; margin: 0 auto; text-align: center;
}
.ec-label {
  display: inline-block; background: var(--floating); color: var(--rose);
  font-size: 11px; font-weight: 600; letter-spacing: 0.1em; text-transform: uppercase;
  padding: 6px 16px; border-radius: 100px; margin-bottom: 20px;
}
.ec-title {
  font-family: 'Playfair Display', serif; font-size: 28px; font-weight: 700;
  color: var(--plum); line-height: 1.25; margin-bottom: 12px;
}
.ec-sub {
  font-size: 14px; color: var(--muted); line-height: 1.7; margin-bottom: 32px;
}
.ec-form { display: flex; gap: 10px; justify-content: center; flex-wrap: wrap; }
.ec-input {
  flex: 1; min-width: 220px; padding: 14px 18px;
  border: 1px solid var(--border); border-radius: 10px;
  font-size: 14px; font-family: 'DM Sans', sans-serif;
  background: #fff; color: var(--text);
}
.ec-input:focus { outline: 2px solid var(--rose); outline-offset: 0; }
.ec-btn {
  padding: 14px 28px; background: var(--rose); color: #fff; border: none;
  border-radius: 10px; font-size: 14px; font-weight: 500; cursor: pointer;
  transition: background 0.2s var(--ease), transform 0.15s var(--spring);
}
.ec-btn:hover { background: #a8567a; transform: translateY(-2px); }
.ec-fine {
  margin-top: 14px; font-size: 11px; color: var(--muted);
}
```

- [ ] **Step 2: Add email capture HTML**

Directly before `<section id="cta-banner">` (~line 2062), add:

```html
<!-- ── Email Capture ── -->
<section id="email-capture" aria-label="Join the newsletter">
  <div class="ec-inner reveal">
    <span class="ec-label">✦ Free Guide</span>
    <h2 class="ec-title">Keep your lashes<br><em>looking flawless</em></h2>
    <p class="ec-sub">Get our free lash aftercare guide — everything you need to know to make your extensions last longer. Straight to your inbox.</p>
    <form class="ec-form" onsubmit="submitEmailCapture(event)">
      <input class="ec-input" type="email" placeholder="your@email.com" required aria-label="Your email address">
      <button class="ec-btn" type="submit">Send me the guide ✦</button>
    </form>
    <p class="ec-fine">No spam. Unsubscribe any time.</p>
  </div>
</section>
```

- [ ] **Step 3: Add email capture JS**

In the `<script>` block, add:

```js
function submitEmailCapture(e) {
  e.preventDefault();
  const btn = e.target.querySelector('.ec-btn');
  btn.textContent = '✓ On its way!';
  btn.style.background = '#4caf50';
  btn.disabled = true;
}
```

---

### Task 12: Create PWA files

**Files:**
- Create: `manifest.json`
- Create: `sw.js`
- Create: `offline.html`
- Modify: `index.html` (add `<link rel="manifest">` to head)

- [ ] **Step 1: Create `manifest.json`**

Create `/Users/kyleairey/Desktop/dolled-by-louise/manifest.json`:

```json
{
  "name": "Dolled by Louise",
  "short_name": "Dolled",
  "description": "Expert lash lifts and extensions in Longtown, Cumbria",
  "start_url": "/",
  "display": "standalone",
  "background_color": "#130a10",
  "theme_color": "#130a10",
  "icons": [
    {
      "src": "https://placehold.co/192x192/130a10/c2688e?text=D",
      "sizes": "192x192",
      "type": "image/png"
    },
    {
      "src": "https://placehold.co/512x512/130a10/c2688e?text=D",
      "sizes": "512x512",
      "type": "image/png"
    }
  ]
}
```

- [ ] **Step 2: Create `sw.js` (service worker)**

Create `/Users/kyleairey/Desktop/dolled-by-louise/sw.js`:

```js
const CACHE = 'dolled-v1';
const OFFLINE = '/offline.html';

self.addEventListener('install', e => {
  e.waitUntil(
    caches.open(CACHE).then(c => c.addAll([OFFLINE, '/', '/marketplace.html', '/welcome.html']))
  );
  self.skipWaiting();
});

self.addEventListener('activate', e => {
  e.waitUntil(caches.keys().then(keys =>
    Promise.all(keys.filter(k => k !== CACHE).map(k => caches.delete(k)))
  ));
  self.clients.claim();
});

self.addEventListener('fetch', e => {
  if (e.request.mode === 'navigate') {
    e.respondWith(
      fetch(e.request).catch(() => caches.match(OFFLINE))
    );
  }
});
```

- [ ] **Step 3: Create `offline.html`**

Create `/Users/kyleairey/Desktop/dolled-by-louise/offline.html`:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Offline — Dolled by Louise</title>
  <style>
    body { margin:0; font-family:'DM Sans',sans-serif; background:#130a10; color:#fce8f0;
      display:flex; align-items:center; justify-content:center; min-height:100vh; text-align:center; padding:24px; }
    h1 { font-family:'Playfair Display',serif; font-size:32px; margin-bottom:16px; }
    p { color:rgba(252,232,240,0.6); line-height:1.7; max-width:400px; }
    a { display:inline-block; margin-top:32px; padding:14px 32px; background:#c2688e;
      color:#fff; text-decoration:none; border-radius:8px; font-weight:500; }
  </style>
  <link href="https://fonts.googleapis.com/css2?family=Playfair+Display:wght@700&family=DM+Sans:wght@400;500&display=swap" rel="stylesheet">
</head>
<body>
  <div>
    <h1>You're offline</h1>
    <p>Check your connection and try again. Louise's booking details are saved below when you're back online.</p>
    <a href="/">Try again</a>
  </div>
</body>
</html>
```

- [ ] **Step 4: Register service worker in `index.html`**

Before the closing `</body>` tag in `index.html`, add:

```html
<script>
  if ('serviceWorker' in navigator) {
    navigator.serviceWorker.register('/sw.js').catch(() => {});
  }
</script>
```

- [ ] **Step 5: Add `<link rel="manifest">` to `index.html` head**

In the `<head>` section of `index.html`, after `<meta name="theme-color">` (added in Task 8), add:

```html
<link rel="manifest" href="/manifest.json">
```

---

### Task 13: Create sitemap.xml

**Files:**
- Create: `sitemap.xml`

- [ ] **Step 1: Create sitemap**

Create `/Users/kyleairey/Desktop/dolled-by-louise/sitemap.xml`:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<urlset xmlns="http://www.sitemaps.org/schemas/sitemap/0.9">
  <url>
    <loc>https://dolledbylouise.co.uk/</loc>
    <changefreq>monthly</changefreq>
    <priority>1.0</priority>
  </url>
  <url>
    <loc>https://dolledbylouise.co.uk/marketplace.html</loc>
    <changefreq>monthly</changefreq>
    <priority>0.8</priority>
  </url>
  <url>
    <loc>https://dolledbylouise.co.uk/welcome.html</loc>
    <changefreq>yearly</changefreq>
    <priority>0.3</priority>
  </url>
</urlset>
```

---

### Task 14: Design pass — tighten spacing, shadows, hover states on index.html

**Files:**
- Modify: `index.html` (style block)

- [ ] **Step 1: Start dev server**

```bash
cd /Users/kyleairey/Desktop/dolled-by-louise && node server.mjs &
```

- [ ] **Step 2: Invoke ui-ux-pro-max for design audit**

Use `Skill` tool with `skill: "ui-ux-pro-max"`. Apply its design audit recommendations specifically to:
- Button hover states (all `.btn` variants — ensure every button has hover + focus-visible + active)
- Card shadow system in services section (layer rose-tinted shadows)
- Gallery hover overlay opacity
- Testimonial card hover lift

Ensure no `transition-all` is present anywhere — replace with specific `transition: transform, opacity, box-shadow`.

- [ ] **Step 3: Screenshot and verify**

```bash
node screenshot.mjs http://localhost:3000
```

Read the screenshot with the Read tool. Check: hover states visible on buttons, gallery has dark overlay + tint on images, testimonials lift on hover, no flat shadows.

---

### Task 15: Playwright test — index.html

**Files:**
- Modify: `index.html` (fix any issues found)

- [ ] **Step 1: Invoke webapp-testing skill**

Use `Skill` tool with `skill: "awesome-claude-skills:webapp-testing"`. Run the following Playwright checks:

- [ ] **Step 2: Golden path — hero CTAs**

Use `mcp__playwright__browser_navigate` to `http://localhost:3000/index.html`.
Verify: hero loads, WhatsApp Book button visible, Lash Club button visible, Shop button visible.

- [ ] **Step 3: Test lash quiz**

Click "Find My Style" tab in hero panel. Step through all 3 quiz questions. Verify result + WhatsApp CTA appears.

- [ ] **Step 4: Test exit intent modal**

Use `mcp__playwright__browser_evaluate` to call `document.dispatchEvent(new MouseEvent('mouseleave', {clientY: -1}))`.
Verify: exit modal opens. Click dismiss. Verify modal closes.

- [ ] **Step 5: Test email capture form**

Scroll to `#email-capture`. Fill in email input. Submit. Verify button changes to "✓ On its way!".

- [ ] **Step 6: Test FAQ section**

Click first FAQ item. Verify answer is visible. Click again. Verify it closes.

- [ ] **Step 7: Mobile viewport check**

Use `mcp__playwright__browser_resize` to 390×844. Screenshot. Check: nav collapses correctly, hero content readable, CTAs not overflowing.

- [ ] **Step 8: Fix any issues found**, then re-screenshot.

---

### Task 16: Lighthouse audit — index.html

**Files:**
- Modify: `index.html` (fix flagged issues)

- [ ] **Step 1: Run Lighthouse audit**

Use `mcp__lighthouse__run_audit` on `http://localhost:3000/index.html`.

- [ ] **Step 2: Check PWA score**

Use `mcp__lighthouse__check_pwa_readiness` on `http://localhost:3000/index.html`.
Expected: manifest detected, service worker detected.

- [ ] **Step 3: Check accessibility score**

Use `mcp__lighthouse__get_accessibility_score`. Target: ≥90.
Fix any missing `aria-label`, contrast failures, or missing form labels.

- [ ] **Step 4: Check performance score**

Use `mcp__lighthouse__get_performance_score`. If score <75, check for render-blocking resources or unoptimised images and fix.

- [ ] **Step 5: Check SEO score**

Use `mcp__lighthouse__get_seo_analysis`. Verify og:image and canonical are detected. Target: ≥90.

- [ ] **Step 6: Fix all flagged issues**, re-run audit, confirm scores pass.

---

### Task 17: Commit and push index.html phase

**Files:**
- Commit: `index.html`, `manifest.json`, `sw.js`, `offline.html`, `sitemap.xml`

- [ ] **Step 1: Stage all changed files**

```bash
git add index.html manifest.json sw.js offline.html sitemap.xml
```

- [ ] **Step 2: Commit**

```bash
git commit -m "Update index.html — design pass, hero video/images, PWA, SEO, exit intent, email capture, FAQ schema"
```

- [ ] **Step 3: Push to GitHub Pages**

```bash
git push origin main
```

---

## PHASE 2 — marketplace.html

### Task 18: Generate product images

**Files:**
- Output 8 image URLs from Nano Banana 2 → used in Task 19

- [ ] **Step 1: Generate Lash Aftercare Starter Kit image**

Prompt: `Luxury lash aftercare starter kit. Elegant blush and cream packaging on white marble. Rose gold accents. Professional beauty product photography. No text on products.`

- [ ] **Step 2: Generate Foam Cleanser image**

Prompt: `Lash extension foam cleanser bottle. Minimal elegant white packaging with rose gold lid. Soft pink background. Clean beauty product photography. No text.`

- [ ] **Step 3: Generate Lash Conditioning Serum image**

Prompt: `Lash conditioning serum in a sleek glass dropper bottle. Blush pink and gold tones. Luxury beauty product on white marble. Soft bokeh background. No text.`

- [ ] **Step 4: Generate Spoolie Brush Set image**

Prompt: `Set of lash spoolie brushes fanned out. Rose gold handles on a white marble surface. Minimal beauty photography. Soft shadows. No text.`

- [ ] **Step 5: Generate Silk Lash Pillowcase image**

Prompt: `Soft blush pink silk pillowcase folded neatly. Luxurious texture close-up. Rose and cream tones. High-end lifestyle product photography. No text.`

- [ ] **Step 6: Generate Luxury Lash Bundle image**

Prompt: `Luxury lash care gift set. Multiple elegant blush-coloured products arranged in a white gift box with gold ribbon. Premium beauty photography. No text.`

- [ ] **Step 7: Generate Lash Remover image**

Prompt: `Gentle lash remover solution in a small white pump bottle. Blush and cream tones. Clean minimal beauty photography on marble. No text.`

- [ ] **Step 8: Generate Gift Card image**

Prompt: `Elegant gift card design for a luxury beauty salon. Blush pink and gold. Minimalist. Flowers or lash motif. No actual text readable in image.`

- [ ] **Step 9: Save all 8 URLs** for Task 19.

---

### Task 19: Replace marketplace placeholder images

**Files:**
- Modify: `marketplace.html` (~lines 744–869)

- [ ] **Step 1: Replace all 8 product card `<img src>` attributes**

For each product card, replace `https://placehold.co/...` with the corresponding Nano Banana 2 URL from Task 18.

Also update each `openCheckout(...)` call — the 4th argument is the image URL passed to the modal. Replace the placeholder URLs there too with matching Nano Banana 2 URLs.

Example for card 1 (Lash Aftercare Starter Kit, ~line 744):
```html
<img src="NANO_BANANA_URL_KIT" alt="Lash Aftercare Starter Kit" loading="lazy">
```
And in the `openCheckout` call:
```js
openCheckout('Lash Aftercare Starter Kit','Kits & Bundles','£24.99','NANO_BANANA_URL_KIT','STRIPE_LINK_1','PAYPAL_LINK_1','...')
```

Repeat for all 8 cards.

---

### Task 20: Product card hover states

**Files:**
- Modify: `marketplace.html` (style block)

- [ ] **Step 1: Find existing `.prod-card` style rules**

Locate `.prod-card` in the `<style>` block. Add hover behaviour:

```css
.prod-card {
  /* existing rules — keep all */
  overflow: hidden;
  transition: transform 0.25s var(--spring), box-shadow 0.25s var(--ease);
}
.prod-card:hover {
  transform: translateY(-4px);
  box-shadow: 0 16px 48px rgba(194,104,142,0.18), 0 4px 12px rgba(19,10,16,0.12);
}
.prod-card img {
  transition: transform 0.4s var(--ease);
}
.prod-card:hover img {
  transform: scale(1.04);
}
```

Ensure the `<img>` tags in product cards are wrapped in a container with `overflow: hidden` if not already — add `style="overflow:hidden"` to the image wrapper div.

---

### Task 21: Add scarcity labels to select products

**Files:**
- Modify: `marketplace.html` (~lines 827, 778)

- [ ] **Step 1: Add scarcity styles**

In the `<style>` block, add:

```css
.prod-scarcity {
  display: inline-block; background: #fff3e0; color: #e65100;
  font-size: 11px; font-weight: 600; letter-spacing: 0.05em;
  padding: 4px 10px; border-radius: 100px; margin-bottom: 8px;
}
```

- [ ] **Step 2: Add scarcity label to Luxury Lash Bundle card (~line 827)**

Inside the `.prod-card` for the Luxury Bundle, directly above the `<h3>` product name, add:

```html
<span class="prod-scarcity">⚡ Only 3 left</span>
```

- [ ] **Step 3: Add scarcity label to Lash Conditioning Serum card (~line 778)**

Inside the `.prod-card` for the Lash Conditioning Serum, directly above the `<h3>`, add:

```html
<span class="prod-scarcity">⚡ Only 5 left</span>
```

---

### Task 22: Free shipping progress bar in checkout modal

**Files:**
- Modify: `marketplace.html` (~checkout modal area, ~line 878)

- [ ] **Step 1: Add progress bar styles**

In the `<style>` block, add:

```css
.shipping-bar-wrap {
  background: var(--elevated); border-radius: 8px; padding: 12px 16px;
  margin-bottom: 20px;
}
.shipping-bar-label {
  font-size: 12px; color: var(--muted); margin-bottom: 8px;
}
.shipping-bar-label strong { color: var(--rose); }
.shipping-bar-track {
  height: 6px; background: var(--border); border-radius: 100px; overflow: hidden;
}
.shipping-bar-fill {
  height: 100%; background: linear-gradient(90deg, var(--rose), var(--gold));
  border-radius: 100px;
  transition: width 0.4s var(--ease);
}
```

- [ ] **Step 2: Add progress bar HTML inside the checkout modal**

In the `#checkout-modal` HTML (~line 878), after `<p id="modal-category">` and before the payment buttons section, add:

```html
<div class="shipping-bar-wrap" id="shipping-bar-wrap">
  <p class="shipping-bar-label" id="shipping-bar-label">Add <strong id="shipping-remaining">£XX</strong> more for free delivery</p>
  <div class="shipping-bar-track">
    <div class="shipping-bar-fill" id="shipping-bar-fill" style="width:0%"></div>
  </div>
</div>
```

- [ ] **Step 3: Update `openCheckout` JS function to populate the bar**

In the `<script>` block, find `function openCheckout(` and update it to calculate and render the shipping bar. Free delivery threshold is £30:

```js
function openCheckout(name, cat, price, img, stripeLink, paypalLink, waMsg) {
  // existing code to populate modal fields...

  // Shipping bar
  const FREE_THRESHOLD = 30;
  const numericPrice = parseFloat(price.replace(/[^0-9.]/g, '')) || 0;
  const remaining = Math.max(0, FREE_THRESHOLD - numericPrice);
  const pct = Math.min(100, (numericPrice / FREE_THRESHOLD) * 100);
  document.getElementById('shipping-bar-fill').style.width = pct + '%';
  if (remaining <= 0) {
    document.getElementById('shipping-bar-label').innerHTML = '✓ <strong>Free delivery included!</strong>';
  } else {
    document.getElementById('shipping-remaining').textContent = '£' + remaining.toFixed(2);
  }

  // rest of existing function...
}
```

---

### Task 23: Add wishlist feature

**Files:**
- Modify: `marketplace.html` (styles + HTML + JS)

- [ ] **Step 1: Add wishlist styles**

In the `<style>` block, add:

```css
.wish-btn {
  position: absolute; top: 12px; right: 12px;
  background: rgba(255,255,255,0.9); border: none; border-radius: 50%;
  width: 36px; height: 36px; display: flex; align-items: center; justify-content: center;
  cursor: pointer; font-size: 16px; z-index: 2;
  box-shadow: 0 2px 8px rgba(19,10,16,0.12);
  transition: transform 0.15s var(--spring), background 0.15s var(--ease);
}
.wish-btn:hover { transform: scale(1.15); }
.wish-btn.active { background: var(--floating); }
.wish-btn.active .wish-icon::before { content: '♥'; color: var(--rose); }
.wish-btn:not(.active) .wish-icon::before { content: '♡'; color: var(--muted); }
```

- [ ] **Step 2: Ensure product card image wrappers are `position: relative`**

For each `.prod-card`, ensure the image container div has `style="position:relative"` so the absolutely-positioned button overlays correctly.

- [ ] **Step 3: Add wishlist button to each product card**

For each of the 8 product cards, inside the image container div (just after the `<img>`), add:

```html
<button class="wish-btn" onclick="toggleWish(this, 'PRODUCT_NAME')" aria-label="Save to wishlist">
  <span class="wish-icon"></span>
</button>
```

Replace `PRODUCT_NAME` with the product name (e.g. `'Lash Aftercare Starter Kit'`).

- [ ] **Step 4: Add wishlist JS**

In the `<script>` block, add:

```js
function toggleWish(btn, productName) {
  const wishes = JSON.parse(localStorage.getItem('wishlist') || '[]');
  const idx = wishes.indexOf(productName);
  if (idx === -1) {
    wishes.push(productName);
    btn.classList.add('active');
    btn.setAttribute('aria-label', 'Remove from wishlist');
  } else {
    wishes.splice(idx, 1);
    btn.classList.remove('active');
    btn.setAttribute('aria-label', 'Save to wishlist');
  }
  localStorage.setItem('wishlist', JSON.stringify(wishes));
}

// Restore wishlist state on load
document.addEventListener('DOMContentLoaded', function() {
  const wishes = JSON.parse(localStorage.getItem('wishlist') || '[]');
  document.querySelectorAll('.wish-btn').forEach(btn => {
    const name = btn.getAttribute('onclick').match(/'([^']+)'\s*\)/)?.[1];
    if (name && wishes.includes(name)) btn.classList.add('active');
  });
});
```

---

### Task 24: Add Quick View modal

**Files:**
- Modify: `marketplace.html` (styles + HTML + JS)

- [ ] **Step 1: Add Quick View modal styles**

In the `<style>` block, add:

```css
#quick-view-modal {
  display: none; position: fixed; inset: 0; z-index: 10001;
  background: rgba(19,10,16,0.7); backdrop-filter: blur(6px);
  align-items: center; justify-content: center; padding: 24px;
}
#quick-view-modal.open { display: flex; }
.qv-box {
  background: var(--surface); border-radius: 16px; max-width: 600px; width: 100%;
  display: grid; grid-template-columns: 1fr 1fr; overflow: hidden;
  box-shadow: 0 8px 64px rgba(19,10,16,0.3);
}
.qv-img-wrap { aspect-ratio: 1; overflow: hidden; }
.qv-img-wrap img { width: 100%; height: 100%; object-fit: cover; }
.qv-body { padding: 32px; display: flex; flex-direction: column; gap: 12px; }
.qv-cat { font-size: 11px; font-weight: 600; letter-spacing: 0.1em; text-transform: uppercase; color: var(--rose); }
.qv-name { font-family: 'Playfair Display', serif; font-size: 22px; font-weight: 700; color: var(--plum); }
.qv-price { font-size: 20px; font-weight: 600; color: var(--rose); }
.qv-desc { font-size: 13px; color: var(--muted); line-height: 1.7; flex: 1; }
.qv-btn {
  padding: 14px; background: var(--rose); color: #fff; border: none;
  border-radius: 10px; font-size: 14px; font-weight: 500; cursor: pointer;
  transition: background 0.2s var(--ease);
}
.qv-btn:hover { background: #a8567a; }
.qv-close {
  position: absolute; top: 16px; right: 16px; background: rgba(255,255,255,0.9);
  border: none; border-radius: 50%; width: 36px; height: 36px;
  cursor: pointer; font-size: 18px; display: flex; align-items: center; justify-content: center;
}
@media (max-width: 540px) {
  .qv-box { grid-template-columns: 1fr; }
  .qv-img-wrap { max-height: 200px; }
}
```

- [ ] **Step 2: Add Quick View modal HTML**

Directly before `<div id="checkout-modal"`, add:

```html
<!-- ── Quick View Modal ── -->
<div id="quick-view-modal" role="dialog" aria-modal="true" style="position:relative">
  <div class="qv-box">
    <div class="qv-img-wrap">
      <img id="qv-img" src="" alt="">
    </div>
    <div class="qv-body">
      <p class="qv-cat" id="qv-cat"></p>
      <h2 class="qv-name" id="qv-name"></h2>
      <p class="qv-price" id="qv-price"></p>
      <p class="qv-desc" id="qv-desc">Premium lash aftercare product. Formulated to extend the life of your extensions and keep lashes healthy between appointments.</p>
      <button class="qv-btn" id="qv-buy-btn">Buy Now ✦</button>
    </div>
  </div>
  <button class="qv-close" onclick="closeQuickView()" aria-label="Close quick view">✕</button>
</div>
```

- [ ] **Step 3: Add Quick View JS**

In the `<script>` block, add:

```js
function openQuickView(name, cat, price, img, stripeLink, paypalLink, waMsg) {
  document.getElementById('qv-img').src = img;
  document.getElementById('qv-img').alt = name;
  document.getElementById('qv-name').textContent = name;
  document.getElementById('qv-cat').textContent = cat;
  document.getElementById('qv-price').textContent = price;
  document.getElementById('qv-buy-btn').onclick = function() {
    closeQuickView();
    openCheckout(name, cat, price, img, stripeLink, paypalLink, waMsg);
  };
  document.getElementById('quick-view-modal').classList.add('open');
}
function closeQuickView() {
  document.getElementById('quick-view-modal').classList.remove('open');
}
document.getElementById('quick-view-modal').addEventListener('click', function(e) {
  if (e.target === this) closeQuickView();
});
```

- [ ] **Step 4: Wire Quick View to product card images**

For each product card `<img>` (~lines 744–860), change the image from a plain `<img>` to a clickable trigger. Wrap the existing `<img>` in a `<button>` or add `onclick` + `cursor:pointer` style:

```html
<img
  src="NANO_BANANA_URL"
  alt="Product Name"
  loading="lazy"
  style="cursor:pointer"
  onclick="openQuickView('Product Name','Category','£Price','NANO_BANANA_URL','STRIPE_LINK','PAYPAL_LINK','WA_MSG')"
>
```

Use the same arguments as the corresponding `openCheckout` call on that card.

---

### Task 25: Add "You might also like" row in checkout modal

**Files:**
- Modify: `marketplace.html` (checkout modal + JS)

- [ ] **Step 1: Add styles**

In the `<style>` block, add:

```css
.modal-also-like { margin-top: 20px; border-top: 1px solid var(--border); padding-top: 16px; }
.modal-also-label { font-size: 11px; font-weight: 600; letter-spacing: 0.08em; text-transform: uppercase; color: var(--muted); margin-bottom: 12px; }
.modal-also-row { display: flex; gap: 10px; overflow-x: auto; }
.modal-also-item {
  flex: 0 0 80px; cursor: pointer; text-align: center;
}
.modal-also-item img { width: 80px; height: 80px; object-fit: cover; border-radius: 8px; border: 1px solid var(--border); }
.modal-also-item p { font-size: 11px; color: var(--muted); margin-top: 4px; line-height: 1.3; }
.modal-also-item:hover img { border-color: var(--rose); }
```

- [ ] **Step 2: Add HTML placeholder in checkout modal**

Inside `#checkout-modal`, before the closing `</div>` of the modal box, add:

```html
<div class="modal-also-like" id="modal-also-like">
  <p class="modal-also-label">You might also like</p>
  <div class="modal-also-row" id="modal-also-row"></div>
</div>
```

- [ ] **Step 3: Define product catalogue and populate row in JS**

In the `<script>` block, define the product catalogue and update `openCheckout` to populate the row:

```js
const PRODUCTS = [
  { name:'Lash Aftercare Starter Kit', cat:'Kits & Bundles', price:'£24.99', img:'TASK18_STEP1_URL', stripe:'STRIPE_LINK_1', paypal:'PAYPAL_LINK_1', wa:"Hi Louise! I'd love to order the Lash Aftercare Starter Kit 💕" },
  { name:'Lash Extension Foam Cleanser', cat:'Aftercare', price:'£9.99', img:'TASK18_STEP2_URL', stripe:'STRIPE_LINK_2', paypal:'PAYPAL_LINK_2', wa:"Hi Louise! I'd love to order the Lash Foam Cleanser 💕" },
  { name:'Lash Conditioning Serum', cat:'Aftercare', price:'£14.99', img:'TASK18_STEP3_URL', stripe:'STRIPE_LINK_3', paypal:'PAYPAL_LINK_3', wa:"Hi Louise! I'd love to order the Lash Conditioning Serum 💕" },
  { name:'Spoolie Brush Set', cat:'Accessories', price:'£5.99', img:'TASK18_STEP4_URL', stripe:'STRIPE_LINK_4', paypal:'PAYPAL_LINK_4', wa:"Hi Louise! I'd love to order the Spoolie Brush Set 💕" },
  { name:'Silk Lash Pillowcase', cat:'Accessories', price:'£19.99', img:'TASK18_STEP5_URL', stripe:'STRIPE_LINK_5', paypal:'PAYPAL_LINK_5', wa:"Hi Louise! I'd love to order the Silk Lash Pillowcase 💕" },
  { name:'The Luxury Lash Bundle', cat:'Kits & Bundles', price:'£44.99', img:'TASK18_STEP6_URL', stripe:'STRIPE_LINK_6', paypal:'PAYPAL_LINK_6', wa:"Hi Louise! I'd love to order the Luxury Lash Bundle 💕" },
  { name:'Gentle Lash Remover', cat:'Aftercare', price:'£11.99', img:'TASK18_STEP7_URL', stripe:'STRIPE_LINK_7', paypal:'PAYPAL_LINK_7', wa:"Hi Louise! I'd love to order the Gentle Lash Remover 💕" },
  { name:'Experience Gift Card', cat:'Gift Cards', price:'From £25', img:'TASK18_STEP8_URL', stripe:'STRIPE_LINK_8', paypal:'PAYPAL_LINK_8', wa:"Hi Louise! I'd love to order a Gift Card 💕" }
];
```

Replace `TASK18_STEP1_URL`–`TASK18_STEP8_URL` with the actual Nano Banana 2 URLs generated in Task 18 Steps 1–8. Keep existing `STRIPE_LINK_*` and `PAYPAL_LINK_*` placeholders.

Also add a `closeCheckout` helper near the existing close button handler (search for `classList.remove('open')` on `#checkout-modal` and wrap it):

```js
function closeCheckout() {
  document.getElementById('checkout-modal').classList.remove('open');
}
```

Then inside `openCheckout`, after populating the main modal fields, add:

```js
// "You might also like"
const related = PRODUCTS.filter(p => p.cat === cat && p.name !== name).slice(0, 3);
const row = document.getElementById('modal-also-row');
row.innerHTML = related.map(p => `
  <div class="modal-also-item" onclick="closeCheckout(); openCheckout('${p.name}','${p.cat}','${p.price}','${p.img}','${p.stripe}','${p.paypal}','${p.wa}')">
    <img src="${p.img}" alt="${p.name}">
    <p>${p.name}</p>
  </div>
`).join('');
document.getElementById('modal-also-like').style.display = related.length ? 'block' : 'none';
```

---

### Task 26: Add og:image and theme-color to marketplace.html

**Files:**
- Modify: `marketplace.html` (head section)

- [ ] **Step 1: Add meta tags to `<head>`**

After `<meta name="description" ...>` in `marketplace.html`, add:

```html
<meta property="og:title" content="Shop — Dolled by Louise">
<meta property="og:description" content="Lash aftercare products and kits from Dolled by Louise.">
<meta property="og:image" content="NANO_BANANA_URL_LUXURY_BUNDLE">
<meta property="og:url" content="https://dolledbylouise.co.uk/marketplace.html">
<meta property="og:type" content="website">
<meta name="theme-color" content="#fdf8f5">
<link rel="canonical" href="https://dolledbylouise.co.uk/marketplace.html">
<link rel="manifest" href="/manifest.json">
```

Replace `NANO_BANANA_URL_LUXURY_BUNDLE` with the Luxury Lash Bundle image URL from Task 18 Step 6.

Also add service worker registration before `</body>`:

```html
<script>
  if ('serviceWorker' in navigator) {
    navigator.serviceWorker.register('/sw.js').catch(() => {});
  }
</script>
```

---

### Task 27: Playwright test — marketplace.html

- [ ] **Step 1: Navigate to marketplace**

`mcp__playwright__browser_navigate` → `http://localhost:3000/marketplace.html`

- [ ] **Step 2: Test product card hover**

Hover over first product card using `mcp__playwright__browser_hover`. Take screenshot. Verify image scales.

- [ ] **Step 3: Test Quick View modal**

Click product image. Verify Quick View modal opens with correct name, price, image. Click Buy Now. Verify checkout modal opens. Close it.

- [ ] **Step 4: Test wishlist toggle**

Click wishlist button on a card. Verify heart becomes active (filled). Reload page. Verify heart is still active (localStorage persisted).

- [ ] **Step 5: Test checkout modal with shipping bar**

Click Buy Now on Foam Cleanser (£9.99). Verify shipping bar shows "Add £20.01 more for free delivery". Close. Click Luxury Bundle (£44.99). Verify bar shows "Free delivery included!".

- [ ] **Step 6: Test "You might also like"**

Open checkout for a Kits & Bundles product. Verify related products section appears with images.

- [ ] **Step 7: Mobile check** — resize to 390×844, screenshot, verify product grid is responsive.

- [ ] **Step 8: Fix any issues found.**

---

### Task 28: Lighthouse audit — marketplace.html

- [ ] **Step 1:** Run `mcp__lighthouse__run_audit` on `http://localhost:3000/marketplace.html`.
- [ ] **Step 2:** Check accessibility (target ≥90), performance, SEO. Fix any flags.
- [ ] **Step 3:** Re-run and confirm scores pass.

---

### Task 29: Commit and push marketplace.html phase

- [ ] **Step 1:**
```bash
git add marketplace.html
git commit -m "Update marketplace.html — generated product images, hover states, wishlist, quick view, shipping bar, also-like, og:image"
git push origin main
```

---

## PHASE 3 — welcome.html

### Task 30: Generate welcome page background image

**Files:**
- Output 1 image URL from Nano Banana 2 → used in Task 31

- [ ] **Step 1: Generate atmospheric background**

Call `mcp__nano-banana-2__generate_image` with prompt:
```
Deep plum and midnight purple abstract background. Soft bokeh lash particles drifting upward. Ultra dark, luxurious, moody. Rose-gold light glints at edges. Cinematic beauty editorial. No text, no face, pure atmosphere.
```

- [ ] **Step 2: Save the returned image URL** for Task 31.

---

### Task 31: Design pass — welcome.html

**Files:**
- Modify: `welcome.html`

- [ ] **Step 1: Invoke ui-ux-pro-max skill**

Use `Skill` tool with `skill: "ui-ux-pro-max"`. Apply recommendations to welcome.html — animation timing, easing curves, particle density.

- [ ] **Step 2: Set the new background image**

Find the welcome page background CSS (likely on `body` or `.welcome-bg` or a `background-image` property). Update it to use the Nano Banana 2 URL from Task 30 as an additional layer behind the existing gradient overlay.

- [ ] **Step 3: Tighten animation timing**

In welcome.html `<style>` or `<script>`:
- Lash eye SVG draw duration: ensure each stroke takes 0.4–0.6s with `ease-out` — not too fast, not too slow
- Text reveals: stagger by 0.2s, `cubic-bezier(0.4,0,0.2,1)` easing
- Particles: ensure `animation-duration` varies per particle (2s–5s range) for organic feel

- [ ] **Step 4: Screenshot welcome page**

```bash
node screenshot.mjs http://localhost:3000/welcome.html
```

Read screenshot. Verify: background atmospheric image shows through, lash eye is crisp, text is readable on dark bg, Enter button is prominent.

---

### Task 32: Add og:image and theme-color to welcome.html

**Files:**
- Modify: `welcome.html` (head section)

- [ ] **Step 1: Add meta tags to `<head>`**

```html
<meta property="og:title" content="Dolled by Louise — Lash Artist in Longtown, Cumbria">
<meta property="og:description" content="Expert lash lifts and extensions. Book with Louise today.">
<meta property="og:image" content="NANO_BANANA_URL_FROM_TASK_30">
<meta property="og:url" content="https://dolledbylouise.co.uk/welcome.html">
<meta property="og:type" content="website">
<meta name="theme-color" content="#130a10">
<link rel="manifest" href="/manifest.json">
```

Replace `NANO_BANANA_URL_FROM_TASK_30` with the URL from Task 30.

- [ ] **Step 2: Add service worker registration before `</body>`**

```html
<script>
  if ('serviceWorker' in navigator) {
    navigator.serviceWorker.register('/sw.js').catch(() => {});
  }
</script>
```

- [ ] **Step 3: Verify sessionStorage welcome gate still works**

Check that the welcome gate logic is intact:
```js
// In welcome.html — Enter button click handler must still do:
sessionStorage.setItem('visited', 'true');
// then trigger curtain animation → navigate to index.html
```

---

### Task 33: Playwright test — welcome.html

- [ ] **Step 1:** Navigate to `http://localhost:3000/welcome.html` in a fresh context (clear sessionStorage first).
- [ ] **Step 2:** Verify SVG lash eye is visible. Verify "Dolled by Louise" text renders.
- [ ] **Step 3:** Click Enter button. Verify curtain animation plays. Verify redirect to `index.html`.
- [ ] **Step 4:** Reload `index.html`. Verify welcome gate does NOT redirect again (sessionStorage flag set).
- [ ] **Step 5:** Mobile check — resize to 390×844. Verify welcome page is not overflowing.
- [ ] **Step 6: Fix any issues.**

---

### Task 34: Lighthouse audit — welcome.html

- [ ] **Step 1:** Run `mcp__lighthouse__run_audit` on `http://localhost:3000/welcome.html`.
- [ ] **Step 2:** Fix accessibility or performance flags. Welcome page is simple — target ≥90 performance.
- [ ] **Step 3:** Confirm scores pass.

---

### Task 35: Commit and push welcome.html phase

- [ ] **Step 1:**
```bash
git add welcome.html
git commit -m "Update welcome.html — atmospheric bg, animation refinement, og:image, PWA manifest"
git push origin main
```

---

## Done

All three pages shipped:
- `index.html` — design polish, hero video, real images, PWA, SEO, exit intent, email capture, FAQ schema
- `marketplace.html` — real product images, hover states, wishlist, quick view, shipping bar, also-like, og:image
- `welcome.html` — atmospheric background, animation refinement, og:image, PWA

Chatbot/Railway deployment is tracked separately.
