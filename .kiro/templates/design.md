<!--
  TEMPLATE design.md — standar ECC (gaya SRS skill product-capability + arsitektur)
  Menjawab: BAGAIMANA membangunnya.
  Prinsip: ekspos constraint, invariant, interface, dan state transition SEBELUM coding.
  Cara pakai: salin ke .kiro/specs/<fitur>/design.md, isi, hapus komentar ini.
-->

# Design: <Nama Fitur>

| Field | Nilai |
|-------|-------|
| Status | `draft` \| `approved` |
| Sumber Requirements | <path ke requirements.md> |
| Tanggal | <YYYY-MM-DD> |

## 1. Ringkasan Desain
<!-- Restate kapabilitas dalam 1 paragraf: siapa aktornya, apa yang ada setelah ini rilis, outcome apa yang berubah. -->

## 2. Arsitektur
<!-- Diagram/komponen tingkat tinggi. Boleh pakai blok mermaid atau deskripsi. -->
```
<diagram atau deskripsi alur komponen>
```

## 3. Komponen & Tanggung Jawab
| Komponen | Tanggung Jawab | Ketergantungan |
|----------|----------------|----------------|
| <nama> | <apa yang dilakukan> | <depends on> |

## 4. Model Data
<!-- Entitas, field kunci, relasi, indeks. Tautkan ke skema bila ada. -->
| Entitas | Field Kunci | Relasi | Catatan |
|---------|-------------|--------|---------|
| <entitas> | <field> | <relasi> | <indeks/constraint> |

## 5. Interface / Kontrak
<!-- Input/output tiap interface publik: fungsi, endpoint API, event, dsb. -->
| Interface | Input | Output | Error |
|-----------|-------|--------|-------|
| <nama/endpoint> | <bentuk input> | <bentuk output> | <kondisi error> |

## 6. Alur Data & State Transitions
<!-- State yang wajib ada dan transisi yang diizinkan; invariant yang harus terjaga. -->
- **States:** 
- **Transitions:** 
- **Invariants:** 

## 7. UI / Visual Design
<!--
  Lapisan tampilan. Selaras dengan rules/web/design-quality.md (auto-apply ke *.css/*.tsx/dst).
  Isi hanya jika fitur punya antarmuka. Hindari default generik ("clean minimal", template shadcn/Tailwind polos).
-->

### 7.1 Style Direction
<!-- Pilih arah visual yang SPESIFIK & disengaja, mis. editorial, neo-brutalism, glassmorphism
     berdepth, dark/light luxury, bento, Swiss/International, retro-futurism.
     Jangan default ke dark mode otomatis — pilih yang produk memang butuhkan. -->
- **Arah:** 
- **Mood/atmosfer:** 

### 7.2 Design Tokens
<!-- Definisikan token secara sengaja, bukan warna dekoratif acak. Warna dipakai SEMANTIK. -->

**Palette (semantik):**
| Token | Nilai | Penggunaan |
|-------|-------|------------|
| `--color-primary` | `#______` | <aksi utama> |
| `--color-secondary` | `#______` | <aksi sekunder> |
| `--color-bg` / `--color-surface` | `#______` | <latar / permukaan> |
| `--color-text` / `--color-muted` | `#______` | <teks utama / sekunder> |
| `--color-success/warning/danger` | `#______` | <status semantik> |

**Tipografi:**
| Peran | Font | Ukuran / Weight / Line-height |
|-------|------|-------------------------------|
| Display / Heading | <font> | <skala kontras yang jelas> |
| Body | <font> | <ukuran / lh> |
| Mono / UI | <font> | <ukuran> |

**Spacing, radius, depth, motion:**
- **Skala spacing (ritme):** <mis. 4/8/12/16/24/32 — bukan padding seragam di mana-mana>
- **Radius:** <skala, bukan satu radius untuk semua>
- **Shadow / layering:** <depth via overlap/shadow/surface>
- **Motion:** <durasi/easing; motion yang memperjelas alur, bukan distraksi>

### 7.3 Layout & Hierarki
<!-- Hierarki lewat kontras skala; ritme spacing; komposisi grid/bento/editorial bila sesuai. -->
- **Breakpoints:** <mobile / tablet / desktop>
- **Hierarki:** <apa yang paling menonjol dan mengapa>

### 7.4 State Interaktif
<!-- Setiap elemen interaktif punya state yang TERDESAIN, bukan default. -->
- **Hover / Focus / Active / Disabled:** 
- **Loading / Empty / Error states:** 

### 7.5 Aksesibilitas Visual
- **Kontras:** <memenuhi WCAG AA: 4.5:1 teks normal, 3:1 teks besar>
- **Focus visible & target size memadai:** 
- **Tidak mengandalkan warna saja untuk menyampaikan makna:** 

### 7.6 Referensi Visual
<!-- Kumpulkan referensi nyata sebelum menulis kode UI. -->
- 

### 7.7 Component Checklist (anti-template)
- [ ] Tidak terlihat seperti template Tailwind/shadcn default
- [ ] Punya state hover/focus/active yang disengaja
- [ ] Pakai hierarki, bukan emphasis seragam
- [ ] Terlihat believable di screenshot produk nyata
- [ ] Jika dua tema, light & dark sama-sama terasa disengaja

## 8. Keputusan Teknis & Alternatif
<!-- Keputusan penting + alasan + alternatif yang ditolak (mini-ADR inline). -->
| Keputusan | Alasan | Alternatif Ditolak |
|-----------|--------|--------------------|
| <keputusan> | <alasan> | <alternatif + kenapa ditolak> |

## 9. Keamanan
<!-- Trust boundaries, autentikasi/otorisasi, kepemilikan data, penanganan secret. -->
- **Trust boundaries:** 
- **AuthN/AuthZ:** 
- **Data sensitif & secret:** 

## 10. Observability & Operasional
<!-- Logging, metrik, alert, kebutuhan operator, rollback/migrasi. -->
- 

## 11. Pola yang Diikuti (Patterns to Mirror)
<!-- Konvensi kode existing yang harus ditiru — JANGAN mengarang pola baru. -->
| Kategori | Sumber (`path:line`) | Pola |
|----------|----------------------|------|
| Naming | <path> | <deskripsi> |
| Error handling | <path> | <deskripsi> |
| Tests | <path> | <deskripsi> |

## 12. Non-Goals (Desain)
- 

## 13. Risiko Teknis & Mitigasi
| Risiko | Dampak | Mitigasi |
|--------|--------|----------|
| <risiko> | H/M/L | <mitigasi> |

## 14. Open Questions
- [ ] 

---
<!-- Referensi standar ECC (repo asli, bukan path lokal) -->
> **Standar ECC:** https://github.com/affaan-m/ECC
> Template ini selaras dengan:
> - https://github.com/affaan-m/ECC/blob/main/rules/web/design-quality.md (UI/Visual, §7)
> - https://github.com/affaan-m/ECC/blob/main/commands/plan.md (Patterns to Mirror)
