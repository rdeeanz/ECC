<!--
  TEMPLATE test-plan.md — standar ECC
  Fungsi: strategi testing. Selaras skill tdd-workflow, verification-loop, rules/common/testing.md.
  Cara pakai: salin ke docs proyek, isi, hapus komentar ini.
-->

# Test Plan: <Nama Proyek/Fitur>

| Field | Nilai |
|-------|-------|
| Status | `draft` \| `approved` |
| Target Coverage | **80%+** |
| Tanggal | <YYYY-MM-DD> |

## 1. Strategi & Filosofi
<!-- Selaras ECC: TDD (RED→GREEN→REFACTOR), test ditulis sebelum implementasi. -->
- Metodologi: **TDD**
- Tulis test gagal dulu, implementasi minimal, refactor.

## 2. Jenis Test & Cakupan
| Jenis | Cakupan | Tool | Lokasi |
|-------|---------|------|--------|
| Unit | fungsi/util/komponen | <mis. Vitest/Jest/pytest> | <path> |
| Integration | API/DB/service | <tool> | <path> |
| E2E | alur pengguna kritis | <mis. Playwright> | <path> |

## 3. Target Coverage & Gate
- Minimum: **80%** (lines/functions/statements)
- Gate: coverage di-cek di CI; PR gagal bila di bawah ambang.

## 4. Test Data & Fixtures
<!-- Cara menyiapkan data uji; isolasi test; mock dependency eksternal. -->
- **Fixtures:** 
- **Mock/stub:** <boundary eksternal: network, waktu, filesystem>
- **Isolasi:** setiap test independen

## 5. Skenario Kunci & Edge Case
<!-- Kaitkan ke acceptance criteria di requirements.md. -->
| Skenario | Jenis | Requirement terkait |
|----------|-------|---------------------|
| <happy path> | unit/integration/e2e | Req <n> |
| <edge case> | | Req <n> |
| <error path> | | Req <n> |

## 6. Perintah Menjalankan
```bash
# semua test (sekali jalan)
<perintah test>
# dengan coverage
<perintah coverage>
```

## 7. CI & Verification Loop
<!-- Selaras verification-loop: build + lint + type check + test + security scan. -->
- 

## 8. Definition of Done (Testing)
- [ ] Semua acceptance criteria tercakup test
- [ ] Coverage >= 80%
- [ ] Test hijau di CI
- [ ] Edge & error path teruji
- [ ] Tidak ada test yang di-skip tanpa alasan tercatat

## 9. Open Questions
- [ ] 

---
<!-- Referensi standar ECC (repo asli, bukan path lokal) -->
> **Standar ECC:** https://github.com/affaan-m/ECC
> Template ini selaras dengan:
> - https://github.com/affaan-m/ECC/blob/main/skills/tdd-workflow/SKILL.md
> - https://github.com/affaan-m/ECC/blob/main/skills/verification-loop/SKILL.md
> - https://github.com/affaan-m/ECC/blob/main/rules/common/testing.md
