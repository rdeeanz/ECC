# Kiro Commands Quick Reference (ECC)

> 33 agents + 43 skills terpasang. Di sesi chat Kiro mana pun, ketik `/` lalu nama agent/skill.
> **Agent** = "persona ahli" yang mengambil alih tugas. **Skill** = "workflow/panduan langkah" yang dijalankan.
> Selain itu ada **manual steering modes** yang dipanggil dengan `#`: `#dev-mode`, `#review-mode`, `#research-mode`.

## Konvensi Lokasi File

Semua path di bawah relatif terhadap folder `.kiro/` (versi global ada di `~/.kiro/`, versi repo ada di `/Users/fyi/ECC/.kiro/`).

| Jenis | Pola lokasi file | Keterangan |
|-------|------------------|------------|
| Agent | `agents/<nama>.md` **dan** `agents/<nama>.json` | `.md` dipakai IDE Kiro; `.json` dipakai `kiro-cli` (`/agent swap`) |
| Skill | `skills/<nama>/SKILL.md` | satu file `SKILL.md` per skill |
| Steering mode | `steering/<nama>.md` | frontmatter `inclusion: manual`, dipanggil dengan `#` |

---

# BAGIAN 1 — AGENTS (33)

## A. Perencanaan & Arsitektur

| Command | File pendukung | Fungsi | Contoh |
|---------|----------------|--------|--------|
| `/planner` | `agents/planner.md` · `agents/planner.json` | Spesialis perencanaan fitur & refactoring kompleks. Membuat blueprint bertahap (fase, dependensi, risiko, kriteria sukses). | `/planner rencanakan fitur checkout keranjang belanja dengan Stripe` |
| `/architect` | `agents/architect.md` · `agents/architect.json` | Spesialis desain sistem, skalabilitas, dan keputusan teknis. | `/architect haruskah saya pakai monolith atau microservices?` |

## B. Review Umum & Keamanan

| Command | File pendukung | Fungsi | Contoh |
|---------|----------------|--------|--------|
| `/code-reviewer` | `agents/code-reviewer.md` · `agents/code-reviewer.json` | Review kualitas, keamanan, maintainability. Pakai segera setelah menulis/mengubah kode. | `/code-reviewer review perubahan di src/auth/login.ts` |
| `/security-reviewer` | `agents/security-reviewer.md` · `agents/security-reviewer.json` | Deteksi kerentanan: secret, SSRF, injection, crypto tidak aman, OWASP Top 10. | `/security-reviewer audit endpoint /api/users` |

## C. Testing

| Command | File pendukung | Fungsi | Contoh |
|---------|----------------|--------|--------|
| `/tdd-guide` | `agents/tdd-guide.md` · `agents/tdd-guide.json` | Spesialis TDD, tulis test dulu, target coverage 80%+. | `/tdd-guide bantu bangun fungsi validasi email dengan TDD` |
| `/e2e-runner` | `agents/e2e-runner.md` · `agents/e2e-runner.json` | Testing end-to-end (Vercel Agent Browser / Playwright). Kelola journey, karantina test flaky, unggah artefak. | `/e2e-runner buat test alur login sampai dashboard` |

## D. Reviewer per Bahasa/Framework

| Command | File pendukung | Untuk |
|---------|----------------|-------|
| `/typescript-reviewer` | `agents/typescript-reviewer.md` · `.json` | TypeScript/JavaScript — type safety, async, keamanan Node/web |
| `/python-reviewer` | `agents/python-reviewer.md` · `.json` | Python — PEP 8, type hints, keamanan |
| `/go-reviewer` | `agents/go-reviewer.md` · `.json` | Go — idiom, concurrency, error handling |
| `/rust-reviewer` | `agents/rust-reviewer.md` · `.json` | Rust — ownership, lifetime, unsafe |
| `/java-reviewer` | `agents/java-reviewer.md` · `.json` | Java — Spring Boot/Quarkus (deteksi otomatis) |
| `/kotlin-reviewer` | `agents/kotlin-reviewer.md` · `.json` | Kotlin/Android/KMP — coroutine, Compose |
| `/cpp-reviewer` | `agents/cpp-reviewer.md` · `.json` | C++ — memory safety, modern C++, concurrency |
| `/fsharp-reviewer` | `agents/fsharp-reviewer.md` · `.json` | F# — idiom fungsional, pattern matching |
| `/swift-reviewer` | `agents/swift-reviewer.md` · `.json` | Swift — protocol-oriented, ARC, concurrency |
| `/react-reviewer` | `agents/react-reviewer.md` · `.json` | React/JSX — hooks, render performance, boundary server/client |
| `/django-reviewer` | `agents/django-reviewer.md` · `.json` | Django — ORM, DRF, migrasi, keamanan |
| `/database-reviewer` | `agents/database-reviewer.md` · `.json` | PostgreSQL — optimasi query, desain skema, keamanan |
| `/mle-reviewer` | `agents/mle-reviewer.md` · `.json` | ML produksi — pipeline, training, serving, monitoring |

