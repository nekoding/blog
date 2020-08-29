---
tags:
- tutorial
- laravel
- php
- scout
layout: article
title: 'Belajar scafolding laravel auth'
date: 2020-08-29 21:52:00 +0800
key: belajar-scafolding-laravel-auth
---

# Intro
Assalamualaikum wr.wb
Selamat malam, kali ini saya akan menuliskan sebuah tutorial tentang laravel bagian authentification. Untuk tutorial ini akan ada beberapa part yang merupakan sambungan dari tutorial ini yang nantinya akan saya posting dikemudian hari. Rencananya di seri ini akan ada beberapa bagian antara lain :  

1. Scafolding laravel auth
2. Laravel email verification
3. Laravel forgot password
4. Laravel authorization
5. Laravel email queue
6. Laravel roles
7. Laravel JWT

# Ngoding
Untuk kali ini saya hanya akan membahas tentang cara bikin scafolding auth di laravel. untuk itu mari kita mulai

## Instalasi

1. Petama - tama siapkan project laravel

```php
laravel new auth
```

2. Install package laravel/ui 

```php
composer require laravel/ui
```

3. Jika instalasi sudah selesai maka akan muncul artisan command baru yaitu

```php
ui:auth         = Membuat laravel auth beserta view nya
ui:controller   = Membuat laravel auth hanya controllernya saja
```

4. Jika command artisan diatas sudah muncul maka jalankan perintah

```php
php artisan ui bootstrap --auth
```
*Untuk tutorial kali ini saya akan menggunakan bootstrap saja karena saya baru bisa pake itu hehehehe*

5. Jika perintah diatas sudah dieksekusi maka akan muncul folder auth di bagian views dan controller. jika sudah ada maka jalankan perintah

```php
npm install && npm run dev
```

6. Terakhir lakukan migrate database dengan cara

```php
php artisan migrate
```

7. Tunggu proses sampai selesai maka scafolding laravel auth siap digunakan

