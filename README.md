# aplikasi_klik_gigi_fixx
# ⚙️ Database Trigger Documentation - Klinik Gigi

Dokumentasi ini berisi daftar trigger yang digunakan dalam **Sistem Informasi Pelayanan Klinik Gigi** untuk menjaga konsistensi data dan otomatisasi pencatatan waktu (timestamp).

---

## 👥 Tim Pengembang
* **Muhammad Carel Azzami** – Programmer (Back-end & Front-end Developer)
* **Akilah Isnaini** – UI/UX Designer (Interface & User Experience)
* **Talita Azaria** – Database Administrator (Data Architecture & Management)

---
## ERD
<img width="1193" height="683" alt="erd" src="https://github.com/user-attachments/assets/6ca74f9c-1ea1-4cfa-b740-26ed7c8e4c12" />

## 📅 1. Auto Isi Tanggal Daftar

**Problem:**
Sering terjadi kelalaian di mana Staff lupa menginputkan `tanggal_daftar` saat mendaftarkan pasien ke sistem, yang mengakibatkan data laporan menjadi tidak akurat.

**Solusi & Logika:**
Sistem menggunakan trigger **AFTER INSERT** pada tabel pendaftaran. Setiap kali ada data jadwal baru yang masuk, trigger akan secara otomatis mendeteksi baris tersebut dan mengisi kolom `tanggal_daftar` dengan waktu sistem saat itu juga (*real-time*).

---

## 💳 2. Auto Isi Tanggal Pembayaran & Ambil

**Problem:**
Apoteker sering terfokus pada pelayanan fisik obat sehingga lupa melakukan input manual tanggal pengambilan obat atau tanggal pelunasan pembayaran di sistem.

**Solusi & Logika:**
Sistem menggunakan trigger **AFTER INSERT** pada tabel pembayaran obat. Begitu Apoteker melayani transaksi melalui sistem, trigger akan otomatis memperbarui kolom `tanggal_bayar` menggunakan waktu saat transaksi dilakukan. Hal ini memastikan validitas data keuangan dan operasional klinik.

---

## ⚠️ Catatan Penting

* **Integritas Data:** Trigger ini menjamin bahwa setiap transaksi memiliki stempel waktu (timestamp) yang sah tanpa bergantung pada input manual manusia.
* **Otomatisasi:** Mengurangi beban kerja administratif bagi Staff dan Apoteker sehingga mereka bisa lebih fokus pada pelayanan pasien.
* **Keamanan:** Data waktu yang diambil langsung dari server database sehingga tidak bisa dimanipulasi melalui pengaturan jam di komputer lokal (client).

---

## 📌 Ringkasan Fungsi Trigger

| No | Nama Trigger | Role Terkait | Fungsi Utama |
| :-- | :--- | :--- | :--- |
| 1 | Pendaftaran_AutoDate | Staff | Otomatisasi tanggal registrasi pasien |
| 2 | Pembayaran_AutoDate | Apoteker | Otomatisasi tanggal ambil obat & bayar |

---
