# TUGAS 8 - PERTEMUAN 10

```
Nama      : Daiva Paundra Gevano
NIM       : H1D023075
Shift     : A
Shift KRS : F
```

## Screenshot Aplikasi
<img height="400" alt="image" src="https://github.com/user-attachments/assets/7ac6dfd6-6c68-4b6f-8017-db4515d1f880" />
<img height="400" alt="image" src="https://github.com/user-attachments/assets/0abfcb75-e379-4893-b971-32f80e53784b" />
<img height="400" alt="image" src="https://github.com/user-attachments/assets/6ee684b4-45f9-4964-be99-a018db2eda85" />
<img height="400" alt="image" src="https://github.com/user-attachments/assets/fe104b97-5c7b-452b-a524-0cc7257e903c" />
<img height="400" alt="image" src="https://github.com/user-attachments/assets/175b63db-f047-4b9a-af4f-aceb11e42670" />
<img height="400" alt="image" src="https://github.com/user-attachments/assets/965c71f4-95b3-4ca2-8563-2f2421170c57" />
<img height="400" alt="image" src="https://github.com/user-attachments/assets/a86aef3a-52c0-404a-8ebc-bc7d138370cc" />

## 🌟 Fitur Utama

* **Autentikasi Pengguna:**
    * Halaman Login dengan validasi input.
    * Halaman Registrasi dengan validasi form yang ketat (validasi email, password, dll).
* **Manajemen Produk (CRUD):**
    * **List Produk:** Menampilkan daftar produk dengan desain kartu yang interaktif.
    * **Detail Produk:** Melihat rincian informasi produk (Kode, Nama, Harga).
    * **Tambah & Edit Produk:** Formulir dinamis yang dapat digunakan untuk menambah data baru atau mengubah data lama.
    * **Hapus Produk:** Konfirmasi dialog sebelum menghapus data.
* **Navigasi:** Menggunakan *Drawer Menu* dan navigasi halaman standar Flutter (`Navigator`).
* **UI/UX:** Desain antarmuka modern dengan *Gradient Background* dan umpan balik pengguna menggunakan *SnackBar*.

## 📂 Struktur & Penjelasan Kode

Aplikasi ini memisahkan logika data (*Model*) dan tampilan (*UI*) untuk mempermudah pemeliharaan kode. Berikut adalah rincian fungsionalitas setiap file dalam proyek ini:

### 1. Konfigurasi Utama
* **`main.dart`**
    * Merupakan titik awal (*entry point*) aplikasi.
    * Mengatur tema global aplikasi (`ThemeData`) dengan warna dominan biru (`0xFF2196F3`).
    * Menghilangkan banner debug dan mengarahkan pengguna langsung ke `LoginPage` saat aplikasi dibuka.

### 2. Model Data (`/model`)
Folder ini berisi representasi objek data dan konversi format JSON.
* **`produk.dart`**
    * Merepresentasikan data produk (ID, Kode, Nama, Harga).
    * Menyediakan fungsi `fromJson` untuk memparsing data dari API/Database.
* **`login.dart`**
    * Model untuk menangani respon autentikasi login.
    * Menyimpan Token, User ID, dan status request.
* **`registrasi.dart`**
    * Model untuk menangani respon status pendaftaran akun baru.

### 3. Antarmuka Otentikasi (`/ui`)
* **`login_page.dart`**
    * Halaman formulir login.
    * Memiliki validasi input email dan password.
    * Berpindah ke `ProdukPage` jika login berhasil, atau ke `RegistrasiPage` jika ingin mendaftar.
* **`registrasi_page.dart`**
    * Halaman pendaftaran pengguna baru.
    * Memiliki validasi ketat: Nama (min 3 karakter), Email (format regex), dan Password (min 6 karakter & konfirmasi cocok).

### 4. Antarmuka Produk (`/ui`)
* **`produk_page.dart`**
    * Dashboard utama yang menampilkan daftar produk.
    * Dilengkapi dengan **Sidebar (Drawer)** yang berisi profil admin ("Paundra") dan tombol Logout.
    * Menampilkan data produk menggunakan widget `ItemProduk`.
* **`produk_detail.dart`**
    * Halaman detail untuk melihat informasi spesifik satu produk.
    * Berisi tombol aksi untuk **Edit** (navigasi ke form) dan **Hapus** (memunculkan dialog konfirmasi).
* **`produk_form.dart`**
    * Halaman formulir yang bersifat dinamis (Reuasable).
    * **Mode Tambah:** Jika dibuka tanpa data, form kosong dan tombol berlabel "SIMPAN".
    * **Mode Edit:** Jika dibuka dengan membawa data produk, form terisi otomatis dan tombol berlabel "UBAH".
