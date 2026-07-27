<!--
  TEMPLATE CONTRIBUTING.md — standar ECC
  Fungsi: panduan kolaborasi. Selaras rules/common/git-workflow.md & development-workflow.md.
  Cara pakai: salin ke root proyek, isi, hapus komentar ini.
-->

# Contributing to <Nama Proyek>

Terima kasih ingin berkontribusi. Ikuti panduan berikut agar kontribusi lancar.

## 1. Persiapan Lingkungan
```bash
# Clone & install
git clone <repo-url>
cd <repo>
<perintah install>

# Jalankan test untuk memastikan setup sehat
<perintah test>
```

## 2. Alur Kerja Pengembangan (ECC)
<!-- Selaras development-workflow: Plan → TDD → Review → Commit. -->
1. **Plan** — rencanakan perubahan (untuk fitur non-trivial).
2. **TDD** — tulis test dulu, implementasi, refactor (coverage 80%+).
3. **Review** — self-review + code review.
4. **Verify** — build + lint + type check + test hijau sebelum PR.

## 3. Strategi Branch
- Buat branch dari `main`: `<tipe>/<deskripsi-singkat>` (mis. `feat/oauth-login`).
- Jangan push langsung ke `main`.

## 4. Konvensi Commit (Conventional Commits)
<!-- Format ECC: <type>: <deskripsi> -->
Format: `<type>: <deskripsi>`

Tipe: `feat`, `fix`, `refactor`, `docs`, `test`, `chore`, `perf`, `ci`

Contoh: `feat: tambah login OAuth Google`

## 5. Proses Pull Request
- Judul PR ringkas (< 70 karakter).
- Deskripsi berisi: ringkasan perubahan, apa yang dites, dan hal yang belum selesai.
- PR harus lulus CI (test, lint, coverage).
- Minimal <n> approval sebelum merge.

## 6. Standar Kode
<!-- Tautkan ke aturan proyek/ECC: coding-style, security, testing. -->
- Immutability: buat objek baru, hindari mutasi.
- File kecil & fokus; error ditangani di setiap level.
- Validasi semua input di boundary; tanpa secret hardcoded.

## 7. Keamanan
- Jangan commit secret (`.env`, kunci, token).
- Laporkan isu keamanan secara privat ke <kontak keamanan>, bukan lewat issue publik.

## 8. Testing
- Semua kode baru wajib disertai test.
- Coverage minimum: **80%**.

## 9. Kode Etik
<!-- Tautkan CODE_OF_CONDUCT.md bila ada. -->
- Bersikap hormat dan konstruktif.

---
<!-- Referensi standar ECC (repo asli, bukan path lokal) -->
> **Standar ECC:** https://github.com/affaan-m/ECC
> Template ini selaras dengan:
> - https://github.com/affaan-m/ECC/blob/main/rules/common/git-workflow.md
> - https://github.com/affaan-m/ECC/blob/main/rules/common/development-workflow.md
