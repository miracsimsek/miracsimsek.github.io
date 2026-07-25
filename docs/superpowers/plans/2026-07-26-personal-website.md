# miracsimsek.github.io Personal Website Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Build a single-page static personal portfolio site for Mirac Şimşek with a "90s London café" visual identity (sepia/cream background, typewriter headings, film-grain texture), covering About, Projects, and Contact sections.

**Architecture:** Plain HTML/CSS/JS, no build step, no framework. One `index.html`, one `style.css`, one `script.js` for the grain-overlay/scroll-reveal behavior. Deployed by pushing to the `main` branch of the `miracsimsek.github.io` repo (GitHub Pages serves user pages from `main` at the repo root automatically — no `CNAME` needed since this is a `<username>.github.io` user site, not a custom domain).

**Tech Stack:** HTML5, CSS3 (custom properties, Grid/Flexbox), vanilla JS (ES6). Google Fonts: `Special Elite` (typewriter headings) and `Lora` (serif body). Inline SVG icons for GitHub/LinkedIn/Email (no icon library dependency).

## Global Constraints

- No build tooling, no npm dependencies, no JS framework — spec requires plain HTML/CSS/JS (docs/superpowers/specs/2026-07-26-personal-website-design.md, "Tech Stack").
- Background: sepia/cream tone around `#e8ddc7`; text: dark coffee-brown around `#3a2f22`; single warm rust/amber accent used sparingly — exact values locked in Task 2.
- Headings use a typewriter/monospace-style font; body copy uses a serif font.
- No drop shadows, no glassmorphism, minimal motion (small hover transitions only) — per spec's "Motion" note.
- Three sections only: `#about`, `#projects`, `#contact`. No blog, no experience/CV timeline (explicitly out of scope).
- Content is fixed: name "Mirac Şimşek", title "Co-Founder & Engineer", email `miracsimsek@leenar.net`, LinkedIn `https://www.linkedin.com/in/miracsimsek/`, GitHub `https://github.com/miracsimsek`, projects Qrucial (`https://qrucial.app`, "AI-powered team management platform") and Leenar (`https://leenar.net`, "no-code multi-agent orchestration platform").
- Profile photo file is not yet supplied by the user — build the hero with a placeholder image path (`assets/profile.jpg`) and a CSS-only fallback (initials in a polaroid frame) so the page renders correctly before the real photo is dropped in.

---

### Task 1: HTML skeleton

**Files:**
- Create: `index.html`
- Create: `assets/` (directory, for the profile photo the user will add later)

**Interfaces:**
- Produces: the DOM structure and element IDs/classes every later CSS/JS task styles or hooks into:
  - `<body>` has three `<section>` elements with ids `about`, `projects`, `contact`, in that order.
  - Hero: `<header id="about">` containing `<img class="profile-photo" src="assets/profile.jpg" alt="Mirac Şimşek">`, `<h1 class="heading-type">MIRAC ŞİMŞEK — CO-FOUNDER & ENGINEER</h1>`, `<p class="intro">...</p>`, and `<nav class="social-links">` with three `<a>` tags (GitHub, LinkedIn, Email), each containing an inline `<svg class="icon">`.
  - Projects: `<section id="projects">` containing `<h2 class="heading-type">Projects</h2>` and `<div class="project-cards">` with two `<article class="project-card">` elements (Qrucial, Leenar), each with `<h3>`, `<p class="project-desc">`, and `<a class="project-link" href="...">`.
  - Contact: `<section id="contact">` containing `<h2 class="heading-type">Get in touch</h2>` and a repeat of the same three social links (`class="social-links"`).
  - `<link rel="stylesheet" href="style.css">` in `<head>`, `<script src="script.js" defer></script>` before `</body>`.

- [ ] **Step 1: Write index.html with the full section structure**

