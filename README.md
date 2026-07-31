# June's Art Nail — Studio Website

Marketing site for **June's Art Nail**, a nail studio in Lodi, NJ.
Manicures, pedicures, and waxing.

A single-page static site — no build step, no framework, no dependencies.
Just HTML, CSS, and a little vanilla JavaScript.

## Structure

```
juneartnails/
├── index.html        # the entire site (inline CSS + JS)
├── assets/
│   ├── gallery-01.jpg # "The forever French"
│   └── gallery-02.jpg # "Cobalt, hand-painted"
├── vercel.json        # clean URLs, cache + security headers
├── design.md          # the design system / brand spec
└── README.md
```

## Run locally

Any static server works. With Node installed:

```bash
npx serve .
```

Or just open `index.html` in a browser.

## Deploy to Vercel

This is a zero-config static deployment.

**Option A — Vercel CLI**

```bash
npm i -g vercel
vercel        # preview deploy
vercel --prod # production deploy
```

When prompted for framework, choose **Other** (it's plain static HTML).
No build command, no output directory — Vercel serves the folder as-is.

**Option B — Git + Vercel dashboard**

1. Push this folder to a GitHub/GitLab/Bitbucket repo.
2. In Vercel, **Add New → Project** and import the repo.
3. Framework preset: **Other**. Leave build & output settings empty.
4. **Deploy.**

`vercel.json` handles clean URLs, long-lived caching for `/assets`, and
basic security headers automatically.

## Editing content

Everything lives in `index.html`:

- **Phone / booking** — search `tel:+19737784494` (and the `(973) 778-4494` label).
- **Address** — search `441 Passaic Ave`.
- **Hours** — the `<ul class="hours">` list; today's row is highlighted
  automatically by the script.
- **Menu & services** — the `.svc-list` and `.menu-grid` sections.
- **Shades of the month** — the `.chips` grid (six `--c` gradient swatches).
- **Gallery** — swap the files in `assets/` and update the `alt` text.

Design tokens (colors, fonts, motion) are documented in [design.md](design.md).
