# WORKLOG: Website Portofolio Agung Gumelar

## METADATA
- **Direktori:** `01_Projects/portofolio-agung-gumelar`
- **Tanggal Mulai:** 2026-11-17
- **Tanggal Pembaruan & Audit QA:** 2026-11-21
- **Komando Tertinggi:** Mas Agung Gumelar
- **Pure Orchestrator:** Bunga
- **Sub-Agent Eksekutor:** Lala (Frontend & Vercel), Amelia (Caveman Optimizer & QA Guard), Angelica (DevOps & CI/CD Pipeline)
- **Status Proyek:** `DEPLOYED (PRODUCTION)`

## 1. OBJEKTIF & RUANG LINGKUP
Membangun dan memelihara website portofolio resmi **Agung Gumelar** (Event Organizer, Project Management, Creative Production, serta rekam jejak kepemimpinan organisasi) dengan arsitektur zero-bloat (`index.html` statis + Tailwind CSS + Lucide Icons + Vanilla JS) yang dapat dijalankan baik secara offline (`file://`) maupun di-host pada Vercel (`outputDirectory: "."`).

Pembaruan dan audit QA pada siklus **2026-11-21** mencakup:
1. Penambahan interaksi **Modal Galeri Foto** (`#gallery-modal`) yang memuat **113 aset dokumentasi foto dari 18 event** (`EVENTS_GALLERY` di `index.html` tersinkronisasi 100% dengan `events_gallery.json`), lengkap dengan navigasi prev/next, keyboard shortcut (`Escape`, `ArrowLeft`, `ArrowRight`), thumbnail strip, dan fallback image.
2. Perbaikan typo pada kartu organisasi menjadi **`BEM FKOM Universitas Kuningan`** (`index.html` baris 1240).
3. Penambahan atribut **`onerror` fallback pada 18/18 kartu event** (`index.html`), serta verifikasi seluruh path fallback menuju `./assets/images/`.
4. Audit integritas case-sensitive path seluruh aset dan pengecekan kesiapan deployment Vercel via CLI.

## 2. TIMELINE & FASE PENGEMBANGAN
- [x] Fase 1: Perencanaan Arsitektur & Spesifikasi Portofolio (Bunga)
- [x] Fase 2: Implementasi Landing Page, Modal Galeri 113 Aset (18 Event), Perbaikan Typo `BEM FKOM Universitas Kuningan`, & `onerror` Fallback 18/18 Kartu (Lala)
- [x] Fase 3: Audit QA Ketat, Verifikasi Case-Sensitive Asset & Mechanical Proof Exit Code 0 (Amelia)
- [x] Fase 4: Deployment Produksi ke Vercel via CLI (`npx --yes vercel --prod --yes`) & penambahan `.vercelignore` (Angelica)

## 3. DAFTAR DELIVERABLES
| Nama Berkas | Ukuran / Baris | Fungsi Utama | Penanggung Jawab |
|---|---|---|---|
| `index.html` | 1,850 lines (155,091 bytes) | Halaman utama portofolio, filter event, modal galeri 113 foto (18 event), dan `onerror` fallback 18/18 kartu | Lala / Amelia |
| `events_gallery.json` | 349 lines (18,764 bytes) | Manifest metadata 18 event dan daftar 113 aset foto dokumentasi | Lala |
| `vercel.json` | 22 lines (446 bytes) | Konfigurasi static hosting Vercel v2 (`cleanUrls: true`, cache headers `/assets/*` & `/Event Organizer/*`) | Lala |
| `.vercelignore` | 13 lines | Mengecualikan berkas non-web (`WORKLOG.md`, `chat.bat`, `inventaris_event_organizer.txt`, `events_gallery.json`, dll.) dari upload Vercel | Angelica |
| `inventaris_event_organizer.txt` | 138 lines (23,419 bytes) | Inventaris folder & berkas dokumentasi Event Organizer | Rachel / Lala |
| `Event Organizer/` | 113 files (84.31 MB) | Aset foto dokumentasi asli dari 18 event | Lala |
| `assets/` | 41 files (25.47 MB) | Foto profil & aset fallback gambar untuk 18 event | Lala |
| `WORKLOG.md` | - | Catatan kerja resmi & bukti mekanis pengujian SOP Bunga Engine | Amelia |

## 4. BUKTI MEKANIS PENGUJIAN (MECHANICAL PROOF)
Audit QA terotomasi via Node.js (`v20.18.2`) memeriksa validitas JSON, sintaks JavaScript di seluruh tag `<script>`, kesinkronan `EVENTS_GALLERY` vs `events_gallery.json`, eksistensi **case-sensitive** untuk seluruh 113 foto + 18 cover + fallback, cakupan `onerror` pada 18/18 kartu event, serta pengecekan teks `BEM FKOM Universitas Kuningan`:

```text
VERCEL_JSON_VALID: true
GALLERY_EVENTS: 18
GALLERY_PHOTOS: 113
MISSING_COVERS: 0 []
MISSING_PHOTOS: 0 []
SCRIPT_BLOCKS_CHECKED: 2 JS_ERRORS: 0 []
EMBEDDED_EVENTS: 18 EMBEDDED_PHOTOS: 113
MISSING_EMBEDDED_FALLBACKS: 0 []
GALLERY_JSON_SYNC_DIFFS: 0 []
TOTAL_IMG_TAGS: 20 EVENT_CARD_IMGS: 18 EVENT_CARD_ONERROR: 18
DATA_EVENT_IDS: 18 [1,2,3,4,5,6,7,8,9,10,11,12,13,14,15,16,17,18]
IMG_SRC_MISSING: 0 []
IMG_ONERROR_MISSING: 0 []
DEPLOY_PAYLOAD_FILES: 159 DEPLOY_PAYLOAD_MB: 109.97
Command exited with code 0.
```

