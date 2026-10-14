# Aeera Showcase — Project Plan

Plan for a new, premium, Apple/Aesop-register **product showcase** (not a store)
for Aeera, under the PT Babybelanja Berkah Bersama umbrella.

> **Scope note: this document is the planning record for the `getaeera` project
> (this repository). The `babybelanja.github.io` site and the `getaeera.com`
> PHP store are separate and **not modified** by this plan.**

---

## 1. Goal

Build a brand showcase in the **Aesop register**: warm neutrals, copy-led
literary Indonesian, Aeera as hero, Babybelanja as umbrella. No cart, no prices —
transactions route off-site (WhatsApp / marketplace / partner sites).

Primary reference: **Aesop**. Supporting references, each for one reason:
The Row (whitespace/restraint), Arc'teryx Veilance (product deep-dive),
COS (full-bleed image rhythm), On (scroll choreography).

---

## 2. The Aesop register — rules

1. **Warm neutrals, no stark white, no loud accents.** Parchment/sand/stone/charcoal;
   a single muted ochre accent.
2. **Copy-led, literary, calm.** Words carry equal weight to images; long-form, unhurried.
3. **Serif display with italic accents.** Fraunces for display, Plus Jakarta Sans for UI;
   small-caps labels, wide letter-spacing, hairline rules.
4. **Full-bleed, warm, muted photography.** Slow, gentle reveals — no parallax whiplash.
5. **Understated UI.** Text links, thin rules, small caps. No gradients, no glassmorphism.

---

## 3. Design tokens

| Token        | Value                    | Use                          |
| ------------ | ------------------------ | ---------------------------- |
| `--bg`       | `#f4f0e8`                | Page background (parchment)  |
| `--bg-soft`  | `#ebe5d9`                | Alternating sections (sand)  |
| `--ink`      | `#2b2b28`                | Primary text (charcoal)      |
| `--ink-soft` | `#6b6a63`                | Secondary text               |
| `--rule`     | `#d8d2c6`                | Hairline rules               |
| `--ochre`    | `#a9843c`                | Accent (muted)               |

- **Display:** Fraunces, italic used for emphasis.
- **UI/body:** Plus Jakarta Sans.
- **Labels:** uppercase, `0.72rem`, `0.14em` letter-spacing, weight 500.
- **Rules:** `1px` solid `--rule`; generous whitespace; no shadows/gradients.

---

## 4. Repository structure (new project)

```
_config.yml                  # collections, defaults, sass, plugins
_data/site.yml               # nav, contact, social, analytics id
_data/brands.yml             # Aeera (hero) + Samuroh entries
_includes/head.html          # meta, seo tag, fonts, JSON-LD
_includes/header.html        # minimal nav (word links, small caps)
_includes/footer.html        # quiet footer
_includes/analytics.html     # gtag (single source, removes duplication)
_layouts/default.html        # slim shell
_layouts/brand.html          # per-brand "learn more" page
_brands/aeera.md             # collection, output: true
                             # (Samuroh has no standalone page — home mention only)
index.html                   # Aesop narrative
404.html                     # restyled warm neutral
_sass/                       # _variables, _base, _type, _components
assets/css/main.scss         # @use partials; sass compressed
assets/img/                  # WebP photography
assets/img/slides/           # hero carousel slides (webp, 16:9)
Gemfile                      # + jekyll-seo-tag, jekyll-sitemap, jekyll-minifier
.github/workflows/pages.yml  # GitHub Actions deploy
CNAME                        # custom domain (getaeera.id — apex; flip pending DNS)
ART-DIRECTION.md             # photography brief (deliverable)
TONE.md                      # copy tone guide (deliverable)
docs/plan.md                 # this planning record (excluded from build)
```

---

## 5. Home narrative

1. **Opening line** — full viewport, serif, one quiet statement.
   Draft: *"Pakaian yang tenang. Dibuat untuk bertahan."*
2. **Manifesto** — 2–3 short paragraphs (amanah, ketenangan, keberkahan); copy-led.
3. **Aeera chapter** — full-bleed image + 3 lines + "Kenali Aeera →".
4. **Samuroh chapter** — quieter, secondary; **no standalone page** (mention only).
5. **Craft essay** — "Bahan & Ketelitian" (kain, jahitan, siluet) — the ingredient story.
6. **Kontak** — quiet contact block, no hard sell.

---

## 6. Copy tone guide (summary; full version in `TONE.md`)

