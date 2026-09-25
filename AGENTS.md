# AGENTS.md

Coderhythm landing page: one hand-authored static HTML page. No framework, no build step.

## Stack
- Plain HTML (`index.html`, ~1200 lines) styled with Tailwind utility classes in the markup.
- Scroll animations via AOS (`data-aos="..."` attributes) plus Animate.css; icons via Font Awesome.
- Also loaded: Font Awesome JS, GSAP, particles.js, PapaParse (all vendored under `assets/`).
- Published with GitHub Pages on the custom domain in `CNAME` (`coderhythm.art`).

## Layout
- `index.html` — the whole site: markup, inline `tailwind.config` (brand colours, fonts, keyframes), inline scripts.
- `assets/` — images plus vendored, prebuilt `style_*.css` / `script_*.js` with opaque hash suffixes.
- `assets/style_iandin.css` — the only hand-written stylesheet (`.video-container` etc.). Put custom CSS here.
- `CNAME` — GitHub Pages custom domain. Do not edit casually.

## Commands
- Serve locally (the only real command): `python3 -m http.server 8000` from the repo root, then open http://localhost:8000/.
- Install dependencies: none. No package manager, no dependencies.
- Build: none. The site is served from source; `assets/` is prebuilt and committed.
- Lint: none. No linter config exists.
- Test: none. No test suite or runner exists.
- `npm install` / `npm run ...` do nothing useful: there is no `package.json`. Do not run `npm init` or add tooling unasked.
- Sanity check after an edit: with the server running, the page and every `assets/...` path referenced by
  `index.html` should return HTTP 200 (checked: `/` and all 24 referenced assets returned 200).

## Conventions and gotchas
- Tailwind is a prebuilt bundle (`assets/script_9877227e.js`), not built from this repo. A utility class
  not already in that bundle has no effect (e.g. `grid-cols-3` and `aspect-video` are absent). There is no
  tooling here to rebuild it, so use classes that already work, or add custom CSS to `assets/style_iandin.css`.
- Load order in `index.html`: Tailwind bundle, Animate.css, AOS CSS, Font Awesome CSS, `style_iandin.css`,
  then FA/GSAP/particles/PapaParse scripts. The AOS script loads after the page content (~line 938), not in `<head>`.
- Hash-suffixed filenames in `assets/` are opaque. Reference them exactly as `index.html` does; don't rename them.
- Do not prune `assets/`: some files are unreferenced and some are byte-identical copies. That is pre-existing.
- Known caveat: `assets/style_885c2d39.css` (Font Awesome) expects `../webfonts/`, which does not exist, and
  `index.html` declares `@font-face` at `/chat/webfonts/`. Icon webfonts may not load.
- Known leftovers: `og:url` is still the placeholder `YOUR_ACTUAL_WEBSITE_URL_HERE`, and a few inline
  JS functions are stubs ("Implementation needed when code is downloaded").

## Deployment
- No CI, build or deploy pipeline in the repo. Anything merged to `main` goes live as-is, so check the page
  in a local static server first.
