# TUGAS 8 - PERTEMUAN 10

```
Nama      : Daiva Paundra Gevano
NIM       : H1D023075
Shift     : A
Shift KRS : F
```

Aplikasi Toko ini dibuat menggunakan **Flutter** sebagai bagian dari proyek kuliah untuk mempelajari:

## Screenshot Aplikasi
<img height="400" alt="image" src="https://github.com/user-attachments/assets/7ac6dfd6-6c68-4b6f-8017-db4515d1f880" />
<img height="400" alt="image" src="https://github.com/user-attachments/assets/0abfcb75-e379-4893-b971-32f80e53784b" />
<img height="400" alt="image" src="https://github.com/user-attachments/assets/6ee684b4-45f9-4964-be99-a018db2eda85" />
<img height="400" alt="image" src="https://github.com/user-attachments/assets/fe104b97-5c7b-452b-a524-0cc7257e903c" />
<img height="400" alt="image" src="https://github.com/user-attachments/assets/175b63db-f047-4b9a-af4f-aceb11e42670" />
<img height="400" alt="image" src="https://github.com/user-attachments/assets/965c71f4-95b3-4ca2-8563-2f2421170c57" />
<img height="400" alt="image" src="https://github.com/user-attachments/assets/a86aef3a-52c0-404a-8ebc-bc7d138370cc" />

## 📂 Struktur Folder

lib/
│── main.dart
│── login.dart
│── login_page.dart
│── registrasi.dart
│── registrasi_page.dart
│── produk.dart
│── produk_page.dart
│── produk_detail.dart
│── produk_form.dart

yaml
Copy code

---

# 📘 3. Penjelasan Setiap Halaman & Function Utama

---

## ## 3.1 **main.dart**

File entry point aplikasi dan routing.

### 🔧 Function Penting

#### **`main()`**
```dart
void main() {
  runApp(const MyApp());
}
```
Menjalankan aplikasi.

build() – MyApp
Mengatur:
<img width="442" height="898" alt="image" src="https://github.com/user-attachments/assets/4609855f-03bb-468a-a093-6ba0dbaf0670" />

Tema

Routing

Halaman awal (LoginPage)

## 3.2 login.dart
Berisi logika autentikasi sederhana (dummy login).

🔧 Function Penting
login(String email, String password)
dart
Copy code
bool login(String email, String password) {
  return email == "admin@gmail.com" && password == "admin123";
}
## 3.3 login_page.dart
Halaman login (UI).

🔧 Function Penting
_login()
dart
Copy code
void _login() {
  if (_formKey.currentState!.validate()) {
    bool status = login(_email.text, _password.text);
    if (status) {
      Navigator.pushReplacementNamed(context, '/produk');
    }
  }
}
Validasi input

Panggil fungsi login

Navigasi ke halaman produk

Validator
dart
Copy code
if (value == null || value.isEmpty) {
  return 'Email tidak boleh kosong';
}
## 3.4 registrasi.dart
Berisi logika pendaftaran user.

🔧 Function Penting
dart
Copy code
bool register(String nama, String email, String password) {
  return true;
}
## 3.5 registrasi_page.dart
Form untuk registrasi user baru.

🔧 Function Penting
_register()
dart
Copy code
void _register() {
  if (_formKey.currentState!.validate()) {
    register(_nama.text, _email.text, _password.text);
    Navigator.pop(context);
  }
}
Validator Konfirmasi Password
dart
Copy code
if (_password.text != _confirm.text) {
  return "Password tidak sama";
}
## 3.6 produk.dart
Model data untuk produk.

🔧 Class Penting
dart
Copy code
class Produk {
  String id;
  String nama;
  int harga;

  Produk({
    required this.id,
    required this.nama,
    required this.harga,
  });
}
## 3.7 produk_page.dart
Menampilkan daftar produk + aksi CRUD.

🔧 Function Penting
List Produk
dart
Copy code
ListView.builder(
  itemCount: produkList.length,
  itemBuilder: (context, index) {
    final p = produkList[index];
    return ListTile(
      title: Text(p.nama),
      subtitle: Text("Rp ${p.harga}"),
      onTap: () => Navigator.pushNamed(context, '/detail', arguments: p),
    );
  },
)
Hapus Produk + Dialog
dart
Copy code
void _hapusProduk(Produk p) {
  showDialog(
    context: context,
    builder: (_) => AlertDialog(
      title: Text('Hapus Produk?'),
      actions: [
        TextButton(onPressed: () => Navigator.pop(context), child: Text("Batal")),
        TextButton(
          onPressed: () {
            setState(() => produkList.remove(p));
            Navigator.pop(context);
          },
          child: Text("Hapus"),
        ),
      ],
    ),
  );
}
Tombol Tambah Produk
dart
Copy code
FloatingActionButton(
  onPressed: () => Navigator.pushNamed(context, '/form'),
)
## 3.8 produk_form.dart
Digunakan untuk tambah & edit produk.

🔧 Function Penting
initState()
dart
Copy code
if (widget.produk != null) {
  _nama.text = widget.produk!.nama;
  _harga.text = widget.produk!.harga.toString();
}
_simpan()
dart
Copy code
void _simpan() {
  if (_formKey.currentState!.validate()) {
    if (widget.produk == null) {
      produkList.add(Produk(
        id: DateTime.now().toString(),
        nama: _nama.text,
        harga: int.parse(_harga.text),
      ));
    } else {
      widget.produk!.nama = _nama.text;
      widget.produk!.harga = int.parse(_harga.text);
    }
    Navigator.pop(context);
  }
}
## 3.9 produk_detail.dart
Halaman detail produk.

🔧 Function Penting
Navigasi ke Edit Produk
dart
Copy code
IconButton(
  icon: Icon(Icons.edit),
  onPressed: () => Navigator.pushNamed(context, '/form', arguments: produk),
)
🎯 4. Alur Aplikasi
scss
Copy code
Login Page
   ↓ (Belum punya akun)
Registrasi Page
   ↓
Login
   ↓ (Berhasil)
Produk Page
   ↓
Detail Produk → Edit Produk → Simpan
   ↓
Tambah Produk
