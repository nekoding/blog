---
tags:
- tutorial
- vuejs
layout: article
title: 'Belajar vue js'
date: 2020-08-30 09:00:00 +0800
key: belajar-vue-js
---

# Intro
Assalamualaikum we.wb
Selamat pagi, kali ini saya akan sedikit memposting soal belajar vuejs. Postingan ini juga saya gunakan untuk mengasah pemahaman saya tentang vuejs. Jadi, jika saya salah tulis mungkin bisa dikoreksi.

# Perkenalan 
>Apa itu vuejs ?   

dihalam resminya vuejs mengatakan bahwa  

>Vue (pronounced /vjuː/, like view) is a progressive framework for building user interfaces. Unlike other monolithic frameworks, Vue is designed from the ground up to be incrementally adoptable. The core library is focused on the view layer only, and is easy to pick up and integrate with other libraries or existing projects. On the other hand, Vue is also perfectly capable of powering sophisticated Single-Page Applications when used in combination with modern tooling and supporting libraries.  

Kalau saya terjemahin kurang lebih begini : Vue js adalah sebuah progressive framework yang menawarkan kemudahan dalam membangun user interfaces.

# Ngoding
Untuk tahap ngoding nya saya bagi menjadi beberapa tahap yaitu :  
1. Integrasi VueJS dengan cdn
2. VueJS dasar
    - Instansiasi VueJS ke dalam dokumen HTML
    - Menghubungkan element input HTML
    - Looping
    - Event Listener
    - Methods
    - Kondisional
    - Membuat attribut HTML dinamis
    - Membuat class HTML dinamis
    - Computed

