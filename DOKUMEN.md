# Kerangka Dokumen Pra-Vibe-Coding (Standar ECC)

Dokumen ini adalah **basis keputusan** untuk Perplexity Space *"ECC Document Scoping Advisor"*. Isinya: dokumen `.md` apa saja yang dibutuhkan sebelum mulai "vibe coding" aplikasi web, fungsi masing-masing, keterkaitannya, dan aturan memilih **hanya yang penting sesuai kebutuhan** (tidak semua aplikasi butuh semua dokumen).

Semua rujukan standar mengacu ke repositori asli ECC: **https://github.com/affaan-m/ECC** (branch `main`). Setiap dokumen punya **file template** yang diunggah ke Space yang sama.

Filosofi inti ECC: **Plan Before Execute** + **konteks persisten via steering**. Vibe coding tanpa dokumen = AI menebak-nebak. Dokumen ini adalah "otak konteks" yang membuat AI konsisten dengan maksud Anda.

---

## Peta Keterkaitan Dokumen

```
                      PRD.md  (apa & mengapa)
                        │
                        ▼
               requirements.md  (kebutuhan dapat diuji / EARS)
                        │
                        ▼
                    design.md  (arsitektur + UI/visual)
                   /    │    \
                  ▼     ▼     ▼
        data-model.md  api-spec.md  security.md   (detail domain, sesuai kebutuhan)
                        │
                        ▼
                    tasks.md  (rincian eksekusi)  ───►  test-plan.md (strategi uji)

  Konteks persisten (dibaca AI tiap sesi):  product.md · tech.md · structure.md · AGENTS.md
  Tingkat proyek/tim (opsional):            ROADMAP.md · CONTRIBUTING.md · README.md · docs/adr/*
```

Alur turunan: **PRD → requirements → design → tasks**. `design.md` memicu dokumen detail (`data-model`, `api-spec`, `security`) hanya bila konteks membutuhkan. Dokumen steering menopang semuanya di setiap sesi.

---

## TIER 1 — Wajib (jangan mulai coding tanpa ini)

