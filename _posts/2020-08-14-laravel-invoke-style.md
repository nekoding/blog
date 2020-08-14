---
tags:
- tutorial
- laravel
- php
layout: article
title: 'Memisahkan method controller dengan invoke di laravel'
date: 2020-08-14 11:04:00 +0800
key: memisahkan-method-dengan-invoke
---

# Intro
Jadi tadi sewaktu scroll - scroll bacaan di dev.to saya menemukan artikel yang menarik yaitu : [Turbo charge php development](https://dev.to/jump24/turbocharged-php-development-with-xdebug-docker-phpstorm-1n6c).  
Salah satu yang menarik perhatian saya adalah penggunaan fungsi __invoke di salah satu screenshot. Karena penasaran saya langsung mencari artikel yang terkait fungsi __invoke di laravel dan menemukan artikel yang relevan di medium [Laravel controller with magic method](https://medium.com/@vivekdhumal/laravel-controller-with-magic-method-b48b763b49bc).  
Di artikel tersebut menjelaskan tentang bagaimana mengenkapsulasi setiap custom method ke dalam class berbeda dengan memanfaatkan fungsi __invoke di PHP. di artikel tersebut juga disematkan sebuah video dari Laracon US 2017, untuk saat membuat artikel ini saya juga belum menontonnya hahaha. Untuk videonya saya embed juga dibawah ini 
[![Never Write Custom Action](https://img.youtube.com/vi/MF0jFKvS4SI/0.jpg)](https://www.youtube.com/watch?v=MF0jFKvS4SI).

# Contoh kasus
Untuk contoh kasus sebut saja kita punya custom action di controller User yaitu sebagai berikut :

```php
class UserController extends Controller
{
    public function login()
    {
        // Code Logic
    }

    public function register()
    {
        // Code Logic
    }
}
```

disitu kan ada 2 custom method yaitu login dan register nah ketika mau membuat route maka kita akan menampilkannya seperti ini :

```php
Route::group(['prefix' => 'user'], function () {
    Route::post('login', 'UserController@login');
    Route::post('register', 'UserController@register');
});
```

sebenarnya tidak ada yang salah sih bener - bener saja. tetapi jika kita menggunakan fungsi __invoke tadi controller kita dapat mendefiniskan routenya seperti ini :

```php
Route::group(['prefix' => 'user'], function () {
    Route::post('login', 'User/LoginController');
    Route::post('register', 'User/RegisterController');
});
```
untuk contoh controllernya seperti ini :

```php
# LoginController
class LoginController extends Controller
{
    public function __invoke()
    {
        return 'login method';
    }

}

#RegisterController
class RegisterController extends Controller
{
    public function __invoke()
    {
        return 'register method';
    }

}
```

Mungkin akan sedikit membuang - buang waktu karena membungkus setiap method ke dalam class yang berbeda. **Ya memang :p**. Metode penulisan ini direkomendasikan jika kita ingin membuat sebuah method tapi kita tidak tahu mau kita masukkan ke class yang mana. Maka dengan teknik ini kita membuatnya jauh lebih *clean* dan mudah dimaintenance di kemudian hari. karena kita tinggal buat class baru dengan nama yang sesuai dengan method nya lalu kita panggil fungsi __invoke.  

>Referensi : 
>https://www.php.net/manual/en/language.oop5.magic.php


