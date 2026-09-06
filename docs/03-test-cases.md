## Sistem Informasi Pengelolaan Lahan Pertanian — Optimus Farm

**Dokumen:** Test Cases  
**Sistem:** Sistem Informasi Pengelolaan Lahan Pertanian  
**Organisasi:** Kelompok Tani Optimus Farm, Pangalengan  
**Versi:** 1.0  
**Status:** Draft Test Cases  
**Tanggal:** 6 September 2026  
**Referensi:** SRS dan Test Plan Sistem Informasi Pengelolaan Lahan Pertanian

---

## 1. Tujuan

Dokumen ini mendefinisikan test case yang digunakan untuk memverifikasi kebutuhan fungsional dan sebagian kebutuhan kualitas Sistem Informasi Pengelolaan Lahan Pertanian Optimus Farm.

Test case diturunkan dari requirement pada SRS dan strategi pengujian pada Test Plan. Dokumen ini berfungsi sebagai instrumen eksekusi pengujian, sehingga hasil aktual dan status Pass/Fail dicatat pada saat pengujian dilakukan.

**Catatan:** Nilai `Actual Result`, `Status`, dan `Evidence` pada dokumen ini harus diisi berdasarkan eksekusi aktual. Jangan menganggap expected result sebagai hasil pengujian.

---

## 2. Konvensi Status

| Status | Arti |
|---|---|
| PASS | Hasil aktual sesuai dengan expected result |
| FAIL | Hasil aktual tidak sesuai dengan expected result |
| BLOCKED | Pengujian tidak dapat dilakukan karena environment, dependency, atau kondisi lain |
| NOT RUN | Test case belum dieksekusi |

---

## 3. Ringkasan Test Case

| Kelompok Pengujian | Jumlah |
|---|---:|
| Use Case Scenario Testing | 22 |
| Boundary Value Analysis | 12 |
| State Transition Testing | 4 |
| Authorization Testing | 6 |
| Data Integrity & Consistency | 6 |
| Calculation Verification | 6 |
| Performance | 4 |
| Responsive & Compatibility | 6 |
| **Total** | **66** |

Jumlah tersebut merupakan baseline test case. Test case dapat bertambah apabila ditemukan kebutuhan baru, defect, atau kondisi tambahan selama proses pengujian.

---

# 4. Use Case Scenario Testing

## 4.1 UC-01 — Login

| ID | Requirement | Skenario | Preconditions | Test Data / Input | Expected Result |
|---|---|---|---|---|---|
| TC-UC01-01 | FR-01 | Login Admin dengan kredensial valid | Akun Admin terdaftar dan aktif | Email: `admin@test.local`; Password: `ValidPassword123!` | Sistem memvalidasi kredensial dan mengarahkan Admin ke halaman yang sesuai dengan role Admin. |
| TC-UC01-02 | FR-01 | Login User dengan kredensial valid | Akun User terdaftar dan aktif | Email: `user@test.local`; Password: `ValidPassword123!` | Sistem memvalidasi kredensial dan mengarahkan User ke halaman yang sesuai dengan role User. |
| TC-UC01-03 | FR-01 | Login dengan password salah | Email terdaftar | Email: `admin@test.local`; Password: `WrongPassword!` | Sistem menolak login dan menampilkan pesan kesalahan autentikasi. |
| TC-UC01-04 | FR-01 | Login dengan email tidak terdaftar | Tidak ada akun dengan email tersebut | Email: `unknown@test.local`; Password: `ValidPassword123!` | Sistem menolak login dan menampilkan pesan bahwa kredensial/akun tidak valid. |
| TC-UC01-05 | FR-01 | Login dengan field kosong | Halaman login tersedia | Email: kosong; Password: kosong | Sistem menolak pengiriman form dan menampilkan validasi field wajib. |
| TC-UC01-06 | FR-01 | User mencoba mengakses fitur Admin | User telah login | URL/endpoint fitur Admin | Sistem menolak akses User ke fitur yang hanya diperuntukkan bagi Admin. |

---

## 4.2 UC-02 — Input Data Pertanian

