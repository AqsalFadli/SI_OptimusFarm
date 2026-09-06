# Test Plan
## Sistem Informasi Pengelolaan Lahan Pertanian — Optimus Farm

**Dokumen:** Test Plan  
**Sistem:** Sistem Informasi Pengelolaan Lahan Pertanian  
**Organisasi:** Kelompok Tani Optimus Farm, Pangalengan  
**Versi:** 1.0  
**Status:** Draft Test Plan  
**Tanggal:** 6 September 2026  
**Referensi Utama:** Software Requirements Specification (SRS) Sistem Informasi Pengelolaan Lahan Pertanian

---

## 1. Tujuan Pengujian

Test Plan ini menjadi acuan pelaksanaan pengujian Sistem Informasi Pengelolaan Lahan Pertanian Optimus Farm. Pengujian dilakukan untuk memastikan sistem memenuhi kebutuhan yang telah ditetapkan dalam SRS, berjalan sesuai alur bisnis, menjaga pembatasan hak akses, serta dapat digunakan oleh pengguna akhir.

Tujuan pengujian meliputi:

1. Memverifikasi implementasi seluruh kebutuhan fungsional FR-01 sampai FR-10.
2. Memastikan autentikasi dan otorisasi Admin dan User berjalan sesuai hak akses.
3. Memastikan proses pencatatan aktivitas pertanian dan hasil panen berjalan dengan benar.
4. Memastikan proses validasi laporan oleh Admin menghasilkan status yang sesuai.
5. Memverifikasi konsistensi data antara input, database, dashboard, dan laporan.
6. Memverifikasi perhitungan biaya dan performa finansial berdasarkan data yang tersedia.
7. Memastikan notifikasi penyimpanan data ditampilkan sesuai kondisi proses.
8. Mengevaluasi aspek usability, khususnya penggunaan sistem melalui perangkat mobile oleh User.
9. Mengukur kompleksitas kode backend menggunakan Halstead Metrics sebagai evaluasi kualitas kode, apabila pengukuran tersebut ditetapkan sebagai bagian dari evaluasi proyek.

---

## 2. Ruang Lingkup Pengujian

Pengujian mencakup fitur dan komponen utama yang secara langsung mendukung kebutuhan pada SRS.

### 2.1 Fitur yang Diuji

| Area | Cakupan | Referensi |
|---|---|---|
| Autentikasi dan Otorisasi | Login, validasi kredensial, pembatasan akses berdasarkan peran | FR-01 |
| Data Anggota | Tambah, lihat, ubah, hapus data anggota | FR-02 |
| Profil Lahan/Blok | Tambah, lihat, ubah, hapus data blok, kode blok, komoditas | FR-03 |
| Aktivitas Pertanian | Input aktivitas harian berdasarkan blok | FR-04 |
| Validasi Laporan | Pemeriksaan, penerimaan, dan penolakan laporan | FR-05 |
| Hasil Panen | Input hasil panen berdasarkan blok | FR-06 |
| Rekapitulasi Biaya | Perhitungan dan penyajian biaya | FR-07 |
| Performa Finansial | Perhitungan untung/rugi berdasarkan biaya dan hasil panen | FR-08 |
| Dashboard | Status lahan, biaya, estimasi/hasil panen, dan ringkasan data | FR-09 |
| Notifikasi | Umpan balik keberhasilan atau kegagalan penyimpanan | FR-10 |

### 2.2 Lingkungan Pengujian

Lingkungan pengujian mengikuti teknologi yang didefinisikan pada SRS:

| Komponen | Lingkungan/Teknologi |
|---|---|
| Backend | Laravel 11.x |
| Runtime | PHP 8.2+ |
| Frontend | React.js + Inertia.js |
| Styling | Tailwind CSS |
| Build Tool | Vite |
| Database | MySQL 9.x |
| Development Server | Lingkungan lokal seperti DBngin/XAMPP |
| Browser Desktop | Google Chrome, Mozilla Firefox, Apple Safari |
| Perangkat Mobile | Smartphone dengan mobile browser |