```html
<!DOCTYPE html>
<html lang="tr">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Mirac Şimşek</title>
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link href="https://fonts.googleapis.com/css2?family=Special+Elite&family=Lora:ital,wght@0,400;0,600;1,400&display=swap" rel="stylesheet">
  <link rel="stylesheet" href="style.css">
</head>
<body>
  <header id="about">
    <div class="photo-frame">
      <img class="profile-photo" src="assets/profile.jpg" alt="Mirac Şimşek" onerror="this.parentElement.classList.add('photo-fallback')">
      <span class="photo-fallback-initials">MŞ</span>
    </div>
    <h1 class="heading-type">MIRAC ŞİMŞEK<br>CO-FOUNDER &amp; ENGINEER</h1>
    <p class="intro">Yazılım mühendisi ve Qrucial &amp; Leenar'ın kurucu ortağı. Ürün, altyapı ve yapay zeka odaklı takımlarla çalışıyorum.</p>
    <nav class="social-links" aria-label="Sosyal bağlantılar">
      <a href="https://github.com/miracsimsek" target="_blank" rel="noopener" aria-label="GitHub">
        <svg class="icon" viewBox="0 0 24 24" fill="currentColor" aria-hidden="true"><path d="M12 .5C5.65.5.5 5.65.5 12c0 5.09 3.29 9.4 7.86 10.93.58.1.79-.25.79-.56 0-.28-.01-1.02-.02-2-3.2.7-3.88-1.54-3.88-1.54-.52-1.34-1.28-1.7-1.28-1.7-1.04-.72.08-.7.08-.7 1.16.08 1.77 1.2 1.77 1.2 1.03 1.77 2.7 1.26 3.36.96.1-.75.4-1.26.73-1.55-2.55-.29-5.24-1.28-5.24-5.7 0-1.26.45-2.29 1.19-3.1-.12-.29-.52-1.46.11-3.05 0 0 .97-.31 3.18 1.18.92-.26 1.9-.39 2.88-.39.98 0 1.96.13 2.88.39 2.2-1.49 3.17-1.18 3.17-1.18.63 1.59.24 2.76.12 3.05.74.81 1.19 1.84 1.19 3.1 0 4.43-2.7 5.41-5.27 5.69.42.36.78 1.08.78 2.17 0 1.57-.01 2.83-.01 3.22 0 .31.21.67.8.56C20.21 21.39 23.5 17.08 23.5 12 23.5 5.65 18.35.5 12 .5z"/></svg>
      </a>
      <a href="https://www.linkedin.com/in/miracsimsek/" target="_blank" rel="noopener" aria-label="LinkedIn">
        <svg class="icon" viewBox="0 0 24 24" fill="currentColor" aria-hidden="true"><path d="M20.45 20.45h-3.56v-5.57c0-1.33-.03-3.04-1.85-3.04-1.86 0-2.14 1.45-2.14 2.94v5.67H9.34V9h3.42v1.56h.05c.48-.9 1.64-1.85 3.38-1.85 3.61 0 4.28 2.38 4.28 5.47v6.27zM5.34 7.43a2.06 2.06 0 1 1 0-4.12 2.06 2.06 0 0 1 0 4.12zM7.12 20.45H3.56V9h3.56v11.45z"/></svg>
      </a>
      <a href="mailto:miracsimsek@leenar.net" aria-label="Email">
        <svg class="icon" viewBox="0 0 24 24" fill="currentColor" aria-hidden="true"><path d="M2 5.5C2 4.67 2.67 4 3.5 4h17c.83 0 1.5.67 1.5 1.5v13c0 .83-.67 1.5-1.5 1.5h-17c-.83 0-1.5-.67-1.5-1.5v-13zm2.2.5 7.8 5.85L19.8 6H4.2zM20 8.1l-7.4 5.55a1 1 0 0 1-1.2 0L4 8.1V18h16V8.1z"/></svg>
      </a>
    </nav>
  </header>

  <section id="projects">
    <h2 class="heading-type">Projects</h2>
    <div class="project-cards">
      <article class="project-card">
        <h3>Qrucial</h3>
        <p class="project-desc">AI-powered team management platform.</p>
        <a class="project-link" href="https://qrucial.app" target="_blank" rel="noopener">qrucial.app &rarr;</a>
      </article>
      <article class="project-card">
        <h3>Leenar</h3>
        <p class="project-desc">No-code multi-agent orchestration platform.</p>
        <a class="project-link" href="https://leenar.net" target="_blank" rel="noopener">leenar.net &rarr;</a>
      </article>
    </div>
  </section>

  <section id="contact">
    <h2 class="heading-type">Get in touch</h2>
    <p class="intro">miracsimsek@leenar.net</p>
    <nav class="social-links" aria-label="Sosyal bağlantılar">
      <a href="https://github.com/miracsimsek" target="_blank" rel="noopener" aria-label="GitHub">
        <svg class="icon" viewBox="0 0 24 24" fill="currentColor" aria-hidden="true"><path d="M12 .5C5.65.5.5 5.65.5 12c0 5.09 3.29 9.4 7.86 10.93.58.1.79-.25.79-.56 0-.28-.01-1.02-.02-2-3.2.7-3.88-1.54-3.88-1.54-.52-1.34-1.28-1.7-1.28-1.7-1.04-.72.08-.7.08-.7 1.16.08 1.77 1.2 1.77 1.2 1.03 1.77 2.7 1.26 3.36.96.1-.75.4-1.26.73-1.55-2.55-.29-5.24-1.28-5.24-5.7 0-1.26.45-2.29 1.19-3.1-.12-.29-.52-1.46.11-3.05 0 0 .97-.31 3.18 1.18.92-.26 1.9-.39 2.88-.39.98 0 1.96.13 2.88.39 2.2-1.49 3.17-1.18 3.17-1.18.63 1.59.24 2.76.12 3.05.74.81 1.19 1.84 1.19 3.1 0 4.43-2.7 5.41-5.27 5.69.42.36.78 1.08.78 2.17 0 1.57-.01 2.83-.01 3.22 0 .31.21.67.8.56C20.21 21.39 23.5 17.08 23.5 12 23.5 5.65 18.35.5 12 .5z"/></svg>
      </a>
      <a href="https://www.linkedin.com/in/miracsimsek/" target="_blank" rel="noopener" aria-label="LinkedIn">
        <svg class="icon" viewBox="0 0 24 24" fill="currentColor" aria-hidden="true"><path d="M20.45 20.45h-3.56v-5.57c0-1.33-.03-3.04-1.85-3.04-1.86 0-2.14 1.45-2.14 2.94v5.67H9.34V9h3.42v1.56h.05c.48-.9 1.64-1.85 3.38-1.85 3.61 0 4.28 2.38 4.28 5.47v6.27zM5.34 7.43a2.06 2.06 0 1 1 0-4.12 2.06 2.06 0 0 1 0 4.12zM7.12 20.45H3.56V9h3.56v11.45z"/></svg>
      </a>
      <a href="mailto:miracsimsek@leenar.net" aria-label="Email">
        <svg class="icon" viewBox="0 0 24 24" fill="currentColor" aria-hidden="true"><path d="M2 5.5C2 4.67 2.67 4 3.5 4h17c.83 0 1.5.67 1.5 1.5v13c0 .83-.67 1.5-1.5 1.5h-17c-.83 0-1.5-.67-1.5-1.5v-13zm2.2.5 7.8 5.85L19.8 6H4.2zM20 8.1l-7.4 5.55a1 1 0 0 1-1.2 0L4 8.1V18h16V8.1z"/></svg>
      </a>
    </nav>
  </section>

  <script src="script.js" defer></script>
</body>
</html>
```

