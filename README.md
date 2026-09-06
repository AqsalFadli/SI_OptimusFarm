#  Optimus Farm — Web-Based Farm Management System

![PHP](https://img.shields.io/badge/PHP-8.2+-777BB4?style=flat-square&logo=php&logoColor=white)
![Laravel](https://img.shields.io/badge/Laravel-11.x-FF2D20?style=flat-square&logo=laravel&logoColor=white)
![React](https://img.shields.io/badge/React-18.x-61DAFB?style=flat-square&logo=react&logoColor=black)
![MySQL](https://img.shields.io/badge/MySQL-8.x-4479A1?style=flat-square&logo=mysql&logoColor=white)
![QA Pass Rate](https://img.shields.io/badge/QA%20Pass%20Rate-95%25-brightgreen?style=flat-square)

Sistem Informasi Pengelolaan Lahan Pertanian berbasis web yang dirancang untuk mendigitalisasi pencatatan operasional harian, pengelolaan riwayat blok lahan, serta rekapitulasi hasil panen dan performa finansial pada Kelompok Tani Optimus Farm, Pangalengan.

Repositori ini difokuskan sebagai **Portofolio Pengujian dan Implementasi Perangkat Lunak (Software Quality Assurance & System Analysis)**, mencakup siklus analisis kebutuhan (*SRS*), perancangan strategi uji (*Test Plan*), eksekusi pengujian (*Black-Box Testing*), manajemen temuan cacat (*Defect Log & Root Cause Analysis*), hingga evaluasi penerimaan pengguna (*User Acceptance Testing*).

---

## 📑 Dokumentasi QA & Analisis Sistem

Seluruh artefak pengujian dan analisis sistem tersusun secara terstruktur di dalam direktori [`docs/`](./docs/):

| Dokumen | Deskripsi Isi | Link Berkas |
| :--- | :--- | :---: |
| **01. Software Requirement Specification** | Deskripsi sistem, pemetaan aktor, matriks hak akses, kebutuhan fungsional (FR-01 s.d FR-10), non-fungsional, dan use case. | [`docs/01-srs.md`](./docs/01-srs.md) |
| **02. Test Plan** | Perencanaan pengujian, strategi pengujian, lingkungan uji, dan analisis risiko pengujian. | [`docs/02-test-plan.md`](./docs/02-test-plan.md) |
| **03. Test Cases** | Skenario pengujian rinci berbasis *Use Case Scenario*, *Boundary Value Analysis* (BVA), dan *State Transition Testing* (STT). | [`docs/03-test-cases.md`](./docs/03-test-cases.md) |
| **04. Bug & Test Report** | Rekapitulasi hasil eksekusi pengujian, persentase keberhasilan (*pass rate*), *Defect Log*, dan *Root Cause Analysis*. | [`docs/04-bug-and-test-reports.md`](./docs/04-bug-and-test-reports.md) |
| **05. UAT Report** | Hasil pengujian penerimaan pengguna (*User Acceptance Testing*) bersama 5 petani/pengurus di Pangalengan. | [`docs/05-uat-reports.md`](./docs/05-uat-reports.md) |
| **06. System Quality Evaluation** | Evaluasi kualitatif dan kuantitatif aspek *Functionality*, *Reliability*, *Usability* (ISO/IEC 25010), serta analisis kesiapan implementasi. | [`docs/06-system-evaluation.md`](./docs/06-system-evaluation.md) |

---

## 🛠️ Arsitektur & Teknologi

Aplikasi dibangun menggunakan arsitektur *Monolith* dengan pendekatan *Single Page Application* (SPA) memanfaatkan Inertia.js untuk menghubungkan backend dan frontend tanpa perlu membangun REST API secara terpisah.

* **Frontend:** React.js, Inertia.js, Tailwind CSS
* **Backend:** Laravel 11.x (PHP 8.2+)
* **Database:** MySQL (Lokal: DBngin/XAMPP, Produksi: Managed MySQL Aiven)
* **Testing & QA Tools:**
  * Black-Box Testing (Use Case Scenario, BVA, STT)
  * User Acceptance Testing (UAT)
  * Chrome DevTools & Postman
* **Deployment:** Vercel (Frontend/Web Application), Aiven (Cloud Database)

---

## 🎯 Ruang Lingkup Sistem

### Fitur Utama (In-Scope)
* **Autentikasi & Otorisasi:** Akses berbasis peran (*Role-Based Access Control*) untuk Admin (Sekretaris/Bendahara) dan User (Ketua/Anggota).
* **Manajemen Master Data:** Pengelolaan data anggota kelompok tani dan profil/blok lahan pertanian.
* **Pencatatan Lapangan (Petani):** Input laporan aktivitas harian (biaya operasional) dan pencatatan hasil panen per blok lahan.
* **Console Admin & Validasi:** Pemeriksaan, persetujuan (*Terima*), atau penolakan (*Tolak*) terhadap laporan yang dikirim petani secara real-time.
* **Pelaporan & Finansial:** Dashboard statistik operasional, rekapitulasi laba/rugi, dan ekspor laporan ke format PDF.

### Batasan Sistem (Out-of-Scope)
* Transaksi e-commerce / penjualan hasil panen langsung ke konsumen akhir.
* Manajemen stok gudang (*warehouse inventory*).
* Integrasi perangkat keras atau sensor otomatis (*Internet of Things*).

---

## 🧪 Ringkasan Hasil Pengujian (QA Highlights)

### 1. Metrik Keberhasilan Eksekusi (Pass Rate)
Dari **20 skenario uji** yang dieksekusi menggunakan teknik *Black-Box Testing*, sistem mencatatkan persentase keberhasilan sebesar **95%**.

$$\text{Pass Rate} = \left( \frac{19 \text{ Pass}}{20 \text{ Skenario}} \right) \times 100\% = 95\%$$

### 2. Temuan Cacat Sistem (Defect Summary)
Teridentifikasi **5 bug** selama pengujian dengan rincian status saat ini:

* **High Severity (2 Bug):** Kesalahan penafsiran tanda koma (`,`) pada bidang input nominal biaya operasional dan pendapatan panen yang menyusutkan nilai angka pada basis data.
* **Medium Severity (1 Bug):** Kurangnya pesan peringatan (*warning feedback*) pada frontend saat pengguna memasukkan angka negatif.
* **Low Severity (2 Bug):** Teks nominal meluap (*overflow*) pada kartu statistik di layar ponsel dan belum adanya sanitasi karakter spasi/titik pada field registrasi nama.

### 3. Hasil User Acceptance Testing (UAT)
Pengujian bersama 5 responden di Pangalengan menunjukkan **100% tingkat keberhasilan eksekusi skenario UAT**. Responden memberikan respons positif terhadap kesederhanaan antarmuka *mobile* dan kejelasan alur pencatatan harian.

---