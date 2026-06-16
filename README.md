# ON Tech — website (`on-tech-fe`)

Static bilingual (日本語 / English) marketing site for **ON Tech**. Plain HTML + CSS, no
JavaScript, no build step. Structured so more languages can be added later.

## Structure

```
/
├── index.html              # root: x-default language picker (no auto-redirect)
├── robots.txt
├── sitemap.xml             # all URLs + hreflang alternates
├── assets/
│   └── css/
│       └── style.css       # single shared stylesheet (all styling lives here)
├── ja/                     # Japanese (default language)
│   ├── index.html
│   ├── services.html
│   ├── pricing.html
│   ├── process.html
│   ├── about.html
│   ├── company.html
│   └── contact.html
└── en/                     # English (same page set, mirrored)
    └── …
```

**DRY note:** with plain HTML there is no server-side include, so the header/footer
markup repeats per page. All *styling* is centralized in `assets/css/style.css`
(colors, spacing, components — change once, applies everywhere). Page structure is
kept identical across pages so edits are mechanical.

## Run locally

Any static file server works. From the repo root:

```bash
python -m http.server 8000
```

Then open <http://localhost:8000/>. (Use a server, not `file://`, so the
root-relative `/assets/…` and `/ja/…` links resolve.)

## Before going live — replace placeholders

Search the repo for `TODO` and `ontech.co.jp`:

1. **Domain** — `https://ontech.co.jp` is a placeholder in every `canonical`,
   `hreflang`, Open Graph URL, `sitemap.xml`, and `robots.txt`. Replace with the
   real domain once secured.
2. **Email** — `info@ontech.co.jp` in contact/company pages and JSON-LD.
3. **OG image** — add `assets/img/og.png` and an `og:image` meta tag for nicer
   social/chat link previews.
4. **Favicon** — add `favicon.ico` / `apple-touch-icon.png` and link them.

## Adding a new language (e.g. `zh`)

1. Copy the `en/` folder to `zh/` and translate the content.
2. Set `<html lang="zh">` and translate nav/footer/labels.
3. In **every** page (all languages, incl. root + sitemap), add the reciprocal
   alternate so search engines link the versions:
   ```html
   <link rel="alternate" hreflang="zh" href="https://ontech.co.jp/zh/…">
   ```
4. Add the new URLs (with alternates) to `sitemap.xml`.
5. Add a link to the language switcher (`.lang-switch`) and root `index.html`.

## SEO / quality checklist (already in place)

- Unique `<title>` + meta description per page
- `canonical` + reciprocal `hreflang` (ja / en / x-default)
- Open Graph + Twitter card tags
- JSON-LD structured data (`ProfessionalService`, `Organization`, `BreadcrumbList`)
- `sitemap.xml` with hreflang alternates + `robots.txt`
- Semantic HTML5, skip-link, breadcrumbs, `aria-current`, responsive layout
