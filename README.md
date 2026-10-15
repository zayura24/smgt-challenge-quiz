# SMGT Challenge: Seberapa Tangguh Lu?!

Kuis 10 soal kampanye collab Cellos × SMGT. Situs statis satu halaman, tanpa build step dan tanpa dependensi npm.

Live: https://smgt-challenge-quiz.vercel.app

## Isi folder

| File | Fungsi |
|---|---|
| `index.html` | Seluruh aplikasi (HTML, CSS, JS) |
| `cellos-juara.jpg` | Foto Cellos di hero dan avatar |
| `vendor/phosphor/` | Ikon Phosphor 2.1.1 (MIT), di-host sendiri |
| `vercel.json` | Header keamanan dan cache untuk Vercel |

Gambar tokoh, logo, dan foto produk diambil dari `https://umm-website.vercel.app/assets/img/` (lihat `ASSET` di `index.html`).

## Upload / deploy

Upload isi folder ini apa adanya ke hosting statis mana pun (Vercel, Netlify, Cloudflare Pages, cPanel, S3).

Dengan Vercel CLI:

```bash
npx vercel@latest deploy --prod
```

Preview lokal: buka lewat server statis apa pun, misalnya `npx serve .`. Jangan buka `index.html` langsung dari file, karena kartu share butuh origin http.

## Wajib diisi sebelum promosi

Semua ada di objek `CONFIG` di bagian atas `<script>` di `index.html`.

| Kunci | Status sekarang | Isi dengan |
|---|---|---|
| `lead.endpoint` | kosong, lead tidak terkirim | URL penerima POST JSON (Supabase Edge Function, Apps Script, webhook CRM) |
| `lead.platformUrl` | sementara `umm-website.vercel.app` | URL login/daftar platform Challenge 7 Hari |
| `lead.batchMulai` | `Senin depan` | jadwal batch berikutnya |
| `produk.toko[].url` | `shopee.co.id`, `shop.tiktok.com` | link toko resmi SMGT! |
| `analyticsEndpoint` | kosong | opsional, penerima event via `sendBeacon` |

Tracking: pasang GTM, GA4, Meta Pixel, atau TikTok Pixel di `<head>`. Semua event otomatis masuk ke `dataLayer`, `gtag`, `fbq`, dan `ttq` bila ada. Tambahkan `?debug=1` di URL untuk melihat event di layar.

Event (semua diberi awalan `smgt_` saat dikirim): `landing_view`, `challenge_visit`, `quiz_cta`, `age_input`, `age_gate_block`, `gender_pick`, `quiz_start`, `quiz_progress`, `quiz_complete`, `card_open`, `share`, `share_cta_atas`, `challenge_link_create`, `nama_diminta`, `nama_diisi`, `nama_batal`, `detail_open`, `habit_check`, `misi_lihat_semua`, `lead_start`, `lead_submit`, `lead_error`, `platform_open`, `offer_click`, `quiz_restart`.

Data lead (nama, email, nomor WA) hanya dikirim ke `lead.endpoint`, tidak pernah ke analytics.

## Link tantangan

`?dari=<tokoh>&s=<skor>&nama=<nama>`. Teman sesama gender melihat duel skor; pasangan lawan jenis langsung melihat kombinasi tokoh.

## Sebelum tayang

- Copy atas nama Cellos dan klaim manfaat SMGT! perlu disetujui tim Cellos dan tim regulasi.
- Batas usia 21+: pengguna mengisi umur sendiri (21-99), bukan verifikasi identitas. Umur juga menentukan segmen suara copy: `muda` (<30), `inti` (30-44), `senior` (45+), dan tersimpan di `localStorage` perangkat.
- Belum ada gambar preview link (`og:image`, JPG 1200×630).
