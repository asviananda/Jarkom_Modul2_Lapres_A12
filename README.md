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

**1. Memmbuat website utama dengan alamat http://www.semerua12.pw***

Pertama, buat topologi kemudian di bash dengan ```bash topologi2.sh```
<p align ="center"><img width="500" src="https://user-images.githubusercontent.com/62512432/98713601-662c4a80-23ba-11eb-906d-b33057087c6a.png"></p>
Kemudian login semua UML dengan username=```root``` dan password=```praktikum``` dan pada IP Malang, dilakukan update dan instalasi bind9 dengan cara
```
apt-get update
apt-get install bind9 -y
```
Kemudian untuk membuat domain, isikan konfigurasi domain semerua12.pw pada IP Malang dengan syntax
```
zone "semerua12.pw" {
	type master;
	file "/etc/bind/jarkom/semerua12.pw";
};
```
<p align ="center"><img width="500" src="https://user-images.githubusercontent.com/62512432/98716432-236c7180-23be-11eb-8c7f-06e807fbefb5.png"></p>
Lalu buat folder jarkom dengan ```mkdir /etc/bind/jarkom``` dan copykan file ```db.local``` pada path ```/etc/bind``` ke dalam folder jarkom dengan ```cp /etc/bind/db.local /etc/bind/jarkom/semerua12.pw``` dan edit file semerua12.pw pada IP Malang ```nano /etc/bind/jarkom/semerua12.pw```
<p align ="center"><img width="500" src="https://user-images.githubusercontent.com/62512432/98716894-e359be80-23be-11eb-8103-699c5b79794b.png"></p>
