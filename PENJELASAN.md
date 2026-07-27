

# Analisa Repository: Everything Claude Code (ECC)

## 1. Ini Repository Apa?

**ECC (Everything Claude Code)** adalah sebuah **"agent harness operating system"** — bukan aplikasi biasa, melainkan **kumpulan konfigurasi + tooling** yang membuat AI coding assistant (seperti Claude Code, Cursor, Codex, dll.) bekerja jauh lebih terstruktur, aman, dan konsisten.

Analoginya: kalau AI coding assistant adalah "mesin", maka ECC adalah **"sistem operasi + toolkit"** yang dipasang di atasnya agar mesin itu punya aturan kerja, spesialisasi, otomasi, dan memori.

Fakta kunci dari codebase:
- Nama paket npm: `ecc-universal`, versi `2.0.0`, lisensi MIT.
- Penulis: Affaan Mustafa.
- Bersifat **lintas-harness** (cross-harness): satu repo yang sama bisa dipakai di Claude Code, Cursor, Codex, OpenCode, Gemini, Zed, GitHub Copilot, dan Kiro.
- Isinya **didominasi Markdown** (agents, skills, rules) + **script Node.js** (installer, hooks, tooling) + sedikit Python (`src/llm/`, `ecc_dashboard.py`) + prototipe Rust (`ecc2/`).

## 2. Terdiri dari Komponen Apa Saja?

Berdasarkan isi folder yang saya baca, ECC punya 6 pilar:

### a. Agents (folder `agents/` — ~67 file `.md`)
Sub-agen AI terspesialisasi. Masing-masing punya YAML frontmatter (`name`, `description`, `tools`, `model`) + prompt. Contoh yang saya lihat langsung:
- `planner.md` — bikin rencana implementasi detail (read-only: `Read`, `Grep`, `Glob`, model `opus`).
- `code-reviewer.md`, `security-reviewer.md`, `architect.md`, `tdd-guide.md`.
- Reviewer per bahasa: `go-reviewer`, `python-reviewer`, `rust-reviewer`, `java-reviewer`, `kotlin-reviewer`, `cpp-reviewer`, `typescript-reviewer`, `swift-reviewer`, dll.
- Build resolver: `build-error-resolver`, `go-build-resolver`, `rust-build-resolver`, `pytorch-build-resolver`, dll.

Menariknya, tiap agent punya **"Prompt Defense Baseline"** — proteksi terhadap prompt injection.

### b. Skills (folder `skills/` — ratusan folder, tiap folder ada `SKILL.md`)
Workflow siap-pakai yang bisa dipanggil on-demand. Ini adalah **permukaan kerja utama (canonical surface)** ECC. Contoh yang saya baca: `tdd-workflow/SKILL.md` berisi alur TDD lengkap (RED → GREEN → REFACTOR), cara deteksi test runner, pola mocking, sampai laporan bukti (evidence report).

### c. Rules / Steering (folder `rules/` + `.kiro/steering/`)
Aturan "selalu-diikuti". Dibagi `common/` (universal) + per-bahasa (`typescript/`, `python/`, `golang/`, dll.). Isinya soal immutability, keamanan, testing 80% coverage, git workflow.

### d. Hooks (folder `hooks/hooks.json`)
Otomasi yang jalan otomatis pada event tertentu. Dari `hooks.json` saya lihat ada:
- `PreToolUse` — cek sebelum tool jalan (GateGuard untuk perintah berbahaya, deteksi secret, proteksi file config).
- `SessionStart` — muat konteks sesi sebelumnya + deteksi package manager.
- `Stop` — format + typecheck otomatis, cek `console.log`, simpan state sesi, lacak biaya token, notifikasi desktop.
- `PreCompact` — simpan state sebelum konteks dipadatkan.

### e. Tooling / Control-plane (folder `scripts/`)
Script Node.js lintas-platform. Entry point utama CLI: `scripts/ecc.js` (perintah `ecc`). Ada juga `install-apply.js`, `doctor.js`, `repair.js`, `uninstall.js`, `harness-audit.js`, `status.js`, `consult.js`, dll.

### f. MCP configs (`.mcp.json`, `mcp-configs/`)
Konfigurasi Model Context Protocol. Default hanya 1 konektor: `chrome-devtools`. Sisanya opt-in.

## 3. Dipakai Untuk Apa Saja?

Berdasarkan analisa, ECC berguna untuk:

1. **Menstandarkan kualitas kode tim** — semua orang di tim dapat aturan coding style, security, dan testing yang sama otomatis.
2. **Mempercepat development dengan TDD** — skill `tdd-workflow` memaksa tulis test dulu, target coverage 80%+.
3. **Code review otomatis & terspesialisasi** — agent reviewer per bahasa.
4. **Keamanan (security-first)** — deteksi secret, cegah SQL injection/XSS, audit dengan AgentShield (`/security-scan`).
5. **Otomasi berulang** — hooks untuk format, typecheck, cek `console.log`, review sebelum `git push`.
6. **Manajemen biaya & konteks token** — pemilihan model, kompaksi strategis, pelacakan biaya.
7. **Konsistensi lintas-tool** — tim yang pakai editor berbeda tetap dapat pengalaman yang sama.
8. **Continuous learning** — sistem "instinct" yang belajar pola dari sesi kerja.