Contoh: `/go-reviewer periksa pola concurrency di worker.go`

## E. Perbaikan Build (Build Resolvers)

| Command | File pendukung | Untuk saat build gagal di |
|---------|----------------|---------------------------|
| `/build-error-resolver` | `agents/build-error-resolver.md` · `.json` | Umum / TypeScript (perbaikan minimal) |
| `/go-build-resolver` | `agents/go-build-resolver.md` · `.json` | Go (build, vet, linter) |
| `/rust-build-resolver` | `agents/rust-build-resolver.md` · `.json` | Rust/Cargo (borrow checker, dependency) |
| `/java-build-resolver` | `agents/java-build-resolver.md` · `.json` | Java/Maven/Gradle (deteksi Spring Boot/Quarkus) |
| `/kotlin-build-resolver` | `agents/kotlin-build-resolver.md` · `.json` | Kotlin/Gradle |
| `/cpp-build-resolver` | `agents/cpp-build-resolver.md` · `.json` | C++/CMake (linker, template) |
| `/react-build-resolver` | `agents/react-build-resolver.md` · `.json` | React (Vite, webpack, Next.js, hydration) |
| `/pytorch-build-resolver` | `agents/pytorch-build-resolver.md` · `.json` | PyTorch (tensor shape, CUDA, gradient) |

Contoh: `/rust-build-resolver perbaiki error kompilasi cargo build ini`

## F. Pemeliharaan & Operasional

| Command | File pendukung | Fungsi | Contoh |
|---------|----------------|--------|--------|
| `/refactor-cleaner` | `agents/refactor-cleaner.md` · `.json` | Hapus dead code, duplikat, konsolidasi (knip, depcheck, ts-prune). | `/refactor-cleaner hapus kode tak terpakai di folder utils` |
| `/doc-updater` | `agents/doc-updater.md` · `.json` | Update dokumentasi & codemap, README, panduan. | `/doc-updater perbarui README dengan endpoint API baru` |
| `/performance-optimizer` | `agents/performance-optimizer.md` · `.json` | Analisis bottleneck, optimasi kode lambat, kurangi bundle, profiling, memory leak. | `/performance-optimizer kenapa render halaman produk lambat?` |
| `/harness-optimizer` | `agents/harness-optimizer.md` · `.json` | Analisis & tingkatkan konfigurasi agent harness (reliabilitas, biaya, throughput). | `/harness-optimizer audit konfigurasi hooks untuk efisiensi biaya` |
| `/loop-operator` | `agents/loop-operator.md` · `.json` | Operasikan loop agent otonom, pantau progres, intervensi saat macet. | `/loop-operator jalankan loop perbaikan test sampai hijau` |
| `/chief-of-staff` | `agents/chief-of-staff.md` · `.json` | Triase komunikasi (email/Slack/LINE/Messenger), klasifikasi 4 tier, buat draft balasan. | `/chief-of-staff triase inbox dan buat draft balasan yang perlu aksi` |

---

# BAGIAN 2 — SKILLS (43)

## A. Workflow Inti

