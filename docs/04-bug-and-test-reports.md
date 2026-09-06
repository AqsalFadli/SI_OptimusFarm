# Laporan Pengujian dan Temuan Cacat Sistem (Bug & Test Report)
## Sistem Informasi Pengelolaan Lahan Pertanian — Optimus Farm

**Dokumen:** Bug & Test Execution Report  
**Sistem:** Sistem Informasi Pengelolaan Lahan Pertanian  
**Organisasi:** Kelompok Tani Optimus Farm, Pangalengan  
**Versi:** 1.0  
**Status:** Final Draft  
**Tanggal:** 6 September 2026  

---

## 1. Pendahuluan

### 1.1 Tujuan Dokumen
Dokumen Bug & Test Report ini mendokumentasikan hasil pelaksanaan pengujian perangkat lunak, rekapitulasi tingkat keberhasilan skenario uji, serta rincian temuan cacat sistem (*bug*) beserta analisis akar masalah (*root cause analysis*) pada Sistem Informasi Pengelolaan Lahan Pertanian Kelompok Tani Optimus Farm.

Dokumen ini berfungsi sebagai bahan evaluasi kualitas perangkat lunak dari aspek keandalan (*reliability*) dan fungsionalitas (*functionality*) sebelum sistem diimplementasikan di lingkungan produksi.

### 1.2 Ringkasan Hasil Pengujian
Pengujian dilakukan menggunakan kombinasi metode *Black-Box Testing* (terdiri atas *Use Case Scenario Testing*, *Boundary Value Analysis*, dan *State Transition Testing*). Berdasarkan total 20 skenario uji yang dieksekusi, sistem mencatatkan persentase keberhasilan sebesar **95%** dengan rincian 19 skenario dinyatakan *Pass* dan 1 skenario dinyatakan *Fail*.

Terdapat 5 temuan *bug* yang teridentifikasi selama proses pengujian dengan distribusi tingkat keparahan (*severity*) terdiri atas 2 *High*, 1 *Medium*, dan 2 *Low*. Seluruh *bug* tersebut saat ini berada dalam status *Open* dan memerlukan tindakan perbaikan.

---

## 2. Rekapitulasi Hasil Pengujian (Test Execution Report)

### 2.1 Ringkasan Pengujian Berdasarkan Modul

| No | Modul / Teknik Pengujian | Total Skenario | Pass | Fail | Persentase Keberhasilan |
| :---: | :--- | :---: | :---: | :---: | :---: |
| 1 | UC-01 Modul Autentikasi (Login) | 4 | 3 | 1 | 75% |
| 2 | UC-02 Modul Registrasi Akun Petani | 3 | 3 | 0 | 100% |
| 3 | UC-03 Modul Console Admin | 3 | 3 | 0 | 100% |
| 4 | UC-04 Modul Pencatatan Lahan dan Panen | 3 | 3 | 0 | 100% |
| 5 | Boundary Value Analysis (BVA) | 5 | 5 | 0 | 100% |
| 6 | State Transition Testing (STT) | 2 | 2 | 0 | 100% |
| **Total** | **Keseluruhan Pengujian Fungsional** | **20** | **19** | **1** | **95%** |

### 2.2 Perhitungan Persentase Keberhasilan
Formula kalkulasi tingkat keberhasilan eksekusi pengujian adalah sebagai berikut:

$$\text{Persentase Keberhasilan} = \left( \frac{\text{Jumlah Test Case Pass}}{\text{Jumlah Total Test Case}} \right) \times 100\%$$

$$\text{Persentase Keberhasilan} = \left( \frac{19}{20} \right) \times 100\% = 95\%$$

---

## 3. Daftar Temuan Bug (Defect Log)

| Bug ID | Severity | Deskripsi Masalah | Status |
| :---: | :---: | :--- | :---: |
| BUG-01 | Medium | Tidak ada umpan balik (*warning message*) saat menginput angka negatif (`-100000`) pada field nilai/pendapatan panen (Rp). Data tidak tersimpan namun sistem merespons dengan status HTTP `302 Found`. | Open |
| BUG-02 | High | Kesalahan pembacaan tanda koma (`,`) pada field biaya operasional (Rp). Input `100,000` salah ditafsirkan sebagai pemisah desimal, sehingga nominal yang terbaca pada riwayat laporan menyusut menjadi `Rp 100`. | Open |
| BUG-03 | High | Kesalahan pembacaan tanda koma (`,`) pada field nilai/pendapatan panen (Rp). Input `100,000` salah ditafsirkan sebagai pemisah desimal, sehingga nominal yang terbaca pada riwayat laporan menyusut menjadi `Rp 100`. | Open |
| BUG-04 | Low | Teks nominal angka pada kartu statistik finansial meluap (*overflow*) keluar dari kontainer saat diakses melalui perangkat *mobile*. | Open |
| BUG-05 | Low | Form pendaftaran akun menerima input nama pengguna yang diakhiri dengan karakter spasi atau titik (`.`). | Open |

---

