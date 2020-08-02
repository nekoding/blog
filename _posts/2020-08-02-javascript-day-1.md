---
tags:
- tutorial
- javascript
- es6
layout: article
title: 'Javascript Day #1'
key: belajar-javascript
date: 
cover: ''

---
# Template Literal

Template literal digunakan untuk _mengembed_ variabel javascript ke dalam string.

Jika sebelumnya menuliskan string di javascript seperti ini :

    const name = "John";
    const email = "johndoe@gmail.com"
    
    console.log("Name : " + name + " Email : " + email);

Maka di ES6 dipermudah dengan cara :

    const name = "John";
    const email = "johndoe@gmail.com"
    
    console.log(`Name : ${name} Email : ${email}`);

> Referensi : 
>
> [https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Template_literals](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Template_literals "Referensi")

# Object 

Untuk memecah object di ES6 ke dalam variabel baru dapat menggunakan tanda kurung kurawal.

    const jusBuah = {
    	rasa: "Apel",
        harga: 40000,
     }
     
     const {rasa, harga} = jusBuah;
     
     console.log(rasa);
     console.log(harga);

Untuk mengganti isian dari sebuah variabel dengan isian dari sebuah object dapat dilakukan dengan cara seperti ini :

    const jusBuah = {
    	rasa: "Apel",
        harga: 40000,
     }
     
     let rasa = "Mangga";
     let harga = 30000;
     
     // overwrite variabel rasa dan harga dengan nilai jusBuah
     ({rasa, harga} = jusBuah)
     
     console.log(rasa);
     console.log(harga);

Jika nama variabel yang digunakan berbeda dengan nama variabel yang ada diobjek dapat menggunakan cara seperti ini :

    const jusBuah = {
    	rasas: "Apel",
      hargas: 40000,
     }
     
     let rasa = "Mangga";
     let harga = 30000;
     
     ({rasas: rasa, hargas: harga} = jusBuah)
     
     console.log(rasa);
     console.log(harga);

Jika ingin mendefinisikan default value dapat dilakukan dengan cara seperti ini :

    const jusBuah = {
    	rasas: "Apel",
      hargas: 40000,
     }
     
     let rasa = "Mangga";
     let harga = 30000;
     
     ({rasas: rasa, hargas: harga, penjual = "Pak John"} = jusBuah)
     
     console.log(rasa);
     console.log(harga);
     console.log(penjual);

# Array

Untuk memecah array ke dalam variabel baru dapat menggunakan cara seperti ini :

    const roti = ["Coklat", "Keju", "Strawberry"];
    
    const [rasaCoklat, rasaKeju, rasaStrawberry] = roti;
    
    console.log(rasaCoklat);
    console.log(rasaKeju);
    console.log(rasaStrawberry);

Untuk mengganti isian dari sebuah variabel dengan isian dari sebuah array dapat dilakukan dengan cara seperti ini :

    const bunga = ["Mawar", "Merah"]
    
    let jenisBunga = "Lavender";
    let warnaBunga = "Biru";
    
    [jenisBunga, warnaBunga] = bunga;
    
    console.log(jenisBunga);
    console.log(warnaBunga);

Selain itu teknik ini juga berguna untuk menukar dua isian variabel yang berbeda.

