# Aeera — Showcase

Situs *showcase* (bukan toko) untuk merek **Aeera** di bawah naungan
**PT Babybelanja Berkah Bersama**. Mengikuti *register* Aesop: warna netral hangat,
teks yang tenang, dan fotografi yang lembut. Tanpa keranjang, tanpa harga —
transaksi dialihkan ke WhatsApp / marketplace / situs mitra.

- Dibangun dengan **Jekyll 4.4**
- Deploy: **GitHub Actions** (`.github/workflows/pages.yml`) → GitHub Pages
- Repo: `babybelanja/getaeera`
- Domain: `getaeera.id` (apex + `www`) — lihat `CNAME`.
  `showcase.getaeera.id` diarahkan 301 ke apex.

## Struktur

```
_config.yml               # konfigurasi situs, collections (brands, products), plugins, sass
_data/site.yml            # navigasi, kontak, sosial, analytics, latest_product
_data/brands.yml          # bab merek di beranda
_data/resellers.yml       # direktori agen/reseller (116 agen)
_data/sizechart.yml       # panduan ukuran (per produk)
_includes/                # head, header, footer, analytics
_layouts/default.html     # shell halaman
_layouts/brand.html       # halaman "kenali merek"
_layouts/product.html     # halaman produk (swatch warna, galeri warna, tabel ukuran)
_brands/aeera.md          # konten halaman merek (collection)
_products/orelia.md       # halaman produk (collection) → /produk/orelia/
_sass/                    # token, base, tipografi, komponen
assets/css/main.scss      # meng-@use seluruh partial
assets/img/               # WebP fotografi
assets/img/slides/        # slide carousel beranda (16:9)
assets/img/orelia/        # foto colorway produk Orelia
index.html                # narasi beranda + produk terbaru (config-driven)
reseller.html             # /reseller/ — direktori agen
404.html
ART-DIRECTION.md          # brief fotografi
TONE.md                   # panduan nada penulisan
docs/plan.md               # catatan perencanaan (tak dipublikasikan)
```

> Produk terbaru di beranda dikendalikan satu nilai: `latest_product` di
> `_data/site.yml`.

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