| Command | File pendukung | Fungsi | Contoh |
|---------|----------------|--------|--------|
| `/tdd-workflow` | `skills/tdd-workflow/SKILL.md` | Alur TDD lengkap (RED → GREEN → REFACTOR), coverage 80%+. | `/tdd-workflow` lalu "bangun fitur pencarian produk" |
| `/verification-loop` | `skills/verification-loop/SKILL.md` | Verifikasi menyeluruh: build + type check + lint + test + security scan + review diff. | `/verification-loop` sebelum push |
| `/security-review` | `skills/security-review/SKILL.md` | Checklist keamanan komprehensif. Pakai saat menambah auth/handle input/endpoint API. | `/security-review` saat membangun login |
| `/coding-standards` | `skills/coding-standards/SKILL.md` | Standar coding universal (TS/JS/React/Node). | `/coding-standards` saat mulai project |
| `/search-first` | `skills/search-first/SKILL.md` | Metodologi "cari solusi yang ada dulu sebelum menulis kode sendiri". | `/search-first` sebelum membuat util dari nol |
| `/strategic-compact` | `skills/strategic-compact/SKILL.md` | Saran kompaksi konteks di titik logis (hemat token). | — |
| `/agentic-engineering` | `skills/agentic-engineering/SKILL.md` | Pola rekayasa perangkat lunak berbasis agent (eval-first, dekomposisi, routing model). | — |
| `/autonomous-loops` | `skills/autonomous-loops/SKILL.md` | Pola loop otonom: pipeline sekuensial sampai orkestrasi DAG multi-agent. | — |
| `/deep-research` | `skills/deep-research/SKILL.md` | Riset mendalam multi-sumber (firecrawl/exa), sintesis dengan sitasi. | `/deep-research bandingkan Drizzle vs Prisma dengan sumber` |
| `/content-hash-cache-pattern` | `skills/content-hash-cache-pattern/SKILL.md` | Pola cache hasil pemrosesan file pakai SHA-256 (auto-invalidating). | — |

## B. API, Backend & Frontend

| Command | File pendukung | Untuk |
|---------|----------------|-------|
| `/api-design` | `skills/api-design/SKILL.md` | Desain REST API (resource naming, pagination, error, versioning) |
| `/backend-patterns` | `skills/backend-patterns/SKILL.md` | Pola backend Node.js/Express/Next.js API routes |
| `/frontend-patterns` | `skills/frontend-patterns/SKILL.md` | Pola React/Next.js, state management, performa UI |
| `/react-patterns` | `skills/react-patterns/SKILL.md` | Pola React 18/19 (hooks, server/client component, Suspense) |
| `/react-testing` | `skills/react-testing/SKILL.md` | Test komponen React (Testing Library, Vitest/Jest, MSW, axe) |
| `/nextjs-turbopack` | `skills/nextjs-turbopack/SKILL.md` | Next.js 16+ & Turbopack (bundling inkremental) |
| `/nestjs-patterns` | `skills/nestjs-patterns/SKILL.md` | Arsitektur NestJS (modul, controller, guard, interceptor) |
| `/fastapi-patterns` | `skills/fastapi-patterns/SKILL.md` | FastAPI async, dependency injection, Pydantic |

Contoh: `/api-design rancang endpoint CRUD untuk resource "order"`

## C. Testing per Bahasa

| Command | File pendukung | Untuk |
|---------|----------------|-------|
| `/e2e-testing` | `skills/e2e-testing/SKILL.md` | E2E Playwright/Cypress, Page Object Model |
| `/golang-testing` | `skills/golang-testing/SKILL.md` | Test Go (table-driven, benchmark, race detection) |
| `/python-testing` | `skills/python-testing/SKILL.md` | Test Python (pytest, fixture, mock, coverage) |
| `/kotlin-testing` | `skills/kotlin-testing/SKILL.md` | Test Kotlin (Kotest, MockK, Kover) |
| `/rust-testing` | `skills/rust-testing/SKILL.md` | Test Rust (unit, integrasi, async, property-based) |
| `/cpp-testing` | `skills/cpp-testing/SKILL.md` | Test C++ (GoogleTest, CTest, sanitizer) |

## D. Pola per Bahasa

