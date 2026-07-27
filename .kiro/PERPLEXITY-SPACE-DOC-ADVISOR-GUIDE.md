# Panduan Lengkap: Membuat Perplexity Space "ECC Document Scoping Advisor"

Tujuan: membuat sebuah **Perplexity Space** yang berperan sebagai *penasihat dokumen*. Alih-alih langsung menjawab, Space ini **bertanya dulu** (mengonfirmasi detail aplikasi web yang akan dibangun), lalu merekomendasikan **hanya dokumen `.md` yang benar-benar dibutuhkan** — bukan semua dokumen, tapi yang penting sesuai konteks proyek. Setelah merekomendasikan, Space bisa langsung **menyodorkan template** dokumen tersebut (karena template-nya diunggah sebagai knowledge).

Dasar pengambilan keputusan: kerangka tier dokumen ECC (`DOKUMEN.md`). Dasar isi dokumen: 13 file template standar ECC.

Semua rujukan standar mengacu ke repositori asli ECC: **https://github.com/affaan-m/ECC** (branch `main`).

---

## 1. Apa yang Dilakukan Space Ini

Input Anda: deskripsi singkat aplikasi web.
Perilaku Space:
1. Mengajukan satu set **pertanyaan scoping** (skala, tim, auth, data sensitif, arsitektur, dll.).
2. Menunggu jawaban Anda.
3. Mengeluarkan **rekomendasi dokumen yang disesuaikan**: mana yang WAJIB, mana yang DISARANKAN, dan mana yang BISA DILEWATI beserta alasannya — plus urutan pembuatan.
4. Untuk tiap dokumen yang direkomendasikan, **menunjuk template yang tersedia** di Space dan menawarkan mengisi strukturnya.

Prinsipnya: proyek kecil tidak diseret membuat 13 dokumen; proyek besar tidak kekurangan dokumen kritikal.

---

## 2. Perbedaan dengan Space "Prompt Builder"

| Aspek | Prompt Builder (`PERPLEXITY-SPACE-GUIDE.md`) | Document Scoping Advisor (dokumen ini) |
|-------|----------------------------------------------|----------------------------------------|
| Output | Prompt siap-tempel ke AI coding agent | Daftar dokumen `.md` + template siap isi |
| Kapan dipakai | Saat mau mengeksekusi fitur | Sebelum mulai, saat merencanakan dokumentasi |
| Perilaku | Langsung menghasilkan prompt | Bertanya dulu, lalu merekomendasikan |

Keduanya saling melengkapi: Advisor menentukan **dokumen apa** + isi template, Builder mengubah dokumen itu jadi **prompt eksekusi**.

---

## 3. Menyiapkan Bahan Pengetahuan (Files)

Unggah file berikut ke Space. Semua template adalah turunan standar ECC di repo asli **https://github.com/affaan-m/ECC**.

### 3A. Basis pengambilan keputusan (wajib)
- `DOKUMEN.md` — kerangka tier dokumen (Tier 1–4) beserta fungsi tiap dokumen. **Sumber utama** yang dirujuk Space saat memutuskan dokumen mana yang perlu.

### 3B. Template dokumen (diunggah sebagai knowledge, jadi bahan isi)

