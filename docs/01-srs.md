# Software Requirements Specification (SRS)
## Sistem Informasi Pengelolaan Lahan Pertanian — Optimus Farm

**Dokumen:** Software Requirements Specification  
**Sistem:** Sistem Informasi Pengelolaan Lahan Pertanian  
**Organisasi:** Kelompok Tani Optimus Farm, Pangalengan  
**Versi:** 1.0  
**Status:** Draft SRS  
**Tanggal:** 6 September 2026

---

## 1. Pendahuluan

### 1.1 Tujuan Dokumen

Dokumen Software Requirements Specification (SRS) ini mendefinisikan kebutuhan perangkat lunak untuk Sistem Informasi Pengelolaan Lahan Pertanian pada Kelompok Tani Optimus Farm di wilayah Pangalengan.

Dokumen ini menjadi acuan bagi proses analisis, perancangan, implementasi, pengujian, dan pengembangan sistem. Kebutuhan yang tercantum di dalamnya digunakan sebagai dasar untuk memastikan bahwa sistem yang dibangun sesuai dengan proses operasional dan kebutuhan pengguna.

### 1.2 Ruang Lingkup Sistem

Sistem dikembangkan untuk mendigitalisasi pencatatan dan pengelolaan operasional lahan pertanian yang sebelumnya dilakukan secara manual menggunakan buku fisik.

Ruang lingkup sistem meliputi:

- Pengelolaan data anggota kelompok tani.
- Pengelolaan profil lahan atau blok.
- Pencatatan aktivitas harian penanaman.
- Pencatatan hasil panen berdasarkan blok lahan.
- Validasi laporan aktivitas oleh Admin.
- Penyajian dashboard kondisi lahan dan ringkasan operasional.
- Rekapitulasi biaya hasil panen.
- Perhitungan dan penyajian performa finansial berupa untung atau rugi.
- Notifikasi setelah data aktivitas atau panen berhasil disimpan.

Sistem tidak menggantikan proses operasional lapangan, tetapi berfungsi sebagai media pencatatan, validasi, penyimpanan, rekapitulasi, dan penyajian informasi.

### 1.3 Deskripsi Umum Sistem

Sistem Informasi Pengelolaan Lahan Pertanian merupakan aplikasi berbasis web yang menyediakan pencatatan operasional lahan secara terpusat dalam satu basis data. Setiap aktivitas yang dicatat dari lapangan dapat dikaitkan dengan blok lahan yang dikelola sehingga riwayat aktivitas, hasil panen, biaya, dan performa finansial dapat ditelusuri berdasarkan periode maupun blok.

Sistem menggunakan arsitektur monolith dengan pendekatan Single Page Application (SPA) melalui Inertia.js. Komponen utama sistem terdiri atas:

| Komponen | Teknologi | Fungsi |
|---|---|---|
| Frontend | React | Menyediakan antarmuka interaktif dan responsif |
| Backend | Laravel | Menangani routing, autentikasi, otorisasi, validasi, logika bisnis, dan perhitungan |
| Database | MySQL | Menyimpan data sistem secara terpusat |
| Database Produksi | Aiven | Mendukung penyimpanan database pada lingkungan produksi |

Sistem memiliki dua kelompok hak akses, yaitu Admin dan User. Admin terdiri atas Sekretaris dan Bendahara, sedangkan User terdiri atas Ketua dan Anggota.

### 1.4 Sasaran Pengguna

Sistem ditujukan untuk:

- **Admin (Sekretaris dan Bendahara):** mengelola data master, memvalidasi laporan, serta memantau laporan biaya dan performa finansial.
- **User (Ketua dan Anggota):** mencatat aktivitas pertanian dan hasil panen pada blok yang dikelolanya serta melihat informasi yang tersedia sesuai hak akses.

---

## 2. Aktor dan Hak Akses

