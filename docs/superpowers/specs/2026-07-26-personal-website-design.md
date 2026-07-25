# miracsimsek.github.io — Personal Website Design

## Purpose

A single-page personal portfolio site for Mirac Şimşek (Co-Founder & Engineer at Qrucial/Leenar), inspired in structure by mahmutefedara.github.io but with a distinct visual identity: a "90s London, dimly-lit café" nostalgic/vintage feel rather than the source site's neo-brutalist style.

## Reference Site Analysis

`mahmutefedara.github.io` (React + TypeScript + Vite, deployed to GitHub Pages via CNAME) uses a Neo-Brutalist/Bauhaus design system (thick black borders, offset color blocks, bold accent colors) and a single-page structure: sticky nav → hero/about → projects → expertise → contact → footer.

We are reusing the **information architecture** (single page, sticky-ish nav, hero, projects, contact) but not the visual language or tech stack.

## Visual Direction: "90s London Café"

Selected via visual mockup comparison (option B — "Eski Kağıt & Daktilo" / Old Paper & Typewriter):

- **Background:** dirty cream / sepia paper tone (`#e8ddc7` range)
- **Text:** dark coffee-brown / soot black (`#3a2f22` range)
- **Accent:** a single warm rust/amber tone, used sparingly (links, hover states, small "stamp" details) — evokes neon signage glow through a café window
- **Typography:** typewriter/monospace for headings (e.g. a Special Elite–style webfont, falling back to `Courier New`), a readable serif for body copy
- **Texture:** subtle film-grain/paper-noise overlay across the page background; no drop shadows or glassmorphism; slightly worn/imperfect edges rather than crisp geometry
- **Motion:** minimal — small hover transitions only, no flashy animation (keeps the "quiet café" mood rather than a lively/energetic one)

## Page Structure (single page, three sections)

### 1. Hero / About (`#about`)
- Typewriter-style headline: "MIRAC ŞİMŞEK — CO-FOUNDER & ENGINEER"
- Profile photo (user-supplied), styled with a sepia/polaroid-style frame
- Short intro copy (to be drafted with the user during implementation)
- Icon links: GitHub, LinkedIn, Email

### 2. Projects (`#projects`)
Two project cards, styled as paper/index cards:
- **Qrucial** — AI-powered team management platform — links to https://qrucial.app
- **Leenar** — no-code multi-agent orchestration platform — links to https://leenar.net

### 3. Contact (`#contact`)
- Closing section restating contact channels:
  - Email: miracsimsek@leenar.net
  - LinkedIn: https://www.linkedin.com/in/miracsimsek/
  - GitHub: https://github.com/miracsimsek

No separate footer section beyond contact; no blog or experience/CV timeline (explicitly out of scope per user decision).

## Tech Stack

Plain HTML/CSS/JS — no build step, no framework. Deployed directly to GitHub Pages from the repo root (or `docs/` — decided during implementation planning). Chosen over the source site's React+Vite stack because a static personal portfolio of this size doesn't need componentization or a build pipeline, and it keeps deployment friction-free (push to `main`, GitHub Pages serves it directly).

Files: `index.html`, `style.css`, `script.js` (script only if needed for grain overlay / minor interactivity — no JS framework).

## Content Provided by User

- Name: Mirac Şimşek
- Title: Co-Founder & Engineer
- Email: miracsimsek@leenar.net
- LinkedIn: https://www.linkedin.com/in/miracsimsek/
- GitHub: https://github.com/miracsimsek
- Projects: Qrucial (https://qrucial.app), Leenar (https://leenar.net) — descriptions reused from the reference site, confirmed accurate by the user: Qrucial = AI-powered team management platform, Leenar = no-code multi-agent orchestration platform
- Profile photo: to be supplied by the user during implementation

## Explicitly Out of Scope

- Experience/CV timeline section
- Blog/writing section
- React/build tooling
- Neo-brutalist visual elements from the reference site (thick borders, offset shadows, primary-color blocks)
