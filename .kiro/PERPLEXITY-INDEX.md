# Perplexity Assets — Master Index (ECC)

Daftar semua aset untuk membangun Perplexity Space berbasis ECC. Semua file ada di folder `.kiro/`.

## Panduan (Guides)

| File | Ukuran | Fungsi |
|------|--------|--------|
| `PERPLEXITY-SPACE-GUIDE.md` | 11K | Panduan membuat Space **"ECC Web App Prompt Builder"** — mengubah ide fitur menjadi prompt pengembangan siap-tempel ke AI coding agent, sesuai standar ECC (TDD, security-first, immutability). Berisi custom instructions siap-tempel. |
| `PERPLEXITY-SPACE-DOC-ADVISOR-GUIDE.md` | 9K | Panduan membuat Space **"ECC Document Scoping Advisor"** — bertanya dulu tentang aplikasi, lalu merekomendasikan dokumen `.md` yang benar-benar dibutuhkan (WAJIB/DISARANKAN/LEWATI) sesuai konteks. Berisi custom instructions + aturan pemetaan. |

## Bahan Pengetahuan (Knowledge Files — diunggah ke Space)

| File | Ukuran | Fungsi |
|------|--------|--------|
| `ecc-bundle-rules.md` | 68K | Gabungan 23 file aturan ECC: `AGENTS.md` + `rules/common/*` + `rules/web/*` + `rules/typescript/*` + `rules/react/*`. Penanda sumber menunjuk ke repo asli `affaan-m/ECC`. |
| `ecc-bundle-skills.md` | 160K | Gabungan 15 skill inti web dev (coding-standards, api-design, react-patterns, tdd-workflow, security-review, verification-loop, dll.). Penanda sumber menunjuk ke repo asli `affaan-m/ECC`. |
| `../DOKUMEN.md` | — | Kerangka tier dokumen (PRD → requirements → design → tasks → steering → dst.). **Sumber utama** untuk Space Document Scoping Advisor. Berada di root repo. |

## Peta Penggunaan

| Space | Guide | Knowledge files yang diunggah |
|-------|-------|-------------------------------|
| Prompt Builder | `PERPLEXITY-SPACE-GUIDE.md` | `ecc-bundle-rules.md` + `ecc-bundle-skills.md` |
| Document Scoping Advisor | `PERPLEXITY-SPACE-DOC-ADVISOR-GUIDE.md` | `../DOKUMEN.md` (wajib) + kedua bundle (opsional) |

## Alur Kerja yang Disarankan

```
1. Document Scoping Advisor  → tentukan dokumen .md apa saja yang perlu dibuat
2. Isi/susun dokumen tersebut (PRD, requirements, design, dll.)
3. Prompt Builder            → ubah dokumen jadi prompt eksekusi siap-tempel
4. Kiro / Claude Code        → jalankan prompt: /planner → /tdd-workflow → /code-reviewer → /verification-loop
```

## Catatan

- Semua penanda path di dalam bundle mengacu ke repo asli `https://github.com/affaan-m/ECC` (branch `main`), bukan path lokal.
- Regenerasi bundle bila aturan/skill ECC berubah: lihat skrip di `PERPLEXITY-SPACE-GUIDE.md` bagian "Opsi bundling".
- Batas file per Space berbeda per paket Perplexity (Enterprise: 50 file). Jika terbatas, unggah bundle gabungan alih-alih file terpisah.