| Aktor | Peran dan Tanggung Jawab |
|---|---|
| Admin (Sekretaris, Bendahara) | Mengelola data anggota dan profil lahan/blok, memvalidasi laporan aktivitas harian, serta mengakses laporan biaya dan performa finansial. |
| User (Ketua, Anggota) | Menginput aktivitas harian penanaman dan hasil panen pada blok yang dikelolanya serta melihat dashboard dan laporan hasil panen sesuai hak akses. |

### 2.1 Matriks Hak Akses

| Fitur | Admin | User |
|---|:---:|:---:|
| Login | ✓ | ✓ |
| Kelola anggota | ✓ | - |
| Kelola profil lahan/blok | ✓ | - |
| Input aktivitas harian | - | ✓ |
| Validasi aktivitas harian | ✓ | - |
| Input hasil panen | - | ✓ |
| Lihat dashboard | ✓ | ✓ |
| Lihat laporan hasil panen | ✓ | ✓ |
| Lihat rekapitulasi biaya | ✓ | ✓ |
| Lihat performa finansial | ✓ | ✓ |
| Notifikasi penyimpanan data | ✓ | ✓ |

---

## 3. Kebutuhan Fungsional

| ID | Kebutuhan Fungsional | Aktor |
|---|---|---|
| FR-01 | Sistem harus menyediakan autentikasi login berbasis peran untuk Admin dan User. | Admin, User |
| FR-02 | Sistem harus menyediakan fungsi CRUD untuk data anggota kelompok tani. | Admin |
| FR-03 | Sistem harus menyediakan fungsi CRUD untuk profil lahan/blok, termasuk kode blok dan komoditas. | Admin |
| FR-04 | Sistem harus memungkinkan User mencatat aktivitas harian penanaman pada blok yang dikelolanya. | User |
| FR-05 | Sistem harus memungkinkan Admin memeriksa dan memvalidasi atau menolak laporan aktivitas harian yang dikirim User. | Admin |
| FR-06 | Sistem harus memungkinkan User mencatat hasil panen berdasarkan blok lahan yang dikelolanya. | User |
| FR-07 | Sistem harus menghasilkan laporan rekapitulasi biaya yang berkaitan dengan hasil panen. | Admin, User |
| FR-08 | Sistem harus menghasilkan laporan performa finansial berdasarkan biaya modal penanaman dan hasil panen. | Admin, User |
| FR-09 | Sistem harus menampilkan dashboard ringkasan yang mencakup status lahan, biaya, dan estimasi hasil. | Admin, User |
| FR-10 | Sistem harus menampilkan notifikasi ketika laporan aktivitas harian atau hasil panen berhasil disimpan. | Sistem |

---

## 4. Kebutuhan Non-Fungsional

| ID | Kategori | Kebutuhan |
|---|---|---|
| NFR-01 | Security | Sistem harus menerapkan autentikasi dan otorisasi berbasis peran. Password harus disimpan menggunakan mekanisme hashing yang aman dan tidak dalam bentuk plaintext. |
| NFR-02 | Usability | Antarmuka harus sederhana, konsisten, dan mudah digunakan oleh pengguna dengan tingkat literasi digital yang beragam. Label, instruksi, validasi, dan alur input harus jelas. |
| NFR-03 | Performance | Waktu respons untuk operasi input dan tampilan laporan harus berada pada rentang maksimal 2–3 detik pada kondisi jaringan normal dan beban penggunaan yang ditetapkan. |
| NFR-04 | Reliability | Sistem harus menjaga konsistensi data dan mencegah kehilangan data ketika terjadi kegagalan validasi, proses penyimpanan, atau gangguan koneksi. |
| NFR-05 | Portability | Sistem harus dapat digunakan melalui browser desktop maupun perangkat mobile dengan desain responsif. |
| NFR-06 | Maintainability | Backend Laravel dan frontend React harus mengikuti struktur dan konvensi framework yang digunakan serta menerapkan pemisahan tanggung jawab kode yang jelas agar mudah dipelihara dan dikembangkan. |

---

## 5. Use Case

### 5.1 Daftar Use Case