- [ ] **Step 2: Create the assets directory placeholder**

```bash
mkdir -p assets
touch assets/.gitkeep
```

- [ ] **Step 3: Verify structure in a browser**

Open `index.html` directly in a browser (double-click or `start index.html` on Windows). Expected: unstyled but readable HTML — hero heading, intro paragraph, three icon links, two project blocks with working links, contact block. A broken-image icon is expected for the profile photo (no file yet) — confirm the `onerror` fallback logic doesn't crash the page (no JS errors in DevTools console).

- [ ] **Step 4: Commit**

```bash
git add index.html assets/.gitkeep
git commit -m "Add site HTML skeleton with about, projects, contact sections"
```

---

### Task 2: Color palette, typography, and base layout CSS

**Files:**
- Create: `style.css`
- Modify: `index.html:1-10` (no change expected, listed for reference only — the `<link>` tag already added in Task 1)

**Interfaces:**
- Consumes: element structure and classes from Task 1 (`#about`, `#projects`, `#contact`, `.heading-type`, `.intro`, `.social-links`, `.icon`, `.project-cards`, `.project-card`, `.project-desc`, `.project-link`, `.photo-frame`, `.profile-photo`, `.photo-fallback`, `.photo-fallback-initials`).
- Produces: CSS custom properties on `:root` that Tasks 3–7 build on: `--color-bg`, `--color-bg-alt`, `--color-text`, `--color-accent`, `--font-heading`, `--font-body`.

