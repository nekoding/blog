---
tags:
- tutorial
- laravel
- php
layout: article
title: 'Fulltext search dengan laravel scout'
date: 2020-08-28 20:02:00 +0800
key: fulltext-search-dengan-laravel-scout
---

# Intro
Assalamualaikum wr.wb  
Selamat malam semua, kali ini saya akan memberikan sedikit tutorial tentang fulltext search dengan laravel scout.  
Untuk kali ini kita akan menggunakan driver mysql saja ~~dikarenakan saya belum punya akun algolia hehehehe~~.  
Sebelum lanjut ke tutorial kita akan membahas dulu apa itu full text searching ?  

Mengutip dari situs sybase.com
>Full text search is a more advanced way to search a database. Full text search quickly finds all instances of a term (word) in a table without having to scan rows and without having to know which column a term is stored in. Full text search works by using text indexes. A text index stores positional information for all terms found in the columns you create the text index on. Using a text index can be faster than using a regular index to find rows containing a given value.

Jadi intinya full text search mengijinkan kita mencari semua kata yang ingin dicari dari semua kolom di dalam tabel tanpa harus melakukan scanning terhadap baris dan kolom tempat kata itu disimpan. Kalau gambaran umumnya mungkin seperti search engine seperti google kali ya. atau search engine miliki perusahaan - perusahaan e-comerce yang ketika kita mengetik suatu nama barang maka kita akan diberikan data dari barang tersebut serta toko yang relevan / menjual barang yang kita cari tadi.

# Persiapan
1. Pertama siapkan project laravel-nya ( Jika sudah bisa dilewati untuk step yang ini )
```php
laravel new scout
```
2. Install package laravel scout 
```php
composer require laravel/scout
```
3. Setelah proses instalasi laravel scout berhasil lakukan publish vendor dengan php artisan 
```php
php artisan vendor:publish --provider="Laravel\Scout\ScoutServiceProvider"
```
Setelah sukses publish vendor maka akan mengenerate file baru di bagian `config/scout.php`
4. Install package Laravel Scout MySQL Driver
```php
composer require yab/laravel-scout-mysql-driver
```
5. Jika sudah selanjutnya tambahkan service provider di bagian `config/app.php`
```php
        /*
         * Package Service Providers...
         */
        Yab\MySQLScout\Providers\MySQLScoutServiceProvider::class, 
```
6. Setelah itu tambahkan konfigurasi berikut di `config/scout.php`
```php
'mysql' => [
        'mode' => 'NATURAL_LANGUAGE',
        'model_directories' => [app_path()],
        'min_search_length' => 0,
        'min_fulltext_search_length' => 4,
        'min_fulltext_search_fallback' => 'LIKE',
        'query_expansion' => false
    ]
```
7. sekarang tambahkan .env dengan nilai
```
SCOUT_DRIVER=mysql
SCOUT_QUEUE=false
```
8. sekarang waktunya ngoding

# Ngoding

Untuk tutorial ini saya akan membuat sebuah tabel post yang berelasi dengan tabel user. Dimana nanti setiap user bisa punya banyak post.

## Membuat model Post
>kenapa gak bikin tabel user dulu ? karena tabel user udah disediain sama laravel sebagai bawaan aplikasi

1. ketikan perintah 
```php
php artisan make:model Post -mcf
```
Perintah diatas akan membuat model beserta migration, controller dan factorynya. 
>keterangan flag :  
>-m : migration  
>-c : controller  
>-f : factory
2. Jika sudah isikan file migration post dengan
```php
<?php

use Illuminate\Database\Migrations\Migration;
use Illuminate\Database\Schema\Blueprint;
use Illuminate\Support\Facades\Schema;

class CreatePostsTable extends Migration
{
    /**
     * Run the migrations.
     *
     * @return void
     */
    public function up()
    {
        Schema::create('posts', function (Blueprint $table) {
            $table->id();
            $table->unsignedBigInteger('user_id');
            $table->string('title');
            $table->text('content');
            $table->timestamps();

            $table->foreign('user_id')->references('id')->on('users')->onDelete('cascade');
        });
    }

    /**
     * Reverse the migrations.
     *
     * @return void
     */
    public function down()
    {
        Schema::dropIfExists('posts');
    }
}

``` 
3. Jika sudah sekarang lanjut ke bagian factory untuk mengenerate dummy data
```php
<?php

/** @var \Illuminate\Database\Eloquent\Factory $factory */

use App\Post;
use Faker\Generator as Faker;

$factory->define(Post::class, function (Faker $faker) {
    return [
        'user_id'   => rand(1,10),
        'title'     => $faker->sentence(4),
        'content'   => $faker->paragraph()
    ];
});
```
4. Jika sudah sekarang kita buat seeder untuk tabel posts terlebih dahulu dengan cara
```php
php artisan make:seeder PostSeeder
```
5. Selanjutnya tinggal kita panggil fungsi factory di dalam file seedernya tadi
```php
<?php

use App\Post;
use Illuminate\Database\Seeder;

class PostSeeder extends Seeder
{
    /**
     * Run the database seeds.
     *
     * @return void
     */
    public function run()
    {
        factory(Post::class, 40)->create();
    }
}
```
disini saya ingin mengenerate sebanyak 40 buah data, jika kalian ingin mengurangi / menambahkan jumlahnya silahkan saja.  
6. Selanjutnya kita tambahkan trait `Searchable` dibagian model Post dan jangan lupa set mass assignment dengan guarded set ke array kosong. + setting juga sekalian relasinya.
```php
<?php

namespace App;

use Illuminate\Database\Eloquent\Model;
use Laravel\Scout\Searchable;

class Post extends Model
{
    use Searchable;
    protected $guarded = [];

    public function user()
    {
        return $this->belongsTo('App\User');
    }
}
```
Oke untuk model Post sudah jadi selanjutnya pindah ke model User