| ID | Use Case | Aktor |
|---|---|---|
| UC-01 | Login | Admin, User |
| UC-02 | Input Data Pertanian | User |
| UC-03 | Mengelola Data Kelompok Tani | Admin |
| UC-04 | Melihat Dashboard dan Laporan | Admin, User |

### 5.2 UC-01 — Login

| Item | Spesifikasi |
|---|---|
| Aktor | Admin, User |
| Tujuan | Melakukan autentikasi dan memperoleh akses ke sistem sesuai peran pengguna. |
| Prasyarat | Akun pengguna telah terdaftar dan aktif. |
| Pemicu | Pengguna membuka halaman login. |
| Alur Utama | 1. Pengguna membuka halaman login. 2. Pengguna memasukkan username/email dan password. 3. Sistem memvalidasi kredensial. 4. Sistem menentukan peran pengguna. 5. Sistem mengarahkan pengguna ke halaman yang sesuai dengan hak aksesnya. |
| Alur Alternatif | Jika kredensial tidak valid, sistem menampilkan pesan kesalahan dan pengguna dapat melakukan percobaan login kembali. |
| Kondisi Akhir | Pengguna berhasil terautentikasi dan memperoleh akses sesuai hak aksesnya. |

### 5.3 UC-02 — Input Data Pertanian

| Item | Spesifikasi |
|---|---|
| Aktor | User |
| Tujuan | Mencatat aktivitas pertanian dan hasil panen pada blok yang dikelola. |
| Prasyarat | User telah login dan blok lahan yang bersangkutan telah terdaftar oleh Admin. |
| Pemicu | User memilih menu input data pertanian. |
| Alur Utama | 1. User memilih blok lahan. 2. User memilih jenis data yang akan dicatat. 3. User mengisi tanggal dan detail aktivitas atau hasil panen. 4. Sistem melakukan validasi data. 5. Sistem menyimpan data. 6. Sistem menampilkan notifikasi bahwa data berhasil disimpan. |
| Alur Alternatif | Jika data tidak lengkap atau tidak valid, sistem menampilkan pesan validasi dan meminta User memperbaiki data sebelum disimpan. |
| Kondisi Akhir | Data pertanian tersimpan dalam database dan laporan aktivitas berada dalam status yang sesuai untuk proses validasi Admin. |

### 5.4 UC-03 — Mengelola Data Kelompok Tani

| Item | Spesifikasi |
|---|---|
| Aktor | Admin |
| Tujuan | Mengelola data master dan melakukan validasi laporan yang dikirim User. |
| Prasyarat | Admin telah login. |
| Pemicu | Admin membuka menu pengelolaan data atau validasi laporan. |
| Alur Utama | 1. Admin membuka data anggota, profil lahan/blok, atau daftar laporan. 2. Admin menambah, melihat, mengubah, atau menghapus data master sesuai kebutuhan. 3. Untuk laporan masuk, Admin memeriksa kelengkapan dan kesesuaian data. 4. Admin memilih validasi atau penolakan laporan. 5. Sistem memperbarui status data. |
| Alur Alternatif | Jika laporan tidak sesuai atau tidak lengkap, Admin menolak laporan dan sistem mencatat status penolakan. |
| Kondisi Akhir | Data master diperbarui atau laporan memiliki status tervalidasi/ditolak. |

### 5.5 UC-04 — Melihat Dashboard dan Laporan

| Item | Spesifikasi |
|---|---|
| Aktor | Admin, User |
| Tujuan | Menampilkan kondisi lahan, biaya, hasil panen, dan performa finansial. |
| Prasyarat | Pengguna telah login dan data yang diperlukan tersedia dalam sistem. |
| Pemicu | Pengguna membuka dashboard atau menu laporan. |
| Alur Utama | 1. Pengguna membuka dashboard atau laporan. 2. Pengguna memilih periode atau blok lahan jika tersedia. 3. Sistem mengambil data yang relevan. 4. Sistem menghitung atau merekap biaya dan hasil panen. 5. Sistem menampilkan ringkasan dan performa finansial. |
| Alur Alternatif | Jika data pada periode atau blok yang dipilih belum tersedia, sistem menampilkan informasi bahwa tidak terdapat data yang dapat ditampilkan. |
| Kondisi Akhir | Pengguna memperoleh informasi kondisi lahan dan performa finansial sebagai bahan evaluasi dan pengambilan keputusan. |

