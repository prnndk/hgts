# MODUL 1 Pengenalan Laravel dan MVC

## Daftar Isi
1. [Pendahuluan](#1-pendahuluan)
2. [Laravel](#2-laravel)
3. [MVC](#3-mvc)


## 1. Pendahuluan
Siapa yang tidak ingin membuat aplikasi web dengan cepat dan mudah? Dengan Laravel, impian itu bisa terwujud! Laravel adalah framework web paling populer di dunia PHP. Dengan fitur-fitur canggih dan sintaks yang elegan, Laravel memungkinkan Anda untuk merancang aplikasi web yang kuat dengan cepat dan efisien.

Pada Modul ini akan dijelaskan dasar-dasar Laravel, termasuk konsep penting Model-View-Controller (MVC) yang menjadi landasan kerja Laravel. Diharapkan telah mendownload laravel dan dapat dijalankan. Apabila belum, dapat mengikuti modul [sebelumnya](../Modul0/readme.md)

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

Berikut gambaran dari siklus untuk MVC.
![image](https://github.com/prnndk/hgts-laravel/assets/136108856/cc553164-e1f6-4824-a522-c648479ef46d)


### Model
Laravel menggunakan Eloquent sebagai Object Relational Mapper (ORM) untuk memudahkan berinteraksi langsung dengan database. Ketika menggunakan Eloquent, Model digunakan untuk berinteraksi dengan entitas dari database tersebut seperti melakukan Create, Read, Update, dan Delete (CRUD) yang akan dibahas lebih detail pada [Modul 2](../Modul2/readme.md).

Untuk lebih detail mengenai pembuatan model, dapat mengikuti petunjuk pada gambar dibawah ini.

![image](https://github.com/prnndk/hgts-laravel/assets/136108856/f9f3157e-0413-475a-af9b-b540ec744051)

Untuk lebih detail mengenai model, disarankan untuk mengakses langsung dokumentasi laravel untuk model yang terdapat pada link [ini](https://laravel.com/docs/11.x/eloquent).

### View
View merupakan file berisi kode yang akan menampilkan desain dari suatu web. Pada laravel, file view terletak di direktori <code>resources/views/</code>. File view dari laravel menggunakan [Blade templating engine](https://laravel.com/docs/11.x/blade).

```php
<!-- View stored in resources/views/greeting.blade.php -->
 
<html>
    <body>
        <h1>Hello, {{ $name }}</h1>
    </body>
</html>
```

Setelah itu, view yang telah dibuat dapat dipanggil melalui controller yang atau melalui route langsung. Berikut contoh kode untuk routes dari view yang dibuat.
```php
Route::get('/', function () {
    return view('greeting', ['name' => 'James']);
});
```

Untuk lebih detail mengenai pembuatan view, dapat mengikuti petunjuk pada gambar dibawah ini.

![image](https://github.com/prnndk/hgts-laravel/assets/136108856/16d4a511-5896-4235-87af-818fd2738280)

Untuk lebih detail mengenai view, disarankan untuk mengakses langsung dokumentasi laravel untuk model yang terdapat pada link [ini](https://laravel.com/docs/11.x/views).

### Controller 
Controller merupakan suatu komponen yang berfungsi untuk mengelola business logic dan sebagai penghubung antara Model dan View. Setelah Route menghubungkan ke controller dan method mana yang akan dituju, method dari suatu controller akan mengembalikan nilai atau tujuan url yang akan dituju. Sebagai contoh, UserController class menghandle semua request yang berhubungan dengan users termasuk CRUD akan mengembalikan data dalam bentuk JSON apabila sukses. Sedangkan apabila gagal, maka akan mengembalikan pesan mengenai informasi yang menyebabkan kegagalan tersebut seperti User tidak ditemukan dan lainnya.    

Berikut contoh kode dari UserController untuk menunjukkan profile berdasarkan userID.
```php
<?php
 
namespace App\Http\Controllers;
 
use App\Models\User;
use Illuminate\View\View;
 
class UserController extends Controller
{
    /**
     * Show the profile for a given user.
     */
    public function show(string $id): View
    {
        return view('user.profile', [
            'user' => User::findOrFail($id)
        ]);
    }
}
```

Setelah menulis class dan method, maka definisikan route yang terdapat di dalam folder <code>routes</code>. Berikut contoh kode untuk routes dari UserController.
```php
use App\Http\Controllers\UserController;
 
Route::get('/user/{id}', [UserController::class, 'show']);
```

Untuk membuat controller, dapat menggunakan Artisan command. By default, semua controller untuk aplikasi ditempatkan di <code>app/Http/Controllers</code>.
```bash
php artisan make:controller UserController
```

Untuk lebih detailnya mengenai pembuatan controller menggunakan Artisan command, dapat mengikuti petunjuk pada gambar dibawah ini.

![image](https://github.com/prnndk/hgts-laravel/assets/136108856/3d1b89a5-94cd-44a7-b003-3c88bfa9107d)

Untuk lebih detail mengenai controller, disarankan untuk mengakses langsung dokumentasi laravel untuk model yang terdapat pada link [ini](https://laravel.com/docs/11.x/controllers).

## Referensi
1. https://laravel.com/docs/11.x/
2. https://selftaughtcoders.com/from-idea-to-launch/lesson-17/laravel-5-mvc-application-in-10-minutes/