| Command | File pendukung | Untuk |
|---------|----------------|-------|
| `/golang-patterns` | `skills/golang-patterns/SKILL.md` | Idiom Go, concurrency, functional options |
| `/python-patterns` | `skills/python-patterns/SKILL.md` | Idiom Python (protocol, dataclass, decorator, async) |
| `/rust-patterns` | `skills/rust-patterns/SKILL.md` | Ownership, error handling, trait, concurrency Rust |
| `/kotlin-patterns` | `skills/kotlin-patterns/SKILL.md` | Coroutine, null safety, DSL builder Kotlin |
| `/cpp-coding-standards` | `skills/cpp-coding-standards/SKILL.md` | Standar C++ (C++ Core Guidelines) |
| `/java-coding-standards` | `skills/java-coding-standards/SKILL.md` | Standar Java (Spring Boot/Quarkus, deteksi otomatis) |

## E. Framework Backend Spesifik

| Command | File pendukung | Untuk |
|---------|----------------|-------|
| `/django-patterns` | `skills/django-patterns/SKILL.md` | Arsitektur Django, DRF, ORM, caching, middleware |
| `/django-security` | `skills/django-security/SKILL.md` | Keamanan Django (auth, CSRF, SQL injection, XSS) |
| `/springboot-patterns` | `skills/springboot-patterns/SKILL.md` | Arsitektur Spring Boot, layered services, caching |
| `/springboot-security` | `skills/springboot-security/SKILL.md` | Spring Security (authn/authz, CSRF, rate limiting) |
| `/jpa-patterns` | `skills/jpa-patterns/SKILL.md` | JPA/Hibernate (entity, relasi, optimasi query) |

## F. Swift & Mobile

| Command | File pendukung | Untuk |
|---------|----------------|-------|
| `/swift-actor-persistence` | `skills/swift-actor-persistence/SKILL.md` | Persistensi data thread-safe di Swift pakai actor |
| `/swift-protocol-di-testing` | `skills/swift-protocol-di-testing/SKILL.md` | Dependency injection berbasis protocol untuk kode Swift yang testable |

## G. Machine Learning

| Command | File pendukung | Untuk |
|---------|----------------|-------|
| `/mle-workflow` | `skills/mle-workflow/SKILL.md` | Workflow ML produksi (data contract, training reproducible, evaluasi, deployment, monitoring) |
| `/pytorch-patterns` | `skills/pytorch-patterns/SKILL.md` | Pola deep learning PyTorch (pipeline training, arsitektur model, data loading) |

## H. Data & Infrastruktur

| Command | File pendukung | Untuk |
|---------|----------------|-------|
| `/database-migrations` | `skills/database-migrations/SKILL.md` | Pola migrasi skema (Prisma, Drizzle, Django, dll.) |
| `/postgres-patterns` | `skills/postgres-patterns/SKILL.md` | Optimasi PostgreSQL, indexing, desain skema |
| `/docker-patterns` | `skills/docker-patterns/SKILL.md` | Docker/Compose, networking, volume, keamanan container |
| `/deployment-patterns` | `skills/deployment-patterns/SKILL.md` | Strategi deployment, CI/CD, health check, rollback |

---

# BAGIAN 3 — STEERING MODES (manual, dipanggil dengan `#`)

| Command | File pendukung | Untuk |
|---------|----------------|-------|
| `#dev-mode` | `steering/dev-mode.md` | Mode fokus pengembangan/implementasi |
| `#review-mode` | `steering/review-mode.md` | Mode fokus review kode menyeluruh |
| `#research-mode` | `steering/research-mode.md` | Mode fokus eksplorasi & riset |

> Catatan: steering lain di `steering/` dengan `inclusion: auto` (mis. `coding-style.md`, `security.md`, `testing.md`, `product.md`, `tech.md`, `structure.md`) aktif otomatis tanpa perlu dipanggil.

---

# Alur Kerja Gabungan (contoh nyata)

**Membangun fitur baru dari nol:**
```
/planner            → rencana implementasi
/tdd-workflow       → tulis test dulu, implementasi
/code-reviewer      → review hasil
/security-reviewer  → audit keamanan (jika sensitif)
/verification-loop  → cek final sebelum PR
```

**Memperbaiki build yang gagal (project Rust):**
```
/rust-build-resolver  → perbaiki error kompilasi
/rust-reviewer        → pastikan idiomatik & aman
```

**Optimasi performa React lambat:**
```
/performance-optimizer  → temukan bottleneck
/react-patterns         → terapkan pola yang benar
/react-testing          → verifikasi tidak ada regresi
```
