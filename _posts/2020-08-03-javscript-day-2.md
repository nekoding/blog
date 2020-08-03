---
layout: article
date: 2020-08-03 20:51:00 +0800
tags:
- tutorial
- javascript
- es6
title: 'Javscript day #2'
key: belajar-javascript
cover: ''

---
# Async dan Sync

Async : proses yang dilakukan oleh sebuah program tidak harus menunggu proses lain selesai

Sync : Proses yang dilakukan oleh program berurutan

## setTimeout

setTimeout digunakan untuk memberikan delay sebelum mengeksekusi sebuah proses.

{% highlight javascript %}

    console.log("Selamat datang!");
    setTimeout( () => {
        console.log("Terima kasih. sampai jumpa.")
    }, 3000)
    console.log("Ada yang bisa dibantu ? ");

{% endhighlight %}

## callback

digunakan untuk menangkap nilai dari sebuah proses async

{% highlight javascript %}

    const masakMie = callback => {
        let finish = null;
        console.log("Sedang merebus mie instan");
        setTimeout(() => {
            finish = "indomie siap dihidangkan";
            callback(finish);
        }, 3000)
    }
    
    masakMie(finish => {
        console.log(mie);
    });

{% endhighlight %}

## Promise

Promise digunakan untuk melakukan penghitungan proses asynchronous.

Promise ada tiga tipe yaitu :

1\. pending ( sedang dalam proses )

2\. resolve ( berhasil )

3\. reject ( gagal )

### then

then digunakan untuk menghandle output dari proses promise baik resolve maupun reject.

tetapi lebih sering digunakan untuk menghandle output dari resolve.

{% highlight javascript %}

    const masakTelur = (resolve, reject) => {
      const adaTelur = false;
    
      if(adaTelur) {
        resolve("Mulai memasak telur");
      } else {
        reject("Ke warung pak john beli telur dulu dah");
      }
    }
    
    const masakMie = resolvedValue => {
      console.log(resolvedValue);
      console.log("Mulai memasak mie instan");
    }
    
    const beliTelur = rejectedValue => {
      console.log(rejectedValue)
      console.log("'Pak beli telur 1Kg'")
    }
    
    let membuatMie = new Promise(masakTelur);
    
    // .then(resolve, reject)
    membuatMie.then(masakMie, beliTelur);

{% endhighlight %}

### catch

catch digunakan untuk menghandle reject dari promise

{% highlight javascript %}

    catch digunakan untuk menghandle reject dari promise
    {% highlight javascript %}
    ``` 
    const masakTelur = (resolve, reject) => {
      const adaTelur = false;
    
      if(adaTelur) {
        resolve("Mulai memasak telur");
      } else {
        reject("Ke warung pak john beli telur dulu dah");
      }
    }
    
    const masakMie = resolvedValue => {
      console.log(resolvedValue);
      console.log("Mulai memasak mie instan");
    }
    
    const beliTelur = rejectedValue => {
      console.log(rejectedValue)
      console.log("'Pak beli telur 1Kg'")
    }
    
    let membuatMie = new Promise(masakTelur);
    membuatMie.then(masakMie).catch(beliTelur);

{% endhighlight %}

### promise chain

Melakukan proses asynchronous secara berantai

{% highlight javascript %}

    const bahan = {
      isKomporSiap : true,
      isTelurAda : true,
      stock: {
        merk: 'indomie',
        jumlah: 3
      }
    }
    
    const getMie = (merk, jumlah) => {
      return new Promise((resolve, reject) => {
        if (jumlah < bahan.stock.jumlah && merk == bahan.stock.merk) {
          resolve('Stock mie tersedia');
        } else {
          reject('Stock mie kurang');
        }
      });
    }
    
    const makeMie = mie => {
      return new Promise((resolve, reject) => {
        if (bahan.isKomporSiap) {
          resolve("Mulai memasak mie");
        } else {
          reject("Gagal memasak mie");
        }
      });
    }
    
    const makeTelur = telur => {
      return new Promise((resolve, reject) => {
        if (bahan.isTelurAda) {
          resolve("Tambahkan telur");
        } else {
          reject("Mie tanpa telur");
        }
      });
    }
    
    const mieTelur = mie => {
      return new Promise(resolve => {
        resolve("Memasak mie + telur selesai");
      })
    }
    
    function start(merk, jumlah) {
      getMie(merk, jumlah)
      .then(makeMie)
      .then(makeTelur)
      .then(mieTelur)
      .then(resolvedValue => {
        console.log(resolvedValue)
      })
      .catch(rejectValue => {
        console.log(rejectValue)
      })
    }
    
    start("indomie", 1);

{% endhighlight %}

### promise all

Melakukan proses asynchronous secara bersamaan

{% hightlight javascript %}

    const sedapKuah = () => {
      return new Promise(resolve => {
        setTimeout(() => {
          console.log("Mie sedap kuah selesai");
        }, 4000)
      })
    }
    
    const indomieGoreng = () => {
      return new Promise(resolve => {
        setTimeout(() => {
          console.log("Mie indomie goreng selesai");
        }, 4000)
      })
    }
    
    const pesanan = [sedapKuah(), indomieGoreng()];
    
    Promise.all(pesanan)
    .then(resolveValue => {
      console.log(resolveValue);
    })

{% endhighlight %}

## Async dan Await

Async : digunakan untuk memberitahu program untuk menjalankan sebuah proses secara asynchronous

Await : Menghentikan program sementara sampai proses asynchronous berhasil mengirimkan nilai

{% highlight javascript %}

    const prosesMasak = () => {
      let siap = true;
      return new Promise((resolve, reject) => {
        setTimeout(() => {
          if(siap) {
            resolve("Mulai memasak");
          } else {
            reject("Gagal memasak");
          }
        }, 4000)
      });
    }
    
    // Tanpa Async dan Await
    function buatMiee() {
      prosesMasak()
      .then(proses => {
        console.log(proses)
      })
    }
    
    // Async dan Await
    async function buatMie() {
      let start = await prosesMasak();
      console.log(start);
    }
    
    buatMiee();
    buatMie();

{% endhighlight %}