# Jarkom_Modul2_Lapres_A12

- Achmad Sofyan Pratama (05111840000061)
- Oktarizka Asviananda Nursanty (05111840000156)

## SOAL ##
Kalian diminta untuk membuat sebuah website utama dengan (1) alamat http://semeruyyy.pw yang
memiliki (2) alias http://www.semeruyyy.pw, dan (3) subdomain http://penanjakan.semeruyyy.pw
yang diatur DNS-nya pada MALANG dan mengarah ke IP Server PROBOLINGGO serta dibuatkan (4)
reverse domain untuk domain utama. Untuk mengantisipasi server dicuri/rusak, Bibah minta dibuatkan
(5) DNS Server Slave pada MOJOKERTO agar Bibah tidak terganggu menikmati keindahan Semeru
pada Website. Selain website utama Bibah juga meminta dibuatkan (6) subdomain dengan alamat
http://gunung.semeruyyy.pw yang didelegasikan pada server MOJOKERTO dan mengarah ke IP
Server PROBOLINGGO. Bibah juga ingin memberi petunjuk mendaki gunung semeru kepada anggota
komunitas sehingga dia meminta dibuatkan (7) subdomain dengan nama
http://naik.gunung.semeruyyy.pw, domain ini diarahkan ke IP Server PROBOLINGGO.
Setelah selesai membuat keseluruhan domain, kamu diminta untuk segera mengatur web server. (8)
Domain http://semeruyyy.pw memiliki DocumentRoot pada /var/www/semeruyyy.pw. Awalnya web
dapat diakses menggunakan alamat http://semeruyyy.pw/index.php/home. Karena dirasa alamat urlnya
kurang bagus, maka (9) diaktifkan mod rewrite agar urlnya menjadi http://semeruyyy.pw/home.
(10) Web http://penanjakan.semeruyyy.pw akan digunakan untuk menyimpan assets file yang

memiliki DocumentRoot pada /var/www/penanjakan.semeruyyy.pw dan memiliki struktur
folder sebagai berikut:
/var/www/penanjakan.semeruyyy.pw

/public/javascripts
/public/css
/public/images
/errors

(11) Pada folder /public dibolehkan directory listing namun untuk folder yang berada di dalamnya
tidak dibolehkan. (12) Untuk mengatasi HTTP Error code 404, disediakan file 404.html pada
folder /errors untuk mengganti error default 404 dari Apache. (13) Untuk mengakses file assets
javascript awalnya harus menggunakan url http://penanjakan.semeruyyy.pw/public/javascripts.
Karena terlalu panjang maka dibuatkan konfigurasi virtual host agar ketika mengakses file assets
menjadi http://penanjakan.semeruyyy.pw/js.
Untuk web http://gunung.semeruyyy.pw belum dapat dikonfigurasi pada web server karena
menunggu pengerjaan website selesai. (14) sedangkan web http://naik.gunung.semeruyyy.pw
sudah bisa diakses hanya dengan menggunakan port 8888. DocumentRoot web berada pada
/var/www/naik.gunung.semeruyyy.pw. Dikarenakan web http://naik.gunung.semeruyyy.pw
bersifat private (15) Bibah meminta kamu membuat web http://naik.gunung.semeruyyy.pw agar
diberi autentikasi password dengan username “semeru” dan password “kuynaikgunung” supaya
aman dan tidak sembarang orang bisa mengaksesnya.
Saat Bibah mengunjungi IP PROBOLINGGO, yang muncul bukan web utama
http://semeruyyy.pw melainkan laman default Apache yang bertuliskan “It works!”. (16) Karena
dirasa kurang profesional, maka setiap Bibah mengunjungi IP PROBOLINGGO akan dialihkan
secara otomatis ke http://semeruyyy.pw. (17) Karena pengunjung pada
/var/www/penanjakan.semeruyyy.pw/public/images sangat banyak maka semua request gambar
yang memiliki substring “semeru” akan diarahkan menuju semeru.jpg.

## JAWAB ##
Sebelum mulai menjawab, lakukan dulu langkah-langkah yang ada di modul pengenalan UML, baru lanjut menjawab soal.

**1. Membuat website utama dengan alamat http://www.semerua12.pw**

