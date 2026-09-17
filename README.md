# CAT 2026 — Sectionals & Workshops

A static portal for IMS CAT 2026 practice: a PIN-gated landing hub, five self-contained
sectional papers (Numbers, DILR, Geometry, Arithmetic, Algebra), an admin console, and a
Workshops area. Hosted on GitHub Pages.

This is a clone of the original **CAT26-Sectionals** frontend by Vipul TG, set up for use
by the IMS team.

## Structure

| Path              | What it is                                                        |
|-------------------|-------------------------------------------------------------------|
| `index.html`      | PIN-gated landing hub — lists a student's papers                  |
| `Numbers/`, `DILR/`, `Geometry/`, `Arithmetic/`, `Algebra/` | The five sectional papers |
| `admin.html`      | Faculty admin console (connect your Worker + ADMIN_KEY here)      |
| `Workshops/`      | Workshops area — scaffolded, ready for content                    |
| `.nojekyll`       | Tells GitHub Pages to serve files as-is                           |

## ⚠️ Backend

Only the **frontend** lives in this repo. Every page calls a Cloudflare Worker for the PIN
roster, paper unlocking, scoring, cohort rank, and admin actions:

```js
CONFIG.ENDPOINT = "https://ims-cat26.vipul-tg.workers.dev"
```

That Worker belongs to the original author and is **not** included here. As shipped, this
clone authenticates against, and submits to, that backend.

To make it fully yours you need your own Worker exposing the same API, then update
`CONFIG.ENDPOINT` in `index.html` and each paper. Setting `ENDPOINT` to `""` makes the
individual papers run in offline mode (questions are baked in), but the landing hub needs a
Worker to sign anyone in. The admin console lets you point at your own Worker URL directly.

## Local preview

```bash
python3 -m http.server 8000
# open http://localhost:8000
```
