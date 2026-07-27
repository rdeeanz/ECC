<!--
  TEMPLATE structure.md (steering) — standar ECC
  Fungsi: konvensi organisasi file/folder agar AI menaruh kode di tempat benar.
  Cara pakai: salin ke .kiro/steering/structure.md, isi, hapus komentar ini.
-->
---
inclusion: auto
name: structure
description: Layout repositori dan konvensi organisasi untuk <nama>.
---

# Project Structure

## Layout Tingkat Atas
```
<root>/
├── <folder>/     # <tanggung jawab>
├── <folder>/     # <tanggung jawab>
└── ...
```

## Tanggung Jawab Direktori
| Direktori | Isi / Tanggung Jawab |
|-----------|----------------------|
| `<dir>` | <deskripsi> |

## Konvensi Penamaan
<!-- File, komponen, fungsi, variabel, test. -->
- **File:** 
- **Komponen:** 
- **Test:** <mis. *.test.ts di samping sumber, atau di /tests>

## Prinsip Organisasi (ECC)
<!-- Selaras ECC: banyak file kecil, per fitur/domain, kohesi tinggi. -->
- Banyak file kecil ketimbang sedikit file besar (tipikal 200-400 baris, maks 800).
- Organisasi **per fitur/domain**, bukan per tipe.
- High cohesion, low coupling.

## Di Mana Menaruh Apa
<!-- Aturan praktis: komponen baru, util, tipe, test, config, aset. -->
- **Komponen baru:** 
- **Util bersama:** 
- **Tipe/kontrak:** 
- **Test:** 

---
<!-- Referensi standar ECC (repo asli, bukan path lokal) -->
> **Standar ECC:** https://github.com/affaan-m/ECC
> Template ini selaras dengan:
> - https://github.com/affaan-m/ECC/blob/main/rules/common/coding-style.md