- [ ] **Step 1: Write style.css with reset, custom properties, and typography**

```css
:root {
  --color-bg: #e8ddc7;
  --color-bg-alt: #ddcfae;
  --color-text: #3a2f22;
  --color-accent: #a35226;
  --font-heading: 'Special Elite', 'Courier New', monospace;
  --font-body: 'Lora', Georgia, serif;
}

* { box-sizing: border-box; margin: 0; padding: 0; }

body {
  background-color: var(--color-bg);
  color: var(--color-text);
  font-family: var(--font-body);
  line-height: 1.6;
  -webkit-font-smoothing: antialiased;
}

.heading-type {
  font-family: var(--font-heading);
  letter-spacing: 0.04em;
  line-height: 1.3;
  text-transform: uppercase;
}

h1.heading-type { font-size: clamp(1.6rem, 4vw, 2.6rem); }
h2.heading-type { font-size: clamp(1.2rem, 3vw, 1.8rem); margin-bottom: 1.5rem; }

.intro { max-width: 40ch; font-size: 1.05rem; }

a { color: var(--color-accent); text-decoration: none; }
a:hover { text-decoration: underline; }

section, header { padding: 4rem 1.5rem; max-width: 900px; margin: 0 auto; }
```

- [ ] **Step 2: Verify in browser**

Open `index.html`. Expected: cream background, dark brown text, typewriter-style uppercase headings, serif body text, orange-brown link color. Confirm via DevTools that `Special Elite` and `Lora` load (Network tab shows the Google Fonts CSS request succeeding, not blocked).

- [ ] **Step 3: Commit**

```bash
git add style.css
git commit -m "Add base color palette, typography, and layout tokens"
```

---

### Task 3: Hero/About section styling (photo frame, social icons)

**Files:**
- Modify: `style.css` (append)

**Interfaces:**
- Consumes: `.photo-frame`, `.profile-photo`, `.photo-fallback`, `.photo-fallback-initials`, `.social-links`, `.icon` from Task 1's HTML; `--color-*` tokens from Task 2.
- Produces: `.photo-frame` sized at 160×190px so Task 6 (grain overlay) and Task 7 (responsive) can reference it without renaming.

- [ ] **Step 1: Add hero layout and polaroid photo frame styles**

```css
header#about {
  display: flex;
  flex-direction: column;
  align-items: center;
  text-align: center;
  gap: 1.25rem;
}

.photo-frame {
  width: 160px;
  height: 190px;
  background: #f5efdd;
  border: 1px solid #c9b78f;
  padding: 10px 10px 24px;
  box-shadow: 0 4px 10px rgba(58, 47, 34, 0.25);
  transform: rotate(-2deg);
  position: relative;
  display: flex;
  align-items: center;
  justify-content: center;
}

.profile-photo {
  width: 100%;
  height: 100%;
  object-fit: cover;
  filter: sepia(0.35) contrast(1.05);
  display: block;
}

.photo-fallback .profile-photo { display: none; }

.photo-fallback-initials {
  display: none;
  font-family: var(--font-heading);
  font-size: 2.5rem;
  color: var(--color-text);
}

.photo-fallback .photo-fallback-initials { display: block; }

.social-links {
  display: flex;
  gap: 1.25rem;
}

.icon {
  width: 22px;
  height: 22px;
  color: var(--color-text);
  transition: color 0.2s ease, transform 0.2s ease;
}

.social-links a:hover .icon {
  color: var(--color-accent);
  transform: translateY(-2px);
}
```

