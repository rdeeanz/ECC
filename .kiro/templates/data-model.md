<!--
  TEMPLATE data-model.md — standar ECC
  Fungsi: model data & skema. Selaras skill database-migrations & postgres-patterns.
  Cara pakai: salin ke root/docs proyek, isi, hapus komentar ini.
-->

# Data Model: <Nama Proyek/Fitur>

| Field | Nilai |
|-------|-------|
| Status | `draft` \| `approved` |
| Database | <mis. PostgreSQL 16> |
| ORM/Migrasi | <mis. Prisma / Drizzle / golang-migrate> |
| Tanggal | <YYYY-MM-DD> |

## 1. Ikhtisar
<!-- Ringkas domain data dan entitas utama. Sertakan ERD bila ada. -->
```
<diagram ERD atau deskripsi relasi>
```

## 2. Entitas
<!-- Ulangi blok untuk tiap entitas/tabel. -->

### Entitas: <nama>
| Field | Tipe | Constraint | Deskripsi |
|-------|------|------------|-----------|
| `id` | <uuid/bigint> | PK | <id> |
| `<field>` | <tipe> | <not null/unique/default> | <deskripsi> |
| `created_at` | timestamptz | not null, default now() | |
| `updated_at` | timestamptz | not null | |

## 3. Relasi
| Dari | Ke | Jenis | Aturan (on delete/update) |
|------|----|-------|---------------------------|
| <entitas> | <entitas> | 1:1 / 1:N / N:M | <cascade/restrict/set null> |

## 4. Indeks
<!-- Indeks untuk query panas; hindari over-indexing. -->
| Tabel | Kolom | Jenis | Alasan |
|-------|-------|-------|--------|
| <tabel> | <kolom> | btree/gin/unique | <query yang didukung> |

## 5. Enum / Nilai Terkontrol
| Nama | Nilai |
|------|-------|
| <enum> | <a, b, c> |

## 6. Strategi Migrasi
<!-- Selaras database-migrations: aman, reversibel, zero-downtime bila perlu. -->
- **Tool:** 
- **Konvensi penamaan migrasi:** 
- **Rollback:** 
- **Data migration (jika ada):** 

## 7. Lifecycle & Retensi Data
<!-- Soft delete vs hard delete, arsip, retensi PII, kepatuhan. -->
- 

## 8. Pertimbangan Integritas & Performa
- **Invariants/constraint bisnis:** 
- **Transaksi:** 
- **Volume & skalabilitas yang diharapkan:** 

## 9. Open Questions
- [ ] 

---
<!-- Referensi standar ECC (repo asli, bukan path lokal) -->
> **Standar ECC:** https://github.com/affaan-m/ECC
> Template ini selaras dengan:
> - https://github.com/affaan-m/ECC/blob/main/skills/database-migrations/SKILL.md
> - https://github.com/affaan-m/ECC/blob/main/skills/postgres-patterns/SKILL.md