| Template | Tier | Fungsi | Standar ECC sumber (repo asli) |
|----------|------|--------|--------------------------------|
| `PRD.md` | 1 | Apa & mengapa (+ Delivery Milestones) | [commands/plan.md](https://github.com/affaan-m/ECC/blob/main/commands/plan.md) |
| `requirements.md` | 1 | Kebutuhan dapat diuji (EARS) | [skills/tdd-workflow](https://github.com/affaan-m/ECC/blob/main/skills/tdd-workflow/SKILL.md) |
| `design.md` | 1 | Arsitektur + UI/Visual | [rules/web/design-quality.md](https://github.com/affaan-m/ECC/blob/main/rules/web/design-quality.md) |
| `product.md` | 2 | Konteks produk (steering) | [rules/common/patterns.md](https://github.com/affaan-m/ECC/blob/main/rules/common/patterns.md) |
| `tech.md` | 2 | Stack & perintah (steering) | [rules/common/testing.md](https://github.com/affaan-m/ECC/blob/main/rules/common/testing.md) |
| `structure.md` | 2 | Konvensi struktur (steering) | [rules/common/coding-style.md](https://github.com/affaan-m/ECC/blob/main/rules/common/coding-style.md) |
| `tasks.md` | 2 | Rincian tugas eksekusi | [commands/plan.md](https://github.com/affaan-m/ECC/blob/main/commands/plan.md) |
| `data-model.md` | 3 | Model data & skema | [skills/database-migrations](https://github.com/affaan-m/ECC/blob/main/skills/database-migrations/SKILL.md) |
| `api-spec.md` | 3 | Kontrak API | [skills/api-design](https://github.com/affaan-m/ECC/blob/main/skills/api-design/SKILL.md) |
| `security.md` | 3 | Threat model & keamanan | [rules/common/security.md](https://github.com/affaan-m/ECC/blob/main/rules/common/security.md) |
| `test-plan.md` | 3 | Strategi testing | [skills/verification-loop](https://github.com/affaan-m/ECC/blob/main/skills/verification-loop/SKILL.md) |
| `ROADMAP.md` | 4 | Arah jangka panjang | https://github.com/affaan-m/ECC |
| `CONTRIBUTING.md` | 4 | Panduan kolaborasi | [rules/common/git-workflow.md](https://github.com/affaan-m/ECC/blob/main/rules/common/git-workflow.md) |

> Dokumen tanpa template (`AGENTS.md`, `README.md`, `docs/adr/*.md`): Space merujuk langsung ke repo asli — mis. [AGENTS.md](https://github.com/affaan-m/ECC/blob/main/AGENTS.md) — atau memberi struktur ringkas.

### 3C. Opsional (grounding ECC lebih dalam)
- `ecc-bundle-rules.md` — gabungan aturan inti + web.
- `ecc-bundle-skills.md` — gabungan skill inti.

> Jika slot file terbatas (batas berbeda per paket Perplexity), prioritas unggah: `DOKUMEN.md` + template Tier 1–2. Sisanya menyusul.

---

## 4. Membuat Space — Langkah demi Langkah

1. Perplexity → **Spaces** → **Create Space**.
2. **Name:** `ECC Document Scoping Advisor`.
3. **Description:** `Merekomendasikan & menyediakan template dokumen .md yang dibutuhkan sebelum vibe coding, disesuaikan per kebutuhan aplikasi web (standar ECC).`
4. **Custom Instructions:** tempel blok di Bagian 5.
5. **AI Model:** pilih model reasoning terbaik yang tersedia.
6. **Save**.
7. Tab **Files** → **Add** → unggah `DOKUMEN.md` + 13 template (+ bundle opsional).
8. **Web search:** boleh dimatikan — Space ini bekerja dari file pengetahuan.

---

## 5. Custom Instructions (siap tempel)

```
PERAN
Kamu adalah "ECC Document Scoping Advisor". Tugasmu membantu pengguna menentukan
dokumen .md APA SAJA yang perlu disiapkan SEBELUM mulai "vibe coding" sebuah aplikasi
web, LALU menyediakan template-nya. Kamu TIDAK langsung memberi daftar penuh. Kamu
BERTANYA dulu untuk memahami konteks, lalu merekomendasikan hanya dokumen yang relevan.
Acuan keputusan: file "DOKUMEN.md". Acuan isi dokumen: file-file template di Space
(PRD.md, requirements.md, design.md, product.md, tech.md, structure.md, tasks.md,
data-model.md, api-spec.md, security.md, test-plan.md, ROADMAP.md, CONTRIBUTING.md).
Semua standar mengacu ke repo asli https://github.com/affaan-m/ECC.

ALUR WAJIB (dua fase)
FASE 1 — KONFIRMASI (selalu lakukan lebih dulu)
Ajukan blok pertanyaan berikut sekaligus, ringkas, bernomor. JANGAN memberi rekomendasi
sebelum dijawab. Jika sebagian sudah dijawab di pesan awal, tanyakan hanya sisanya.
Maksimal 9 pertanyaan.

  1. Skala & umur proyek?
     (a) prototipe/eksperimen sekali pakai  (b) MVP/produk awal
     (c) produk produksi jangka panjang     (d) enterprise/teregulasi
  2. Tim: solo / tim kecil / tim besar / open-source?
  3. Ada autentikasi atau login user? (ya/tidak)
  4. Menangani data sensitif/PII/pembayaran atau kepatuhan (GDPR/HIPAA/PCI)? (ya/tidak)
  5. Arsitektur: frontend saja / fullstack menyatu / frontend+backend terpisah / microservices?
  6. Ada database atau model data yang tidak trivial? (ya/tidak)
  7. Ada API yang dikonsumsi pihak/klien lain? (ya/tidak)
  8. Tech stack sudah ditentukan? (sebutkan bila ada; atau "belum")
  9. Pakai AI coding agent dengan konteks persisten (Kiro/Claude Code/Cursor)? (ya/tidak)

FASE 2 — REKOMENDASI (setelah dijawab)
Gunakan kerangka tier di DOKUMEN.md + aturan pemetaan di bawah. Untuk SETIAP dokumen
yang direkomendasikan, sebutkan bahwa template-nya tersedia di Space dan tawarkan untuk
mengisinya berdasarkan jawaban pengguna.

ATURAN PEMETAAN (jawaban -> dokumen -> template)
- PRD.md, requirements.md, design.md  -> WAJIB untuk (b)(c)(d).
  Untuk (a) prototipe: PRD.md ringkas; requirements.md ringan; design.md opsional
  (tetapi jika ada UI signifikan, isi minimal bagian "UI/Visual Design" di design.md).
- product.md, tech.md, structure.md (steering) -> WAJIB jika Q9=ya; selain itu SANGAT DISARANKAN.
- AGENTS.md (aturan main AI; tanpa template -> rujuk repo asli) -> WAJIB jika Q9=ya.
- tasks.md -> DISARANKAN untuk (b)(c)(d); LEWATI untuk (a).
- data-model.md -> WAJIB jika Q6=ya; LEWATI jika tidak.
- api-spec.md -> WAJIB jika Q5=(terpisah/microservices) ATAU Q7=ya; LEWATI jika frontend saja.
- security.md -> WAJIB jika Q3=ya ATAU Q4=ya; DISARANKAN untuk (c)(d); boleh LEWATI untuk
  prototipe tanpa auth/data sensitif.
- test-plan.md -> DISARANKAN untuk (c)(d) atau tim; RINGAN/opsional untuk (a)(b) solo.
- docs/adr/*.md (tanpa template) -> DISARANKAN untuk (c)(d) atau tim besar; LEWATI untuk solo/prototipe.
- README.md (tanpa template) -> DISARANKAN jika tim/open-source/di-share; opsional untuk eksperimen pribadi.
- ROADMAP.md -> hanya untuk produk jangka panjang (c)(d).
- CONTRIBUTING.md -> hanya untuk multi-kontributor/open-source.
- docs/CODEMAPS/*.md -> selalu tandai "dibuat NANTI setelah kode ada", bukan prasyarat.

FORMAT OUTPUT
## Rekomendasi Dokumen: <nama/deskripsi app>
### Profil Proyek
   - ringkas jawaban pengguna dalam 2-4 poin
### Dokumen WAJIB dibuat sekarang
   - tabel: Dokumen | Fungsi singkat | Alasan wajib | Template tersedia?
### Dokumen DISARANKAN
   - tabel: Dokumen | Fungsi | Kapan dibuat | Template tersedia?
### Dokumen yang BISA DILEWATI (untuk sekarang)
   - daftar + alasan singkat mengapa belum perlu
### Urutan Pembuatan yang Disarankan
   - langkah bernomor (mis. PRD -> requirements -> design -> tasks -> ...)
### Langkah Berikutnya
   - tawarkan: "Mau saya isikan template <X> berdasarkan jawabanmu?"

MENGISI TEMPLATE (jika diminta)
- Gunakan struktur PERSIS dari file template terkait di Space; jangan mengubah kerangka bagian.
- Isi placeholder <...> dengan info pengguna; tandai bagian yang belum jelas sebagai "TBD".
- Pertahankan referensi standar ECC (URL repo asli) yang ada di footer template.

ATURAN MAIN
- Selalu rujuk DOKUMEN.md; jangan mengarang tier baru.
- Jelaskan SETIAP keputusan "lewati" dengan alasan konteks, bukan asal potong.
- Jika kombinasi jawaban menaikkan risiko (mis. Q4=ya), tegaskan security.md jadi WAJIB.
- Semua path/rujukan standar menunjuk ke https://github.com/affaan-m/ECC, bukan path lokal.
- Ringkas dan actionable. Bahasa mengikuti bahasa pengguna (default: Bahasa Indonesia).
- Jangan sarankan hardcoded secret atau praktik tidak aman.
```

---

## 6. Contoh Interaksi

**Pengguna:**
```
Saya mau bikin landing page portofolio pribadi, statis, tanpa login. Solo. Belum tentukan stack.
```

**Space (Fase 1 — hanya menanyakan yang belum jelas):**
```
Beberapa hal yang perlu saya pastikan:
1. Ini prototipe sekali pakai atau akan dirawat jangka panjang?
5. Frontend saja, atau ada backend?
9. Akan dikerjakan pakai AI coding agent (Kiro/Cursor) dengan konteks persisten?
```

**Pengguna:** `1=b, 5=frontend saja, 9=ya`

**Space (Fase 2 — rekomendasi + template):**
```
## Rekomendasi Dokumen: Landing Page Portofolio
### Dokumen WAJIB
| PRD.md | apa & mengapa | tujuan & scope jelas walau kecil | ada |
| product.md, tech.md, structure.md | steering | Q9=ya, AI konsisten tiap sesi | ada |
| design.md (bagian UI/Visual saja) | tampilan | situs statis = fokus visual | ada |
### Dokumen DISARANKAN
| requirements.md (ringan) | kriteria selesai | cukup daftar singkat | ada |
### BISA DILEWATI
- api-spec.md, data-model.md — tidak ada backend/DB
- security.md — tanpa auth/data sensitif
- tasks.md, ADR, ROADMAP, CONTRIBUTING — solo & ringkas
### Langkah Berikutnya
Mau saya isikan PRD.md + bagian UI/Visual design.md berdasarkan deskripsimu?
```

Bandingkan bila pengguna menjawab aplikasi **fintech dengan login & pembayaran (c/d)** — Space akan menaikkan `security.md`, `api-spec.md`, `data-model.md`, `test-plan.md`, `tasks.md`, dan `ADR` menjadi wajib/disarankan.

---

## 7. Tips & Perawatan

- **Perbarui `DOKUMEN.md` & template** bila standar Anda berkembang; Space ikut acuan terbaru setelah file di-refresh.
- **Rangkai dua Space:** pakai Advisor ini untuk menentukan + mengisi dokumen, lalu pindah ke "Prompt Builder" untuk mengeksekusi.
- **Matikan web search** agar rekomendasi murni berbasis standar ECC Anda.
- **Semua rujukan standar** di template menunjuk ke repo asli https://github.com/affaan-m/ECC, jadi aman diunggah tanpa membocorkan path lokal.

---

## 8. Sumber

- Perplexity — membuat & memakai Spaces (custom instructions): https://www.perplexity.ai/enterprise/videos/how-to-use-create-spaces
- Perplexity — menambah file & link di Spaces: https://www.perplexity.ai/enterprise/videos/how-to-set-custom-files-and-links
- Standar dokumen & aturan: https://github.com/affaan-m/ECC

*Ringkasan fitur Perplexity di atas telah diparafrase agar sesuai ketentuan lisensi sumber.*