- [ ] **Step 2: Verify in browser**

Open `index.html`. Expected: a rotated polaroid-style frame centered above the heading. Since `assets/profile.jpg` doesn't exist yet, the `onerror` handler should trigger and show "MŞ" initials instead of a broken image icon — confirm this visually. Hover each of the three icon links and confirm the color shifts to the accent tone and the icon nudges up slightly.

- [ ] **Step 3: Commit**

```bash
git add style.css
git commit -m "Style hero section: polaroid photo frame and social icon hovers"
```

---

### Task 4: Projects section styling (index cards)

**Files:**
- Modify: `style.css` (append)

**Interfaces:**
- Consumes: `.project-cards`, `.project-card`, `.project-desc`, `.project-link` from Task 1; `--color-*` tokens from Task 2.
- Produces: `.project-card` fixed min-height not required — later tasks don't depend on card dimensions, only on the class names.

- [ ] **Step 1: Add project card grid and card styling**

```css
#projects { text-align: center; }

.project-cards {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 1.5rem;
  text-align: left;
}

.project-card {
  background: #f5efdd;
  border: 1px solid #c9b78f;
  padding: 1.75rem;
  box-shadow: 3px 3px 0 rgba(58, 47, 34, 0.15);
}

.project-card h3 {
  font-family: var(--font-heading);
  font-size: 1.15rem;
  margin-bottom: 0.5rem;
}

.project-desc { margin-bottom: 1rem; }

.project-link {
  font-family: var(--font-heading);
  font-size: 0.85rem;
}
```

- [ ] **Step 2: Verify in browser**

Open `index.html`. Expected: two side-by-side cream index cards under "Projects", each with a typewriter-style title, description, and an outbound link ending in "→". Click both project links in a new tab and confirm they navigate to `https://qrucial.app` and `https://leenar.net` respectively.

- [ ] **Step 3: Commit**

```bash
git add style.css
git commit -m "Style projects section as index cards"
```

---

### Task 5: Contact section styling

**Files:**
- Modify: `style.css` (append)

**Interfaces:**
- Consumes: `#contact`, `.intro`, `.social-links` from Task 1; tokens from Task 2; `.social-links`/`.icon` hover rules already defined in Task 3 (reused as-is, no redefinition).

- [ ] **Step 1: Add contact section layout**

```css
#contact {
  text-align: center;
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 1rem;
  background: var(--color-bg-alt);
}

#contact .intro {
  font-family: var(--font-heading);
  font-size: 1.1rem;
}
```

- [ ] **Step 2: Verify in browser**

Open `index.html`. Expected: contact section has a slightly darker cream background than the rest of the page (visually separating it as a closing block), centered email text in typewriter font, and the same three hover-reactive icon links as the hero.

- [ ] **Step 3: Commit**

```bash
git add style.css
git commit -m "Style contact section"
```

---

### Task 6: Film-grain texture overlay and scroll-reveal motion

**Files:**
- Create: `script.js`
- Modify: `style.css` (append)

**Interfaces:**
- Consumes: `section, header` selector from Task 2 (applies `.reveal` class to these via JS).
- Produces: a `.grain-overlay` fixed `<div>` inserted by `script.js` into `<body>`, and a `.reveal`/`.reveal.visible` CSS pair — nothing later depends on these names since this is the last visual-effects task.

- [ ] **Step 1: Add grain overlay and reveal CSS**

```css
.grain-overlay {
  position: fixed;
  inset: 0;
  pointer-events: none;
  z-index: 9999;
  opacity: 0.05;
  mix-blend-mode: multiply;
  background-image: url("data:image/svg+xml;utf8,<svg xmlns='http://www.w3.org/2000/svg' width='120' height='120'><filter id='n'><feTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='2' stitchTiles='stitch'/></filter><rect width='100%25' height='100%25' filter='url(%23n)'/></svg>");
}

.reveal {
  opacity: 0;
  transform: translateY(12px);
  transition: opacity 0.6s ease, transform 0.6s ease;
}

.reveal.visible {
  opacity: 1;
  transform: translateY(0);
}
```

