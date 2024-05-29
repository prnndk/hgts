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
View merupakan file berisi kode yang akan menampilkan desain dari suatu web. Pada laravel, file view terletak di direktori <code>resources/views/</code>. File view dari laravel menggunakan [Blade templating engine](https://laravel.com/docs/11.x/blade). Secara sederhana, dengan menggunakan sistem templating dari laravel ini, kita dapat melakukan hal yang tidak bisa file dengan ekstensi html biasa lakukan.

Dengan menggunakan templating ini, kita bisa membuat sistem komponen untuk sebuah elemen yang akan kita gunakan secara terus menerus. Kita juga dapat melakukan beberapa operasi yang mempermudah dalam mengolah data yang diberikan ke view menggunakan templating engine ini.

Salah satu yang paling sering digunakan adalah <code>Layouting</code>. Fungsi dari layouting adalah untuk mengatur tata letak halaman web secara efisien dan konsisten.

Untuk membuat view, dapat mengikuti petunjuk pada gambar dibawah ini.

![image](https://github.com/prnndk/hgts-laravel/assets/136108856/16d4a511-5896-4235-87af-818fd2738280)

Berikut contoh struktur direktori untuk <code>/resources/views</code>.

```txt
views/
├── dashboard
│   ├── keperluan-kunjungan
│   ├── layouts
│   │   ├── main.blade.php
│   │   ├── navbar.blade.php
│   │   └── sidebar.blade.php
│   └── main.blade.php
├── dashboard.blade.php
├── layouts
│   ├── header.blade.php
│   └── main.blade.php
├── login.blade.php
├── main.blade.php
├── newlogin.blade.php
├── test.blade.php
└── welcome.blade.php
```

Dari struktur direktori tersebut, dapat diketahui flow untuk halaman dashboard yaitu:

```txt
layouts/navbar.bladephp + layouts/navbar.blade.php > layouts/main.blade.php > dashboard/main.blade.php
```

Berikut salah satu contoh komponen navbar dengan menggunakan layouting.

```html
<!-- /resources/views/dashboard/layouts/navbar.blade.php -->

<nav class="navbar navbar-expand navbar-light bg-white topbar mb-4 static-top shadow">
  <button id="sidebarToggleTop" class="btn btn-link d-md-none rounded-circle mr-3">
    <i class="fa fa-bars"></i>
  </button>
  <ul class="navbar-nav ml-auto">

    <div class="topbar-divider d-none d-sm-block"></div>
    <li class="nav-item dropdown no-arrow">
      <a class="nav-link dropdown-toggle" href="#" id="userDropdown" role="button"
          data-toggle="dropdown" aria-haspopup="true" aria-expanded="false">
          <span class="mr-2 d-none d-lg-inline text-gray-600 small">Douglas McGee</span>
          <img class="img-profile rounded-circle"
                src="https://ui-avatars.com/api/?name=John+Doe">
      </a>
      <!-- Dropdown - User Information -->
      <div class="dropdown-menu dropdown-menu-right shadow animated--grow-in"
            aria-labelledby="userDropdown">
        <a class="dropdown-item" href="#">
            <i class="fas fa-user fa-sm fa-fw mr-2 text-gray-400"></i>
            Profile
        </a>
        <a class="dropdown-item" href="#">
            <i class="fas fa-cogs fa-sm fa-fw mr-2 text-gray-400"></i>
            Settings
        </a>
        <a class="dropdown-item" href="#">
            <i class="fas fa-list fa-sm fa-fw mr-2 text-gray-400"></i>
            Activity Log
        </a>
        <div class="dropdown-divider"></div>
          <a class="dropdown-item" href="#" data-toggle="modal" data-target="#logoutModal">
            <i class="fas fa-sign-out-alt fa-sm fa-fw mr-2 text-gray-400"></i>
            Logout
          </a>
      </div>
    </li>
  </ul>
</nav>
```

Setelah itu, komponen-komponen yang telah dibuat dapat dipanggil di file lain contohnya <code>/resources/views/dashboard/layouts/main.blade.php</code>. Berikut contoh potongan kode dari file tersebut.

```html
<!-- /resources/views/dashboard/layouts/main.blade.php -->

<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="utf-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no">
  <meta name="description" content="">
  <meta name="author" content="">

  <title>
      @yield('title') - BukuTamu
  </title>

  <!-- Custom fonts for this template-->
  <link href="{{asset("/sb-admin/vendor/fontawesome-free/css/all.min.css")}}" rel="stylesheet" type="text/css">
  <link
      href="https://fonts.googleapis.com/css?family=Nunito:200,200i,300,300i,400,400i,600,600i,700,700i,800,800i,900,900i"
      rel="stylesheet">

  <!-- Custom styles for this template-->
  <link href="{{asset("/sb-admin/css/sb-admin-2.min.css")}}" rel="stylesheet">

</head>

<body id="page-top">

<!-- Page Wrapper -->
<div id="wrapper">

  <!-- Sidebar -->
  @include('dashboard.layouts.sidebar')
  <!-- End of Sidebar -->

  <!-- Content Wrapper -->
  <div id="content-wrapper" class="d-flex flex-column">

    <!-- Main Content -->
    <div id="content">

      <!-- Topbar -->
      @include('dashboard.layouts.navbar')

      <!-- Begin Page Content -->
        <div class="container-fluid">
            @yield('content')
        </div>

      <!-- dan seterusnya -->

<!-- Bootstrap core JavaScript-->
<script src="{{asset("sb-admin/vendor/jquery/jquery.min.js")}}"></script>
<script src="{{asset("sb-admin/vendor/bootstrap/js/bootstrap.bundle.min.js")}}"></script>

<!-- Core plugin JavaScript-->
<script src="{{asset("sb-admin/vendor/jquery-easing/jquery.easing.min.js")}}"></script>

<!-- Custom scripts for all pages-->
<script src="{{asset("sb-admin/js/sb-admin-2.min.js")}}"></script>

<!-- Page level plugins -->
<script src="{{asset("sb-admin/vendor/chart.js/Chart.min.js")}}"></script>

</body>

</html>
```

Kalian bisa membuat banyak @yield(...) untuk berbagai macam style layout berbeda di folder <code>/layouts/</code> kalian dan menggunakan @section(...) untuk berbagai macam style yang ingin kalian aplikasikan di page view kalian.

Berikut contoh potongan kode dari halaman form untuk menampilkan data tamu dengan menggunakan komponen yang telah dibuat sebelumnya. 

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
@endsection
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