# 🌾 Optimus Farm - Web-Based Farm Management System & QA Portfolio

Sistem Informasi Pengelolaan Lahan Pertanian berbasis web yang dirancang untuk mendigitalisasi pencatatan operasional, pemantauan riwayat blok lahan, dan rekapitulasi hasil panen pada Kelompok Tani Optimus Farm, Pangalengan.

Proyek ini berfokus pada **Pengujian dan Implementasi Perangkat Lunak**, mencakup siklus penjaminan kualitas (*Software Quality Assurance*) mulai dari penyusunan *Test Plan*, eksekusi *Black-Box Testing*, manajemen *Bug Report*, hingga *User Acceptance Testing* (UAT).

---

## 📌 Latar Belakang & Permasalahan

Pencatatan operasional pada Kelompok Tani Optimus Farm sebelumnya dilakukan secara manual menggunakan buku fisik. Metode ini memicu sejumlah kendala operasional:
- Risiko kerusakan fisik atau kehilangan dokumen di area pertanian.
- Catatan pengeluaran (bibit, pupuk, upah harian) dan hasil panen yang tidak terstruktur.
- Kesulitan pengurus dalam merekapitulasi performa finansial dan melacak riwayat produktivitas lahan dari musim ke musim.

Sistem ini dikembangkan untuk memusatkan seluruh data operasional ke dalam satu basis data terintegrasi guna mendukung pengambilan keputusan berbasis data (*evidence-based planning*).

---

## 🛠️ Teknologi & Arsitektur

- **Frontend:** React.js
- **Backend:** Laravel (RESTful API)
- **Database:** MySQL
- **QA & Testing Tools:** 
  - Spreadsheet (Test Plan, Test Case, & UAT Tracking)
  - Postman (API Testing & Verification)
  - Issue Tracker / Defect Log (Bug Reporting)

---

## 🎯 Ruang Lingkup Sistem

### Fitur Utama (In-Scope)
- **Manajemen Profil Lahan:** Pendataan blok/petak lahan pertanian beserta kapasitas luasnya.
- **Jadwal Penanaman & Aktivitas:** Pencatatan jadwal tanam, penggunaan pupuk, serta pemantauan biaya harian per blok.
- **Pendataan Hasil Panen:** Rekapitulasi volume panen dan riwayat historis produksi per blok lahan.

### Batasan Sistem (Out-of-Scope)
- Transaksi penjualan / e-commerce hasil panen ke konsumen akhir.
- Manajemen stok gudang (*inventory warehouse*).
- Integrasi sensor otomatis atau perangkat keras Internet of Things (IoT).

---

## 🧪 Strategi Pengujian Perangkat Lunak (QA Strategy)

Pengujian dilakukan secara sistematis untuk memastikan keandalan fungsionalitas dan kesesuaian sistem dengan kebutuhan pengguna akhir.

### 1. Metodologi Pengujian
- **Black-Box Testing:** Pengujian fungsionalitas antarmuka dan alur kerja aplikasi berbasis skenario penggunaan (*use case scenario*) tanpa mengakses kode internal.
- **User Acceptance Testing (UAT):** Pengujian validasi bersama pengurus dan anggota Kelompok Tani Optimus Farm di Pangalengan.
- *(Catatan: Pengujian tidak mencakup penetration testing maupun load/stress testing skala besar).*

### 2. Artefak Pengujian (Testing Deliverables)
- **Test Plan:** Perencanaan cakupan pengujian, kriteria keberhasilan (*entry/exit criteria*), dan alokasi sumber daya.
- **Test Cases:** Skenario pengujian terstruktur untuk modul Lahan, Penanaman, dan Hasil Panen.
- **Bug Report & Defect Log:** Pendokumentasian temuan *bug*, analisis keparahan (*severity*), dan status resolusi.
- **Test & UAT Report:** Dokumen evaluasi kelayakan sistem sebelum tahap implementasi final.
