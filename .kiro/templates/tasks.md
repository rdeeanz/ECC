<!--
  TEMPLATE tasks.md — standar ECC (struktur output command /plan + spec Kiro)
  Menjawab: langkah eksekusi bertahap. Tiap tugas dapat dieksekusi & diverifikasi.
  Prinsip ECC: tiru pola existing, jangan reinvent; setiap tugas punya perintah validasi.
  Cara pakai: salin ke .kiro/specs/<fitur>/tasks.md, isi, hapus komentar ini.
-->

# Tasks: <Nama Fitur>

| Field | Nilai |
|-------|-------|
| Sumber PRD | <path ke PRD.md> |
| Sumber Design | <path ke design.md> |
| Milestone Terpilih | <nama milestone> |
| Kompleksitas | `Small` \| `Medium` \| `Large` |

## 1. Ringkasan
<!-- 2-3 kalimat tentang apa yang dikerjakan pada batch tugas ini. -->

## 2. Pola yang Ditiru (Patterns to Mirror)
| Kategori | Sumber (`path:line`) | Pola |
|----------|----------------------|------|
| Naming | <path> | <deskripsi> |
| Error handling | <path> | <deskripsi> |
| Tests | <path> | <deskripsi> |

## 3. File yang Diubah
| File | Aksi | Alasan |
|------|------|--------|
| `<path>` | CREATE / UPDATE / DELETE | <alasan> |

## 4. Daftar Tugas
<!--
  Tugas berurutan & kecil. Centang saat selesai.
  Setiap tugas: Action (apa), Mirror (pola diikuti), Validate (perintah pembukti),
  dan Requirements (kaitkan ke requirement di requirements.md).
-->

- [ ] **Task 1: <nama>**
  - **Action:** <apa yang dilakukan>
  - **Mirror:** <pola yang diikuti / `path:line`>
  - **Validate:** `<perintah yang membuktikan benar>`
  - **Requirements:** <mis. Req 1.2, Req 3>

- [ ] **Task 2: <nama>**
  - **Action:** 
  - **Mirror:** 
  - **Validate:** 
  - **Requirements:** 

## 5. Validasi
<!-- Perintah spesifik proyek untuk memverifikasi keseluruhan. -->
```bash
<mis. npm test && npm run lint && npm run build>
```

## 6. Risiko
| Risiko | Kemungkinan | Mitigasi |
|--------|-------------|----------|
| <risiko> | H/M/L | <mitigasi> |

## 7. Acceptance / Definition of Done
- [ ] Semua tugas selesai
- [ ] Validasi lulus (test, lint, build hijau)
- [ ] Coverage >= 80%
- [ ] Pola ditiru, bukan diciptakan ulang
- [ ] Tanpa secret hardcoded; input tervalidasi
- [ ] Review lulus (code-review + security-review bila relevan)

---
<!-- Referensi standar ECC (repo asli, bukan path lokal) -->
> **Standar ECC:** https://github.com/affaan-m/ECC
> Template ini selaras dengan:
> - https://github.com/affaan-m/ECC/blob/main/commands/plan.md (struktur Tasks/Validate)
> - https://github.com/affaan-m/ECC/blob/main/skills/tdd-workflow/SKILL.md