## 4. Analisis Akar Masalah dan Rencana Perbaikan

### 4.1 BUG-01 (Medium) — Tidak Ada Umpan Balik Validasi Input Negatif
* **Gambaran Masalah:** Tester menginput nominal `-100000` pada field nilai/pendapatan panen. Data ditolak oleh backend, tetapi antarmuka frontend tidak menampilkan pesan kesalahan.
* **Akar Penyebab (*Root Cause*):** Komponen frontend React tidak menangkap dan menampilkan respons galat validasi (*validation error state*) yang dikirimkan oleh server Laravel.
* **Dampak:** Pengguna mengalami kebingungan karena menganggap sistem mengalami kegagalan atau data telah berhasil disimpan padahal ditolak.
* **Rencana Solusi (*Action Plan*):** Menghubungkan *error handler* dari respons Inertia.js ke komponen *form UI* agar teks peringatan validasi tampil langsung di bawah bidang input yang bersangkutan.

### 4.2 BUG-02 (High) — Kesalahan Pembacaan Tanda Koma pada Biaya Operasional
* **Gambaran Masalah:** Tester menginput `100,000` dengan maksud mencatat nominal seratus ribu rupiah. Sistem menyimpan nilai tersebut sebagai `100`.
* **Akar Penyebab (*Root Cause*):** Parser angka pada server mengandalkan format standar internasional yang menganggap tanda koma (`,`) sebagai pemisah desimal (*decimal mark*), bukan pemisah ribuan (*thousand separator*).
* **Dampak:** Terjadi kerusakan integritas data keuangan. Akumulasi pengeluaran petani tercatat jauh di bawah nilai aktual dan merusak perhitungan laba bersih.
* **Rencana Solusi (*Action Plan*):** Menambahkan fungsi *string sanitization* pada backend untuk menghapus seluruh karakter non-numerik (koma dan titik) sebelum diubah menjadi tipe data numerik (*integer/float*).

### 4.3 BUG-03 (High) — Kesalahan Pembacaan Tanda Koma pada Nilai Pendapatan Panen
* **Gambaran Masalah:** Tester menginput `100,000` pada field pendapatan panen. Sistem menyimpan nilai tersebut sebagai `100`.
* **Akar Penyebab (*Root Cause*):** Parser angka pada server mengandalkan format standar internasional yang menganggap tanda koma (`,`) sebagai pemisah desimal.
* **Dampak:** Data pendapatan panen tercatat tidak akurat, yang berimplikasi pada ketidaksesuaian laporan finansial dan evaluasi performa lahan.
* **Rencana Solusi (*Action Plan*):** Menerapkan fungsi *sanitization* data masukan yang sama seperti pada BUG-02 sebelum variabel disimpan ke dalam basis data.

### 4.4 BUG-04 (Low) — Teks Nominal Angka Meluap pada Perangkat Mobile
* **Gambaran Masalah:** Saat dibuka di peranti bergerak (*mobile browser*), teks angka pada kartu ringkasan finansial keluar melampaui batas kontainer.
* **Akar Penyebab (*Root Cause*):** Penataan ukuran teks (*font size*) pada kartu ringkasan diatur secara statis tanpa mengikuti titik henti (*responsive breakpoints*) layar *mobile*.
* **Dampak:** Tampilan antarmuka tidak rapi secara visual dan informasi finansial menjadi terpotong sehingga sulit dibaca.
* **Rencana Solusi (*Action Plan*):** Memperbaiki kelas CSS Tailwind menggunakan variabel *responsive typography* (misalnya `text-base sm:text-lg md:text-2xl`) atau menerapkan *fluid typography*.

### 4.5 BUG-05 (Low) — Karakter Spasi dan Titik pada Akhiran Nama Registrasi
* **Gambaran Masalah:** Pendaftaran akun baru menerima string nama yang diakhiri dengan spasi atau karakter titik (contoh: `Nama .`).
* **Akar Penyebab (*Root Cause*):** Form pendaftaran akun belum memiliki aturan sanitasi atau pembersihan karakter (*string trimming*) pada input nama.
* **Dampak:** Kualitas dan konsistensi data nama pengguna di dalam basis data menjadi tidak seragam.
* **Rencana Solusi (*Action Plan*):** Menyisipkan fungsi pemotong spasi `.trim()` pada pengendali registrasi di backend sebelum proses pembuatan akun dilakukan.

---

## 5. Evaluasi Kesiapan Implementasi

Berdasarkan hasil pengujian fungsionalitas, sistem telah memenuhi **95%** dari total skenario uji yang dirancang. Namun, ditinjau dari aspek keandalan (*reliability*), sistem memiliki **2 bug tingkat High** (BUG-02 dan BUG-03) yang berdampak langsung pada kalkulasi data finansial.

Sistem dinyatakan **belum layak untuk diimplementasikan secara penuh di lingkungan produksi** sebelum BUG-02 dan BUG-03 diselesaikan dan diverifikasi ulang melalui pengujian regresi (*regression testing*).

---

**Akhir Dokumen**