Versi aktual komponen yang digunakan pada saat eksekusi pengujian harus dicatat pada Test Report agar hasil dapat direproduksi.

### 2.3 Di Luar Ruang Lingkup

Pengujian berikut tidak termasuk dalam Test Plan ini:

- Penetration testing tingkat lanjut.
- Pengujian ketahanan terhadap beban jaringan ekstrem.
- Integrasi dengan perangkat keras eksternal.
- Sensor otomatis berbasis IoT.
- Integrasi dengan sistem gerbang pembayaran.

---

## 3. Strategi Pengujian

Pengujian menggunakan pendekatan berlapis agar fungsi, batas input, perubahan status, kualitas kode, dan penerimaan pengguna dapat dievaluasi.

| Metode | Tujuan | Objek |
|---|---|---|
| Black-Box Testing | Memverifikasi perilaku sistem berdasarkan input dan output | FR-01–FR-10 |
| Use Case Scenario Testing | Memastikan alur utama dan alternatif berjalan sesuai spesifikasi | UC-01–UC-04 |
| Boundary Value Analysis | Menguji nilai batas pada input yang relevan | Form aktivitas, panen, biaya |
| State Transition Testing | Memverifikasi perubahan status laporan | Menunggu Validasi → Tervalidasi/Ditolak |
| Integration/Data Consistency Testing | Memastikan data antar proses tetap konsisten | Input → Database → Dashboard/Laporan |
| Halstead Metrics | Mengukur kompleksitas kode secara kuantitatif | Controller backend terpilih |
| User Acceptance Testing | Mengevaluasi penerimaan dan usability pengguna akhir | Admin dan User |

---

## 4. Black-Box Testing

Black-box testing dilakukan tanpa bergantung pada struktur internal kode. Penguji memberikan input tertentu kemudian membandingkan hasil aktual dengan hasil yang diharapkan.

### 4.1 Teknik Use Case Scenario Testing

Skenario pengujian diturunkan dari UC-01 sampai UC-04.

| Use Case | Skenario Utama | Skenario Alternatif |
|---|---|---|
| UC-01 Login | Login menggunakan kredensial valid | Kredensial salah, field kosong |
| UC-02 Input Data Pertanian | Input aktivitas/panen dengan data valid | Data kosong, format salah, nilai batas |
| UC-03 Kelola Data Kelompok Tani | CRUD data dan validasi laporan | Data tidak valid, laporan ditolak |
| UC-04 Dashboard/Laporan | Menampilkan data berdasarkan periode/blok | Data tidak tersedia |

### 4.2 Boundary Value Analysis

BVA diterapkan pada field yang mempunyai batas nilai atau format tertentu.

Contoh nilai yang perlu diuji:

| Input | Nilai Batas yang Diuji |
|---|---|
| Jumlah/berat panen | 0, nilai minimum valid, nilai normal, nilai maksimum valid, nilai di atas maksimum |
| Biaya | 0, nilai minimum valid, nilai normal, nilai maksimum valid, nilai negatif |
| Luas lahan | 0, nilai minimum valid, nilai normal, nilai maksimum valid, nilai negatif |
| Tanggal | Format valid, format tidak valid, tanggal kosong |
| Field teks | Kosong, panjang minimum, panjang normal, panjang maksimum, melebihi batas |

Nilai maksimum/minimum yang bersifat spesifik harus mengikuti aturan validasi aktual pada implementasi sistem. Test Plan tidak menetapkan angka baru apabila belum didefinisikan dalam SRS.

### 4.3 State Transition Testing

Status laporan aktivitas diuji berdasarkan perubahan keadaan berikut:

```text
[Data Belum Dikirim]
        |
        v
[Laporan Terkirim]
        |
        v
[Menunggu Validasi]
       / \
      /   \
     v     v
[Tervalidasi] [Ditolak]
                  |
                  v
           [Perbaikan/Pengajuan
              Kembali*]
```

