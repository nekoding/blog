---
tags:
- tutorial
- composer
- php
layout: article
title: 'Mengatasi composer error environment'
date: 2020-08-10 16:33:00 +0800
key: memperbaiki-composer-home
---

# Cara mengatasi composer error

Jika bertemu dengan error seperti ini 

```
The HOME or COMPOSER_HOME environment variable must be set for 
composer to run correctly
```

lakukan :
```
export HOME="/home/username"

atau

export COMPOSER_HOME="$HOME/.config/composer";
```

> Referensi :
> https://laracasts.com/discuss/channels/laravel/composer-install-not-working-through-php?page=1
> https://stackoverflow.com/questions/47195283/successful-install-of-composer-but-message-shows-the-home-or-composer-home-env