Pertama, buat topologi kemudian di bash dengan ```bash topologi2.sh```
<p align ="center"><img width="500" src="https://user-images.githubusercontent.com/62512432/98713601-662c4a80-23ba-11eb-906d-b33057087c6a.png"></p>

Kemudian login semua UML dengan username= ```root``` dan password= ```praktikum``` dan pada Server Malang, dilakukan update dan instalasi bind9 dengan cara
```
apt-get update
apt-get install bind9 -y
```
Kemudian untuk membuat domain, isikan konfigurasi domain semerua12.pw pada Server Malang dengan syntax
```
zone "semerua12.pw" {
	type master;
	file "/etc/bind/jarkom/semerua12.pw";
};
```
<p align ="center"><img width="500" src="https://user-images.githubusercontent.com/62512432/98727942-549f6e80-23cb-11eb-87f6-478f1f3914d4.png"></p>

Lalu buat folder jarkom dengan ```mkdir /etc/bind/jarkom``` dan copykan file ```db.local``` pada path ```/etc/bind``` ke dalam folder jarkom dengan ```cp /etc/bind/db.local /etc/bind/jarkom/semerua12.pw``` dan edit file semerua12.pw pada Server Malang ```nano /etc/bind/jarkom/semerua12.pw```

<p align ="center"><img width="500" src="https://user-images.githubusercontent.com/62512432/98716894-e359be80-23be-11eb-8103-699c5b79794b.png"></p>

**2. Membuat alias http://www.semerua12.pw**

Tambahkan isian konfigurasi sesuai dengan gambar dibawah, kemudian lakukan restart bind9 seperti nomor 1

<p align ="center"><img width="500" src="https://user-images.githubusercontent.com/62512432/98723557-228b0e00-23c5-11eb-8b9b-cc3850242afe.png"></p>

Kemudian untuk memeriksa benar atau tidak, lakukan ```ping semerua12.pw``` pada Klien Gresik dan Sidoarjo

Gresik :

<p align ="center"><img width="500" src="https://user-images.githubusercontent.com/62512432/98724429-53b80e00-23c6-11eb-9230-ff50377e91ba.png"></p>

Sidoarjo :

<p align ="center"><img width="500" src="https://user-images.githubusercontent.com/62512432/98724557-8235e900-23c6-11eb-8230-6f616eb96ce8.png"></p>

**3. Membuat subdomain http://penanjakan.semerua12.pw yang diatur DNSnya pada MALANG dan mengarah ke IP PROBOLINGGO**

Edit isi file semerua12.pw dan tambahkan subdomain ```penanjakan.semerua12.pw``` yang mengarah ke IP Probolinggo dari IP Malang

<p align ="center"><img width="500" src="https://user-images.githubusercontent.com/62512432/98724700-b3aeb480-23c6-11eb-94cb-f814aca9b427.png"></p>

Lalu restart bind9 dan ping subdomain pada Klien Gresik dan Sidoarjo seperti nomor 2

**4. Membuat reverse domain untuk domain utama**

Pertama, buka ```nano /etc/bind/named.conf.local``` dan tambahkan konfigurasi seperti gambar dibawah ini

<p align ="center"><img width="500" src="https://user-images.githubusercontent.com/62512432/98726014-7e0acb00-23c8-11eb-9750-18db309c72b9.png"></p>

kemudian di restart bind9 dan periksa pada Klien Gresik dan Sidoarjo dengan cara
```
apt-get update
apt-get install dnsutils

host -t PTR 10.151.73.106
```

**5. Membuat DNS Server Slave pada MOJOKERTO**

Pada Server Malang, tambahkan syntax seperti pada gambar dibawah ini

<p align ="center"><img width="500" src="https://user-images.githubusercontent.com/62512432/98727744-ff635d00-23ca-11eb-8ca8-a68711565165.png"></p>

Lalu restart bind9 seperti nomor-nomor sebelumnya. Kemudian pada Server Mojokerto, lakukan update dan install bind9. Setelah selesai, edit isi file ```/etc/bind/named.conf.local``` sesuai dengan gambar dibawah

<p align ="center"><img width="500" src="https://user-images.githubusercontent.com/62512432/98728533-37b76b00-23cc-11eb-9752-d850b6d6ca25.png"></p>

