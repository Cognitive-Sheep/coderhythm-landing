# Coderhythm landing

Landing page for Code Rhythm, which creates thematic music albums for programmers, helping them achieve deep work focus.

## Preview locally

From the repo root:

```bash
python3 -m http.server 8000
```

Open http://localhost:8000/. Press Ctrl+C to stop the server.

## Repository layout

- `index.html` — the landing page itself, a single static HTML file.
- `assets/` — PNG images plus vendored CSS and JS bundles. `index.html` loads most of them; some are unreferenced leftovers.
- `CNAME` — the custom domain, `coderhythm.art`.
- `AGENTS.md` — notes for coding agents on the stack, layout and commands.
- `README.md` — this file.
