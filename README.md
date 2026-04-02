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

## Pertemuan 2