| ID | Requirement | Skenario | Preconditions | Test Data / Input | Expected Result |
|---|---|---|---|---|---|
| TC-UC02-01 | FR-04 | Input aktivitas harian valid | User login dan blok tersedia | Blok: `Lembang`; Tanggal: `2026-08-09`; Biaya: `7000000`; Catatan: `Tanam stroberi` | Sistem memvalidasi dan menyimpan laporan aktivitas. Status laporan menjadi `Menunggu Validasi` sesuai alur bisnis. |
| TC-UC02-02 | FR-04 | Input aktivitas dengan field wajib kosong | User login dan form tersedia | Blok: kosong; Tanggal: `2026-08-09`; Catatan: kosong | Sistem menolak pengiriman dan menampilkan validasi pada field wajib. |
| TC-UC02-03 | FR-06 | Input hasil panen valid | User login dan blok tersedia | Blok: `Lembang`; Tanggal: `2026-08-09`; Hasil: `230 kg`; Pendapatan: `1500000`; Catatan: `Panen stroberi` | Data hasil panen tersimpan dan ringkasan/statistik panen diperbarui sesuai data. |
| TC-UC02-04 | FR-06 | Input hasil panen dengan field wajib kosong | User login dan form tersedia | Blok: kosong; Hasil panen: kosong | Sistem menolak pengiriman dan menampilkan validasi field wajib. |
| TC-UC02-05 | FR-04 | User menginput aktivitas pada blok yang tidak menjadi kewenangannya | User login; blok lain tersedia | Blok milik User lain | Sistem menolak akses/input terhadap blok yang tidak menjadi kewenangan User. |
| TC-UC02-06 | FR-06 | Penyimpanan hasil panen gagal | User login; terjadi kondisi kegagalan server/database | Data panen valid | Sistem menampilkan informasi kegagalan dan tidak menampilkan data sebagai berhasil tersimpan. |

---

## 4.3 UC-03 — Mengelola Data Kelompok Tani dan Validasi

| ID | Requirement | Skenario | Preconditions | Test Data / Input | Expected Result |
|---|---|---|---|---|---|
| TC-UC03-01 | FR-02 | Menambah anggota | Admin login | Data anggota valid | Data anggota tersimpan dan muncul pada daftar anggota. |
| TC-UC03-02 | FR-02 | Mengubah data anggota | Data anggota tersedia | Perubahan nama/informasi anggota | Perubahan tersimpan dan ditampilkan pada daftar anggota. |
| TC-UC03-03 | FR-02 | Menghapus anggota | Data anggota tersedia | Pilih anggota untuk dihapus | Sistem menghapus atau menonaktifkan data sesuai aturan bisnis dan memperbarui daftar. |
| TC-UC03-04 | FR-03 | Menambah profil blok | Admin login | Kode blok, luas, komoditas valid | Profil blok tersimpan dan dapat dipilih pada proses pencatatan. |
| TC-UC03-05 | FR-03 | Mengubah profil blok | Blok tersedia | Perubahan informasi blok | Perubahan tersimpan dan ditampilkan pada data blok. |
| TC-UC03-06 | FR-03 | Menghapus profil blok | Blok tersedia dan memenuhi aturan penghapusan | Pilih blok | Sistem menjalankan penghapusan sesuai aturan integritas data. |
| TC-UC03-07 | FR-05 | Menerima laporan aktivitas | Laporan berstatus `Menunggu Validasi` | Admin memilih `Terima` | Status laporan berubah menjadi `Tervalidasi` dan dapat digunakan pada proses laporan sesuai aturan bisnis. |
| TC-UC03-08 | FR-05 | Menolak laporan aktivitas | Laporan berstatus `Menunggu Validasi` | Admin memilih `Tolak` dan mengisi alasan jika diwajibkan | Status laporan berubah menjadi `Ditolak` dan informasi penolakan tersimpan sesuai implementasi. |
| TC-UC03-09 | FR-05 | User mencoba melakukan validasi | User login | User mengakses fungsi validasi | Sistem menolak operasi validasi. |

---

## 4.4 UC-04 — Dashboard dan Laporan

