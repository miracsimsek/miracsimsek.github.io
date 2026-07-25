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
