<!--
  TEMPLATE security.md — standar ECC (security-first)
  Fungsi: threat model & kebutuhan keamanan. Selaras rules/common/security.md + skill security-review.
  WAJIB bila menangani auth / pembayaran / data sensitif / kepatuhan.
  Cara pakai: salin ke docs proyek, isi, hapus komentar ini.
-->

# Security: <Nama Proyek/Fitur>

| Field | Nilai |
|-------|-------|
| Status | `draft` \| `approved` |
| Klasifikasi Data | <public / internal / confidential / PII / regulated> |
| Kepatuhan | <none / GDPR / HIPAA / PCI-DSS> |
| Tanggal | <YYYY-MM-DD> |

## 1. Aset & Klasifikasi Data
<!-- Data/aset yang dilindungi dan tingkat sensitivitasnya. -->
| Aset | Sensitivitas | Catatan |
|------|--------------|---------|
| <aset> | <tingkat> | <mis. dienkripsi at-rest> |

## 2. Threat Model (ringkas)
<!-- Aktor ancaman, vektor, skenario. Boleh pakai STRIDE. -->
| Ancaman | Vektor | Dampak | Mitigasi |
|---------|--------|--------|----------|
| <ancaman> | <vektor> | H/M/L | <kontrol> |

## 3. Trust Boundaries
<!-- Di mana data berpindah antar zona kepercayaan (klien↔server, server↔DB, pihak ketiga). -->
- 

## 4. Autentikasi & Otorisasi
- **AuthN:** <metode, MFA, sesi/token, kedaluwarsa>
- **AuthZ:** <model peran/izin, prinsip least privilege>

## 5. Validasi Input & Output
<!-- Selaras ECC: validasi semua input di boundary; cegah injection/XSS. -->
- **Validasi input:** <schema-based di server>
- **Cegah SQLi:** parameterized query
- **Cegah XSS:** sanitasi/encode output
- **CSRF:** <proteksi>

## 6. Manajemen Secret
<!-- ECC: TIDAK PERNAH hardcode secret. -->
- Secret via environment variable / secret manager
- Validasi secret wajib saat startup
- Rotasi bila terekspos
- `.env` masuk `.gitignore`

## 7. Checklist OWASP Top 10 (sebelum rilis)
- [ ] Broken Access Control ditangani
- [ ] Kegagalan kriptografi (data sensitif dienkripsi in-transit & at-rest)
- [ ] Injection (SQL/NoSQL/command) dicegah
- [ ] Insecure Design ditinjau
- [ ] Security Misconfiguration diperiksa
- [ ] Komponen usang/rentan dicek (dependency scan)
- [ ] Identifikasi & autentikasi kuat
- [ ] Integritas data & supply chain
- [ ] Logging & monitoring memadai (tanpa membocorkan PII)
- [ ] SSRF dicegah

## 8. Rate Limiting & Abuse Prevention
- 

## 9. Logging, Audit & Privasi
<!-- Error tidak membocorkan detail sensitif; PII tidak masuk log. -->
- 

## 10. Dependency & Supply Chain
- **Pinning versi:** 
- **Scan otomatis:** 

## 11. Incident Response (ringkas)
<!-- Selaras protokol ECC: STOP → security-review → fix CRITICAL → rotasi secret → cek pola serupa. -->
- 

## 12. Open Questions
- [ ] 

---
<!-- Referensi standar ECC (repo asli, bukan path lokal) -->
> **Standar ECC:** https://github.com/affaan-m/ECC
> Template ini selaras dengan:
> - https://github.com/affaan-m/ECC/blob/main/rules/common/security.md
> - https://github.com/affaan-m/ECC/blob/main/skills/security-review/SKILL.md