| ID | Requirement | Skenario | Preconditions | Test Data / Input | Expected Result |
|---|---|---|---|---|---|
| TC-UC04-01 | FR-09 | Melihat dashboard dengan data | Data tersedia | Periode/blok valid | Dashboard menampilkan ringkasan sesuai data pada periode/blok yang dipilih. |
| TC-UC04-02 | FR-09 | Melihat dashboard tanpa data | Tidak ada data pada periode/blok | Periode/blok tanpa data | Sistem menampilkan kondisi kosong secara informatif dan tidak menghasilkan angka yang menyesatkan. |
| TC-UC04-03 | FR-07 | Melihat rekapitulasi biaya | Data biaya tersedia | Periode/blok valid | Sistem menampilkan total/rekapitulasi biaya sesuai data yang diperhitungkan. |
| TC-UC04-04 | FR-08 | Melihat performa finansial | Data biaya dan hasil tersedia | Periode/blok valid | Sistem menampilkan performa finansial sesuai formula yang ditetapkan. |
| TC-UC04-05 | FR-07 | Menghasilkan laporan | Data laporan tersedia | Pilih periode/blok | Sistem menghasilkan laporan dengan data sesuai filter. |
| TC-UC04-06 | FR-10 | Notifikasi setelah penyimpanan berhasil | Form valid | Simpan aktivitas/panen | Sistem menampilkan notifikasi keberhasilan setelah server mengonfirmasi penyimpanan. |

---

# 5. Boundary Value Analysis

BVA digunakan pada field yang memiliki batas nilai atau aturan validasi. Batas numerik final harus mengikuti validation rule pada implementasi sistem.

## 5.1 Hasil Panen

| ID | Skenario | Input | Expected Result |
|---|---|---:|---|
| TC-BVA-01 | Nilai negatif | `-1 kg` | Sistem menolak nilai negatif jika hasil panen mensyaratkan nilai non-negatif. |
| TC-BVA-02 | Nilai minimum valid | `0 kg` | Sistem menerima nilai 0 apabila aturan bisnis memperbolehkannya. |
| TC-BVA-03 | Nilai normal | `1 kg` | Sistem menerima dan menyimpan data. |
| TC-BVA-04 | Nilai pecahan | `0.5 kg` | Sistem menerima atau menolak sesuai tipe data dan aturan validasi yang ditetapkan. |
| TC-BVA-05 | Nilai sangat besar | Nilai maksimum yang diperbolehkan | Sistem menerima apabila masih berada dalam batas valid. |
| TC-BVA-06 | Melebihi batas | Nilai maksimum + 1 | Sistem menolak apabila melewati batas validasi. |

## 5.2 Biaya Operasional

| ID | Skenario | Input | Expected Result |
|---|---|---:|---|
| TC-BVA-07 | Nilai negatif | `-100000` | Sistem menolak nominal negatif. |
| TC-BVA-08 | Nilai minimum | `0` | Sistem menerima nilai Rp0 apabila diperbolehkan aturan bisnis. |
| TC-BVA-09 | Nilai normal | `7000000` | Sistem menerima dan menyimpan biaya. |
| TC-BVA-10 | Nilai maksimum valid | Nilai maksimum yang ditetapkan validation rule | Sistem menerima apabila berada dalam batas. |
| TC-BVA-11 | Melebihi batas | Nilai maksimum + 1 | Sistem menolak apabila melewati batas. |
| TC-BVA-12 | Format bukan angka | `abc` | Sistem menolak input dan menampilkan validasi format angka. |

---

# 6. State Transition Testing

State Transition Testing digunakan untuk memverifikasi perubahan status laporan.

State utama:

```text
[Menunggu Validasi]
       |
       +--------> [Tervalidasi]
       |
       +--------> [Ditolak]
```

| ID | Requirement | Current State | Action | Expected State |
|---|---|---|---|---|
| TC-STT-01 | FR-05 | Menunggu Validasi | Admin memilih Terima | Tervalidasi |
| TC-STT-02 | FR-05 | Menunggu Validasi | Admin memilih Tolak | Ditolak |
| TC-STT-03 | FR-05 | Tervalidasi | User mencoba mengubah status | Status tetap Tervalidasi dan operasi ditolak |
| TC-STT-04 | FR-05 | Ditolak | User/Admin membuka riwayat | Status tetap Ditolak dan informasi penolakan ditampilkan sesuai implementasi |