## 4. Contoh-Contoh Penerapan

**Contoh 1 — Membangun fitur baru (autentikasi):**
```
/plan "Tambah autentikasi user dengan OAuth"   → agent planner bikin blueprint
skill tdd-workflow                              → tulis test dulu, lalu implementasi
/code-review                                    → code-reviewer cek hasil
/security-scan                                  → audit keamanan
```

**Contoh 2 — Memperbaiki bug:**
```
skill tdd-workflow   → tulis test gagal yang mereproduksi bug (RED)
                     → implementasi fix sampai test lulus (GREEN)
/code-review         → cek regresi
```

**Contoh 3 — Persiapan produksi:**
```
/security-scan     → audit OWASP Top 10
skill e2e-testing  → test alur pengguna kritis (Playwright)
/test-coverage     → verifikasi coverage 80%+
```

**Contoh 4 — Kerja per bahasa (Go):**
```
agent go-reviewer      → review pola concurrency
skill golang-patterns  → terapkan idiom Go
```

## 5. Cara Menggunakan — Langkah demi Langkah

Karena Anda menjalankan ini di dalam **Kiro** (`.kiro/` sudah lengkap), saya bagi jadi dua jalur.

### JALUR A: Menggunakan ECC di dalam Kiro (paling relevan untuk Anda sekarang)

Repo ini sudah punya folder `.kiro/` yang siap pakai (33 agents, 43 skills, 22 steering, 13 hooks).

**Langkah 1 — Pasang ke project Kiro Anda**
```bash
cd .kiro
./install.sh /path/ke/project-anda
# atau ke direktori saat ini:
./install.sh
# atau global (semua project Kiro):
./install.sh ~
```
Installer bersifat **non-destruktif** (tidak menimpa file yang sudah ada).

**Langkah 2 — Gunakan Agent di sesi chat Kiro**
Ketik `/` lalu nama agent, contoh:
```
/planner       → untuk merencanakan fitur
/code-reviewer → setelah menulis kode
/security-reviewer → untuk kode sensitif (auth, API)
```

**Langkah 3 — Panggil Skill lewat menu `/`**
```
/tdd-workflow      → mulai fitur baru dengan test dulu
/security-review   → checklist keamanan
/verification-loop → build + test + lint sebelum PR
```

**Langkah 4 — Steering files otomatis aktif**
File `coding-style.md`, `security.md`, `testing.md` di `.kiro/steering/` dengan `inclusion: auto` langsung berlaku tanpa aksi tambahan. (Termasuk `product.md`, `tech.md`, `structure.md` yang baru saya buat.)

**Langkah 5 — Aktifkan/atur Hooks**
Buka panel **Agent Hooks** di Kiro IDE untuk toggle hook seperti `quality-gate`, `typecheck-on-edit`, `tdd-reminder`.

### JALUR B: Menggunakan ECC sebagai Claude Code plugin (jalur utama repo asli)

**Langkah 1 — Pasang plugin (rekomendasi):**
```bash
/plugin marketplace add https://github.com/affaan-m/ECC
/plugin install ecc@ecc
```

**PENTING:** Jangan menumpuk metode install. Pilih **satu** jalur saja (plugin ATAU installer manual), jangan keduanya — ini penyebab paling umum setup rusak/duplikat.

**Langkah 2 — Pasang Rules manual (plugin tidak bisa distribusi rules):**
```bash
git clone https://github.com/affaan-m/ECC.git
cd ECC
npm install
mkdir -p ~/.claude/rules/ecc
cp -R rules/common ~/.claude/rules/ecc/
cp -R rules/typescript ~/.claude/rules/ecc/   # pilih stack Anda
```

**Langkah 3 — (Opsional) Pasang hook runtime:**
```bash
bash ./install.sh --target claude --modules hooks-runtime
```

**Langkah 4 — Cari komponen yang tepat pakai advisor bawaan:**
```bash
npx ecc consult "security reviews" --target claude
```

**Langkah 5 — Mulai bekerja:**
```
/ecc:plan "Tambah autentikasi user"   (plugin)
# atau /plan "..."                     (install manual)
```

### Perintah Verifikasi & Perawatan (untuk kontributor/dev repo ini)
```bash
npm test              # validasi + test suite lengkap
npm run lint          # ESLint + markdownlint
npm run coverage      # cek coverage (target 80%)
node scripts/ecc.js doctor    # diagnosa masalah instalasi
node scripts/ecc.js repair    # perbaiki file ECC yang rusak
node scripts/ecc.js list-installed
```

### Cara Uninstall / Reset (kalau terasa duplikat/rusak)
```bash
node scripts/uninstall.js --dry-run   # preview dulu
node scripts/uninstall.js             # hapus file yang dikelola ECC
```

## Ringkasan

ECC adalah **sistem operasi untuk AI coding agent**: paket berisi 67 agent spesialis, ratusan skill workflow, aturan coding, hooks otomatis, dan tooling CLI, yang bisa dipasang lintas editor AI. Tujuannya membuat kerja AI assistant lebih terstruktur, aman (security-first), berbasis TDD, dan konsisten antar-anggota tim. 

Untuk situasi Anda sekarang (di dalam Kiro), jalur tercepat: `cd .kiro && ./install.sh`, lalu panggil agent/skill lewat menu `/` di sesi chat.