Lalu restart bind9. Untuk testing, matikan bind9 pada Server Malang dengan cara ```service bind9 stop```. Setelah itu, pastikan nameserver pada klien sudah mengarah pada Server Malang dan Server Mojokerto dengan memasukkan IP Malang dan IP Mojokerto kedalam ```/etc/resolv.conf```

Gresik :

<p align ="center"><img width="500" src="https://user-images.githubusercontent.com/62512432/98729003-cfb55480-23cc-11eb-8270-520b3308ec34.png"></p>

Sidoarjo :

<p align ="center"><img width="500" src="https://user-images.githubusercontent.com/62512432/98728896-ad233b80-23cc-11eb-9d53-e209eb71719e.png"></p>

**6. Membuat subdomain dengan alamat
http://gunung.semeruyyy.pw yang didelegasikan pada server MOJOKERTO dan mengarah ke Server PROBOLINGGO**

Pertama, buka file semerua12.pw pada Malang, kemudian tambahkan seperti yang ada pada gambar 

<p align ="center"><img width="500" src="https://user-images.githubusercontent.com/62512432/99185534-06002480-277d-11eb-8a58-d343c84079cc.png"></p>

Kemudian edit file ```/etc/bind/named.conf.options``` pada Server Malang dan tambahkan isi seperti gambar dibawah

<p align ="center"><img width="500" src="https://user-images.githubusercontent.com/62512432/99185578-59727280-277d-11eb-8f16-b4fc4e38adf8.png"></p>

Lalu restart bind9. Selanjutnya pada Server Mojokerto, edit isi file ```/etc/bind/named.conf.options``` dengan menambahkan seperti pada gambar dibawah

<p align ="center"><img width="500" src="https://user-images.githubusercontent.com/62512432/99185778-a6a31400-277e-11eb-84e4-d25d7800fc0e.png"></p>

Lalu edit file ```/etc/bind/named.conf.local``` seperti dibawah

<p align ="center"><img width="500" src="(https://user-images.githubusercontent.com/62512432/99185826-e1a54780-277e-11eb-84af-2b7b1d642b97.png"></p>

Lalu buat direktori dengan delegasi dan copy ```db.local``` ke direktori delegasi dan beri nama ```gunung.semerua12.pw``` dan edit filenya seperti gambar dibawah

<p align ="center"><img width="500" src="https://user-images.githubusercontent.com/62512432/99186070-49a85d80-2780-11eb-9cc4-9afd31fb70bd.png"></p>

Lalu restart bind9 seperti nomor-nomor sebelumnya

**7. Membuat subdomain dengan nama http://naik.gunung.semeruyyy.pw, domain ini diarahkan ke IP Server PROBOLINGGO**

Buka file gunung.semerua12.pw dan edit isinya seperti gambar dibawah 

<p align ="center"><img width="500" src="https://user-images.githubusercontent.com/62512432/99185904-55475480-277f-11eb-8ca5-c346085d032c.png"></p>

Kemudian restart bind9 dan lakukan testing pada klien Gresik dan Sidoarjo

**8. Mengatur webserver domain http://semerua12.pw memiliki DocumentRoot pada /var/www/semerua12.pw.**

Pertama, pindah ke directory ```etc/apache2/sites-available``` pada Server Probolinggo dan buka file semerua12.pw lalu tambahkan seperti gambar dibawah

<p align ="center"><img width="500" src="https://user-images.githubusercontent.com/62512432/99186265-bd973580-2781-11eb-8917-a8e29e3f7871.png"></p>

Kemudian, gunakan perintah ```a2ensite semerua12.pw```, selanjutnya gunakan perintah ```service apache2 restart``` untuk merestart apache. Setelah itu, pindahkan directory ke ```/var/www``` dan download file zip pada ```wget 10.151.36.202/semeru.pw.zip``` lalu unzip file dan diubah namanya menjadi semerua12.pw. Terakhir, buka browser untuk mengakses web ```http://semerua12.pw```. Berikut hasilnya

<p align ="center"><img width="500" src="https://user-images.githubusercontent.com/62512432/99186382-7fe6dc80-2782-11eb-9311-6ceee069e027.png"></p>