---

# 7. Authorization Testing

Pengujian dilakukan pada level UI dan backend. Hilangnya tombol/menu pada UI saja tidak cukup untuk menyatakan otorisasi berhasil.

| ID | Skenario | Aktor | Expected Result |
|---|---|---|---|
| TC-AUTH-01 | Mengakses dashboard Admin | Admin | Akses diberikan |
| TC-AUTH-02 | Mengakses fungsi pengelolaan anggota | Admin | Akses diberikan |
| TC-AUTH-03 | User membuka URL fitur pengelolaan anggota | User | Akses ditolak |
| TC-AUTH-04 | User mengirim request validasi laporan | User | Request ditolak oleh backend |
| TC-AUTH-05 | User mengubah data blok yang bukan kewenangannya | User | Operasi ditolak |
| TC-AUTH-06 | Pengguna belum login membuka halaman terproteksi | Guest | Pengguna diarahkan ke login atau akses ditolak |

---

# 8. Data Integrity & Consistency Testing

| ID | Area | Kondisi | Expected Result |
|---|---|---|---|
| TC-DATA-01 | Persistence | Data berhasil disimpan kemudian halaman di-refresh | Data tetap tersedia |
| TC-DATA-02 | Database | Data aktivitas berhasil disimpan | Data terdapat pada database sesuai record yang dibuat |
| TC-DATA-03 | Validation | Laporan ditolak | Data tidak diperlakukan sebagai laporan tervalidasi |
| TC-DATA-04 | Relationship | Aktivitas dikaitkan dengan blok | Relasi aktivitas dan blok sesuai data |
| TC-DATA-05 | Duplicate | Form dikirim lebih dari satu kali | Sistem mencegah atau menangani duplikasi sesuai aturan yang ditetapkan |
| TC-DATA-06 | Failure Recovery | Koneksi/server gagal saat penyimpanan | Sistem tidak menampilkan proses sebagai berhasil apabila transaksi belum tersimpan |

---

# 9. Calculation Verification

Perhitungan diverifikasi menggunakan data uji yang hasilnya dapat dihitung secara manual.

## 9.1 Total Biaya

| ID | Input | Expected |
|---|---|---:|
| TC-CALC-01 | Biaya Rp500.000 + Rp250.000 | Rp750.000 |
| TC-CALC-02 | Tidak ada biaya | Rp0 atau kondisi kosong sesuai aturan bisnis |

## 9.2 Laba/Rugi

Formula baseline:

```text
Laba/Rugi = Total Pendapatan - Total Biaya
```

| ID | Pendapatan | Biaya | Expected |
|---|---:|---:|---:|
| TC-CALC-03 | Rp1.500.000 | Rp1.000.000 | Laba Rp500.000 |
| TC-CALC-04 | Rp1.000.000 | Rp1.000.000 | Impas/Rp0 |
| TC-CALC-05 | Rp800.000 | Rp1.000.000 | Rugi Rp200.000 |
| TC-CALC-06 | Rp0 | Rp1.000.000 | Rugi Rp1.000.000 |

Jika sistem memiliki formula pendapatan yang lebih spesifik, misalnya berdasarkan bobot panen × harga jual, test case harus diperbarui mengikuti formula bisnis final.

---

# 10. Performance Test Cases

Target waktu respons mengikuti SRS, yaitu maksimal 2–3 detik pada kondisi jaringan normal.

| ID | Area | Kondisi | Expected Result |
|---|---|---|---|
| TC-PERF-01 | Login | Kredensial valid, jaringan normal | Respons ≤ 2–3 detik |
| TC-PERF-02 | Input data | Form valid, jaringan normal | Konfirmasi penyimpanan ≤ 2–3 detik |
| TC-PERF-03 | Dashboard | Dataset pengujian tersedia | Dashboard tampil ≤ 2–3 detik |
| TC-PERF-04 | Laporan | Filter periode/blok dengan dataset pengujian | Laporan tampil ≤ 2–3 detik |