`*` Mekanisme pengajuan kembali perlu disesuaikan dengan implementasi final sistem. Jika fitur tersebut belum tersedia, skenario tidak boleh dinyatakan sebagai fitur yang telah diuji.

Pengujian harus memastikan:

- User tidak dapat menetapkan sendiri status validasi.
- Admin dapat mengubah status sesuai kewenangannya.
- Laporan yang ditolak tidak dihitung sebagai data tervalidasi.
- Laporan tervalidasi dapat digunakan dalam proses laporan sesuai aturan bisnis.
- Status yang ditampilkan pada frontend sesuai dengan status yang tersimpan.

---

## 5. Data Test

Data uji harus dibuat terkontrol dan dapat diulang. Dataset minimal terdiri atas:

| Dataset | Contoh Kondisi |
|---|---|
| Akun Admin valid | Akun dengan role Admin |
| Akun User valid | Akun dengan role User |
| Kredensial salah | Password atau username/email tidak sesuai |
| Anggota valid | Data anggota lengkap |
| Blok valid | Kode blok, luas, dan komoditas lengkap |
| Aktivitas valid | Data aktivitas lengkap dan terkait blok yang tersedia |
| Aktivitas tidak valid | Data kosong atau tidak sesuai aturan validasi |
| Panen valid | Data hasil panen dengan nilai valid |
| Biaya valid | Data biaya dengan nilai valid |
| Data tanpa laporan | Periode/blok tanpa data untuk menguji kondisi kosong |

Data produksi tidak boleh digunakan sebagai data uji tanpa mekanisme pemisahan yang jelas.

---

## 6. Test Case

Test case diberi ID unik agar dapat ditelusuri ke kebutuhan fungsional.

| ID | Requirement | Skenario | Input/Kondisi | Expected Result |
|---|---|---|---|---|
| TC-001 | FR-01 | Login valid | Kredensial Admin valid | Admin berhasil login dan memperoleh akses Admin |
| TC-002 | FR-01 | Login User valid | Kredensial User valid | User berhasil login dan memperoleh akses User |
| TC-003 | FR-01 | Login gagal | Password salah | Sistem menolak login dan menampilkan pesan kesalahan |
| TC-004 | FR-01 | Akses tidak sesuai role | User mengakses fitur Admin | Sistem menolak akses |
| TC-005 | FR-02 | Tambah anggota | Data anggota valid | Data tersimpan |
| TC-006 | FR-02 | Ubah anggota | Data anggota valid | Perubahan tersimpan |
| TC-007 | FR-02 | Hapus anggota | Anggota tersedia | Data terhapus sesuai aturan |
| TC-008 | FR-03 | Tambah blok | Data blok valid | Blok tersimpan |
| TC-009 | FR-03 | Ubah blok | Data blok tersedia | Perubahan tersimpan |
| TC-010 | FR-03 | Hapus blok | Blok tersedia | Blok terhapus sesuai aturan |
| TC-011 | FR-04 | Input aktivitas valid | Data aktivitas lengkap | Data tersimpan dan status sesuai alur |
| TC-012 | FR-04 | Input aktivitas tidak valid | Field wajib kosong | Sistem menolak data dan menampilkan validasi |
| TC-013 | FR-05 | Validasi laporan | Laporan menunggu validasi | Status menjadi tervalidasi |
| TC-014 | FR-05 | Tolak laporan | Laporan tidak sesuai | Status menjadi ditolak |
| TC-015 | FR-06 | Input panen valid | Data panen lengkap | Data panen tersimpan |
| TC-016 | FR-06 | Input panen tidak valid | Nilai tidak sesuai aturan | Sistem menolak input |
| TC-017 | FR-07 | Rekap biaya | Data biaya tersedia | Total/rekap biaya ditampilkan sesuai data |
| TC-018 | FR-08 | Performa finansial | Biaya dan hasil tersedia | Nilai untung/rugi dihitung sesuai aturan |
| TC-019 | FR-09 | Dashboard | Data tersedia | Ringkasan ditampilkan |
| TC-020 | FR-09 | Dashboard tanpa data | Periode/blok tanpa data | Sistem menampilkan kondisi kosong dengan benar |
| TC-021 | FR-10 | Penyimpanan berhasil | Data valid | Notifikasi berhasil ditampilkan |
| TC-022 | FR-10 | Penyimpanan gagal | Data tidak valid/gagal diproses | Sistem menampilkan informasi kegagalan |