- Calm, literary, unhurried; short declarative sentences.
- Concrete nouns: kain, jahitan, siluet, warna.
- **Avoid:** superlatives, exclamation marks, urgency, "mewah".
- Voice: declarative, minimal first-person; sparse "kami"/"Anda".

---

## 7. Art-direction brief (summary; full version in `ART-DIRECTION.md`)

- **Light:** soft, diffused window light; single warm key; gentle falloff.
- **Palette:** warm neutrals only — sand, stone, cream, charcoal; natural skin tones.
- **Set:** uncluttered — linen, plaster, stone; no competing props.
- **Crop/lens:** one focal length (~85mm), consistent negative space;
  3:4 portrait for product, 16:9 for lifestyle.
- **Deliverables:** 2400px+ masters, WebP/AVIF, hero image LCP-preloaded.

---

## 8. Jekyll implementation notes

- Jekyll Sass converter (`sass: { style: compressed }`) with CSS custom properties.
- Reveal-on-scroll via IntersectionObserver (as in the current site), slowed and softened.
- Plugins: `jekyll-seo-tag`, `jekyll-sitemap`, `jekyll-minifier`.
  (Skip `jekyll_picture_tag` in phase 1 — needs native image libs in CI; add in phase 2
  with real photography.)
- Analytics ID centralised in `_data/site.yml`; GA retained.

---

## 9. Phasing

1. **Now** — scaffold new repo; structure refactor; Aesop restyle; full Indonesian copy
   + `TONE.md`; `ART-DIRECTION.md`; placeholders; brand pages.
2. **After shoot** — replace placeholders with real imagery; add AVIF/WebP pipeline.
3. **Later** — journal (`_posts` + `jekyll-feed`); Lighthouse/sitemap polish.

---

## 10. Verification

- `bundle install && bundle exec jekyll build` with `JEKYLL_ENV=production`.
- `bundle exec jekyll serve --livereload` for local review.
- Confirm the GitHub Actions workflow builds green on the default branch.

---

## 11. Orelia — colors, size chart, resellers (planned)

Extend the showcase with richer Orelia product information. Still **no prices**;
transactions route off-site (WhatsApp / reseller).

### 11.1 Product model

- Add a `products` collection → `permalink: /produk/:name/`.
- `_products/orelia.md` + `_layouts/product.html` (hero, color swatches, size chart,
  prose, CTA).

### 11.2 Colors

- **Decision:** colors provided as **names + hex** by the client (Onyx is the first).
- **Source imagery:** shared Google Drive folder "Orelia" (see §12); per-colour photos
  can be pulled from there.
- Render as small muted swatch dots with labels (hairline ring), no loud fills;
  per-color image via a `colorways` gallery (photo, name, piece type).
- Store as a list in the product front matter:
  `colors: [{ name: Onyx, hex: "#2b2b28" }, …]` and
  `colorways: [{ name, piece, image, alt }, …]`.
- **Built (colors from client photos):** Onyx, Sky, Azure, Slate, Cream + eleven
  colorway photos — Dress (Sky, Onyx, Slate, Azure), One Set (Sky, Azure, Slate,
  Onyx), Mix One Set (Cream & Sky/Azure/Onyx). Hex sampled from imagery pending
  official values.
- **Interactive viewer:** picker swaps a single large photo (with a slow fade);
  clicking the photo opens a keyboard-accessible lightbox (`Esc`/arrows);
  the palette dots behind the selected colourway pulse (zoom + ochre ring).

### 11.3 Size chart

- **Decision:** measurements provided by the client.
- `_data/sizechart.yml`; columns e.g. lingkar dada / pinggang / panjang / lengan /
  lingkar pinggul.
- Rendered as a hairline-bordered table; horizontal-scroll on mobile (no zebra).

### 11.4 Resellers (agen)

- **Decision:** **list grouped by city** (text only; no map for now).
- **Source:** `https://linktr.ee/getaeera` — the "Agen <kota>" links, each a WhatsApp
  deep link. Extracted **116 agen across 59 kota** into `_data/resellers.yml`
  (`{ name, city, wa }`).
- `reseller.html` page; quiet list grouped by city, each linking `https://wa.me/<wa>`.
- **No street addresses** are published on the Linktree — only WhatsApp contacts.

### 11.5 Wiring

- Add **Orelia** (`/produk/orelia/`) and **Reseller** (`/reseller/`) to
  `_data/site.yml` nav (footer follows automatically) + a link from the Aeera brand page.

