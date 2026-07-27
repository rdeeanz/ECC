<!--
  TEMPLATE PRD (Product Requirements Document) — standar ECC
  Menjawab: APA yang dibangun dan MENGAPA.
  Cara pakai: salin ke root proyek sebagai PRD.md (atau {nama-fitur}.prd.md),
  isi setiap bagian, hapus komentar <!-- ... --> ini.
  Catatan: tabel "Delivery Milestones" dibaca oleh command /plan ECC.
-->

# PRD: <Nama Produk / Fitur>

| Field | Nilai |
|-------|-------|
| Status | `draft` \| `in-review` \| `approved` |
| Pemilik (Owner) | <nama> |
| Tanggal | <YYYY-MM-DD> |
| Versi | 0.1 |

## 1. Ringkasan
<!-- 2-3 kalimat: apa produk/fitur ini dan nilai utamanya. -->

## 2. Masalah & Latar Belakang
<!-- Masalah apa yang diselesaikan? Untuk siapa? Kenapa penting sekarang? -->

## 3. Tujuan & Metrik Sukses
<!-- Tujuan terukur. Setiap tujuan idealnya punya metrik yang bisa diverifikasi. -->

| Tujuan | Metrik Sukses | Target |
|--------|---------------|--------|
| <tujuan> | <metrik> | <angka/kondisi> |

## 4. Non-Goals (Di Luar Ruang Lingkup)
<!-- Apa yang SECARA SENGAJA tidak dikerjakan pada iterasi ini. -->
- 

## 5. Target Pengguna & Persona
<!-- Siapa penggunanya, kebutuhan/motivasi utama mereka. -->
- **Persona 1:** <deskripsi, kebutuhan>

## 6. Fitur Utama (User-Facing)
<!-- Kemampuan yang dilihat pengguna. Tetap tingkat tinggi; detail teknis ke design.md. -->
- 

## 7. User Stories (Tingkat Tinggi)
<!-- Format: Sebagai <peran>, saya ingin <kemampuan>, agar <manfaat>. -->
- Sebagai <peran>, saya ingin <kemampuan>, agar <manfaat>.

## 8. Delivery Milestones
<!-- Dibaca oleh /plan. Kolom Plan diisi otomatis dengan path .plan.md saat direncanakan. -->

| Milestone | Deskripsi | Status | Plan |
|-----------|-----------|--------|------|
| M1: <nama> | <ringkas> | `pending` | — |
| M2: <nama> | <ringkas> | `pending` | — |

## 9. Asumsi & Batasan
<!-- Asumsi yang dianggap benar; batasan teknis/bisnis/waktu/anggaran. -->
- **Asumsi:** 
- **Batasan:** 

## 10. Risiko
| Risiko | Dampak | Kemungkinan | Mitigasi |
|--------|--------|-------------|----------|
| <risiko> | H/M/L | H/M/L | <mitigasi> |

## 11. Open Questions
<!-- Keputusan yang belum final dan memblokir kejelasan. Tandai jelas. -->
- [ ] 

## 12. Referensi
<!-- Tautan riset, desain, diskusi, dokumen terkait. -->
- 

---
<!-- Referensi standar ECC (repo asli, bukan path lokal) -->
> **Standar ECC:** https://github.com/affaan-m/ECC
> Template ini selaras dengan:
> - https://github.com/affaan-m/ECC/blob/main/commands/plan.md (mode PRD artifact + Delivery Milestones)