## Membuat model User
1. Dikarenakan model User sudah diinclude factory jadi tahap bikin factorynya kita skip saja
2. Buat file user seedernya dengan cara
```php
php artisan make:seeder UserSeeder
```
3. Lalu panggil fungsi factory ke dalam file
```php
<?php

use App\User;
use Illuminate\Database\Seeder;

class UserSeeder extends Seeder
{
    /**
     * Run the database seeds.
     *
     * @return void
     */
    public function run()
    {
        factory(User::class, 10)->create();
    }
}
```
4. Jika sudah tambahkan relasi ke model User
```php
<?php

namespace App;

use Illuminate\Contracts\Auth\MustVerifyEmail;
use Illuminate\Foundation\Auth\User as Authenticatable;
use Illuminate\Notifications\Notifiable;

class User extends Authenticatable
{
    use Notifiable;

    /**
     * The attributes that are mass assignable.
     *
     * @var array
     */
    protected $fillable = [
        'name', 'email', 'password',
    ];

    /**
     * The attributes that should be hidden for arrays.
     *
     * @var array
     */
    protected $hidden = [
        'password', 'remember_token',
    ];

    /**
     * The attributes that should be cast to native types.
     *
     * @var array
     */
    protected $casts = [
        'email_verified_at' => 'datetime',
    ];

    public function posts()
    {
        return $this->hasMany('App\Post', 'user_id');
    }
}
```
Oke sip dah jadi.

## Mendaftarkan seeder
1. Sekarang kita harus mendaftarkan file seeder kita ke DatabaseSeeder.php
```php
<?php

use Illuminate\Database\Seeder;

class DatabaseSeeder extends Seeder
{
    /**
     * Seed the application's database.
     *
     * @return void
     */
    public function run()
    {
        $this->call(UserSeeder::class);
        $this->call(PostSeeder::class);
    }
}
```
Oke mantabb.

## Lakukan migrate + seed
untuk melakukan migrate + seed dapat dilakukan dengan cara
```php
php artisan migrate --seed
```
*Pastikan setingan database di file .env sudah benar sebelum melakukan migrate*

## Indexing
Untuk dapat menggunakan full text search di mysql kita perlu mendaftarkan nama kolom ke dalam index. untuk itu kita dapat menggunakan artisan command dengan cara
```php
scout:mysql-index
```
Command diatas akan melakukan indexing di setiap tabel yang file modelnya menggunakan trait `Searchable`. Jika ingin tabel tertentu saja bisa dengan cara

```php
scout:mysql-index NamaModel
```

## Routing 
Untuk routing nya kita bikin sederhana saja yaitu :
```php
<?php

use Illuminate\Support\Facades\Route;

/*
|--------------------------------------------------------------------------
| Web Routes
|--------------------------------------------------------------------------
|
| Here is where you can register web routes for your application. These
| routes are loaded by the RouteServiceProvider within a group which
| contains the "web" middleware group. Now create something great!
|
*/

Route::get('/', function () {
    return view('welcome');
});

Route::get('/post', 'PostController@index')->name('post.index');
Route::get('/dump', 'PostController@dumpData')->name('post.dump');
```

## Controller 
untuk settingan dicontroller nya kita bikin sederhana saja
```php
<?php

namespace App\Http\Controllers;

use App\Post;
use Illuminate\Http\Request;

class PostController extends Controller
{
    public function index()
    {
        $posts = Post::search('error')->get();

        return $posts;
    }

    public function dumpData()
    {
        return Post::all();
    }
}
```
Untuk sekarang fokus saja ke bagian method index-nya disitu saya memanggil static function search yang merupakan fungsi dari trait `Searchable`. Jika kita buka url `url/post` maka kita akan diberikan data json yang isinya berupa data - data yang memiliki teks `error`. 
![Data dengan teks error](/assets/search-error.png)
Hal ini karena saya melakukan pencarian data dengan teks `error`. Sekarang saya coba ubah teks nya dengan `temporibus`

```php
<?php

namespace App\Http\Controllers;

use App\Post;
use Illuminate\Http\Request;

class PostController extends Controller
{
    public function index()
    {
        $posts = Post::search('temporibus')->get();

        return $posts;
    }

    public function dumpData()
    {
        return Post::all();
    }
}
```
![Data dengan teks error](/assets/search-temporibus.png)
maka akan ditampilkan data yang memiliki teks `temporibus`

Sekian dari tutorial sederhana dari saya semoga berguna. Untuk post selanjutnya mungkin akan kita coba tambahkan livewire / vuejs agar data yang dicari lebih dinamis. tapi sebelum itu mungkin saya akan memposting tentang livewire / vuejs nya terlebih dahulu.  
Sekian terima kasih.  
Wassalamualaikum wr.wb

