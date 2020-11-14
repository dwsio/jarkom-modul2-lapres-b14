# **Jarkom_Modul2_Lapres_B14**
### Anggota Kelompok:
- IQBAAL PRATAMA PUTRA  (05111840000021)
- DWI WAHYU SANTOSO     (05111840000121)

<img src="images/topologi.PNG" width="500">

## Topologi:
- SURABAYA    : Router
- MALANG      : DNS Server Master
- MOJOKERTO   : DNS Server Slave
- PROBOLINGGO : Web Server
- GRESIK      : Client
- SIDOARJO    : Client

## Langkah-langkah pengerjaan:
**1. Membuat domain `http://semerub14.pw` dengan DNS MALANG dan mengarah ke IP Server PROBOLINGGO.** <br>
- Edit file `etc/bind/named.conf.local` pada MALANG dengan setting berikut: <br>
![alt text](/images/1.1.png) <br>
- Buat folder `/jarkom` di dalam folder`/etc/bind`. <br> 
- Salin file `db.local` ke `/etc/bind/jarkom` dan diubah namanya menjadi `semerub14.pw`. <br>
- Buka file `semerub14.pw` dan edit seperti gambar di bawah ini: <br>
![alt text](/images/1.2.png) <br>
- Kemudian restart bind9 dengan cara `service bind9 restart`. <br>
- Untuk mengecek, `ping semerub14.pw` pada GRESIK. <br>
![alt text](/images/1.3.png) <br>

**2. Membuat alias `http://www.semerub14.pw`.** <br>
- Edit file `etc/bind/jarkom/semerub14.pw` pada MALANG dengan setting berikut: <br>
![alt text](/images/2.1.png) <br>
- Untuk mengecek, `ping www.semerub14.pw` pada GRESIK. <br>
![alt text](/images/2.2.png) <br>

**3. Membuat subdomain `http://penanjakan.semerub14.pw`.** <br>
- Edit file `etc/bind/jarkom/semerub14.pw` pada MALANG dengan setting berikut: <br>
![alt text](/images/3.1.png) <br>
- Untuk mengecek, `ping penanjakan.semerub14.pw` pada GRESIK. <br>
![alt text](/images/3.2.png) <br>

**4. Membuat reverse domain untuk domain utama.** <br>
- Edit file `/etc/bind/named.conf.local` pada MALANG dengan setting berikut: <br>
![alt text](/images/4.1.png) <br>
- Salin file `db.local` pada `/etc/bind/jarkom` dan diubah namanya menjadi `83.151.10.in-addr.arpa`. <br>
- Edit file `/etc/bind/jarkom/83.151.10.in-addr.arpa` seperti gambar di bawah ini: <br>
![alt text](/images/4.2.png) <br>
- Untuk mengecek, `host -t PTR 10.151.83.124` pada GRESIK. <br>
![alt text](/images/4.3.png) <br>

**5. Membuat DNS Server Slave pada MOJOKERTO.** <br>
- Edit file `/etc/bind/named.conf.local` pada MALANG dengan setting berikut: <br>
![alt text](/images/5.1.png) <br>
- Edit file `/etc/bind/named.conf.local` pada MOJOKERTO dengan setting berikut: <br>
![alt text](/images/5.2.png) <br>
- Untuk mengecek, matikan dulu MALANG dengan `service bind9 stop`. <br>
![alt text](/images/5.3.png) <br>
- Kemudian `ping semerub14.pw` pada GRESIK. <br>
![alt text](/images/5.4.png) <br>
- Nyalakan kembali server MALANG `service bind9 restart`. <br>

**6. Membuat subdomain `http://gunung.semerub14.pw` pada server MOJOKERTO dan mengarah ke IP Server PROBOLINGGO.** <br>
- Edit file `etc/bind/jarkom/semerub14.pw` pada MALANG dengan setting berikut: <br>
![alt text](/images/6.1.png) <br>
- Edit file `etc/bind/jarkom/named.conf.options` pada MALANG dengan setting berikut: <br>
- Comment pada bagian `dnssec-validation auto` dan tambahkan baris berikut. <br>
![alt text](/images/6.2.png) <br>
- Edit file `etc/bind/jarkom/named.conf.options` pada MOJOKERTO dengan setting berikut: <br>
- Comment pada bagian `dnssec-validation auto` dan tambahkan baris berikut. <br>
![alt text](/images/6.3.png) <br>
- Buat folder `/delegasi` di dalam folder`/etc/bind`. <br> 
- Salin file `db.local` ke `/etc/bind/delegasi` dan diubah namanya menjadi `gunung.semerub14.pw`. <br>
- Buka file `/etc/bind/delegasi/gunung.semerub14.pw` dan edit seperti gambar di bawah ini: <br>
![alt text](/images/6.4.png) <br>
- Kemudian `ping gunung.semerub14.pw` pada GRESIK. <br>
![alt text](/images/6.5.png) <br>

**7. Membuat subdomain `http://naik.gunung.semerub14.pw` pada MOJOKERTO dan mengarah ke IP Server PROBOLINGGO.** <br>
- Buka file `/etc/bind/delegasi/gunung.semerub14.pw` pada MOJOKERTO dan edit seperti gambar di bawah ini: <br>
![alt text](/images/7.1.png) <br>
- Kemudian `ping naik.gunung.semerub14.pw` pada GRESIK. <br>
![alt text](/images/7.2.png) <br>

**8. Membuat `DocumentRoot` pada `/var/www/semerub14.pw` yang dapat diakses melalui `http://semerub14.pw/index.php/home`.** <br>
- Buka file `var/www/semerub14.pw` pada PROBOLINGGO dan edit seperti gambar di bawah ini: <br>
- Tambahkan `ServerName` dan `DocumentRoot`. <br>
![alt text](/images/8.1.PNG) <br>
- Untuk melihat hasilnya dapat diakses dengan browser ke `semerub14.pw`. <br>
![alt text](/images/8.2.jpeg) <br>

**9. Mengatifkan mode rewrite sehingga menjadi `http://semerub14.pw/home`.** <br>
- Aktifkan `a2enmod rewrite` pada PROBOLINGGO. <br>
![alt text](/images/9.1.png) <br>
- Buka file `var/www/semerub14.pw` dan edit seperti gambar di bawah ini: <br>
- Ganti `All` pada `AllowOverride`. <br>
![alt text](/images/9.2.png) <br>
- Edit file `.htaccess` seperti berikut: <br>
![alt text](/images/9.3.png) <br>
- Untuk melihat hasilnya dapat diakses dengan browser ke `semerub14.pw/home`. <br>
![alt text](/images/9.4.jpeg) <br>

10. 

