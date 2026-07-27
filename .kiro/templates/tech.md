<!--
  TEMPLATE tech.md (steering) — standar ECC
  Fungsi: stack teknologi & perintah umum agar AI tidak salah tool / library.
  Cara pakai: salin ke .kiro/steering/tech.md, isi, hapus komentar ini.
-->
---
inclusion: auto
name: tech
description: Stack teknologi, tooling, dan perintah umum untuk <nama>.
---

# Technology Stack

## Bahasa & Runtime
<!-- Bahasa utama + versi minimum runtime. -->
- 

## Framework & Library Utama
| Kategori | Pilihan | Catatan |
|----------|---------|---------|
| Frontend | <mis. Next.js/React> | |
| Backend | <mis. Node/Express> | |
| Database | <mis. PostgreSQL> | |
| ORM/Query | <mis. Prisma/Drizzle> | |
| Styling | <mis. Tailwind> | |
| Testing | <mis. Vitest + Playwright> | |

## Package Manager
<!-- npm / pnpm / yarn / bun — dan versi bila di-pin. -->
- 

## Perintah Umum
```bash
# Install
<perintah install>
# Dev server (jalankan manual di terminal)
<perintah dev>
# Build
<perintah build>
# Test (mode sekali jalan)
<perintah test>
# Lint & format
<perintah lint>
# Type check
<perintah typecheck>
```

## Testing & Kualitas
<!-- Selaras ECC: target coverage >= 80%, verification-loop sebelum PR. -->
- Target coverage: **80%+**
- Sebelum PR: build + lint + type check + test

## Batasan & Konvensi Teknis
<!-- Versi terkunci, kompatibilitas, hal yang tidak boleh diubah, variabel env wajib. -->
- 

---
<!-- Referensi standar ECC (repo asli, bukan path lokal) -->
> **Standar ECC:** https://github.com/affaan-m/ECC
> Template ini selaras dengan:
> - https://github.com/affaan-m/ECC/blob/main/rules/common/testing.md (coverage 80%+)
> - https://github.com/affaan-m/ECC/blob/main/skills/verification-loop/SKILL.md