---

## 6. Aturan Bisnis

| ID | Aturan |
|---|---|
| BR-01 | Setiap pengguna harus memiliki akun dan peran yang terdaftar sebelum dapat mengakses sistem. |
| BR-02 | User hanya dapat mencatat data pertanian pada blok yang menjadi kewenangannya. |
| BR-03 | Data aktivitas harian yang dikirim User harus melalui proses validasi Admin sebelum digunakan sebagai data tervalidasi dalam laporan. |
| BR-04 | Laporan yang ditolak tidak boleh diperlakukan sebagai data tervalidasi sampai dilakukan perbaikan dan pengajuan kembali sesuai mekanisme sistem. |
| BR-05 | Profil lahan/blok harus tersedia terlebih dahulu sebelum aktivitas atau hasil panen dapat dicatat pada blok tersebut. |
| BR-06 | Perhitungan performa finansial menggunakan biaya modal penanaman dan nilai hasil panen yang tersedia pada periode terkait. |
| BR-07 | Data yang ditampilkan pada laporan harus mengikuti status validasi yang ditetapkan sistem. |

---

## 7. Data dan Informasi yang Dikelola

Sistem sekurang-kurangnya mengelola kelompok data berikut:

| Kelompok Data | Informasi Utama |
|---|---|
| Pengguna | Identitas akun, kredensial, dan peran |
| Anggota | Identitas dan informasi keanggotaan kelompok tani |
| Lahan/Blok | Kode blok, luas lahan, komoditas, dan informasi terkait |
| Aktivitas Pertanian | Tanggal, blok, jenis aktivitas, jumlah/luas, dan keterangan |
| Hasil Panen | Tanggal panen, blok, jumlah hasil, dan informasi pendukung |
| Biaya | Komponen biaya/modal penanaman dan nilai terkait |
| Validasi | Status laporan, waktu validasi, dan informasi pendukung |
| Laporan | Rekapitulasi aktivitas, biaya, hasil panen, dan performa finansial |

---

## 8. Persyaratan Antarmuka

### 8.1 Antarmuka Pengguna

Antarmuka harus:

- Menggunakan bahasa dan istilah yang mudah dipahami pengguna.
- Menampilkan navigasi berdasarkan hak akses pengguna.
- Menyediakan form input dengan label yang jelas.
- Menampilkan validasi kesalahan secara langsung dan mudah dipahami.
- Menampilkan notifikasi setelah proses penyimpanan berhasil atau gagal.
- Menggunakan desain responsif untuk desktop dan mobile.
- Menyediakan tabel atau komponen visual yang memungkinkan data laporan dibaca dengan mudah.

### 8.2 Antarmuka Perangkat Lunak

Sistem harus menyediakan integrasi internal antara:

- React sebagai lapisan antarmuka.
- Inertia.js sebagai penghubung frontend dan backend.
- Laravel sebagai lapisan aplikasi dan logika bisnis.
- MySQL sebagai basis data utama.
- Aiven sebagai layanan database pada lingkungan produksi apabila digunakan dalam deployment.

---

## 9. Persyaratan Keamanan

Sistem harus memenuhi persyaratan keamanan berikut:

1. Setiap akses ke fitur yang membutuhkan autentikasi harus dilakukan oleh pengguna yang telah login.
2. Hak akses harus diverifikasi berdasarkan peran pengguna.
3. Password tidak boleh disimpan dalam bentuk plaintext.
4. Input pengguna harus divalidasi sebelum diproses dan disimpan.
5. Akses terhadap data harus dibatasi berdasarkan kewenangan pengguna.
6. Operasi yang mengubah data penting harus diproses melalui mekanisme validasi backend.
7. Sistem harus menggunakan mekanisme sesi atau autentikasi yang sesuai dengan standar keamanan Laravel.
8. Informasi sensitif tidak boleh ditampilkan kepada pengguna yang tidak memiliki hak akses.

