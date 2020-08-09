---
tags:
- tutorial
- javascript
- es6
layout: article
title: 'Javascript Dasar #1'
date: 2020-08-09 07:28:00 +0800
key: belajar-javascript
---

# Variabel
variabel digunakan untuk menyimpan sebuah data. karena javascript merupakan Unscripted Dynamic Language maka kita tidak perlu mendefinisikan tipe data di tiap variabel.
> Disarankan menggunakan model penulisan camel case

contoh : 

```javascript
var hargaGula = 10000;
```

# Operator

Binary : 
2 + 3 : 2 dan 3 sebagai operand, + sebagai operator

Unary :
x++ : x sebagai operand, ++ sebagai operator

Operator di javascript ada beberapa yaitu :

## Aritmatika
```javascript
*
/
%
+
-
```

## Assignment
```javascript
=
+=
-=
/=
*=
%=
```

# Komparasi
```javascript
==
===
```

# Increment dan Decrement

digunakan untuk mengurangi nilai variabel dengan 1. biasanya digunakan di dalam looping

## Increment
di wakilikan dengan operator ++

contoh :
```javascript
x++
++x
```
## Decrement
di wakilkan dengan operator --

contoh :
```javascript
x--
--x
```

# Object
menyimpan data berdasarkan kata kunci. ada beberapa cara penulisan object di javascript.

## normal
```javascript
var car = {
    roda: 4,
    warna: "merah"
}
```

## dot notation
```javascript
var car = {};
car.roda = 4;
car.warna = "merah";
```
## braket notation
```javascript
var car = {};
car['roda'] = 4;
car['warna'] = "merah";
```

# Array
menyimpan data secara bertumpuk dan dapat diakses menggunakan index. index array di javascript dimulai dari 0.

contoh :
```javascript
var nilaiUjian = [80,90,100];
console.log(nilaiUjian[0]);
```

## method dan properties di dalam array

### Method
array.pop() -> Mengeluarkan array paling terakhir
array.push() -> Memasukkan array di paling terakhir
array.shift() -> Mengeluarkan array paling depan
array.unshift() -> Memasukkan array paling depan

### Properties
array.length -> Menghitung panjang array

## concat di dalam array
menggabungkan 2 array.

contoh :
```javascript

var heroDC = ['superman', 'batman'];
var heroMarvel = ['spiderman', 'iron man'];

var allStarHero = heroDC.concat(heroMarvel);
```

## Reverse array
Membalik urutan array berdasarkan index.

```javascript
var allStarHeroReverse = allStarHero.reverse();
```

## Sort
Mengurutkan array berdasarkan abjad ( jika datanya berupa string )  
apabila datanya angka tambahakan :

### Ascending
```javascript
array.sort(function(a,b) { 
    return a-b
})
```

### Descending
```javascript
array.sort(function(a,b){
    return b-a
})
```

## Slice

```javascript
var x = [1,2,3,4,5];
x.slice(1,3);
```

# Function
Kumpulan dari suatu statement yang menjalankan suatu tugas. function yang baik adalah yang hanya menjalankan 1 tugas saja.  

## Cara penulisan

### Deklarasi
```javascript
function hello() {
    return "hello";
}
```

### Ekspresi
```javascript
var hello = function () {
    return "hello";
}

// atau bisa juga dengan arrow function

var hello = () => {
    return "hello";
}
```

## IIFE 
IIFE atau Immediately Invoke Function Expression  

```javascript
var hello = (function() {
    return "hello";
}());
```

### Anonymous IIFE
```javascript
(function(){
    return "hello";
}());
```

# Looping
Perulangan  

## For loop
```javascript

for(let i=0; i<10; i++) {
    console.log(i);
}

var animals = ['singa', 'kucing'];
for(let animal of animals) {
    console.log(animal);
}
```

## While 

### do while
lakukan setidaknya 1 kali sebelum looping

```javascript
var a = 1;
do{
    console.log(a);
    a++;
}while(a<100;
```

### while
lakukan looping jika kondisinya benar

```javascript
var a = 0;
while(a < 10) {
    console.log(a);
    a++;
}
```

# Regex
Regular Expression : Digunakan untuk mencari dengan pattern yang ditentukan.

## Patern dan Modifiers

```javascript
var regex = /ou/i;

// regex : /ou/i
// pattern : ou
// modifiers : i ( case insensitive )
```

## match
```javascript
var alphabet = 'abcde';
var regex = /abc/i;

var regexAlphabet = alphabet.match(regex).length
```

> referensi regex : [https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_Expressions](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_Expressions "Referensi")