![](https://www.i-programmer.info/images/stories/BabBag/xorswap/cereal2.jpg)

jika sebelumnya kita butuh variabel tmp untuk menyimpan hasil sementara maka di es6 dapat dilakukan seperti ini :

    let a = 1;
    let b = 2;
    let c = 3;
    let d = 4;
    
    // Tanpa array destructuring assignment
    // Menukar nilai a dengan b
    let tmp = a;
    a = b;
    b = tmp;
    
    console.log(a);
    console.log(b);
    
    // Dengan aray destructing assignment
    // Menukar nilai c dengan d
    [c,d] = [d,c]
    console.log(c);
    console.log(d);

Untuk menambahkan default value ke dalam array dapat dilakukan dengan :

    const warna = ["jingga"];
    
    const [jingga, biru = "biru"] = warna;
    
    console.log(jingga);
    console.log(biru);

# Spread Syntax

spread syntax membuat array dapat diterasi dan ditampilkan seperti string.

    const hewan = ["sapi", "kambing", "kucing", "anjing"];
    console.log(...hewan);
    
    //setara dengan
    console.log(hewan[0], hewan[1], hewan[2], hewan[3]);

Menggabungkan array dengan spread syntax

    const hewan = ["sapi", "kambing", "kucing", "anjing"];
    const hewan2 = ["belalang", "gajah", "singa"];
    
    const kumpulanHewan = [...hewan, ...hewan2];
    console.log(kumpulanHewan);

# Rest syntax

menggabungkan banyak element menjadi 1

    function jumlah(...numbers) {
        let hasil = 0;
        for(let number of numbers) {
            hasil += number
        }
        return hasil;
    }
    
    console.log(jumlah(1,3,5,7,9,11));

> Referensi :
>
> [https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_syntax](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_syntax "https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_syntax")

# Arrow function

Arrow function digunakan untuk mempersingkat penulisan function di javascript. metode ini diperkenalkan di ES6.

    // Tanpa arrow function
    const hello = function(nama) {
      console.log(`Hallo ${nama}, salam kenal`);
    }
    
    
    // Dengan arrow function
    const hi = nama => console.log(`Hallo ${nama}, salam kenal`);
    
    hello('john');
    hi('john');

kedua kode diatas akan menghasilkan output yang sama. contoh penggunaan arrow function lainnya.

    // stored in variable
    const hi = nama => console.log(`Hallo ${nama}, salam kenal`);
    
    hi('john');
    
    // as an argument
    const mobil = ["toyota", "honda", "suzuki"];
    
    mobil.forEach( merk => console.log(`Merk mobil saya adalah ${merk}`));
    
    // stored in object
    const hewan = {
      nama: "Kucing",
      suara: bunyi => console.log(`bunyi suara ${hewan.nama} itu ${bunyi}`)
    }
    
    hewan.suara("Meong");

untuk menghandle multi parameter dapat ditambahkan tanda kurung dan koma.

    // Multiple parameters
    
    const sayHi = (nama, waktu = "pagi") => console.log(`Selamat ${waktu} ${nama}, selamat beraktifitas`);
    sayHi("John", "Sore");

Jika sebelumnya arrow function hanya menampilkan 1 baris kode saja maka jika ingin menampilkan block kode dapat menambahkan kurung kurawal.

    // Multiple parameters + block body
    
    const sayHi = (nama, waktu) => {
      (waktu < 10) ? console.log(`Selamat pagi ${nama}`) : 
      (waktu < 14) ? console.log(`Selamat siang ${nama}`) :
      (waktu < 18) ? console.log(`Selamat sore ${nama}`) :
      console.log(`Selamat malam ${nama}`);
    }
    
    sayHi('john',17);

# Class

Class adalah blueprint/kerangka dari sebuah objek yang akan dibuat. 

![](https://javatutorial.net/wp-content/uploads/2014/11/class-object-featured-image.png)

Seperti gambar diatas class diabaratkan blueprint dari sebuah mobil. entah nanti mobil itu bentuk nya beda - beda tapi kerangkanya tetap sama. Di dalam class variabel disebut sebagai property dan function disebut method/behaviour.

Membuat class di javascript sebelum ada ES6.

    function Mobil(merk, warna) {
      this.merk = merk;
      this.warna = warna;
    } 
    
    Mobil.prototype.info = function() {
      console.log("Merk Mobil : " + this.merk);
      console.log("Warna Mobil : " + this.warna);
    }
    
    var honda = new Mobil('Honda', 'putih');
    honda.info();

Membuat class setelah ada ES6

    class Mobil
    {
      constructor(merk, warna) {
        this.merk = merk;
        this.warna = warna;
      }
    
      info() {
        console.log("Merk Mobil : " + this.merk);
      console.log("Warna Mobil : " + this.warna);
      }
    }
    
    let honda = new Mobil("Honda", "merah");
    honda.info();

### constructor

sebuah method yang akan dijalankan ketika sebuah class diinstansiasi.

    class Mobil
    {
      constructor(merk, warna) {
        this.merk = merk;
        this.warna = warna;
      }
    }
    
    let honda = new Mobil("Honda", "merah");
    console.log(honda.merk);

### getter dan setter

method yang digunakan untuk merubah dan mendapatkan nilai dari sebuah property. untuk property yang digunakan sebagai getter dan setter sebaiknya diawali dengan undescore lalu diikuti nama propertinya. contoh : _warna

    class Mobil
    {
      constructor(merk, warna) {
        this.merk = merk;
        this._warna = warna;
      }
    
      info() {
        console.log(`Merk mobil : ${this.merk} Warna mobil : ${this._warna}`);
      }
    
      get warna() {
        console.log(this._warna);
      }
    
      set warna(value) {
        console.log(`Warna mobil dirubah dari ${this._warna} ke ${value}`);
        this._warna = value;
      }
    }
    
    let suzuki = new Mobil("Suzuki", "putih");
    
    suzuki.info();
    suzuki.warna;
    
    suzuki.warna = "Hitam";
    suzuki.info();
    suzuki.warna;

### Inheritance

Dalam javascript inheritance menggunakan keyword extends.

    class Kendaraan
    {
      constructor(engine, bahanBakar) {
        this.engine = engine;
        this.bahanBakar = bahanBakar;
      }
    
      info() {
        console.log(`Engine : ${this.engine}, Bahan Bakar : ${this.bahanBakar}`);
      }
    }
    
    class Mobil extends Kendaraan
    {
      constructor(engine, bahanBakar, merk, warna) {
        super(engine, bahanBakar);
        this.merk = merk;
        this.warna = warna;
      }
    
      info() {
        super.info();
        console.log(`Merk : ${this.merk}
        Engine : ${this.engine}
        Bahan Bakar : ${this.bahanBakar}
        Warna : ${this.warna}`);
      }
    }
    
    let honda = new Mobil("400HP", "Pertamax", "Honda", "Merah");
    honda.info();

Keyword super digunakan untuk memanggil property/method dari class parent.

### Static function

    class Kendaraan
    {
      constructor(engine, bahanBakar) {
        this.engine = engine;
        this.bahanBakar = bahanBakar;
      }
    
      info() {
        console.log(`Engine : ${this.engine}, Bahan Bakar : ${this.bahanBakar}`);
      }
    }
    
    class Mobil extends Kendaraan
    {
      constructor(engine, bahanBakar, merk, warna) {
        super(engine, bahanBakar);
        this.merk = merk;
        this.warna = warna;
      }
    
      info() {
        super.info();
        console.log(`Merk : ${this.merk}
        Engine : ${this.engine}
        Bahan Bakar : ${this.bahanBakar}
        Warna : ${this.warna}`);
      }
    }
    
    class pimpMyRide
    {
      static pimpIt(...kendaraan)
      {
        kendaraan.forEach( mobil => {
          console.log(`Mobil ${mobil.merk} sedang dimodif`)
        })
      }
    }
    
    let honda = new Mobil("400HP", "Pertamax", "Honda", "Merah");
    let suzuki = new Mobil("400HP", "Pertamax", "Suzuki", "Merah");
    
    pimpMyRide.pimpIt(honda,suzuki)