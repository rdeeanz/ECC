<!--
  TEMPLATE api-spec.md — standar ECC
  Fungsi: kontrak API. Selaras skill api-design (envelope konsisten, status code, pagination, versioning).
  Cara pakai: salin ke docs proyek, isi, hapus komentar ini.
-->

# API Spec: <Nama Proyek/Layanan>

| Field | Nilai |
|-------|-------|
| Status | `draft` \| `approved` |
| Base URL | `https://api.example.com` |
| Versi | `v1` |
| Auth | <mis. Bearer JWT / API key / OAuth2> |
| Tanggal | <YYYY-MM-DD> |

## 1. Konvensi Umum
<!-- Selaras api-design. -->
- **Versioning:** <mis. prefix path `/v1`>
- **Content-Type:** `application/json`
- **Penamaan:** resource jamak, kebab/snake konsisten
- **Auth:** <cara mengirim kredensial>

## 2. Format Response (Envelope)
<!-- Envelope konsisten: indikator sukses, data, error, metadata paginasi. -->
```json
{
  "success": true,
  "data": {},
  "error": null,
  "meta": { "page": 1, "pageSize": 20, "total": 0 }
}
```

## 3. Format Error
```json
{
  "success": false,
  "data": null,
  "error": { "code": "<KODE>", "message": "<pesan aman, tidak bocorkan detail internal>" }
}
```

## 4. Status Code
| Code | Makna | Kapan |
|------|-------|-------|
| 200/201 | OK / Created | sukses |
| 400 | Bad Request | validasi gagal |
| 401/403 | Unauthorized / Forbidden | auth/otorisasi |
| 404 | Not Found | resource tidak ada |
| 409 | Conflict | bentrok state |
| 422 | Unprocessable | validasi semantik |
| 429 | Too Many Requests | rate limit |
| 500 | Server Error | kegagalan internal |

## 5. Pagination, Filtering, Sorting
- **Pagination:** <mis. `?page=&pageSize=` atau cursor>
- **Filtering:** <mis. `?status=active`>
- **Sorting:** <mis. `?sort=-created_at`>

## 6. Rate Limiting
<!-- Batas per klien + header yang dikembalikan. -->
- **Batas:** <mis. 100 req/menit>
- **Header:** `X-RateLimit-Limit`, `X-RateLimit-Remaining`

## 7. Endpoints
<!-- Ulangi blok untuk tiap endpoint. -->

### `<METHOD> /v1/<resource>`
- **Deskripsi:** 
- **Auth:** <ya/tidak, role>
- **Request (body/query/params):**
```json
{}
```
- **Response 200:**
```json
{}
```
- **Error:** <kode & kondisi>

## 8. Open Questions
- [ ] 

---
<!-- Referensi standar ECC (repo asli, bukan path lokal) -->
> **Standar ECC:** https://github.com/affaan-m/ECC
> Template ini selaras dengan:
> - https://github.com/affaan-m/ECC/blob/main/skills/api-design/SKILL.md
