# Laporan Pengujian Penerimaan Pengguna (User Acceptance Testing Report)
## Sistem Informasi Pengelolaan Lahan Pertanian — Optimus Farm

**Dokumen:** User Acceptance Testing (UAT) Report  
**Sistem:** Sistem Informasi Pengelolaan Lahan Pertanian  
**Organisasi:** Kelompok Tani Optimus Farm, Pangalengan  
**Versi:** 1.0  
**Status:** Final Draft  
**Tanggal:** 6 September 2026  

---

## 1. Pendahuluan

### 1.1 Tujuan UAT
Dokumen User Acceptance Testing (UAT) ini mendokumentasikan pelaksanaan dan hasil pengujian penerimaan pengguna akhir terhadap Sistem Informasi Pengelolaan Lahan Pertanian Optimus Farm. Pengujian ini bertujuan untuk memastikan bahwa sistem dapat beroperasi secara optimal dalam mendukung kegiatan operasional sehari-hari pengurus dan anggota kelompok tani di lapangan.

Secara spesifik, pengujian UAT dirancang untuk:
1. Memvalidasi bahwa fitur-fitur fungsional yang telah lolos *black-box testing* dapat dijalankan dengan lancar oleh pengguna nyata tanpa pendampingan teknis langsung dari tim pengembang.
2. Menilai kemudahan antarmuka sistem (*usability*) saat diakses oleh pengguna dengan tingkat literasi digital terbatas, sesuai dengan pemenuhan kebutuhan non-fungsional NFR-02.
3. Memastikan kesesuaian hasil kalkulasi biaya operasional dan performa finansial yang disajikan sistem dengan estimasi atau catatan manual pengguna.
4. Mengidentifikasi kendala penggunaan di lingkungan nyata (seperti stabilitas koneksi internet di area pertanian atau kebiasaan pengisian data anggota).

---

## 2. Demografi Responden

Pengujian UAT melibatkan 5 responden dari Kelompok Tani Optimus Farm di wilayah Pangalengan, terdiri atas 1 perwakilan Admin dan 4 perwakilan User. Responden User merupakan petani aktif yang mengelola komoditas utama khas kawasan Pangalengan, yaitu kentang, labu siam, cabai, dan kol.

### 2.1 Daftar Responden Pengujian

| No | Nama / Inisial | Peran Sistem | Komoditas / Deskripsi | Fitur Utama yang Diuji |
| :---: | :--- | :---: | :--- | :--- |
| 1 | Peneliti | Admin | Petani Aktif / Pengurus | Validasi Laporan dan Kelola Data Master |
| 2 | Aditya Ramadhan | User | Petani Aktif (Kentang) | Input Aktivitas Harian dan Hasil Panen |
| 3 | Danis Yudistira | User | Petani Aktif (Labu Siam) | Input Aktivitas Harian dan Hasil Panen |
| 4 | Aryani Agustina | User | Petani Aktif (Cabai) | Input Aktivitas Harian dan Hasil Panen |
| 5 | Bayu Rifaldi A | User | Petani Aktif (Kol) | Input Aktivitas Harian dan Hasil Panen |

*Catatan Penetapan Peran:* Pada tahap awal uji coba, sebagian anggota kelompok tani mengalami kesulitan dalam memahami alur pengelolaan data master pada tingkat admin. Oleh karena itu, peran Admin untuk sementara dipegang oleh peneliti (yang juga merupakan petani aktif di Pangalengan), sedangkan peran User sepenuhnya diisi oleh petani asli guna menjaga representasi penggunaan sistem di lapangan.

---

## 3. Pelaksanaan dan Skenario UAT

Mengingat tingkat pemahaman awal responden terhadap perangkat digital bervariasi, tim pengembang memberikan sesi sosialisasi dan simulasi singkat sebelum skenario formal dijalankan. Sesi ini mencakup penjelasan alur autentikasi, pengisian laporan aktivitas harian, serta pembacaan ringkasan *dashboard*.

### 3.1 Daftar Skenario Pengujian UAT

| ID Skenario | Deskripsi Skenario Pengujian | Aktor | Target Hasil |
| :---: | :--- | :---: | :---: |
| UAT-01 | Pengguna melakukan login ke sistem menggunakan akun masing-masing | User / Admin | Berhasil |
| UAT-02 | User mencatat dan mengirim laporan aktivitas harian pada blok lahannya | User | Berhasil |
| UAT-03 | User mencatat dan mengirim data hasil panen per blok lahan | User | Berhasil |
| UAT-04 | User mengakses *dashboard* dan membaca laporan performa finansial | User | Berhasil |
| UAT-05 | Admin memeriksa dan memvalidasi/menolak laporan masuk dari User | Admin | Berhasil |
| UAT-06 | Admin mengelola data master (anggota, profil lahan/blok, dan jadwal tanam) | Admin | Berhasil |

---

## 4. Hasil Pengujian dan Evaluasi Penerimaan

Berdasarkan pengujian yang dilakukan oleh 4 responden User dan 1 responden Admin, seluruh skenario pengujian berhasil dieksekusi tanpa ditemukannya *error* teknis seperti *server error*, kegagalan tombol, atau kegagalan penyimpanan data.

### 4.1 Rekapitulasi Hasil Eksekusi UAT

| ID Skenario | Skenario Pengujian | Hasil Eksekusi | Catatan Evaluasi Responden |
| :---: | :--- | :---: | :--- |
| UAT-01 | Pengguna melakukan login ke sistem | Berhasil | Alur masuk tergolong mudah dipahami. |
| UAT-02 | User menginput laporan aktivitas harian | Berhasil | Pengisian formulir berjalan lancar dan aman. |
| UAT-03 | User menginput data hasil panen | Berhasil | Proses pencatatan volume dan nilai panen sesuai. |
| UAT-04 | User melihat *dashboard* finansial | Berhasil | Informasi ringkasan mudah dibaca di layar HP. |
| UAT-05 | Admin memvalidasi laporan masuk | Berhasil | Proses persetujuan/penolakan data berjalan baik. |
| UAT-06 | Admin mengelola data master | Berhasil | Catatan aktivitas pada tabel master kurang terlihat menonjol. |

### 4.2 Umpan Balik Kualitatif Responden

Seluruh responden (100%) memberikan respons positif terhadap kesederhanaan alur dan keterbacaan antarmuka *mobile*. Beberapa umpan balik kualitatif yang dicatat meliputi:

> *"Aplikasi ini sangat simpel."*  
> — **Aditya Ramadhan**

> *"Sangat membantu buat para petani buat pencatatan hasil panen dan biaya operasional."*  
> — **Aryani Agustina**

### 4.3 Kesimpulan Penerimaan Pengguna

Hasil pengujian menunjukkan bahwa sesi sosialisasi awal secara signifikan berhasil memangkas hambatan adaptasi teknologi bagi petani dengan literasi digital terbatas. Kesederhanaan rancangan antarmuka dan kejelasan alur pencatatan menjadi faktor utama tinggi penerimaan pengguna (*acceptance rate*) terhadap sistem ini.

Secara umum, sistem dinyatakan **dapat diterima dengan baik oleh pengguna akhir** untuk mendukung pencatatan operasional Kelompok Tani Optimus Farm.

---

**Akhir Dokumen**