# Evaluasi Kualitas Sistem (System Quality Evaluation)
## Sistem Informasi Pengelolaan Lahan Pertanian — Optimus Farm

**Dokumen:** System Quality Evaluation Report  
**Sistem:** Sistem Informasi Pengelolaan Lahan Pertanian  
**Organisasi:** Kelompok Tani Optimus Farm, Pangalengan  
**Versi:** 1.0  
**Status:** Final Draft  
**Tanggal:** 6 September 2026  

---

## 1. Pendahuluan

Dokumen ini menyajikan analisis kualitatif dan kuantitatif terhadap kualitas perangkat lunak Sistem Informasi Pengelolaan Lahan Pertanian Optimus Farm[cite: 1]. Evaluasi dilakukan berdasarkan tiga kualifikasi utama standar ISO/IEC 25010, yaitu fungsionalitas (*functionality*), keandalan (*reliability*), dan kebolehgunaan (*usability*)[cite: 1]. 

Hasil evaluasi ini menjadi acuan utama bagi pengurus kelompok tani dan tim pengembang untuk menentukan tingkat kesiapan implementasi (*implementation readiness*) sistem di lingkungan produksi[cite: 1].

---

## 2. Evaluasi Fungsionalitas (Functionality)

Evaluasi fungsionalitas mengukur sejauh mana sistem mampu menyediakan fungsi-fungsi yang memenuhi kebutuhan operasional sesuai dengan dokumen spesifikasi (*Software Requirement Specification*)[cite: 1].

### 2.1 Evaluasi Berdasarkan Hasil Uji Skenario (Test Case)

| No | Modul / Fitur yang Diuji | Jumlah Skenario | Pass | Fail | Persentase Keberhasilan |
| :---: | :--- | :---: | :---: | :---: | :---: |
| 1 | Modul Autentikasi (Login) | 4 | 3 | 1 | 75% |
| 2 | Modul Registrasi Akun Petani | 3 | 3 | 0 | 100% |
| 3 | Modul Console Admin | 3 | 3 | 0 | 100% |
| 4 | Modul Pencatatan Lahan dan Panen | 3 | 3 | 0 | 100% |
| 5 | Boundary Value Analysis (BVA) | 5 | 5 | 0 | 100% |
| 6 | State Transition Testing (STT) | 2 | 2 | 0 | 100% |
| **Total** | **Keseluruhan Skenario Uji** | **20** | **19** | **1** | **95%** |

### 2.2 Analisis Persentase Keberhasilan Fungsional

Kalkulasi persentase keberhasilan pengujian fungsionalitas dilakukan menggunakan rumus berikut[cite: 1]:

$$\text{Persentase Keberhasilan} = \left( \frac{\text{Jumlah Test Case Pass}}{\text{Jumlah Total Test Case}} \right) \times 100\%$$

$$\text{Persentase Keberhasilan} = \left( \frac{19}{20} \right) \times 100\% = 95\%$$

Berdasarkan total 20 skenario uji yang dieksekusi, sebanyak 19 skenario dinyatakan *Pass* dan satu skenario dinyatakan *Fail*[cite: 1]. Kegagalan terjadi pada pengujian validasi login dengan kredensial yang belum terdaftar[cite: 1]. Hasil pencapaian **95%** menunjukkan bahwa sistem secara fungsional telah memenuhi sebagian besar kebutuhan operasional yang dirancang[cite: 1].

---

## 3. Evaluasi Keandalan (Reliability)

Evaluasi keandalan menilai kemampuan sistem dalam mempertahankan tingkat kinerja tertentu saat digunakan dalam kondisi yang ditentukan[cite: 1]. Parameter keandalan diukur berdasarkan keberadaan cacat sistem (*bug*) yang belum terselesaikan[cite: 1].

### 3.1 Ringkasan Temuan Bug Berdasarkan Severity

| No | Bug ID | Deskripsi Masalah | Severity | Status |
| :---: | :---: | :--- | :---: | :---: |
| 1 | BUG-01 | Tidak ada umpan balik saat menginput angka negatif pada field nilai/pendapatan panen (Rp) | Medium | Open |
| 2 | BUG-02 | Kesalahan pembacaan tanda koma (`,`) pada field biaya operasional | High | Open |
| 3 | BUG-03 | Kesalahan pembacaan tanda koma (`,`) pada field nilai/pendapatan panen | High | Open |
| 4 | BUG-04 | Teks nominal angka pada kartu finansial meluap (*overflow*) di layar *mobile* | Low | Open |
| 5 | BUG-05 | Registrasi menerima input field nama dengan akhiran spasi dan titik (`.`) | Low | Open |

