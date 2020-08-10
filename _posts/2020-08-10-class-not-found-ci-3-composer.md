---
tags:
- tutorial
- composer
- php
layout: article
title: 'Mengatasi missing class CI3 karena package composer'
date: 2020-08-10 16:44:00 +0800
key: mengatasi-missing-class-ci3
---

# Cara mengatasi 
Jika menemui missing class error di CI3 sewaktu di deploy ke hosting. maka pastikan composer nya jalan / lakukan

```
composer update
composer dump-autoload
```

jika masih tetap coba tambahkan line dibawah di file /application/config/config.php

```php
$config['composer_autoload'] = TRUE;
$config['composer_autoload'] = FCPATH . 'vendor/autoload.php';
```

> Tidak direkomendasikan : untuk melakukan composer dump-autoload dibutuhkan akses shell ke server. jika tidak dapat akses ke ssh-nya / ssh-nya sedang error coba lakukan backconnect sendiri ke server dengan mengupload backdoor lalu spawn tty shell nya.

