# MODUL 1 Pengenalan Laravel dan MVC

## Daftar Isi
1. [Pendahuluan](#1-pendahuluan)
2. [Laravel](#2-laravel)
3. [MVC](#3-mvc)


## 1. Pendahuluan
Siapa yang tidak ingin membuat aplikasi web dengan cepat dan mudah? Dengan Laravel, impian itu bisa terwujud! Laravel adalah framework web paling populer di dunia PHP. Dengan fitur-fitur canggih dan sintaks yang elegan, Laravel memungkinkan Anda untuk merancang aplikasi web yang kuat dengan cepat dan efisien.

Pada Modul ini akan dijelaskan dasar-dasar Laravel, termasuk konsep penting Model-View-Controller (MVC) yang menjadi landasan kerja Laravel. Diharapkan telah mendownload laravel dan dapat dijalankan. Apabila belum, maka dapat mengikuti modul [sebelumnya](../Modul0/readme.md) terlebih dahulu.

## 2. Laravel
Laravel adalah kerangka aplikasi web dengan sintaks yang ekspresif dan elegan. Sebuah kerangka kerja web menyediakan struktur dan titik awal untuk membuat aplikasi, memungkinkan fokus pada menciptakan sesuatu yang luar biasa.

Untuk membuat Laravel project via composer dapat digunakan command:
```bash
composer create-project laravel/laravel {namaApp}

# Masuk ke folder dari laravel project yang telah dibuat
cd {namaApp}
```

Untuk menjalankannya secara developement, dapat digunakan Artisan command:
```bash
php artisan serve
```

## 3. MVC
Model-View-Controller (MVC) adalah pola arsitektur yang memisahkan aplikasi menjadi tiga komponen utama: model, view, dan controller. Tiap komponen tersebut memiliki fungsi masing-masing. Seperti model yang berhubungan langsung dengan database, View yang berhubungan dengan UI, dan Controller yang berperan sebagai penghubung antara model dan view untuk memproses business logic.

### Kenapa MVC?
<ul>
  <li>Kode terorganisir dan terstruktur</li>
  <li>Proses pengembangan aplikasi menjadi lebih efisien</li>
  <li>Penulisan kode menjadi lebih rapir</li>
  <li>Dapat melakukan testing dengan lebih mudah</li>
  <li>Perbaikan bug atau error lebih cepat untuk diselesaikan</li>
  <li>Mempermudah pemeliharaan</li>
  <li>Digunakan oleh banyak web application framework</li> 
</ul>

### Siklus MVC
![image](https://github.com/prnndk/hgts-laravel/assets/136108856/cc553164-e1f6-4824-a522-c648479ef46d)

### Routing
Sebelum Masuk ke dalam MVC, perlu diketahui konsep dari routing. Setiap request dari alamat yang dimasukkan ke client browser, akan direspon oleh server sesuai yang telah dibuat di dalam routing. By default, routing web akan berada di <code>routes/web.php</code>.

Selain itu, dapat dilakukan return string. Cobalah copy syntax dibawah ini dan tempatkan di file <code>routes/web.php</code>.

```php
Route::get('/halo', function () {
    return "Hello world";
});
```

Pada client browser kalian, coba akses <code>/halo</code> dan akan menampilkan string yang telah di-return sebelumnya.

Pada routing juga dapat dilakukan request dengan method-method di bawah ini:

```php
Route::get($uri, $callback);
Route::post($uri, $callback);
Route::put($uri, $callback);
Route::patch($uri, $callback);
Route::delete($uri, $callback);
Route::options($uri, $callback);
```

Untuk lebih detailnya mengenai routing disarankan untuk mengakses langsung dokumentasi laravel untuk model yang terdapat pada link [ini](https://laravel.com/docs/11.x/routing)

### Model
Laravel menggunakan Eloquent sebagai Object Relational Mapper (ORM) untuk memudahkan berinteraksi langsung dengan database. Ketika menggunakan Eloquent, Model digunakan untuk berinteraksi dengan entitas dari database tersebut seperti melakukan Create, Read, Update, dan Delete (CRUD) yang akan dibahas lebih detail pada [Modul 2](../Modul2/readme.md).

By default, semua model untuk aplikasi ditempatkan di folder <code>app/Models</code>. Untuk lebih detail mengenai pembuatan model, dapat mengikuti petunjuk pada gambar dibawah ini.

![image](https://github.com/prnndk/hgts-laravel/assets/136108856/f9f3157e-0413-475a-af9b-b540ec744051)

Dikarenakan modul ini belum membahas database, maka digunakan data statis. Data ini berisi mengenai tamu. Jika sudah terhubung dengan database, model Tamu akan merepresentasikan table Tamu di database yang akan dibahas lebih lanjut pada [Modul 2](../Modul2/readme.md).

Berikut contoh potongan kode untuk membuat data statis beserta cara memanggilnya.
```php
private static $dataTamu = [
  [
      'id' => 1,
      'name' => 'Budi',
      'no_telp' => '08123456789',
      'alamat' => 'Jl. Merdeka No. 1',
      'keperluan_kunjungan_id' => 1,
      'pesan' => 'Halo, saya ingin berkunjung',
      'created_at' => '2021-01-01 00:00:00',
  ],
  [
      'id' => 2,
      'name' => 'Dodi',
      'no_telp' => '08123456788',
      'alamat' => 'Jl. Merdeka No. 2',
      'keperluan_kunjungan_id' => 2,
      'pesan' => 'Halo, saya ingin berkunjung',
      'created_at' => '2021-01-02 00:00:00',
  ],
  ...
];

public static function getAllTamu(): array {
  return self::$dataTamu;
}
```

Untuk lebih detail mengenai model, disarankan untuk mengakses langsung dokumentasi laravel untuk model yang terdapat pada link [ini](https://laravel.com/docs/11.x/eloquent).

### View
View merupakan file berisi kode yang akan menampilkan desain dari suatu web. Pada laravel, file view terletak di direktori <code>resources/views/</code>. File view dari laravel menggunakan [Blade templating engine](https://laravel.com/docs/11.x/blade).

Untuk lebih detail mengenai pembuatan view, dapat mengikuti petunjuk pada gambar dibawah ini.

![image](https://github.com/prnndk/hgts-laravel/assets/136108856/16d4a511-5896-4235-87af-818fd2738280)

Berikut contoh potongan kode dari halaman form untuk menampilkan data tamu.

```html
<!-- resources/views/dashboard/main.blade.php -->
@extends('dashboard.layouts.main')
@section('title', 'Dashboard')

@section('content')
  <div class="d-sm-flex align-items-center justify-content-between mb-4">
    <h1 class="h3 mb-0 text-gray-800">Dashboard</h1>
  </div>

  <div class="card shadow mb-4">
    <div class="card-header py-3">
      <h6 class="m-0 font-weight-bold text-primary">Data Tamu</h6>
    </div>
    <div class="card-body">
      <div class="row">
        <div class="col-md-6 mb-3">
          <form action="/dashboard" method="get">
            <label for="tanggal" class="form-label">Tanggal Kunjungan</label>
            <div class="input-group">
              <input type="date" class="form-control" id="tanggal" name="tanggal">
              <button class="btn btn-outline-primary mx-3" type="submit">Filter</button>
            </div>
          </form>
        </div>
    <!-- dan seterusnya -->
```

Untuk lebih detailnya mengenai view, disarankan untuk mengakses langsung dokumentasi laravel untuk model yang terdapat pada link [ini](https://laravel.com/docs/11.x/views).

### Controller 
Controller merupakan suatu komponen yang berfungsi untuk mengelola business logic dan sebagai penghubung antara Model dan View. Setelah Route menghubungkan ke controller dan method mana yang akan dituju, method dari suatu controller akan mengembalikan nilai atau tujuan url yang akan dituju. Sebagai contoh, UserController class menghandle semua request yang berhubungan dengan users termasuk CRUD akan mengembalikan data dalam bentuk JSON apabila sukses. Sedangkan apabila gagal, maka akan mengembalikan pesan mengenai informasi yang menyebabkan kegagalan tersebut seperti User tidak ditemukan dan lainnya.    

Untuk kasus kita yaitu DashboardController, maka perlu dibuat DashboardController yang dapat dilakukan dengan menggunakan Artisan command. By default, semua controller untuk aplikasi ditempatkan di folder <code>app/Http/Controllers</code>.

```bash
php artisan make:controller Dashboard
```

Untuk lebih detailnya mengenai pembuatan controller dengan menggunakan Artisan command, dapat mengikuti petunjuk pada gambar dibawah ini.

![image](https://github.com/prnndk/hgts-laravel/assets/136108856/3d1b89a5-94cd-44a7-b003-3c88bfa9107d)

Berikut contoh potongan kode dari DashboardController untuk menampilkan data-data tamu.

```php
public function index(): View {
  $tamus = Tamu::getAllTamu();
  return view('dashboard.main', compact('tamus'));
}
```

Setelah menulis class dan method, maka definisikan route yang terdapat di dalam folder <code>routes</code>. Berikut contoh potongan kode untuk routes dari DashboardController.

```php
// routes/web.php
Route::get('/dashboard', [\App\Http\Controllers\DashboardController::class, 'index']);
```

Berikut tampilan halaman ketika mengakses <code>/dashboard</code> di client browser yang akan menampilkan data dari tamu yang telah dibuat sebelumnya.
![image](https://github.com/prnndk/hgts/assets/136108856/f860b4f1-1707-4792-b09a-24bfc8b5b59c)

Untuk lebih detailnya mengenai controller, disarankan untuk mengakses langsung dokumentasi laravel untuk model yang terdapat pada link [ini](https://laravel.com/docs/11.x/controllers).

## Referensi
1. https://laravel.com/docs/11.x/
2. https://selftaughtcoders.com/from-idea-to-launch/lesson-17/laravel-5-mvc-application-in-10-minutes/
3. https://github.com/Algoritma-dan-Pemrograman-ITS/camin-2024/wiki/Laravel-:-MVC#konsep-mvc-model---view---controller