Test case di atas merupakan baseline. Saat eksekusi, setiap case perlu dilengkapi dengan tanggal pengujian, tester, actual result, status Pass/Fail, dan evidence.

---

## 7. Pengujian Otorisasi

Pengujian otorisasi harus memastikan bahwa pembatasan hak akses tidak hanya diterapkan pada tampilan menu, tetapi juga pada endpoint atau proses backend.

| ID | Pengujian | Expected Result |
|---|---|---|
| AUTH-01 | User membuka URL fitur Admin | Ditolak |
| AUTH-02 | User mengirim request ke endpoint Admin | Ditolak |
| AUTH-03 | Admin mengakses fitur Admin | Diizinkan |
| AUTH-04 | User mengubah data milik blok yang tidak menjadi kewenangannya | Ditolak |
| AUTH-05 | User mencoba mengubah status validasi | Ditolak |
| AUTH-06 | Pengguna yang belum login mengakses halaman terproteksi | Dialihkan/ditolak sesuai mekanisme autentikasi |

---

## 8. Pengujian Integritas dan Konsistensi Data

Pengujian ini memastikan data yang ditampilkan sistem tidak berbeda dari data yang tersimpan dan diproses.

Area yang diverifikasi:

1. Data form yang berhasil disimpan tersedia kembali setelah halaman di-refresh.
2. Data tersimpan pada database yang benar.
3. Perubahan data pada modul master tercermin pada modul terkait.
4. Data yang ditolak tidak masuk ke rekapitulasi yang hanya menggunakan data tervalidasi.
5. Total biaya sesuai dengan data biaya yang menjadi sumber perhitungan.
6. Hasil panen yang digunakan dalam laporan sesuai dengan data yang tersimpan.
7. Performa finansial menggunakan data biaya dan hasil panen pada periode/blok yang sesuai.
8. Tidak terjadi duplikasi akibat pengiriman form lebih dari satu kali apabila sistem memang menerapkan pencegahan duplikasi.

---

## 9. Pengujian Perhitungan Finansial

Perhitungan finansial harus diuji menggunakan dataset yang nilai input dan hasil yang diharapkan dapat dihitung secara manual.

Secara umum:

```text
Total Biaya = Σ seluruh biaya/modal yang diperhitungkan

Total Pendapatan = nilai hasil panen yang diperhitungkan

Laba/Rugi = Total Pendapatan - Total Biaya
```

Rumus final harus mengikuti aturan bisnis dan implementasi sistem yang disepakati. Test case harus menggunakan angka uji yang menghasilkan nilai yang dapat diverifikasi secara manual.

Contoh:

| Komponen | Nilai Uji |
|---|---:|
| Total biaya | Rp1.000.000 |
| Pendapatan panen | Rp1.500.000 |
| Expected laba/rugi | Rp500.000 laba |

Pengujian juga harus mencakup kondisi:

- Pendapatan lebih besar dari biaya.
- Pendapatan sama dengan biaya.
- Pendapatan lebih kecil dari biaya.
- Tidak terdapat data biaya.
- Tidak terdapat data hasil panen.

---

## 10. Pengujian Respons dan Performance

Pengujian performance dilakukan terhadap operasi yang dianggap kritis:

| Area | Target |
|---|---|
| Login | ≤ 2–3 detik pada kondisi jaringan normal |
| Penyimpanan form | ≤ 2–3 detik pada kondisi jaringan normal |
| Dashboard | ≤ 2–3 detik pada kondisi jaringan normal |
| Laporan | ≤ 2–3 detik pada kondisi jaringan normal |