### 1. `PRD.md` — Product Requirements Document *(paling penting)*
- **Fungsi:** menjawab **APA** yang dibangun dan **MENGAPA**. Masalah, target pengguna, fitur utama, scope, kriteria sukses, dan tabel *Delivery Milestones*.
- **Template:** `PRD.md` · **Standar:** [commands/plan.md](https://github.com/affaan-m/ECC/blob/main/commands/plan.md)
- **Bertaut ke:** menjadi input `requirements.md` dan dibaca command `/plan`.

### 2. `requirements.md` — Requirements / Acceptance Criteria
- **Fungsi:** formalisasi PRD jadi kebutuhan **spesifik & dapat diuji**. User story + acceptance criteria format **EARS** ("WHEN… THE SYSTEM SHALL…"), plus non-fungsional. Fondasi TDD.
- **Template:** `requirements.md` · **Standar:** [skills/tdd-workflow](https://github.com/affaan-m/ECC/blob/main/skills/tdd-workflow/SKILL.md), [rules/common/testing.md](https://github.com/affaan-m/ECC/blob/main/rules/common/testing.md)
- **Bertaut ke:** diturunkan dari `PRD.md`; acceptance criteria dipakai `test-plan.md` dan `tasks.md`.

### 3. `design.md` — Technical Design + UI/Visual
- **Fungsi:** menjawab **BAGAIMANA**. Arsitektur, komponen, model data ringkas, interface/kontrak, state transition, keputusan teknis, keamanan, plus **bagian UI/Visual** (style direction, design tokens, aksesibilitas).
- **Template:** `design.md` · **Standar:** [rules/web/design-quality.md](https://github.com/affaan-m/ECC/blob/main/rules/web/design-quality.md)
- **Bertaut ke:** diturunkan dari `requirements.md`; mendetail ke `data-model.md`, `api-spec.md`, `security.md`; jadi dasar `tasks.md`.

---

## TIER 2 — Sangat Direkomendasikan (konteks persisten untuk AI)

Ini **steering files** — dibaca AI di *setiap* sesi. Krusial untuk vibe coding yang konsisten.

### 4. `product.md` — Ikhtisar Produk (steering)
- **Fungsi:** gambaran besar (apa, untuk siapa, prinsip) agar AI paham konteks tanpa diulang.
- **Template:** `product.md` · **Standar:** [rules/common/patterns.md](https://github.com/affaan-m/ECC/blob/main/rules/common/patterns.md)

### 5. `tech.md` — Stack Teknologi (steering)
- **Fungsi:** stack, dependency, perintah build/test/lint agar AI pakai tool yang benar.
- **Template:** `tech.md` · **Standar:** [rules/common/testing.md](https://github.com/affaan-m/ECC/blob/main/rules/common/testing.md)

### 6. `structure.md` — Konvensi Struktur (steering)
- **Fungsi:** organisasi file/folder (per fitur/domain, file kecil) agar AI menaruh kode di tempat benar.
- **Template:** `structure.md` · **Standar:** [rules/common/coding-style.md](https://github.com/affaan-m/ECC/blob/main/rules/common/coding-style.md)

### 7. `tasks.md` — Rincian Tugas Eksekusi
- **Fungsi:** memecah `design.md` jadi tugas kecil bertahap (Action/Mirror/Validate), peta jalan eksekusi.
- **Template:** `tasks.md` · **Standar:** [commands/plan.md](https://github.com/affaan-m/ECC/blob/main/commands/plan.md)
- **Bertaut ke:** tiap tugas dipetakan ke requirement di `requirements.md`.

### 8. `AGENTS.md` — Aturan Main untuk AI *(tanpa template — rujuk repo asli)*
- **Fungsi:** house rules AI (agent-first, TDD 80%+, security-first, immutability, konvensi commit).
- **Standar:** [AGENTS.md](https://github.com/affaan-m/ECC/blob/main/AGENTS.md)

---

## TIER 3 — Direkomendasikan (spesifik domain)

### 9. `data-model.md` — Model Data & Skema
- **Kapan:** ada database / model data tidak trivial.
- **Template:** `data-model.md` · **Standar:** [skills/database-migrations](https://github.com/affaan-m/ECC/blob/main/skills/database-migrations/SKILL.md), [skills/postgres-patterns](https://github.com/affaan-m/ECC/blob/main/skills/postgres-patterns/SKILL.md)
- **Bertaut ke:** mendetailkan bagian Model Data di `design.md`.

### 10. `api-spec.md` — Kontrak API
- **Kapan:** ada backend terpisah / microservices / API dikonsumsi pihak lain.
- **Template:** `api-spec.md` · **Standar:** [skills/api-design](https://github.com/affaan-m/ECC/blob/main/skills/api-design/SKILL.md)
- **Bertaut ke:** mendetailkan Interface/Kontrak di `design.md`.

### 11. `security.md` — Threat Model & Keamanan
- **Kapan:** **WAJIB** bila ada auth / data sensitif / PII / pembayaran / kepatuhan. Selain itu disarankan untuk produk produksi.
- **Template:** `security.md` · **Standar:** [rules/common/security.md](https://github.com/affaan-m/ECC/blob/main/rules/common/security.md), [skills/security-review](https://github.com/affaan-m/ECC/blob/main/skills/security-review/SKILL.md)
- **Bertaut ke:** memperdalam bagian Keamanan di `design.md`.

### 12. `test-plan.md` — Strategi Testing
- **Kapan:** produk produksi atau tim; ringan untuk MVP/solo.
- **Template:** `test-plan.md` · **Standar:** [skills/verification-loop](https://github.com/affaan-m/ECC/blob/main/skills/verification-loop/SKILL.md), [skills/tdd-workflow](https://github.com/affaan-m/ECC/blob/main/skills/tdd-workflow/SKILL.md)
- **Bertaut ke:** skenario uji dipetakan ke acceptance criteria di `requirements.md`.

---

## TIER 4 — Opsional (kematangan / skala tim)

### 13. `docs/adr/*.md` — Architecture Decision Records *(tanpa template)*
- **Kapan:** produk jangka panjang atau tim besar. Catatan keputusan + alasan.

### 14. `README.md` — Ikhtisar & Setup *(tanpa template)*
- **Kapan:** proyek di-share / tim / open-source. Bisa dibuat belakangan (bantu `doc-updater`).

### 15. `ROADMAP.md` — Arah Jangka Panjang
- **Kapan:** produk jangka menengah/panjang.
- **Template:** `ROADMAP.md` · **Standar:** https://github.com/affaan-m/ECC

### 16. `CONTRIBUTING.md` — Panduan Kolaborasi
- **Kapan:** multi-kontributor / open-source.
- **Template:** `CONTRIBUTING.md` · **Standar:** [rules/common/git-workflow.md](https://github.com/affaan-m/ECC/blob/main/rules/common/git-workflow.md), [rules/common/development-workflow.md](https://github.com/affaan-m/ECC/blob/main/rules/common/development-workflow.md)

### 17. `docs/CODEMAPS/*.md` — Peta Kode *(dibuat NANTI)*
- **Kapan:** setelah kode ada (dihasilkan `doc-updater`). Bukan prasyarat.

---

## Aturan Pemetaan (jawaban scoping → dokumen)

Dipakai Advisor untuk memangkas daftar sesuai kebutuhan:

| Kondisi | Dokumen | Status |
|---------|---------|--------|
| Proyek (b)(c)(d) | `PRD.md`, `requirements.md`, `design.md` | WAJIB |
| Prototipe sekali pakai (a) | `PRD.md` ringkas; `design.md` opsional | RINGAN |
| Pakai AI agent persisten (Kiro/Claude/Cursor) | `product.md`, `tech.md`, `structure.md`, `AGENTS.md` | WAJIB |
| Bukan agent persisten | steering di atas | SANGAT DISARANKAN |
| Ada database / model data | `data-model.md` | WAJIB (jika ya) |
| Backend terpisah / microservices / API publik | `api-spec.md` | WAJIB (jika ya) |
| Ada auth / data sensitif / PII / pembayaran / kepatuhan | `security.md` | WAJIB (jika ya) |
| Produk produksi (c)(d) atau tim | `test-plan.md`, `tasks.md` | DISARANKAN |
| Tim besar / jangka panjang | `docs/adr/*`, `ROADMAP.md` | OPSIONAL |
| Multi-kontributor / open-source | `CONTRIBUTING.md`, `README.md` | OPSIONAL |
| Prototipe / solo | `tasks.md`, `ADR`, `ROADMAP`, `CONTRIBUTING` | LEWATI |

---

## Ringkasan Prioritas

| # | Dokumen | Menjawab | Tier | Template |
|---|---------|----------|------|----------|
| 1 | `PRD.md` | Apa & mengapa | Wajib | ✔ |
| 2 | `requirements.md` | Kebutuhan dapat diuji | Wajib | ✔ |
| 3 | `design.md` | Bagaimana (arsitektur + UI) | Wajib | ✔ |
| 4 | `product.md` | Konteks produk (steering) | Sangat disarankan | ✔ |
| 5 | `tech.md` | Stack (steering) | Sangat disarankan | ✔ |
| 6 | `structure.md` | Konvensi struktur (steering) | Sangat disarankan | ✔ |
| 7 | `tasks.md` | Rincian tugas | Sangat disarankan | ✔ |
| 8 | `AGENTS.md` | Aturan main AI | Sangat disarankan | repo asli |
| 9 | `data-model.md` | Model data/skema | Disarankan | ✔ |
| 10 | `api-spec.md` | Kontrak API | Disarankan | ✔ |
| 11 | `security.md` | Threat model | Disarankan* | ✔ |
| 12 | `test-plan.md` | Strategi testing | Disarankan | ✔ |
| 13 | `docs/adr/*.md` | Catatan keputusan | Opsional | — |
| 14 | `README.md` | Ikhtisar & setup | Opsional | — |
| 15 | `ROADMAP.md` | Arah jangka panjang | Opsional | ✔ |
| 16 | `CONTRIBUTING.md` | Panduan kontribusi | Opsional | ✔ |

*Naik ke Wajib bila menangani auth/pembayaran/data sensitif.

**Aturan praktis:** prototipe/MVP solo → **Tier 1 + steering trio + AGENTS.md**. Produk serius/tim → tambah Tier 3. Tier 4 menyusul seiring proyek matang.

---

## Aset Terkait (di Space & repo)

- **Template dokumen (diunggah ke Space ini):** `PRD.md`, `requirements.md`, `design.md`, `product.md`, `tech.md`, `structure.md`, `tasks.md`, `data-model.md`, `api-spec.md`, `security.md`, `test-plan.md`, `ROADMAP.md`, `CONTRIBUTING.md`.
- **Panduan Space Advisor:** `PERPLEXITY-SPACE-DOC-ADVISOR-GUIDE.md`.
- **Space pelengkap (eksekusi):** *"ECC Prompt Builder"* — mengubah dokumen menjadi prompt siap-tempel (lihat `PERPLEXITY-SPACE-GUIDE.md`).
- **Standar sumber:** https://github.com/affaan-m/ECC

Alur menyeluruh: **Advisor (tentukan + isi dokumen) → dokumen jadi → Prompt Builder (buat prompt) → Kiro/Claude Code (`/planner → /tdd-workflow → /code-reviewer → /verification-loop`)**.
