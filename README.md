# Laporan Praktikum Pertemuan 1 - 4 

|                |                    |
| ------------------ | ------------------ |
|      _Nama_    | Dwi Okta Ramadhani |
|      _NIM_     |      312410056     |
|     _Kelas_    |      I241A    |
|  _Mata Kuliah_ | Bahasa Pemrograman Web 2 |

Tujuan Praktikum

Pada praktikum ini, saya mempelajari:

* Konsep dasar framework
* Konsep MVC (Model View Controller)
* Cara membuat aplikasi sederhana menggunakan CodeIgniter 4


## Pertemuan 1 

1. Persiapan
   Sebelum memulai, saya melakukan konfigurasi pada XAMPP:
Mengaktifkan ekstensi PHP:

  * php-json
  * php-mysqlnd
  * php-xml
  * php-intl
Cara:

  * Buka XAMPP → Apache → Config → php.ini
  * Hilangkan tanda `;` pada ekstensi
  * Restart Apache

2. Instalasi CodeIgniter 4

Langkah instalasi:

1. Download CodeIgniter dari website resmi
2. Extract ke folder `htdocs/lab11_ci`
3. Rename folder menjadi `ci4`
4. Jalankan di browser:

3. Menjalankan CLI CodeIgniter

Masuk ke folder project:

```
xampp/htdocs/lab11_ci/ci4
```

Lalu jalankan:

```
php spark
```

Fungsi: untuk menjalankan perintah CLI CodeIgniter

4. Mengaktifkan Debugging

Langkah:

* Rename file `env` menjadi `.env`
* Ubah:

```
CI_ENVIRONMENT = development
```

5. Struktur Direktori

Struktur penting pada CodeIgniter:

* `app/` → tempat coding utama
* `public/` → file yang bisa diakses user
* `writable/` → untuk log & upload
* `vendor/` → library bawaan

Penjelasan:
Folder `app` adalah tempat utama membuat aplikasi.

6. Konsep MVC

Penjelasan:

**Model** → mengelola data
**View** → tampilan
**Controller** → penghubung

MVC memisahkan logic, tampilan, dan data agar rapi.

7. Routing

Edit file:

```
app/Config/Routes.php
```

Tambahkan:

```php
$routes->get('/about', 'Page::about');
$routes->get('/contact', 'Page::contact');
$routes->get('/faqs', 'Page::faqs');
```

Cek dengan:

```
php spark routes
```

8. Membuat Controller

File:

```
app/Controllers/Page.php
```

Isi:

```php
<?php

namespace App\Controllers;

class Page extends BaseController
{
    public function about()
    {
        echo "Ini halaman About";
    }

    public function contact()
    {
        echo "Ini halaman Contact";
    }

    public function faqs()
    {
        echo "Ini halaman FAQ";
    }
}

9. Auto Routing

Tambahkan method:

```php
public function tos()
{
    echo "Ini halaman Term of Service";
}
```

Akses:

```
http://localhost:8080/page/tos
```

10. Membuat View

File:

```
app/Views/about.php
```

Isi:

```php
<h1><?= $title; ?></h1>
<p><?= $content; ?></p>
```

Ubah controller:

```php
return view('about', [
    'title' => 'Halaman About',
    'content' => 'Ini isi halaman about'
]);
```
11. Membuat Template Layout

Buat:

```
app/Views/template/header.php
app/Views/template/footer.php
```

Gunakan di view:

```php
<?= $this->include('template/header'); ?>
<?= $this->include('template/footer'); ?>
```

Tambahkan CSS di folder:

```
public/style.css
```
<img width="1920" height="1128" alt="Cuplikan layar 2026-04-01 115619" src="https://github.com/user-attachments/assets/262982fa-a0f5-48e2-9309-138f7387cda7" />
<img width="1920" height="1128" alt="Cuplikan layar 2026-04-01 121242" src="https://github.com/user-attachments/assets/e0410369-0080-42e1-a86d-c21e5ab7c32c" />
<img width="1920" height="1128" alt="Cuplikan layar 2026-04-01 122718" src="https://github.com/user-attachments/assets/a53a3efc-ed41-4ebe-a33a-0e69bc911c69" />
<img width="1920" height="1128" alt="Cuplikan layar 2026-04-01 123319" src="https://github.com/user-attachments/assets/b6c19ad1-b647-4fac-8bca-16b1c8d38bf8" />
<img width="1920" height="1128" alt="Cuplikan layar 2026-04-01 123059" src="https://github.com/user-attachments/assets/0a076b1a-d0a0-4f10-9f10-15047a23da5d" />
<img width="1920" height="1128" alt="Cuplikan layar 2026-04-01 124344" src="https://github.com/user-attachments/assets/fbf9cb7b-76bc-4a57-bd24-7adb03cdcf3e" />
<img width="1920" height="1128" alt="Cuplikan layar 2026-04-01 130555" src="https://github.com/user-attachments/assets/d5b9f730-e157-4493-90bf-77dec4d05419" />
<img width="1920" height="1128" alt="Cuplikan layar 2026-04-01 131529" 
<img width="1170" height="629" alt="Cuplikan layar 2026-04-02 153704" src="https://github.com/user-attachments/assets/5d45d4e4-8eae-4201-8f37-81774c218ad1" />


## Pertemuan 2
1. Persiapan Awal

Langkah pertama yang saya lakukan:

* Menyalakan *Apache dan MySQL di XAMPP*
* Membuka *phpMyAdmin*

Kenapa ini penting?
Karena tanpa database aktif, aplikasi tidak bisa menyimpan data.

---

2. Membuat Database dan Tabel

Saya membuat database:

sql
CREATE DATABASE lab_ci4;


Kemudian membuat tabel artikel.

*Cara saya memahami bagian ini:*
Saya menganggap tabel ini seperti “tempat penyimpanan artikel”, jadi saya menentukan kolom yang dibutuhkan:

* id → penanda unik
* judul → judul artikel
* isi → isi konten
* slug → URL yang rapi
* status → status publish
* gambar → gambar artikel
---

3. Menghubungkan Database ke CodeIgniter

Selanjutnya saya konfigurasi file .env

Kenapa pakai .env?
Karena lebih aman dan fleksibel dibanding langsung di config.

*Alur berpikirnya:*

* CodeIgniter itu aplikasi
* Database itu tempat data
* Jadi harus ada “jembatan” → yaitu konfigurasi koneksi

---

4. Membuat Model (Penghubung ke Database)

Saya membuat ArtikelModel.

*Pemahaman saya:*
Model ini ibarat “perantara” antara aplikasi dan database.

Jadi:

* Controller *tidak langsung ke database*
* Tapi lewat Model

Kenapa begitu?
Supaya kode lebih rapi dan terstruktur (konsep MVC)

---

5. Membuat Controller (Pengatur Alur)

Saya membuat controller Artikel.

Di sini saya mulai memahami alur sebenarnya:

User buka halaman →
Controller menerima request →
Controller ambil data dari Model →
Controller kirim ke View

Controller adalah “otak” dari aplikasi

---

6. Menampilkan Data (READ)

Saat membuat method index():

Saya mengambil semua data:

php
$model->findAll();

7. Menambah Data (CREATE)

Saat membuat fitur tambah artikel:

*Alurnya saya pahami seperti ini:*

1. User isi form
2. Data dikirim ke controller
3. Controller kirim ke model
4. Model simpan ke database

8. Mengubah Data (UPDATE)

Saat edit artikel:

*Pemahaman saya:*

* Ambil data lama dari database
* Tampilkan di form
* User ubah
* Simpan kembali

9. Menghapus Data (DELETE)

Saat klik hapus:
*Alurnya:*

* Ambil ID artikel
* Kirim ke controller
* Controller perintahkan model untuk hapus

Ini proses paling sederhana tapi sangat penting dalam CRUD

---
10. Routing (Penghubung URL ke Controller)

Saya menambahkan routing untuk:

* Halaman artikel
* Detail artikel
* Admin

*Pemahaman saya:*
Routing itu seperti “penunjuk jalan”
Contoh:


/artikel → ke controller Artikel


---

11. Halaman Admin (Tempat CRUD)

Saya membuat halaman admin untuk:

* Lihat data
* Tambah
* Edit
* Hapus

*Kenapa dipisah dari user biasa?*
Karena:
User biasa hanya melihat
Admin yang mengelola data

---

12. Alur Lengkap Aplikasi

Ini bagian yang bikin dosen yakin kamu paham:

User membuka halaman
→ Request masuk ke *Controller*
→ Controller meminta data ke *Model*
→ Model mengambil data dari *Database*
→ Data dikirim kembali ke Controller
→ Controller kirim ke *View*
→ View menampilkan ke user

Jadi alurnya:
User → Controller → Model → Database → Controller → View → User
<img width="1507" height="707" alt="Cuplikan layar 2026-04-02 155041" src="https://github.com/user-attachments/assets/0aca9da6-c797-434a-bdc0-b2ab041ec855" />
<img width="1290" height="503" alt="Cuplikan layar 2026-04-02 155829" src="https://github.com/user-attachments/assets/1db0c38b-1344-499c-ba45-eb1c6123d96c" />
<img width="900" height="553" alt="Cuplikan layar 2026-04-02 160020" src="https://github.com/user-attachments/assets/3995eeef-9b6d-43d6-979b-2ffdf9c45758" />

# Praktikum 3 

## Langkah-Langkah Praktikum

### 1. Persiapan

* Membuka project sebelumnya lab7_php_ci
* Menggunakan text editor (VSCode)
* Menjalankan server lokal

---

### 2. Membuat Layout Utama

Lokasi:


app/Views/layout/main.php


Penjelasan:

* Membuat template utama website
* Berisi:

  * Header
  * Navbar
  * Content (dinamis)
  * Sidebar
  * Footer

Bagian penting:


<?= $this->renderSection('content') ?>


Digunakan untuk menampilkan isi halaman yang berbeda-beda

### 3. Modifikasi View (Home)

File:


app/Views/home.php


Perubahan:


<?= $this->extend('layout/main') ?>

<?= $this->section('content') ?>

<h1><?= $title; ?></h1>
<p><?= $content; ?></p>

<?= $this->endSection() ?>


Penjelasan:

* extend() → menggunakan layout utama
* section() → isi konten halaman
---

### 4. Membuat View Cell

Folder:


app/Cells/


File:


ArtikelTerkini.php


Fungsi:

* Mengambil data artikel terbaru dari database
* Menampilkan 5 artikel terbaru

Kode penting:


$model->orderBy('created_at', 'DESC')->limit(5)->findAll();

---

### 5. Membuat Komponen View

Folder:


app/Views/components/


File:


artikel_terkini.php


Fungsi:

* Menampilkan daftar artikel dalam bentuk list

---

### 6. Menampilkan View Cell di Layout

File:


layout/main.php


Tambahkan:


<?= view_cell('App\\Cells\\ArtikelTerkini::render') ?>


Penjelasan:

* Memanggil komponen artikel terbaru
* Bisa digunakan berulang di halaman lain


### 1. Apa manfaat View Layout?

View Layout memudahkan pembuatan tampilan website karena:

* Template bisa digunakan berulang
* Kode lebih rapi dan terstruktur
* Memisahkan desain dan konten

---

### 2. Perbedaan View Cell dan View biasa

| View Biasa                    | View Cell                      |
| ----------------------------- | ------------------------------ |
| Digunakan untuk halaman utama | Digunakan untuk komponen kecil |
| Tidak reusable                | Bisa digunakan berulang        |
| Dipanggil langsung            | Dipanggil dengan view_cell() |

---

### 3. Menampilkan kategori tertentu

Contoh modifikasi:


$model->where('kategori', 'teknologi')
      ->orderBy('created_at', 'DESC')
      ->limit(5)
      ->findAll();


Penjelasan:

* Hanya menampilkan artikel dengan kategori tertentu

---

## Kesimpulan

Pada praktikum ini saya memahami bahwa:

* View Layout membuat tampilan lebih efisien
* View Cell membantu membuat komponen modular
* CodeIgniter 4 mendukung pengembangan aplikasi yang lebih terstruktur

<img width="1114" height="546" alt="Cuplikan layar 2026-04-02 161229" src="https://github.com/user-attachments/assets/8534d712-efde-48f1-9325-bf6918f6dddc" />
<img width="1066" height="527" alt="Cuplikan layar 2026-04-02 161250" src="https://github.com/user-attachments/assets/77121c8d-d63c-41b6-92d4-65492cc25431" />

# Praktikum 4
Langkah-Langkah Praktikum

1. Membuat Database User

Query:

sql
CREATE TABLE user (
  id INT(11) auto_increment,
  username VARCHAR(200) NOT NULL,
  useremail VARCHAR(200),
  userpassword VARCHAR(200),
  PRIMARY KEY(id)
);


Penjelasan:

* Tabel ini digunakan untuk menyimpan data user
* Password disimpan dalam bentuk *hash (aman)*

---

2. Membuat Model User

Lokasi:

bash
app/Models/UserModel.php

Fungsi:

* Menghubungkan aplikasi dengan tabel user
* Mengelola data login

Bagian penting:

php
protected $allowedFields = ['username', 'useremail', 'userpassword'];

---

3. Membuat Controller User

Lokasi:

bash
app/Controllers/User.php

Method:

* index() → menampilkan data user
* login() → proses autentikasi
* logout() → keluar dari sistem

Proses login:

1. Ambil input email & password
2. Cek ke database
3. Verifikasi password (password_verify)
4. Simpan session jika berhasil

Contoh session:

php
'session' => [
    'logged_in' => TRUE
]

4. Membuat View Login

Lokasi:

bash
app/Views/user/login.php

Fungsi:

* Menampilkan form login
* Input email & password

Fitur:

* Menampilkan error (flashdata)
* Form validasi sederhana


---

5. Membuat Seeder (Data Dummy)

Command:

bash
php spark make:seeder UserSeeder
php spark db:seed UserSeeder


Fungsi:

* Menambahkan user otomatis ke database
* Mempermudah testing login

Data:

* Email: [admin@email.com](mailto:admin@email.com)
* Password: admin123
---

6. Membuat Auth Filter

Lokasi:

bash
app/Filters/Auth.php


Fungsi:

* Melindungi halaman admin
* Redirect ke login jika belum login

Logika:

php
if(! session()->get('logged_in')){
    return redirect()->to('/user/login');
}

---

7. Konfigurasi Filter

File:

bash
app/Config/Filters.php


Tambahkan:

php
'auth' => App\Filters\Auth::class

---

8. Uji Coba Login

URL:


http://localhost:8080/user/login


Hasil:

* Jika login berhasil → masuk ke halaman admin
* Jika gagal → muncul pesan error


9. Fungsi Logout

Tambahkan:

php
public function logout()
{
    session()->destroy();
    return redirect()->to('/user/login');
}


Fungsi:

* Menghapus session
* Kembali ke halaman login

## Landasan Teori

1. Authentication (Auth)

Authentication adalah proses untuk memastikan bahwa pengguna adalah *orang yang valid* sebelum mengakses sistem.

Contoh:

* Login menggunakan email & password

Tujuan:

* Mengamankan data
* Membatasi akses pengguna

---

2. Authorization

Authorization adalah proses menentukan *hak akses pengguna* setelah login.

Contoh:

* Admin bisa akses dashboard
* User biasa tidak bisa

---

3. Session Management

Session digunakan untuk menyimpan data sementara pengguna setelah login.

Fungsi:

* Menyimpan status login
* Menyimpan data user

Contoh:

php
session()->set([
    'logged_in' => TRUE
]);


---

4. Password Hashing

Password tidak disimpan dalam bentuk asli, tetapi diubah menjadi hash.

Fungsi:

* Mencegah pencurian password
* Meningkatkan keamanan

Digunakan:

* password_hash()
* password_verify()

---

5. Filter pada CodeIgniter 4

Filter adalah mekanisme untuk menyaring request sebelum atau sesudah controller dijalankan.

Jenis:

* Before Filter → sebelum akses halaman
* After Filter → setelah proses selesai

---

6. Keamanan Aplikasi Web

Dalam sistem login, keamanan sangat penting:

* Validasi input
* Hash password
* Session protection
* Filter akses

---

## Analisis

Dari praktikum ini dapat disimpulkan bahwa:

* Sistem login adalah bagian penting dalam aplikasi web
* Filter membantu membatasi akses pengguna
* Session digunakan untuk menjaga status login

---

## Kesimpulan

Dengan menggunakan CodeIgniter 4, pembuatan sistem login menjadi lebih mudah dan terstruktur. Fitur seperti Model, Controller, Session, dan Filter sangat membantu dalam membangun sistem autentikasi yang aman dan efisien.
<img width="806" height="429" alt="Cuplikan layar 2026-04-02 161451" src="https://github.com/user-attachments/assets/e88fd529-1afb-410c-bffc-e8224599fff5" />