Pengukuran harus dilakukan pada kondisi yang terdokumentasi, termasuk browser, perangkat, jumlah data uji, koneksi, dan waktu pengujian.

Target 2–3 detik merupakan target SRS, bukan jaminan bahwa setiap kondisi jaringan akan selalu memenuhi angka tersebut.

---

## 11. Pengujian Responsive dan Compatibility

Pengujian dilakukan untuk memastikan antarmuka tetap dapat digunakan pada perangkat desktop dan mobile.

Minimum skenario:

- Desktop dengan resolusi umum.
- Smartphone dengan layar kecil.
- Form input pada mobile.
- Tabel atau daftar data pada mobile.
- Navigasi sistem pada mobile.
- Dashboard pada desktop dan mobile.
- Pesan validasi dan notifikasi pada berbagai ukuran layar.

Browser yang menjadi target pengujian mengikuti SRS:

- Google Chrome.
- Mozilla Firefox.
- Apple Safari.

Hasil pengujian harus mencatat perangkat, browser, versi browser, resolusi layar, dan status Pass/Fail.

---

## 12. Pengujian User Acceptance Testing

UAT dilakukan untuk mengevaluasi apakah sistem dapat digunakan sesuai kebutuhan pengguna akhir.

### 12.1 Responden

| Kelompok | Fokus Evaluasi |
|---|---|
| Admin/Pengurus | Pengelolaan data, validasi laporan, dashboard, laporan biaya, dan performa finansial |
| User/Anggota | Kemudahan input aktivitas dan hasil panen melalui smartphone |

### 12.2 Instrumen UAT

Kuesioner menggunakan skala Likert 1–5:

| Nilai | Interpretasi |
|---:|---|
| 1 | Sangat Tidak Setuju |
| 2 | Tidak Setuju |
| 3 | Cukup/Netral |
| 4 | Setuju |
| 5 | Sangat Setuju |

Aspek yang dievaluasi:

- Kemudahan penggunaan.
- Kejelasan informasi.
- Kemudahan navigasi.
- Kemudahan pengisian data.
- Kesesuaian fitur dengan kebutuhan.
- Kecepatan respons yang dirasakan.
- Kesesuaian penggunaan pada perangkat mobile.
- Kepuasan terhadap sistem secara keseluruhan.

### 12.3 Perhitungan Skor UAT

Persentase skor dapat dihitung dengan:

```text
Persentase = (Total Skor Aktual / Total Skor Maksimum) × 100%
```

Interpretasi kategori harus ditetapkan sebelum hasil UAT dianalisis agar penilaian tidak berubah setelah melihat hasil.

---

## 13. Pengukuran Kompleksitas Kode dengan Halstead Metrics

Pengukuran Halstead digunakan sebagai evaluasi kuantitatif terhadap kompleksitas kode pada controller backend yang dipilih.

Parameter dasar:

- `n1` = jumlah operator unik.
- `n2` = jumlah operand unik.
- `N1` = jumlah total operator.
- `N2` = jumlah total operand.

Metrik dasar:

```text
Program Vocabulary:
n = n1 + n2

Program Length:
N = N1 + N2

Volume:
V = N × log2(n)

Difficulty:
D = (n1 / 2) × (N2 / n2)

Effort:
E = D × V
```

Pengukuran harus menyebutkan:

- File yang dianalisis.
- Versi source code.
- Tool atau metode perhitungan.
- Nilai `n1`, `n2`, `N1`, dan `N2`.
- Hasil setiap metrik.
- Interpretasi hasil.

Halstead Metrics digunakan sebagai indikator kompleksitas dan effort pemrograman, bukan sebagai bukti tunggal bahwa sistem bebas dari error.

---

## 14. Defect Management

Setiap kegagalan test case harus dicatat sebagai defect.

Informasi minimal defect:

| Field | Keterangan |
|---|---|
| Defect ID | Identitas unik defect |
| Test Case ID | Test case yang gagal |
| Modul | Modul yang terdampak |
| Deskripsi | Penjelasan masalah |
| Steps to Reproduce | Langkah untuk menghasilkan masalah |
| Expected Result | Hasil yang seharusnya |
| Actual Result | Hasil aktual |
| Severity | Tingkat dampak masalah |
| Priority | Prioritas perbaikan |
| Evidence | Screenshot/log jika tersedia |
| Status | Open, In Progress, Fixed, Retest, Closed |
| Tester | Penguji |
| Developer | Penanggung jawab perbaikan |

### 14.1 Severity

| Level | Definisi |
|---|---|
| Critical | Sistem atau fungsi utama tidak dapat digunakan dan tidak tersedia workaround yang layak |
| High | Fungsi utama gagal dan berdampak signifikan terhadap proses bisnis |
| Medium | Fungsi mengalami masalah tetapi masih terdapat workaround |
| Low | Masalah minor pada tampilan atau fungsi yang tidak berdampak signifikan |

---

## 15. Entry Criteria dan Exit Criteria

### 15.1 Entry Criteria

Pengujian dapat dimulai apabila:

- Versi aplikasi yang akan diuji telah ditentukan.
- Kebutuhan sistem telah disepakati.
- Lingkungan pengujian tersedia.
- Database test dapat digunakan.
- Akun Admin dan User untuk pengujian tersedia.
- Dataset uji telah disiapkan.
- Test case telah dibuat dan direview.
- Fitur yang akan diuji telah tersedia pada build yang diuji.

### 15.2 Exit Criteria

Pengujian dapat dinyatakan selesai apabila:

- Seluruh test case yang direncanakan telah dieksekusi.
- Seluruh kebutuhan FR-01 sampai FR-10 telah memiliki hasil pengujian.
- Defect Critical dan High telah diperbaiki atau memiliki keputusan resmi untuk diterima sebagai known issue.
- Test case yang gagal telah dilakukan retest setelah perbaikan.
- Hasil UAT telah didokumentasikan.
- Hasil pengukuran kompleksitas telah didokumentasikan apabila termasuk dalam ruang lingkup evaluasi.
- Test Report final telah disusun.

---

## 16. Risiko Pengujian dan Mitigasi

| Risiko | Dampak | Mitigasi |
|---|---|---|
| Data test tidak konsisten | Hasil pengujian tidak dapat dipercaya | Gunakan seeder/dataset terkontrol dan reset database test |
| Kerusakan database saat pengujian | Pengujian terhenti | Backup dataset dan gunakan environment khusus pengujian |
| Keterbatasan literasi digital responden | Hasil UAT tidak merepresentasikan usability sebenarnya | Berikan instruksi singkat dan skenario yang jelas tanpa mengarahkan jawaban |
| Perbedaan tampilan perangkat | Fungsi mobile terganggu | Uji beberapa ukuran layar dan browser |
| Pengurus tidak tersedia saat UAT | UAT tertunda | Jadwalkan sesi alternatif dan siapkan skenario/data simulasi |
| Gangguan jaringan | Hasil performance tidak konsisten | Catat kondisi jaringan dan lakukan pengukuran berulang |
| Perubahan source code saat testing | Hasil tidak reproducible | Tetapkan versi/build yang diuji |

---

## 17. Jadwal Pengujian

Jadwal berikut merupakan baseline dan dapat disesuaikan dengan jadwal aktual proyek.

| Tahap | Aktivitas | Durasi | Output |
|---|---|---:|---|
| 1 | Penyusunan Test Plan dan Test Case | 1 hari | Test Plan, Test Case |
| 2 | Persiapan Environment dan Data Test | 1 hari | Environment siap, Dataset |
| 3 | Eksekusi Black-Box Testing | 1–2 hari | Test Execution Result |
| 4 | Pengujian Integritas Data dan Perhitungan | 1 hari | Hasil verifikasi |
| 5 | Pengujian Responsive dan Compatibility | 1 hari | Compatibility Result |
| 6 | Pengukuran Halstead Metrics | 1–2 hari | Hasil metrik kompleksitas |
| 7 | Pelaksanaan UAT | ±2 jam | Kuesioner dan hasil UAT |
| 8 | Retest dan Regression Testing | Sesuai defect | Retest Result |
| 9 | Penyusunan Test Report | 1–2 hari | Final Test Report |