---

## 10. Persyaratan Kinerja dan Keandalan

Sistem harus memenuhi kondisi berikut:

- Operasi input data dan pemuatan laporan ditargetkan memiliki waktu respons maksimal 2–3 detik pada kondisi jaringan normal.
- Transaksi penyimpanan data harus memastikan data tidak berada pada kondisi setengah tersimpan ketika terjadi kegagalan proses.
- Validasi data harus dilakukan pada sisi backend meskipun validasi juga tersedia pada frontend.
- Data yang telah berhasil disimpan harus tetap tersedia setelah pengguna melakukan refresh atau login kembali.
- Sistem harus meminimalkan duplikasi data melalui validasi dan aturan integritas basis data.

---

## 11. Persyaratan Deployment

Lingkungan deployment sistem terdiri atas:

| Lingkungan | Komponen |
|---|---|
| Development | Laravel, React, Inertia.js, MySQL |
| Production | Laravel, React, Inertia.js, MySQL/Aiven |
| Client | Browser desktop atau mobile |

Konfigurasi lingkungan produksi harus memisahkan kredensial dan konfigurasi sensitif dari source code aplikasi.

---

## 12. Kriteria Penerimaan Sistem

Sistem dapat dinyatakan memenuhi kebutuhan apabila sekurang-kurangnya:

1. Admin dan User dapat login menggunakan akun yang valid.
2. Sistem membatasi fitur berdasarkan peran pengguna.
3. Admin dapat melakukan CRUD data anggota dan profil lahan/blok.
4. User dapat mencatat aktivitas pertanian pada blok yang menjadi kewenangannya.
5. User dapat mencatat hasil panen.
6. Admin dapat memeriksa, memvalidasi, atau menolak laporan User.
7. Data yang telah disimpan tetap tersedia setelah halaman dimuat ulang.
8. Dashboard dapat menampilkan ringkasan data lahan, biaya, dan hasil.
9. Sistem dapat menghasilkan rekapitulasi biaya dan performa finansial berdasarkan data yang tersedia.
10. Sistem memberikan notifikasi atas keberhasilan atau kegagalan proses penyimpanan.
11. Sistem dapat digunakan pada perangkat desktop dan mobile.
12. Sistem memenuhi target waktu respons 2–3 detik pada kondisi pengujian yang ditetapkan.

---

## 13. Traceability Kebutuhan

| Kebutuhan | Use Case | Kriteria Penerimaan |
|---|---|---|
| FR-01 | UC-01 | CA-01 |
| FR-02 | UC-03 | CA-02 |
| FR-03 | UC-03 | CA-03 |
| FR-04 | UC-02 | CA-04 |
| FR-05 | UC-03 | CA-05 |
| FR-06 | UC-02 | CA-06 |
| FR-07 | UC-04 | CA-07 |
| FR-08 | UC-04 | CA-08 |
| FR-09 | UC-04 | CA-09 |
| FR-10 | UC-02 | CA-10 |

---

## 14. Catatan Pengembangan

Dokumen ini merupakan spesifikasi kebutuhan perangkat lunak dan tidak dimaksudkan untuk mengunci detail implementasi yang belum ditentukan. Detail seperti struktur tabel database, ERD, API, desain UI, algoritma perhitungan biaya, mekanisme backup, serta konfigurasi deployment dapat didefinisikan pada dokumen teknis atau artefak perancangan terpisah.

Apabila terdapat perubahan proses bisnis, perubahan kebutuhan pengguna, atau penambahan fitur, perubahan harus dicatat pada versi SRS berikutnya agar kebutuhan sistem tetap dapat ditelusuri terhadap desain, implementasi, dan pengujian.

---

**Akhir Dokumen**