## Integrasi vuejs dengan CDN
Untuk integrasinya sebenarnya vuejs menawarkan 3 metode yaitu dengan CDN, NPM, dan Vue CLI. tapi untuk disini saya memakai CDN saja karena saya tidak begitu jago dalam memanfaatkan NPM dan Vue CLI. Baik kalau begitu untuk instalasi dengan CDN nya bisa langsung kesini jika ingin menggunakan versi terbarunya: 
[Vue CDN](https://vuejs.org/v2/guide/installation.html#CDN)  
  
atau bisa juga dengan mengitegrasikan script dibawah ini jika ingin menyesuaikan dengan versi ketika postingan ini dibuat.

```js
<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
```

Untuk script diatas saya menggunakan versi mode development nya karena ketika salah tulis syntax maka akan menampilkan error log di bagian console.

## VueJS dasar
Jika sudah mengintegrasikan script diatas dibagian tag `body` maka selanjutnya kita bisa masuk ke tutorial.

### Instansiasi VueJS ke dalam dokumen HTML
untuk cara instansiasi Vue js cukup sederhana yaitu sebagai berikut :

```html
<div id="app">
    {{ intro }}
</div>

<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>

<script type="text/javascript">
    new Vue({
        el: "#app",
        data : {
            "intro" : "Hello World"
        }
    })
</script>
```

Untuk sekarang saya akan melakukan *breakdown* di dalam tag ini :

```html
<div id="app">
    {{ intro }}
</div>
```

1. Disini attribut `id` diperlukan sebagai selector di vuejs. nantinya semua element yang berada di dalam tag dengan attribut `id="app"` bisa mengimplementasikan vuejs.

2. Untuk menampilkan data di vue js menggunakan template engine. untuk gaya penulisannya mirip dengan milik blade di laravel yaitu menggunakan kurung kurawal 2x  
`{{ data }}`   
variabel yang diapit dialam kurung kurawal akan ditampilkan ke dalam document HTML.

Selanjtunya saya akan melakukan *breakdown* ke dalam tag ini :

```html
<script type="text/javascript">
    new Vue({
        el: "#app",
        data : {
            "intro" : "Hello World"
        }
    })
</script>
```

1. `new Vue({})` : digunakan untuk melakukan instansiasi
2. `el` : digunakan untuk menyeleksi bagian mana yang akan menggunakan vue js. dikarenakan disini saya menyeleksi id `#app` maka semua yang ada didalam tag app bisa menjalankan fungsi milik vue js.
3. `data` : digunakan untuk menyimpan nilai variabel di dalam vue js. model penulisannya mirip seperti `JSON` jadi bukan menggunakan simbol sama dengan `(=)` melainkan simbol titik dua `(:)`. atau bisa dibilang key-value.

### Menghubungkan element input HTML
Salah satu keuntungan menggunakan vue js yaitu kita bisa menghubungkan element input dengan element penampil data dengan mudah. Jika menggunakan javascript murni mungkin seperti ini :

```html
<div>
    <input type="text" id="inputan">
    <p id="result"></p>
</div>

<script>
    const inputan = document.querySelector("#inputan");
    const result = document.querySelector("#result");
    inputan.addEventListener("keyup", function (event) {
        result.innerHTML = inputan.value;
    })
</script>
```

Mungkin jika kalian punya versi yang lebih baiknya dari kode diatas mungkin bisa komen dibawah. Jadi kode diatas itu cara kerjanya ketika user menginputkan data kedalam element input dengan `id="inputan"` maka data tadi akan ter-print kedalam tag `p` dengan `id="result"`. sekarang kita coba menggunakan versi vuejs nya.

```html
<div id="app">
    <input type="text" v-model="whatever">
    <p>{{ whatever }}</p>
</div>

<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>

<script>
    new Vue({
        el: "#app",
        data: {
            whatever: ""
        }
    });
</script>
```

kode diatas sama saja fungsinya seperti kode sebelumnya yaitu ketika user menginputkan data maka data yang diinputkan akan terprint dengan sendirinya. dari kedua contoh kode diatas bisa dibandingkan, ketika menggunakan javascript murni kita perlu melakukan seleksi tag element di kedua tempat yaitu di bagian input dan result sedangkan ketika menggunakan vue js kita diberikan kemudahan dengan memasangkan attribut `v-model:` di bagian tag inputan saja.  
Fungsi dari `v-model:` adalah menghubungkan element yang dipasangkan dengan variabel yang ada dibagian `data` di dalam Vue. di contoh tersebut saya menghubungkan `v-model` dengan data `whatever`.

### Looping
Looping / perulangan di dalam javascript dapat digunakan untuk menampilkan data yang isinya lebih dari 1. contoh nya seperti ketika mengambil data dari API yang isinya berupa data JSON terus kita ingin menampilkannya dalam bentuk list. untuk contoh kode dalam javascript murni nya kurang lebih seperti ini :

```html
<div>
    <ol id="list">
    </ol>
</div>

<script>
    let mobil = [
        {
            merk : "Toyota",
            tipe : "City car"
        },
        {
            merk : "Honda",
            tipe : "City car"
        }
    ];

    const list = document.querySelector("#list");
    mobil.forEach(function (item) {
        list.innerHTML += `<li><ul><li>${item.merk}</li><li>${item.tipe}</li></ul></li>`;
    });
</script>
```

Kode diatas berfungsi untuk menampilkan data dari variabel mobil yang isinya ada merk dan tipe. di dalam javascriptnya pertama - tama saya menseleksi tag `ol` yang digunakan sebagai penanda. kemudian saya melakukan looping dengan `forEach` di dalam array mobil yang nantinya isinya di sisipkan ke dalam tag `ol` tadi. Penggunaan `+=` di bagian `list.innerHTML` digunakan untuk menambahkan data tanpa menghapus data sebelumnya. jika hanya menggunakan simbol `=` maka data yang ditampilkan hanya yang bagian terakhir saja.

Sekarang kita coba menggunakan vue js.

```html
<div id="app">
    <ol>
        <li v-for="item in items" :key="item.merk">
            <ul>
                <li>Merk : {{item.merk}}</li>
                <li>Tipe : {{item.tipe}}</li>
            </ul>
        </li>
    </ol>
</div>

<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
<script>
    let mobil = [
        {
            merk : "Toyota",
            tipe : "City car"
        },
        {
            merk : "Honda",
            tipe : "City car"
        }
    ];

    new Vue({
        el: "#app",
        data : {
            items : mobil
        }
    });
</script>
```
di dalam vue js kita bisa menggunakan attribut `v-for:` untuk melakukan perulangan. peletakkan attribut `v-for` sendiri berada di bagian element yang ingin ditampilkan. contoh kasus :

**Kasus 1 :**  

```html
<div id="app">
    <ul>
        <li v-for="item in items">{{item}}</li>     
    </ul>
</div>
```

maka looping akan berada di dalam tag `li` yang ada dibagian `ul`  

**Kasus 2 :**  

```html
<div id="app">
    <ul>
        <li>
            <ol>
                <li v-for="item in items">{{item}}</li>
            </ol>
        </li>    
    </ul>
</div>
```
maka looping akan berada di dalam tag `li` yang ada dibagian `ol`

### Event Listener
Event listener digunakan untuk menhandle interkasi user dengan interface. controh ketika user mengklik tombol maka akan menampilkan notifikasi. untuk penggunaan event listener sebenarnya baik dari javascript murni maupun vue js sama - sama sederhana. berikut contoh jika menggunakan javascript murni :

```html
<button onclick="alert('Hi Js')">Hallo Js</button>
```

Contoh diatas adalah versi sederhana untuk melakukan popup alert dengan javascript murni. Selanjutnya kita akan menggunakan versi vue js nya.

```html
<div id="app">
    <button v-on:click="this.alert('hi Vue')">Hallo Vue</button>
</div>

<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
<script>
    new Vue({
        el: "#app",
        data: {

        }
    });
</script>
```

fungsi kode diatas sama saja yaitu menampilkan pop up alert ketika tombol di klik. Penggunaan dari `v-on:click` dapat juga dipersingkat dengan cara menambahkan `@` sebelum event seperti ini contohnya `@click`. penggunaan `this` dibagian alert milik vue digunakan sebagai penanda untuk memanggil fungsi asli milik javascript karena jika tidak ditambahkan `this` maka vue akan menjalankan fungsi yang ada dibagian methods. untuk contoh penggunaan event lainnya bisa kunjungi dokumentasi resmi milik vue js nya di (https://vuejs.org/v2/guide/events.html)[https://vuejs.org/v2/guide/events.html]

### Methods
Di vue js ada yang namanya method yang dapat digunakan untuk melakukan manipulasi perubahan data dan menyimpan fungsi - fungsi tertentu. Kalau di javascript mungkin methods bisa di samakan seperti `function`. berikut contoh penggunaan methods di VuesJs. 

```html
<div id="app">
    <button v-on:click="sayHi('john')">Hi</button>
</div>

<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
<script>
    new Vue({
        el: "#app",
        data: {
        },
        methods: {
            sayHi : function (name) {
                return alert('Hallo ' + name);
            }
        }
    });
</script>
```

Fungsi dari kode diatas sangatlah sederhana yaitu ketika tombol Hi ditekan maka akan menampilkan pop up alert yang berisi 'Hallo john'.

### Kondisional
Di vue js ada juga pengkondisian. Pengkondisian ini berfungsi untuk melakukan operasi logika. contoh kasus : ketika tombol open dibuka maka akan menampilkan sebuah text. untuk kode nya sebagai berikut :

```html
<div id="app">
    <button v-on:click="toggle(true)">Open</button>
    <button v-on:click="toggle(false)">Close</button>
    <p v-if="open == true">Halo</p>
</div>

<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
<script>
    new Vue({
        el: "#app",
        data: {
            open: false
        },
        methods: {
            toggle: function (event) {
                this.open = event;
            }
        }
    });
</script>
```

Kode diatas memanfaatkan pengkodisian untuk memunculkan dan menyembunyikan tag `p`.

### Membuat attribut HTML dinamis
Di vue js ada yang namanya `v-bind` yang dapat membuat attribut dinamis yang dapat digunakan untuk melakukan penambahan attribut html yang hanya muncul ketika suatu kondisi. Sebagai contoh ketika kita menginputkan data kurang dari 5 huruf maka tombol save nya akan terdisable sementara. Penggunaan ini sangat membantu jika harus berurusan dengan attribut html seperti `checked`, `disabled` , dll. contoh penggunaan :

```html
<div id="app">
    <input type="text" v-model="name">
    <button v-bind:disabled="name.length < 5">Save</button>

    <ul>
        <li v-for="item in belanja">
            <input type="checkbox" :checked="item.status == true"> {{ item.barang }}
        </li>
    </ul>
</div>

<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
<script>

    let belanja = [
        {
            'barang' : 'wortel',
            'status' : true
        },
        {
            'barang' : 'tomat',
            'status' : false
        }
    ]

    new Vue({
        el: "#app",
        data: {
            name: "",
            belanja : belanja
        }
    });
</script>
```
Disitu ada dua contoh yang pertama adalah penggunaan attribut disabled dan yang kedua adalah penggunaan attribut checked. penggunaan `v-bind` dapat dipersingkat dengan menambahkan simbol titik dua `(:)` sebelum nama attributnya.

### Membuat class HTML dinamis
Penggunaan class dinamis sama seperti penggunaan attribut yaitu dengan menambahkan simbol titik dua `(:)` diikuti dengan `class` atau seperti ini `:class`. Penggunaan class dinamis sangat membantu apabila kita ingin melakukan styling css di dalam sebuah element. sebut saja jika kita menginputkan data kurang dari 10 huruf maka tombol save nya akan berwarna merah dan terdisabled. untuk contoh kodingannya seperti ini :  

```html
<div id="app">
    <div class="container">
        <div class="form-group row mt-4">
            <input type="text" class="form-control col-md-3" v-model="name">
            <button class="btn btn-primary ml-2" :disabled="name.length < 10" :class="{'btn-danger' : name.length < 10}">Save</button>
        </div>
    </div>
</div>

<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
<script>
    new Vue({
        el: "#app",
        data: {
            name: ""
        }
    });
</script>
```

Penggunaan class ada 2 tipe yaitu object dan array.

1. Object : menggunakan kurung kurawal `{}`. biasanya digunakan jika pengkondisiannya sederhana.  
contoh : 

```html 
<li :class="{strikeout : item.purchased}">{{ item }}</li>
```

*Class strikeout akan tampil jika `item.purchased` berstatus `true`*

2. Array : menggunakan kurung siku `[]`. biasany digunakan jika pengkondisiannya kompleks / butuh kontrol lebih.

```html 
<li :class="[item.purchased ? 'strikeout' : '']">{{ item }}</li>
```

*Class strikeout akan tampil jika `item.purchased` berstatus `true`*

### Computed
Di vue js ada fungsi yang namanya computed. menurut yang saya tangkap Computed digunakan untuk melakukan perubahan dan manipulasi data yang tetap tersinkron dengan data yang direferensikan. atau sederhananya method computed **terpanggil** ketika ada perubahan terhadap data yang direferensikan. Berbeda dengan methods yang terpanggil ketika ada sebuah event yang menggunakan fungsi tersebut. untuk contohnya seperti ini :

```html
<div id="app">
    <div class="container">
        <input type="text" class="form-control" v-model="word">
        <button class="btn btn-primary">
            {{ wordCount }}
        </button>
    </div>
</div>

<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
<script>
    new Vue({
        el: "#app",
        data: {
            word: ''
        },
        computed: {
            wordCount() {
                return this.word.length
            }
        }
    });
</script>
```

sebenarnya ada 1 lagi yaitu watchers cuma saya agak bingung perbedaan antara watchers dan computed. jadi cukup sekian dulu postingan dari saya. jika ada salah dari postingan saya silahkan berkomentar. 
Wassalamualaikum wr.wb