Penanggung jawab dan tanggal aktual pelaksanaan harus diisi berdasarkan pembagian tugas tim yang sebenarnya. Nama penanggung jawab tidak ditetapkan di dalam baseline ini agar dokumen tidak mengasumsikan pembagian tugas yang belum disepakati.

---

## 18. Traceability Matrix

| Requirement | Test Case | Metode |
|---|---|---|
| FR-01 | TC-001 s.d. TC-004 | Black-box, Authorization |
| FR-02 | TC-005 s.d. TC-007 | Black-box |
| FR-03 | TC-008 s.d. TC-010 | Black-box |
| FR-04 | TC-011 s.d. TC-012 | Black-box, BVA |
| FR-05 | TC-013 s.d. TC-014 | Black-box, State Transition |
| FR-06 | TC-015 s.d. TC-016 | Black-box, BVA |
| FR-07 | TC-017 | Black-box, Data Consistency |
| FR-08 | TC-018 | Black-box, Calculation Verification |
| FR-09 | TC-019 s.d. TC-020 | Black-box, Performance |
| FR-10 | TC-021 s.d. TC-022 | Black-box |

---

## 19. Format Test Execution Record

Pada saat pengujian aktual, setiap test case dicatat menggunakan format berikut:

| Field | Isi |
|---|---|
| Test Case ID | TC-XXX |
| Requirement ID | FR-XX |
| Tester | Nama penguji |
| Tanggal | YYYY-MM-DD |
| Environment | Browser, OS, perangkat, versi aplikasi |
| Preconditions | Kondisi awal |
| Test Steps | Langkah pengujian |
| Test Data | Data yang digunakan |
| Expected Result | Hasil yang diharapkan |
| Actual Result | Hasil aktual |
| Status | Pass / Fail / Blocked |
| Evidence | Screenshot/log |
| Defect ID | Jika Fail |
| Notes | Catatan tambahan |

---

## 20. Kriteria Pelaporan Hasil

Test Report harus sekurang-kurangnya menyajikan:

- Jumlah test case yang direncanakan.
- Jumlah test case yang dieksekusi.
- Jumlah Pass, Fail, dan Blocked.
- Persentase keberhasilan pengujian.
- Daftar defect berdasarkan severity dan status.
- Hasil pengujian hak akses.
- Hasil pengujian integritas data.
- Hasil pengujian performa.
- Hasil pengujian responsive/compatibility.
- Hasil Halstead Metrics jika termasuk dalam evaluasi.
- Hasil UAT.
- Kesimpulan kelayakan sistem berdasarkan bukti pengujian.

Persentase keberhasilan dapat dihitung sebagai:

```text
Pass Rate = (Jumlah Test Case Pass / Jumlah Test Case yang Dieksekusi) × 100%
```

Blocked test case harus dilaporkan secara terpisah dan tidak boleh secara otomatis dianggap Pass.

---

## 21. Catatan Konsistensi dengan SRS

Test Plan ini menggunakan SRS sebagai baseline kebutuhan. Oleh karena itu, setiap perubahan terhadap fitur, aturan bisnis, hak akses, rumus perhitungan, atau teknologi harus terlebih dahulu dicerminkan pada SRS dan kemudian ditinjau dampaknya terhadap Test Plan serta Test Case.

Beberapa detail implementasi yang belum ditentukan secara eksplisit pada SRS, seperti nilai batas minimum/maksimum field, mekanisme pengajuan ulang laporan yang ditolak, formula pendapatan hasil panen secara rinci, jumlah responden UAT, dan pembagian penanggung jawab pengujian, tidak ditetapkan secara sepihak dalam Test Plan ini. Detail tersebut harus ditentukan sebelum test execution apabila diperlukan oleh skenario pengujian.

---

**Akhir Dokumen**