Verifikasi kesiapan Vercel CLI & link proyek:
```text
npx --no-install vercel --version -> 66.6.0
.vercel/project.json -> {"projectId":"prj_n7iJYdNjdEe69vmTEkwbf88wdhFx","orgId":"team_3VjEKEEjvAyTJgVVfwbFZoNU"}
D:\AI AGENT BUNGA\03_Resources\api vercel.txt -> True
Command exited with code 0.
```

**Catatan Kesiapan Deployment Vercel (QA Guard):**
- Konfigurasi proyek sudah siap (`vercel.json` valid, `.vercel/project.json` sudah ter-link, Vercel CLI `66.6.0` tersedia via `npx --no-install vercel`, dan token Vercel tersedia di `03_Resources/api vercel.txt`).
- **Perhatian Payload Size:** Total payload direktori saat ini adalah **159 file / 109.97 MB** (`Event Organizer/` 84.31 MB + `assets/` 25.47 MB), melebihi ambang 100 MB untuk static upload Vercel Hobby plan. Disarankan menambahkan `.vercelignore` (mengecualikan `chat.bat`, `inventaris_event_organizer.txt`, `WORKLOG.md`) dan/atau mengompresi foto berukuran >3 MB (seperti folder `Bakti Para Dulur Coklat` ~3.9 MB/foto) jika deployment CLI terkena batas ukuran unggahan.

## 5. PANDUAN PENGOPERASIAN
1. **Pratinjau Lokal:** Buka langsung `D:\AI AGENT BUNGA\01_Projects\portofolio-agung-gumelar\index.html` di browser, atau jalankan server statis lokal (`npx serve .`).
2. **Verifikasi Modal Galeri:** Klik salah satu dari 18 kartu event untuk membuka modal galeri foto (`#gallery-modal`), uji navigasi tombol panah/keyboard (`ArrowLeft`/`ArrowRight`/`Escape`), dan klik thumbnail.
3. **Deployment ke Vercel (via CLI):**
   ```powershell
   cd "D:\AI AGENT BUNGA\01_Projects\portofolio-agung-gumelar"
   $token = (Get-Content "D:\AI AGENT BUNGA\03_Resources\api vercel.txt" -Raw).Trim()
   npx vercel --prod --yes --token $token
   ```

## 6. BUKTI DEPLOYMENT PRODUKSI VERCEL (2026-11-21)
- **Executor:** Angelica (DevOps & CI/CD Pipeline Engineer)
- **Command:** `npx --yes vercel --prod --token <TOKEN> --yes` (token dibaca aman dari `D:\AI AGENT BUNGA\03_Resources\api vercel.txt`)
- **Exit Code:** `0`
- **Deployment ID:** `dpl_3it1k7Lt2D82Vvmq1wP3pQaCASLo`
- **Project:** `portfolio_mas_agung` (`team_3VjEKEEjvAyTJgVVfwbFZoNU`)
- **Status (`readyState`):** `READY` (`● Ready`)
- **Production Alias URL:** `https://portfoliomasagung.vercel.app` (terverifikasi `HTTP_STATUS: 200`)
- **Deployment URL:** `https://portfoliomasagung-1rg5v2wpm-agung-gumelar.vercel.app`
- **Inspector URL:** `https://vercel.com/agung-gumelar/portfolio_mas_agung/3it1k7Lt2D82Vvmq1wP3pQaCASLo`
- **Catatan:** `.vercelignore` telah dibuat untuk mengecualikan `WORKLOG.md`, `chat.bat`, `inventaris_event_organizer.txt`, `events_gallery.json`, dan berkas non-web lainnya sebelum upload.

## [2026-11-21 23:06:20] Production Deploy - Image Cleanup (Mechanical Proof Exit Code 0)
- Dikeluarkan foto personal Mas Agung topi bucket dari Napak Jagat Pasundan 2026 diganti foto budaya adat Sunda (IMG-20261115-WA0184.jpg).
- Dikeluarkan foto salah Euro Futsal dari kartu & galeri Ririungan Coklat Kita 2024.
- Deployment ID: dpl_CfRhT4VXDZ5cqwTLF8K2RYiHBbZT, readyState: READY, URL: https://portfoliomasagung.vercel.app

## [2026-11-21 23:23:46] Production Deploy - Mahasiswa Activity Carousel
- Penambahan carousel dokumentasi aktivitas kemahasiswaan Universitas Kuningan (12 kegiatan dengan 2 foto kurasi terbaik per kegiatan).
- Navigasi geser halus kiri/kanan dan interaksi hover foto sekunder.
- Deployment ID: dpl_vRX7V2bJa7Cut9WnqT4AdGXnpFVt, readyState: READY, URL: https://portfoliomasagung.vercel.app

## [2026-11-21 23:43:12] Production Deploy - Mahasiswa Gallery Grid & Role Corrections
- Mengganti format carousel menjadi grid galeri/portofolio acara (12 kartu kegiatan lengkap dengan filter kategori & pop-up modal foto).
- Mengoreksi peran PPK Ormawa Nasional menjadi Ketua Umum Project (Kemendikbudristek RI).
- Mengganti foto BEM FKOM 2024-2025 dengan foto bersama seluruh anggota (IMG-20240609-WA0024.jpg, resolusi 4160x3119).
- Menambahkan auto-refresh script Lucide icons pada DOMContentLoaded & load event agar seluruh ikon tampil sempurna.
- Live verified: HTTP 200, URL: https://portfoliomasagung.vercel.app/#mahasiswa
