# Test Case Bonus — Form Pendaftaran Online

**Tanggal acuan pengujian:** 14 Oktober 2026  
**Asumsi:** Setiap test case menguji satu kondisi, sedangkan field lain diisi valid. Password valid: `Pass123!`.

## Spesifikasi
- Nama: 3–100 karakter
- Email: format email valid
- No. HP: 10–13 digit, diawali `08`
- Tanggal lahir: format `YYYY-MM-DD`, umur minimal 17 tahun
- Password: minimal 8 karakter, mengandung huruf besar, huruf kecil, angka, dan simbol
- Konfirmasi password: harus sama dengan password

## Equivalence Partitioning

| Field | Partisi | Kategori | Kondisi | Contoh |
|---|---|---|---|---|
| Nama | N1 | Valid | 3–100 karakter | Budi Santoso |
| Nama | N2 | Invalid | Kurang dari 3 karakter | AB |
| Nama | N3 | Invalid | Lebih dari 100 karakter | 101 karakter |
| Email | E1 | Valid | Format email benar | budi@example.com |
| Email | E2 | Invalid | Tidak memiliki @ | budiexample.com |
| Email | E3 | Invalid | Domain tidak lengkap | budi@ |
| No. HP | H1 | Valid | 10–13 digit, diawali 08 | 081234567890 |
| No. HP | H2 | Invalid | Kurang dari 10 digit | 081234567 |
| No. HP | H3 | Invalid | Lebih dari 13 digit | 08123456789012 |
| No. HP | H4 | Invalid | Tidak diawali 08 | 071234567890 |
| Tanggal lahir | T1 | Valid | Format benar dan usia ≥17 | 2000-01-01 |
| Tanggal lahir | T2 | Invalid | Usia <17 | 2015-01-01 |
| Tanggal lahir | T3 | Invalid | Format salah | 01-01-2000 |
| Tanggal lahir | T4 | Invalid | Tanggal kalender tidak valid | 2000-02-30 |
| Password | P1 | Valid | Minimal 8 karakter, huruf besar/kecil, angka, simbol | Pass123! |
| Password | P2 | Invalid | Kurang dari 8 karakter | Pa1! |
| Password | P3 | Invalid | Tidak ada huruf besar | pass123! |
| Password | P4 | Invalid | Tidak ada huruf kecil | PASS123! |
| Password | P5 | Invalid | Tidak ada angka | Password! |
| Password | P6 | Invalid | Tidak ada simbol | Pass1234 |
| Konfirmasi | C1 | Valid | Sama dengan password | Pass123! |
| Konfirmasi | C2 | Invalid | Berbeda dari password | Pass124! |
| Konfirmasi | C3 | Invalid | Kosong | string kosong |

## Boundary Value Analysis

### Nama (3–100 karakter)

| Boundary | Nilai | Kategori | Expected Output |
|---|---:|---|---|
| min-1 | 2 karakter | Invalid | Nama ditolak |
| min | 3 karakter | Valid | Nama diterima |
| min+1 | 4 karakter | Valid | Nama diterima |
| max-1 | 99 karakter | Valid | Nama diterima |
| max | 100 karakter | Valid | Nama diterima |
| max+1 | 101 karakter | Invalid | Nama ditolak |

### Nomor HP (10–13 digit)

| Boundary | Nilai | Kategori | Expected Output |
|---|---:|---|---|
| min-1 | 9 digit | Invalid | Nomor ditolak |
| min | 10 digit | Valid | Diterima jika diawali 08 |
| min+1 | 11 digit | Valid | Diterima jika diawali 08 |
| max-1 | 12 digit | Valid | Diterima jika diawali 08 |
| max | 13 digit | Valid | Diterima jika diawali 08 |
| max+1 | 14 digit | Invalid | Nomor ditolak |

### Password (minimal 8 karakter)

| Boundary | Nilai | Kategori | Expected Output |
|---|---:|---|---|
| min-1 | 7 karakter | Invalid | Password ditolak |
| min | 8 karakter | Valid | Diterima jika komposisi karakter sesuai |
| min+1 | 9 karakter | Valid | Diterima jika komposisi karakter sesuai |

### Tanggal lahir (batas usia 17 tahun per 14 Oktober 2026)

| Boundary | Tanggal lahir | Kategori | Expected Output |
|---|---|---|---|
| Sehari sebelum batas | 2009-10-15 | Invalid | Belum berusia 17 tahun |
| Tepat pada batas | 2009-10-14 | Valid | Tepat berusia 17 tahun |
| Sehari setelah batas | 2009-10-13 | Valid | Sudah berusia 17 tahun |

## Test Case Lengkap (25 kasus)

| ID | Field | Input / Skenario | Kategori | Expected Output |
|---|---|---|---|---|
| TC01 | Nama | Budi Santoso | Valid | Nama diterima |
| TC02 | Nama | AB (2 karakter) | Invalid | Nama ditolak: terlalu pendek |
| TC03 | Nama | Nama 3 karakter | Valid | Nama diterima |
| TC04 | Nama | Nama 101 karakter | Invalid | Nama ditolak: terlalu panjang |
| TC05 | Email | budi@example.com | Valid | Email diterima |
| TC06 | Email | budiexample.com | Invalid | Email ditolak: format salah |
| TC07 | Email | budi@ | Invalid | Email ditolak: domain tidak lengkap |
| TC08 | No. HP | 081234567890 (12 digit) | Valid | Nomor diterima |
| TC09 | No. HP | 081234567 (9 digit) | Invalid | Nomor ditolak |
| TC10 | No. HP | 0812345678901 (13 digit) | Valid | Nomor diterima |
| TC11 | No. HP | 071234567890 | Invalid | Nomor ditolak: awalan salah |
| TC12 | Tanggal lahir | 2000-01-01 | Valid | Tanggal diterima, usia memenuhi syarat |
| TC13 | Tanggal lahir | 2015-01-01 | Invalid | Ditolak: usia di bawah 17 tahun |
| TC14 | Tanggal lahir | 15-10-2000 | Invalid | Ditolak: format salah |
| TC15 | Tanggal lahir | 2000-02-30 | Invalid | Ditolak: tanggal tidak valid |
| TC16 | Tanggal lahir | 2009-10-15 | Invalid | Ditolak: belum berusia 17 tahun |
| TC17 | Tanggal lahir | 2009-10-14 | Valid | Diterima: tepat berusia 17 tahun |
| TC18 | Password | Pass123! | Valid | Password diterima |
| TC19 | Password | Pa1! (4 karakter) | Invalid | Ditolak: terlalu pendek |
| TC20 | Password | pass123! | Invalid | Ditolak: tidak ada huruf besar |
| TC21 | Password | Pass1234 | Invalid | Ditolak: tidak ada simbol |
| TC22 | Password | Password! | Invalid | Ditolak: tidak ada angka |
| TC23 | Konfirmasi | Pass123! sama dengan password | Valid | Konfirmasi diterima |
| TC24 | Konfirmasi | Pass124! berbeda dari password | Invalid | Konfirmasi ditolak |
| TC25 | Konfirmasi | Kosong | Invalid | Konfirmasi wajib diisi |

## Catatan
Expected output merupakan hasil yang diharapkan berdasarkan spesifikasi, bukan hasil eksekusi pada aplikasi nyata.