- [ ] **Step 2: Write script.js**

```js
document.addEventListener('DOMContentLoaded', () => {
  const grain = document.createElement('div');
  grain.className = 'grain-overlay';
  document.body.appendChild(grain);

  const revealTargets = document.querySelectorAll('section, header');
  revealTargets.forEach((el) => el.classList.add('reveal'));

  const observer = new IntersectionObserver(
    (entries) => {
      entries.forEach((entry) => {
        if (entry.isIntersecting) {
          entry.target.classList.add('visible');
          observer.unobserve(entry.target);
        }
      });
    },
    { threshold: 0.15 }
  );

  revealTargets.forEach((el) => observer.observe(el));
});
```

- [ ] **Step 3: Verify in browser**

Open `index.html`. Expected: a barely-visible grain texture over the whole page (compare with/without by temporarily setting `opacity: 0` in DevTools). Scroll down — the projects and contact sections should fade/slide into view as they enter the viewport, each only once (check DevTools console for JS errors — none expected).

- [ ] **Step 4: Commit**

```bash
git add style.css script.js
git commit -m "Add film-grain overlay and scroll-reveal motion"
```

---

### Task 7: Responsive layout for mobile

**Files:**
- Modify: `style.css` (append, media query block)

**Interfaces:**
- Consumes: `.project-cards` (Task 4), `header#about` (Task 3), `section, header` padding (Task 2) — no new class names introduced.

- [ ] **Step 1: Add mobile breakpoint styles**

```css
@media (max-width: 640px) {
  section, header { padding: 2.5rem 1.25rem; }

  .project-cards {
    grid-template-columns: 1fr;
  }

  .photo-frame {
    width: 130px;
    height: 155px;
  }
}
```

- [ ] **Step 2: Verify in browser**

Open DevTools, toggle device toolbar to a 375px-wide viewport (e.g. iPhone SE). Expected: project cards stack into a single column, section padding shrinks so content isn't cramped against the edges, photo frame shrinks slightly, no horizontal scrollbar appears anywhere on the page.

- [ ] **Step 3: Commit**

```bash
git add style.css
git commit -m "Add responsive styles for mobile viewports"
```

---

### Task 8: Deployment readiness

**Files:**
- Create: `README.md`

**Interfaces:**
- None — this task only adds documentation and does a final end-to-end check of everything Tasks 1–7 produced.

- [ ] **Step 1: Write README.md with deployment and photo-replacement instructions**

```markdown
# miracsimsek.github.io

Personal portfolio site for Mirac Şimşek. Plain HTML/CSS/JS, no build step.

## Local preview

Open `index.html` directly in a browser, or serve the folder with any static
file server, e.g.:

```bash
python -m http.server 8000
```

Then visit `http://localhost:8000`.

## Adding your profile photo

Drop a photo file at `assets/profile.jpg` (portrait orientation works best
with the polaroid frame). Until that file exists, the hero section shows
"MŞ" initials as a fallback.

## Deploying

This repo is a GitHub Pages **user site** (`<username>.github.io`), so
GitHub Pages serves it automatically from the `main` branch root — no
`CNAME` file or extra configuration needed. Push to `main` and the site
is live at `https://miracsimsek.github.io` within a minute or two:

```bash
git push origin main
```
```

- [ ] **Step 2: Full end-to-end verification in browser**

Open `index.html` fresh (hard refresh to bypass cache). Walk through: hero renders with fallback initials and hover-reactive social icons; Projects section shows Qrucial and Leenar cards with working outbound links; Contact section shows the email and the same social links; page has visible (subtle) grain texture; scrolling triggers the reveal animation once per section; resizing to a narrow viewport reflows correctly with no horizontal scroll. Check the DevTools console across the whole flow — expect zero errors.

- [ ] **Step 3: Commit**

```bash
git add README.md
git commit -m "Add README with local preview and deployment instructions"
```
