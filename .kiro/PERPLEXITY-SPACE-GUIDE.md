# Panduan Lengkap: Membuat Perplexity Space "ECC Web App Prompt Builder"

Tujuan: membuat sebuah **Perplexity Space** yang berfungsi sebagai *generator prompt* untuk pengembangan aplikasi web, di mana seluruh output-nya mengikuti aturan, referensi, dan pengetahuan dari **Everything Claude Code (ECC)** — TDD, security-first, immutability, standar coding, dan pola arsitektur.

Hasil akhir: Anda tinggal mengetik ide fitur, lalu Space mengeluarkan prompt siap-pakai yang bisa Anda tempel ke Kiro/Claude Code/Cursor untuk membangun fitur tersebut sesuai standar ECC.

---

## 1. Apa itu Perplexity Space

Perplexity Space adalah "ruang kerja" yang bisa Anda beri:

- **Custom instructions** — instruksi tetap (tone, format, aturan) yang berlaku untuk semua percakapan di dalam Space tersebut. ([sumber](https://www.perplexity.ai/enterprise/videos/how-to-use-create-spaces))
- **Files & links** — dokumen dan tautan yang jadi basis pengetahuan. File bisa dari lokal, konektor, atau URL. Pada tier Enterprise batasnya sampai 50 file per space. ([sumber](https://www.perplexity.ai/enterprise/videos/how-to-set-custom-files-and-links))

Kombinasi keduanya = Space yang "tahu" standar ECC (dari file) dan "berperilaku" sebagai prompt engineer ECC (dari custom instructions).

> Catatan: batas jumlah file berbeda per paket langganan. Angka 50 file adalah untuk Enterprise. Kalau paket Anda lebih terbatas, gunakan strategi **bundling** di Bagian 3B (menggabungkan beberapa file ECC menjadi satu).
>
> *Content was rephrased for compliance with licensing restrictions.*

---

## 2. Arsitektur Solusi

```
┌─────────────────────────────────────────────────────┐
│  Perplexity Space: "ECC Web App Prompt Builder"      │
│                                                       │
│  [Custom Instructions]  ← peran + aturan main (Bag.4)│
│  [Knowledge Files]      ← aturan ECC (Bag.3)          │
│                                                       │
│  Input Anda:  "fitur login OAuth"                     │
│  Output:      prompt lengkap siap tempel ke Kiro      │
└─────────────────────────────────────────────────────┘
```

---

## 3. Menyiapkan Bahan Pengetahuan dari ECC

### 3A. File yang direkomendasikan untuk diunggah

Fokus ke aturan umum + stack web (TypeScript/React/web) + skill inti. Semua path relatif terhadap root repo ECC (`/Users/fyi/ECC/`).

**Konteks utama (wajib):**
- `AGENTS.md` — prinsip inti ECC (agent-first, TDD, security-first, immutability)

**Aturan umum (`rules/common/`):**
- `coding-style.md`
- `security.md`
- `testing.md`
- `development-workflow.md`
- `git-workflow.md`
- `patterns.md`
- `performance.md`
- `code-review.md`

**Aturan spesifik web:**
- `rules/web/coding-style.md`, `rules/web/design-quality.md`, `rules/web/security.md`, `rules/web/performance.md`, `rules/web/testing.md`, `rules/web/patterns.md`
- `rules/typescript/coding-style.md`, `rules/typescript/security.md`, `rules/typescript/testing.md`, `rules/typescript/patterns.md`
- `rules/react/coding-style.md`, `rules/react/security.md`, `rules/react/testing.md`, `rules/react/patterns.md`

**Skill inti (`skills/<nama>/SKILL.md`):**
- `coding-standards`, `api-design`, `backend-patterns`, `frontend-patterns`
- `react-patterns`, `react-testing`, `nextjs-turbopack`
- `security-review`, `tdd-workflow`, `verification-loop`, `search-first`
- `deployment-patterns`, `docker-patterns`, `database-migrations`, `postgres-patterns`

Total ± 40 file — masih di bawah batas 50 (Enterprise).

### 3B. Opsi bundling (jika slot file terbatas)

Kalau paket Anda tidak mengizinkan banyak file, gabungkan jadi beberapa bundle tematik. Jalankan dari root repo ECC:

```bash
# Bundle 1: aturan inti + web
{ echo "# ECC CORE + WEB RULES"; \
  for f in AGENTS.md rules/common/*.md rules/web/*.md rules/typescript/*.md rules/react/*.md; do \
    echo -e "\n\n===== FILE: $f =====\n"; cat "$f"; done; } > ecc-bundle-rules.md

# Bundle 2: skill inti untuk web dev
{ echo "# ECC WEB SKILLS"; \
  for s in coding-standards api-design backend-patterns frontend-patterns \
           react-patterns react-testing nextjs-turbopack security-review \
           tdd-workflow verification-loop search-first deployment-patterns \
           docker-patterns database-migrations postgres-patterns; do \
    echo -e "\n\n===== SKILL: $s =====\n"; cat "skills/$s/SKILL.md"; done; } > ecc-bundle-skills.md
```

Hasilnya dua file (`ecc-bundle-rules.md`, `ecc-bundle-skills.md`) yang tinggal diunggah.

> Alternatif tanpa unggah file: Anda juga bisa menautkan URL GitHub raw dari file-file ECC sebagai "links" di Space, sehingga Space membacanya langsung dari repo publik.

---

## 4. Membuat Space — Langkah demi Langkah

1. Buka Perplexity → panel kiri → **Spaces** → **Create Space** (atau tombol `+`).
2. **Name:** `ECC Web App Prompt Builder`.
3. **Description:** `Menghasilkan prompt pengembangan aplikasi web sesuai standar ECC (TDD, security-first, immutability).`
4. **Custom Instructions:** tempel blok di Bagian 5 di bawah.
5. **AI Model:** pilih model penalaran terbaik yang tersedia (mis. varian reasoning) untuk kualitas prompt yang lebih tajam.
6. Simpan (**Save**). Space langsung dibuat.
7. Masuk ke tab **Files** → **Add** → unggah file dari Bagian 3A/3B (atau tempel link GitHub raw).
8. (Opsional) Set **Web search** sesuai kebutuhan: matikan bila ingin Space hanya bersandar pada file ECC; nyalakan bila ingin ia juga menautkan praktik terbaru.

---

## 5. Custom Instructions (siap tempel)

Salin seluruh blok di bawah ke kolom Custom Instructions:

```
PERAN
Kamu adalah "ECC Prompt Engineer" — spesialis yang mengubah ide fitur aplikasi web
menjadi PROMPT PENGEMBANGAN yang siap ditempel ke AI coding agent (Kiro, Claude Code,
Cursor). Setiap prompt yang kamu hasilkan WAJIB mematuhi standar Everything Claude Code
(ECC) yang ada di file pengetahuan Space ini.

PRINSIP ECC YANG HARUS SELALU TERCERMIN
1. Agent-first — sarankan agent/skill ECC yang relevan (mis. /planner, /tdd-workflow,
   /code-reviewer, /security-reviewer, /api-design, /react-patterns).
2. Test-Driven — tes ditulis lebih dulu (RED-GREEN-REFACTOR), target coverage >=80%.
3. Security-first — validasi semua input, tanpa hardcoded secret, cegah SQLi/XSS/CSRF,
   rate limiting, error tidak membocorkan data sensitif.
4. Immutability — buat objek baru, jangan mutasi.
5. Plan-before-execute — mulai dari rencana bertahap sebelum menulis kode.
6. File kecil & fokus (<800 baris), organisasi per fitur/domain.

FORMAT OUTPUT (selalu gunakan struktur ini)
## Prompt: <nama fitur>
### 1. Konteks & Tujuan
   - ringkas fitur, pengguna, dan kriteria sukses yang terukur
### 2. Tech Stack & Batasan
   - sebut stack (mis. Next.js + TypeScript + PostgreSQL) & batasan yang relevan
### 3. Agent/Skill ECC yang dipakai
   - urutan pemanggilan, mis. /planner -> /tdd-workflow -> /code-reviewer -> /security-reviewer -> /verification-loop
### 4. Requirements Fungsional
   - daftar bernomor, spesifik, dapat diuji
### 5. Requirements Non-Fungsional (ECC)
   - keamanan, performa, aksesibilitas, error handling, logging
### 6. Rencana Implementasi Bertahap
   - fase-fase kecil dengan dependensi & risiko
### 7. Strategi Testing
   - unit/integration/e2e + target coverage + kasus uji kunci (termasuk edge case)
### 8. Definition of Done
   - checklist: tes hijau, coverage >=80%, tanpa secret, lint bersih, review lulus
### 9. Prompt Final (blok siap-tempel)
   - satu blok teks utuh yang bisa langsung disalin ke AI coding agent

ATURAN MAIN
- Selalu rujuk aturan konkret dari file ECC bila relevan; sebut nama file/skill sumbernya.
- Jika informasi kurang, ajukan maksimal 3 pertanyaan klarifikasi SEBELUM membuat prompt.
- Jangan pernah menyarankan hardcoded secret; selalu pakai environment variable.
- Bila fitur menyentuh auth/pembayaran/data sensitif, WAJIB tambahkan langkah
  /security-reviewer dan checklist keamanan OWASP Top 10.
- Bahasa output mengikuti bahasa permintaan pengguna (default: Bahasa Indonesia).
- Ringkas namun lengkap; hindari basa-basi.
```

---

## 6. Cara Menggunakan Space

### Pola query dasar

```
Buatkan prompt pengembangan untuk: <deskripsi fitur>
Stack: <mis. Next.js 16 + TypeScript + PostgreSQL + Prisma>
```

### Contoh query

```
Buatkan prompt pengembangan untuk: sistem autentikasi user dengan OAuth Google
dan email/password, termasuk reset password.
Stack: Next.js + TypeScript + PostgreSQL + Prisma. Deploy di Vercel.
```

Space akan mengembalikan dokumen berstruktur (Bagian 1-9), diakhiri **Prompt Final** yang bisa langsung Anda tempel ke Kiro. Karena file ECC ada di Space, prompt itu otomatis menyertakan langkah `/tdd-workflow`, checklist keamanan, target coverage 80%, dsb.

### Alur kerja ujung-ke-ujung

```
1. Perplexity Space   → hasilkan "Prompt Final"
2. Salin Prompt Final → tempel ke sesi Kiro
3. Di Kiro:  /planner → /tdd-workflow → /code-reviewer → /security-reviewer → /verification-loop
```

---

## 7. Contoh Ringkas Output yang Diharapkan

Untuk query "form kontak dengan proteksi spam", Space kira-kira menghasilkan:

```
## Prompt: Form Kontak dengan Proteksi Spam
### 3. Agent/Skill ECC yang dipakai
   /planner -> /api-design -> /tdd-workflow -> /security-reviewer -> /verification-loop
### 5. Requirements Non-Fungsional (ECC)
   - Validasi input server-side (rujuk rules/common/security.md)
   - Rate limiting + honeypot/CAPTCHA (cegah spam)
   - Tanpa secret di kode; SMTP key via env var
...
### 9. Prompt Final
   "Bangun endpoint POST /api/contact di Next.js + TypeScript. Terapkan TDD:
    tulis tes gagal dulu... validasi Zod... rate limit... target coverage 80%..."
```

---

## 8. Tips, Perawatan & Batasan

- **Perbarui file saat ECC berubah.** Kalau Anda menarik update ECC (aturan/skill baru), unggah ulang file terkait atau regenerasi bundle di Bagian 3B.
- **Pisahkan Space per stack** bila perlu — mis. satu Space untuk React/Next, satu untuk backend Node, agar file lebih terfokus dan relevan.
- **Web search:** matikan bila Anda ingin jawaban murni berbasis ECC; nyalakan bila ingin ia menambah referensi versi library terbaru (Space tetap mengutip sumbernya).
- **Verifikasi output.** Space membantu menyusun prompt, tapi keputusan akhir arsitektur tetap di tangan Anda — tinjau Prompt Final sebelum dieksekusi.
- **Privasi.** Jangan unggah file ECC yang berisi path personal atau kredensial; file rules/skills ECC bersifat publik jadi aman.

---

## 9. Sumber

- Perplexity — cara membuat & memakai Spaces (custom instructions): https://www.perplexity.ai/enterprise/videos/how-to-use-create-spaces
- Perplexity — menambah file & link di Spaces (batas 50 file Enterprise): https://www.perplexity.ai/enterprise/videos/how-to-set-custom-files-and-links

*Ringkasan fitur Perplexity di atas telah diparafrase agar sesuai ketentuan lisensi sumber.*