Catatan pengukuran harus mencatat perangkat, browser, jumlah data, kondisi jaringan, dan metode pengukuran.

---

# 11. Responsive & Compatibility Test Cases

| ID | Platform | Skenario | Expected Result |
|---|---|---|---|
| TC-UI-01 | Desktop Chrome | Login dan navigasi | Layout tampil dan dapat digunakan |
| TC-UI-02 | Desktop Firefox | Dashboard dan laporan | Layout dan fungsi berjalan |
| TC-UI-03 | Safari | Form dan dashboard | Layout dan fungsi utama berjalan |
| TC-UI-04 | Mobile Chrome | Input aktivitas | Form dapat digunakan tanpa elemen terpotong |
| TC-UI-05 | Mobile browser | Input hasil panen | Form dapat digunakan dan validasi terbaca |
| TC-UI-06 | Mobile browser | Dashboard/riwayat | Informasi dapat dibaca dan navigasi tetap dapat digunakan |

---

# 12. UAT Test Scenario

UAT tidak menggantikan functional testing. UAT digunakan untuk menilai kesesuaian sistem dari perspektif pengguna akhir.

## 12.1 Skenario UAT Admin

| ID | Aktivitas | Expected Outcome |
|---|---|---|
| UAT-ADM-01 | Login sebagai Admin | Pengguna dapat masuk tanpa kesulitan |
| UAT-ADM-02 | Mengelola anggota | Pengguna dapat memahami proses pengelolaan anggota |
| UAT-ADM-03 | Mengelola blok | Pengguna dapat mengelola profil lahan/blok |
| UAT-ADM-04 | Memvalidasi laporan | Pengguna dapat menerima/menolak laporan |
| UAT-ADM-05 | Melihat laporan finansial | Informasi dapat dipahami dan digunakan untuk evaluasi |

## 12.2 Skenario UAT User

| ID | Aktivitas | Expected Outcome |
|---|---|---|
| UAT-USR-01 | Login melalui smartphone | Pengguna dapat login |
| UAT-USR-02 | Mengisi aktivitas harian | Pengguna dapat menyelesaikan input tanpa kebingungan |
| UAT-USR-03 | Mengisi hasil panen | Pengguna dapat menyimpan hasil panen |
| UAT-USR-04 | Melihat status laporan | Pengguna dapat memahami status laporan |
| UAT-USR-05 | Melihat riwayat/dashboard | Informasi dapat dipahami |

---

# 13. Halstead Metrics Test Record

Pengukuran kompleksitas kode dilakukan terhadap controller backend yang dipilih. Karena nilai metrik bergantung pada source code aktual, nilai berikut tidak boleh diisi sebelum analisis source code dilakukan.

| Field | Nilai |
|---|---|
| File yang dianalisis | Diisi saat pengujian |
| Commit/Version | Diisi saat pengujian |
| Tool | Diisi saat pengujian |
| n1 | Diisi saat pengujian |
| n2 | Diisi saat pengujian |
| N1 | Diisi saat pengujian |
| N2 | Diisi saat pengujian |
| Vocabulary (n) | `n1 + n2` |
| Length (N) | `N1 + N2` |
| Volume (V) | `N × log2(n)` |
| Difficulty (D) | `(n1 / 2) × (N2 / n2)` |
| Effort (E) | `D × V` |

Halstead Metrics merupakan pengukuran karakteristik kode dan tidak digunakan sebagai pengganti functional testing, security testing, atau performance testing.

---

# 14. Test Execution Record

Bagian berikut digunakan saat test case benar-benar dieksekusi.

| ID | Actual Result | Status | Evidence | Defect ID | Tester | Date |
|---|---|---|---|---|---|---|
| TC-UC01-01 | — | NOT RUN | — | — | — | — |
| TC-UC01-02 | — | NOT RUN | — | — | — | — |
| TC-UC01-03 | — | NOT RUN | — | — | — | — |
| TC-UC01-04 | — | NOT RUN | — | — | — | — |
| TC-UC01-05 | — | NOT RUN | — | — | — | — |
| TC-UC01-06 | — | NOT RUN | — | — | — | — |