### 3.2 Analisis Dampak Keandalan

Selama proses pengujian, teridentifikasi lima *bug* yang seluruhnya masih berstatus *Open*[cite: 1]. Dua *bug* berkategori **High Severity** (BUG-02 dan BUG-03) berdampak langsung pada kegagalan pembacaan format numerik, sehingga menyebabkan kalkulasi pengeluaran dan pendapatan finansial menjadi tidak akurat[cite: 1]. 

Keberadaan dua *bug* prioritas tinggi ini menyebabkan sistem dinyatakan **belum reliable** untuk mengolah data finansial secara penuh di tingkat produksi[cite: 1].

---

## 4. Evaluasi Kebolehgunaan (Usability)

Evaluasi kebolehgunaan mengukur tingkat kemudahan, efisiensi, dan kepuasan pengguna saat mengoperasikan sistem[cite: 1]. Evaluasi ini didasarkan pada hasil *User Acceptance Testing* (UAT) bersama enam responden (satu Admin dan lima User/petani)[cite: 1].

1. **Kelancaran Skenario UAT:** Seluruh enam skenario pengujian UAT berhasil dijalankan tanpa adanya kegagalan sistem (*zero system crash*)[cite: 1].
2. **Penerimaan Pengguna:** Pengguna memberikan respons positif terhadap kesederhanaan antarmuka *mobile*[cite: 1]. Sebagian besar petani dapat mengoperasikan fitur pencatatan secara mandiri setelah melalui sesi sosialisasi singkat[cite: 1].
3. **Catatan Adaptasi:** Terdapat satu pengguna yang membutuhkan waktu penyesuaian lebih lanjut karena keterbatasan literasi digital awal[cite: 1]. Secara umum, sistem tergolong mudah dipahami dan dapat diterima oleh pengguna sasaran[cite: 1].

---

## 5. Kesiapan Implementasi (Implementation Readiness)

Menimbang hasil evaluasi dari ketiga aspek ISO/IEC 25010[cite: 1]:
* **Fungsionalitas:** Sangat Baik (Tingkat keberhasilan 95%)[cite: 1].
* **Kebolehgunaan:** Baik (Dapat diterima oleh pengguna akhir)[cite: 1].
* **Keandalan:** Kurang (Terdapat dua *bug* *High Severity* yang merusak kalkulasi finansial)[cite: 1].

**Keputusan Akhir Kesiapan:**  
Sistem Informasi Pengelolaan Lahan Pertanian Optimus Farm dinyatakan **BELUM SIAP untuk diimplementasikan secara penuh di lingkungan produksi**[cite: 1]. Sistem wajib melalui tahap perbaikan (*bug fixing*) pada BUG-02 dan BUG-03 serta verifikasi pengujian ulang sebelum digunakan dalam kegiatan operasional Kelompok Tani Optimus Farm secara nyata[cite: 1].

---

## 6. Analisis Kelebihan dan Kekurangan Sistem

### 6.1 Kelebihan Sistem
* Memenuhi 95% kriteria fungsionalitas yang dirancang pada dokumen SRS[cite: 1].
* Fitur-fitur utama (autentikasi, *console* admin, dan pencatatan lahan/panen) berjalan stabil dengan tingkat kelulusan 100%[cite: 1].
* Antarmuka responsif dan sederhana, sehingga memudahkan adaptasi bagi pengguna dengan literasi digital terbatas[cite: 1].
* Alur pencatatan dan validasi data telah selaras dengan skenario penggunaan di lapangan[cite: 1].

### 6.2 Kekurangan Sistem
* Terjadi kesalahan penafsiran format tanda koma (`,`) pada bidang input finansial yang merusak data laba/rugi[cite: 1].
* Belum menyediakan pesan peringatan (*error feedback*) saat pengguna menginput nominal angka negatif[cite: 1].
* Tampilan teks nominal angka pada kartu statistik finansial meluap (*overflow*) saat diakses melalui perangkat *mobile*[cite: 1].
* Belum memiliki sanitasi input (*string trimming*) untuk mencegah masuknya karakter spasi atau titik berlebih pada field nama[cite: 1].
* Membutuhkan sesi pendampingan awal bagi pengguna yang belum terbiasa dengan aplikasi digital[cite: 1].

---

**Akhir Dokumen**