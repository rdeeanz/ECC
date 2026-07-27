<!--
  TEMPLATE requirements.md — standar ECC / alur spec Kiro
  Menjawab: kebutuhan yang SPESIFIK dan DAPAT DIUJI (fondasi TDD).
  Acceptance criteria memakai format EARS: "WHEN <kondisi> THE SYSTEM SHALL <perilaku>".
  Varian EARS: WHEN (event), IF ... THEN (kondisional), WHILE (kontinu), WHERE (fitur ada).
  Cara pakai: salin ke .kiro/specs/<fitur>/requirements.md, isi, hapus komentar ini.
-->

# Requirements: <Nama Fitur>

| Field | Nilai |
|-------|-------|
| Status | `draft` \| `approved` |
| Sumber PRD | <path ke PRD.md> |
| Tanggal | <YYYY-MM-DD> |

## 1. Pendahuluan
<!-- Ringkas cakupan fitur (1-2 kalimat) dan tautkan ke PRD. -->

## 2. Requirements Fungsional
<!-- Ulangi blok "Requirement N" untuk tiap kebutuhan. Setiap kriteria harus dapat diuji. -->

### Requirement 1: <judul singkat>
**User Story:** Sebagai <peran>, saya ingin <kemampuan>, agar <manfaat>.

**Acceptance Criteria (EARS):**
1. WHEN <kondisi/event> THE SYSTEM SHALL <perilaku yang teramati>.
2. IF <kondisi> THEN THE SYSTEM SHALL <perilaku>.
3. WHILE <keadaan berlangsung> THE SYSTEM SHALL <perilaku>.

### Requirement 2: <judul singkat>
**User Story:** Sebagai <peran>, saya ingin <kemampuan>, agar <manfaat>.

**Acceptance Criteria (EARS):**
1. WHEN <...> THE SYSTEM SHALL <...>.

## 3. Requirements Non-Fungsional
<!-- Kualitas sistem. Tetap tulis dalam bentuk yang dapat diverifikasi. -->

| Kategori | Requirement (dapat diuji) |
|----------|---------------------------|
| Keamanan | <mis. semua input divalidasi di server; tanpa secret di kode> |
| Performa | <mis. p95 response < 300ms pada beban X> |
| Aksesibilitas | <mis. memenuhi WCAG AA pada alur utama> |
| Reliability | <mis. retry pada kegagalan transient> |
| Observability | <mis. log terstruktur untuk error kritis> |

## 4. Batasan Teknis
<!-- Stack wajib, kompatibilitas, integrasi yang tidak boleh diubah, dsb. -->
- 

## 5. Definition of Done (Global)
<!-- Kondisi yang harus benar agar fitur dianggap selesai. -->
- [ ] Semua acceptance criteria terpenuhi & terbukti lewat test
- [ ] Coverage >= 80%
- [ ] Tanpa secret hardcoded; input tervalidasi
- [ ] Lint bersih, build hijau
- [ ] Review lulus (code-review + security-review bila relevan)

## 6. Open Questions
- [ ] 

---
<!-- Referensi standar ECC (repo asli, bukan path lokal) -->
> **Standar ECC:** https://github.com/affaan-m/ECC
> Template ini selaras dengan:
> - https://github.com/affaan-m/ECC/blob/main/skills/tdd-workflow/SKILL.md (acceptance criteria -> test)
> - https://github.com/affaan-m/ECC/blob/main/rules/common/testing.md
