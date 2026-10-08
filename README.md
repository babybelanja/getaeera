# Aeera — Showcase

Situs *showcase* (bukan toko) untuk merek **Aeera** di bawah naungan
**PT Babybelanja Berkah Bersama**. Mengikuti *register* Aesop: warna netral hangat,
teks yang tenang, dan fotografi yang lembut. Tanpa keranjang, tanpa harga —
transaksi dialihkan ke WhatsApp / marketplace / situs mitra.

- Dibangun dengan **Jekyll 4.4**
- Deploy: **GitHub Actions** (`.github/workflows/pages.yml`) → GitHub Pages
- Domain: `showcase.getaeera.id` (lihat `CNAME` — sesuaikan bila perlu)

## Struktur

```
_config.yml               # konfigurasi situs, collections, plugins, sass
_data/site.yml            # navigasi, kontak, sosial, analytics
_data/brands.yml          # Aeera (utama) + Samuroh
_includes/                # head, header, footer, analytics
_layouts/default.html     # shell halaman
_layouts/brand.html       # halaman "kenali merek"
_brands/aeera.md          # konten halaman merek (collection)
_brands/samuroh.md
_sass/                    # token, base, tipografi, komponen
assets/css/main.scss      # meng-@use seluruh partial
assets/img/               # placeholder SVG (fase 1)
index.html                # narasi beranda
404.html
ART-DIRECTION.md          # brief fotografi
TONE.md                   # panduan nada penulisan
```

## Menjalankan secara lokal

```sh
bundle install
bundle exec jekyll serve --livereload
# buka http://127.0.0.1:4000
```

## Deploy

Push ke branch `main` memicu workflow GitHub Actions untuk build dengan
`JEKYLL_ENV=production` lalu menerbitkan ke GitHub Pages.

> Setel Pages **Source** ke **GitHub Actions** di
> Settings → Pages → Build and deployment.

## Catatan

- `opencode.json` bersifat lokal dan tidak diikutsertakan (lihat `.gitignore`).
- `Gemfile.lock` di-commit agar build Actions reprodusibel.
- `jekyll_picture_tag` sengaja belum dipakai di fase 1 (butuh lib native di CI);
  ditambahkan saat fotografi asli siap (fase 2).