### 11.6 Status / open inputs

- [x] **Reseller page built** — `/reseller/`, grouped by city from
  `_data/resellers.yml` (116 agen / 59 kota), each a `wa.me` link, with a quiet
  client-side filter. Added to nav.
- [x] Colors built — `_products/orelia.md` + `_layouts/product.html` + `_components.scss`
  (swatches + `colorways` gallery); hex sampled from client photos, official values still welcome.
- [ ] Size chart measurements + which columns (client) — then `_data/sizechart.yml` + table.

---

## 12. Sources

- **Agen / reseller + social — Linktree "Aeera Official":**
  <https://linktr.ee/getaeera> Publicly accessible. Contains the "Agen <kota>"
  WhatsApp links (**116 agen / 59 kota** — captured in `_data/resellers.yml`) plus
  the brand's WhatsApp, Instagram, Facebook, YouTube, and Telegram accounts.
- **Orelia imagery — shared Google Drive folder "Orelia":**
  <https://drive.google.com/drive/folders/1N19yCXLK_fNcjrjT19jHXQZ4hWFUMcfe>
  Publicly shared. Contains **images only** (~50 JPEG/PNG, e.g. `Orelia - n.png`);
  **no documents** — no size chart, color list, or reseller list were present.
  Likely the fullest source for colourways and additional angles.
- **Upscaled derivatives (local):** `~/Downloads/upscaled` — 2400×3000 WebP plus
  4x JPEG masters; web-sized `.webp` committed under `assets/img/`.
  Derivative generation: ImageMagick (`magick`) crops/resizes; hero is a crossfade
  carousel of the slides.

> Note: size-chart measurements, colour names+hex, and reseller details must still be
> supplied directly (see §11.6) — they are not in the Drive folder.

---

## 13. Hosting model — subdirectory single-site at getaeera.id

**Decision (refined):** one site at **`getaeera.id`** (apex) with products as
**subdirectory paths** — `/produk/<slug>/` — rather than one repo per product on
subdomains. One repo, one domain, consolidated SEO.

- **Repo:** `babybelanja/getaeera` (umbrella; renamed from `orelia` ← `aeera-showcase`).
- **Products:** `products` collection → `permalink: /produk/:name/`,
  `_layouts/product.html`, `_products/<slug>.md`.
- **Latest product (config-driven):** `_data/site.yml` → `latest_product: <slug>`.
  The homepage "Produk terbaru" section reads this one value; change it per
  launch — no repo/domain settings change.
- **Apex = brand hub:** `getaeera.id` serves the homepage directly (featuring the
  latest product); no apex redirect needed. Only `showcase.getaeera.id` → 301 → apex.

### 13.1 DNS / domain
- DNS hosted at **Rumahweb** (registrar NS, no Cloudflare needed).
- Apex `@` → GitHub Pages **A** `185.199.108–111.153` (+ AAAA);
  `www` → `CNAME babybelanja.github.io` (**DNS-only**).
- Repo `CNAME` → `getaeera.id`; `_config.yml` `url` → `https://getaeera.id`.
- **Sequencing (avoid downtime):** add DNS first, then flip the repo's
  custom domain. Until then the site stays on `showcase.getaeera.id`.
- Retire `showcase.getaeera.id` with a 301 → `getaeera.id`.

### 13.2 SEO notes
- Subdomains are treated as separate sites by Google; subdirectories consolidate
  authority — hence the subdirectory choice.
- 301 `showcase → getaeera.id`; add `getaeera.id` to Search Console.
- Apex-as-redirect is a *moving* target; consider an apex **brand hub** later so
  `getaeera.id` builds its own authority.

### 13.3 Status
- [x] Repo renamed → `babybelanja/getaeera`.
- [x] `products` collection + `_layouts/product.html` + `_products/orelia.md`.
- [x] `latest_product` config + homepage "Produk terbaru" section.
- [x] DNS apex/www via **Rumahweb** (A → GitHub Pages, `www` CNAME) — no Cloudflare.
- [x] Flip custom domain `showcase` → `getaeera.id` (`CNAME` + `_config.yml`).
- [ ] Redirect `showcase.getaeera.id` → `getaeera.id` (301 via Rumahweb forwarding).
- [x] Colour names + hex sampled from photos + colorway gallery (official hex pending).
- [ ] Size-chart data (client).
