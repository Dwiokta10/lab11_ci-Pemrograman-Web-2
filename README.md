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


## Langkah-langkah Pertemuan 1 

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

Jadi dari awal saya sudah berpikir:
*“Data apa saja yang dibutuhkan oleh aplikasi?”*

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

12. Alur Lengkap Aplikasi (INI YANG PALING PENTING)

Ini bagian yang bikin dosen yakin kamu paham:

User membuka halaman
→ Request masuk ke *Controller*
→ Controller meminta data ke *Model*
→ Model mengambil data dari *Database*
→ Data dikirim kembali ke Controller
→ Controller kirim ke *View*
→ View menampilkan ke user

Jadi alurnya:
*User → Controller → Model → Database → Controller → View → User*

---

# Kesimpulan (Versi “Paham Banget”)

Dari praktikum ini saya memahami bahwa:

* CodeIgniter menggunakan konsep *MVC* untuk memisahkan logic
* CRUD adalah dasar dari hampir semua aplikasi web
* Setiap bagian punya peran:

  * Model → data
  * View → tampilan
  * Controller → pengatur alur

Saya juga memahami bagaimana data mengalir dari user hingga ke database dan kembali ditampilkan ke user.

---