Untuk seluruh test case lainnya, gunakan format yang sama. Actual Result tidak boleh disalin dari Expected Result tanpa melakukan eksekusi.

---

# 15. Defect Classification

Jika test case menghasilkan `FAIL`, buat defect dengan severity:

| Severity | Definisi |
|---|---|
| Critical | Fungsi utama sistem tidak dapat digunakan dan tidak tersedia workaround yang layak |
| High | Fungsi utama gagal dan berdampak signifikan terhadap proses bisnis |
| Medium | Fungsi mengalami masalah tetapi masih terdapat workaround |
| Low | Masalah minor yang tidak berdampak signifikan terhadap proses utama |

Alur defect:

```text
Open
  ↓
In Progress
  ↓
Fixed
  ↓
Retest
  ├── Pass → Closed
  └── Fail → Reopened
```

---

# 16. Regression Testing

Regression testing dilakukan setelah defect diperbaiki untuk memastikan perubahan tidak merusak fungsi yang sebelumnya telah berhasil.

Minimum regression scope:

- Login dan logout.
- Otorisasi Admin/User.
- Input aktivitas.
- Input hasil panen.
- Validasi laporan.
- Dashboard.
- Rekapitulasi biaya.
- Performa finansial.
- Notifikasi penyimpanan.

Regression test harus menggunakan test case yang relevan dengan modul yang mengalami perubahan serta fungsi yang memiliki dependency terhadap perubahan tersebut.

---

# 17. Traceability Matrix

| Requirement | Test Case |
|---|---|
| FR-01 | TC-UC01-01 s.d. TC-UC01-06, TC-AUTH-01, TC-AUTH-03, TC-AUTH-06 |
| FR-02 | TC-UC03-01 s.d. TC-UC03-03 |
| FR-03 | TC-UC03-04 s.d. TC-UC03-06 |
| FR-04 | TC-UC02-01, TC-UC02-02, TC-UC02-05, TC-DATA-01, TC-BVA-07 s.d. TC-BVA-12 |
| FR-05 | TC-UC03-07 s.d. TC-UC03-09, TC-STT-01 s.d. TC-STT-04 |
| FR-06 | TC-UC02-03, TC-UC02-04, TC-UC02-06, TC-BVA-01 s.d. TC-BVA-06 |
| FR-07 | TC-UC04-03, TC-UC04-05, TC-CALC-01, TC-CALC-02 |
| FR-08 | TC-UC04-04, TC-CALC-03 s.d. TC-CALC-06 |
| FR-09 | TC-UC04-01, TC-UC04-02, TC-PERF-03, TC-UI-01, TC-UI-06 |
| FR-10 | TC-UC04-06 |

---

# 18. Acceptance Criteria

Secara umum, fitur dianggap memenuhi pengujian apabila:

1. Expected Result tercapai.
2. Tidak ditemukan defect Critical atau High yang belum memiliki keputusan penyelesaian.
3. Hak akses Admin dan User berjalan sesuai SRS.
4. Data yang berhasil disimpan dapat dipertahankan dan diakses kembali.
5. Perhitungan menghasilkan nilai yang sesuai dengan data uji dan formula yang telah ditetapkan.
6. Target performance tercapai pada kondisi pengujian yang telah ditentukan.
7. Fungsi utama dapat digunakan pada perangkat desktop dan mobile.
8. Hasil UAT menunjukkan tingkat penerimaan sesuai kriteria yang ditetapkan dalam Test Plan.

---

## 19. Catatan Penggunaan Dokumen

Dokumen ini harus diperlakukan sebagai dokumen pengujian yang hidup (*living test document*). Apabila terdapat perubahan requirement, fitur, validation rule, formula finansial, atau hak akses, test case terkait harus ditinjau dan diperbarui.

Khusus nilai input seperti batas minimum/maksimum, pesan error, dan formula finansial yang belum didefinisikan secara eksplisit pada SRS, nilai final harus mengikuti implementasi dan aturan bisnis yang telah disepakati. Jangan mengubah Expected Result hanya agar sesuai dengan hasil aktual; apabila implementasi tidak sesuai requirement, catat sebagai defect atau lakukan perubahan requirement secara formal.

**Akhir Dokumen**
