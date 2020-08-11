---
tags:
- tutorial
- codeigniter
- php
layout: article
title: 'Mengatasi error undefined locale CI4'
date: 2020-08-11 12:04:00 +0800
key: mengatasi-error-undefined-locale-ci4
---

# Cara mengatasi undefined locale di CI4
Jika pertama kali melakukan run 

```php
php spark serve
```
dan bertemu error seperti ini :

```php
PHP Fatal error:  Uncaught Error: Call to undefined function CodeIgniter\locale_set_default() in ...
```
maka cara mengatasinya adalah pastikan ekstensi **php intl** sudah terpasang di dalam sistem ( jika menggunakan linux ) atau jika menggunakan XAMPP maka edit bagian php.ini lalu uncomment / hapus tanda ; di bagian :

```
extension=intl
```

oke sekian.
