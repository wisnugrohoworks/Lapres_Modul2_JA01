# Praktikum Modul 2 Jaringan Komputer 2020
Oleh Kelompok A01
* _Wisnu (05111740000170)_
* _Salsabila Harlen (05111840000127)_

----------------------------------------------------------------
## Soal
* [Nomor 1](#1)
* [Nomor 2](#2)
* [Nomor 3](#3)
* [Nomor 4](#4)
* [Nomor 5](#5)
* [Nomor 6](#6)
* [Nomor 7](#7)
* [Nomor 8](#8)
* [Nomor 9](#9)
* [Nomor 10](#10)
* [Nomor 11](#11)
* [Nomor 12](#12)
* [Nomor 13](#13)
* [Nomor 14](#14)
* [Nomor 15](#15)
* [Nomor 16](#16)
* [Nomor 17](#17)
--------------------------------------------------------------

# Pengerjaan Soal 

Semeru ​adalah salah satu gunung yang terkenal di Jawa Timur. Bibah adalah salah satu juru kunci
Semeru. Bibah ingin menyebarkan keindahan Semeru pada dunia sehingga dia membeli 3 buah server
yang berada di ​MALANG​, ​MOJOKERTO​ dan ​PROBOLINGGO​. Server ​MALANG​ akan digunakan
sebagai DNS Server Master, ​MOJOKERTO​ akan digunakan sebagai DNS Server Slave dan
PROBOLINGGO​ akan digunakan sebagai Web Server. Selain 3 server terdapat 2 klien yang digunakan
untuk testing oleh Bibah yaitu ​GRESIK ​dan ​SIDOARJO​. Untuk menyambungkan semua jaringan
tersebut Bibah memberi router di ​SURABAYA


### Membuat Topologi

![gambar soal](https://user-images.githubusercontent.com/59832754/98809477-2f087880-2450-11eb-9797-251c10b2cf9d.png)

a.  Untuk membuat topologi seperti yang diminta pada soal 
    maka buat topologi dengan 'nano topologi.sh`

b. lalu diisikan dengan konfigurasi seperti berikut
    
c. langsung jalankan`bash topologi.sh`

d. login ke semua uml 
       username : root
       password  : praktikum
       
e. jalankan `nano /etc/sysctl.conf` untuk menghilangkan tanda pagar (#) bagian net.ipv4.ip_forward=1 dengan perintah pada router surabaya hingga seperti dibawah ini

   ![pre-1](https://github.com/wisnugrohoworks/Lapres_Modul2_JA01/blob/main/img/pre-1.jpg?raw=true)

f. jalankan  `sysctl -p`
g. jalankan  `nano /etc/network/interfaces` untuk setting IP dari setiap UML 

    SURABAYA
    
   ![pre-2](https://github.com/wisnugrohoworks/Lapres_Modul2_JA01/blob/main/img/pre-2.jpg?raw=true)
   
   SIDOARJO
   
   ![pre-3](https://github.com/wisnugrohoworks/Lapres_Modul2_JA01/blob/main/img/pre-3.jpg?raw=true)
   
   GRESIK
   
   ![pre-4](https://github.com/wisnugrohoworks/Lapres_Modul2_JA01/blob/main/img/pre-4.jpg?raw=true)
   
   PROBOLINGGO
   
   ![pre-5](https://github.com/wisnugrohoworks/Lapres_Modul2_JA01/blob/main/img/pre-5.jpg?raw=true)
   
   MALANG
   
   ![pre-6](https://github.com/wisnugrohoworks/Lapres_Modul2_JA01/blob/main/img/pre-6.jpg?raw=true)
   
   MOJOKERTO
   
   ![pre-7](https://github.com/wisnugrohoworks/Lapres_Modul2_JA01/blob/main/img/pre-7.jpg?raw=true)
   
   
h. Restart network dengan mengetikkan service networking restart atau /etc/init.d/networking restart di setiap UML.

i. Export proxy pada setiap UML dengan sintaks seperti di bawah ini:
      export http_proxy=”http://[username-vpn]:[password]@proxy.its.ac.id:8080”
      export https_proxy=”http://[username-vpn]:[password]@proxy.its.ac.id:8080”
      export ftp_proxy=”http://[username-vpn]:[password]@proxy.its.ac.id:8080”

j. setelah itu lakukan perintah apt-get update.


### 1.
​Kalian diminta untuk membuat sebuah website utama dengan (1) alamat​http://semeruyyy.pw 
yyy adalah nama kelompok (misal a01) jadi website utamanya adalah http://semerua01.pw

a. pada server MALANG,update package list dengan perintah `apt-get update`
b. install  bind9 pada dengan perintah  `apt-get install bind9 -y`
c. konfigurasi domain pada server MALANG dengan nano /etc/bind/named.conf.local
  ![1-1](https://github.com/wisnugrohoworks/Lapres_Modul2_JA01/blob/main/img/1-1.jpg?raw=true)
  
d. buat folder dengan perintah mkdir /etc/bind/semerua01.com
e. copykan file db.local pada path /etc/bind ke dalam folder semerua01.com yang baru saja dibuat dan diubah namanya menjadi jarkom
f. lakukan `nano /etc/bind/jarkom/semeru.a01.pw` dan koonfigurasikan seperti pada gambar
  ![1-2](https://github.com/wisnugrohoworks/Lapres_Modul2_JA01/blob/main/img/1-2.jpg?raw=true)
  
  
### 2.  
​yang memiliki (2) alias​ http://www.semeruyyy.pw  
a. lakukan  `nano /etc/bind/jarkom/semerua01.pw`
b. tambahkan dibawahnya 
  seperti pada gambar dibawah ini 
    ![2-1](https://github.com/wisnugrohoworks/Lapres_Modul2_JA01/blob/main/img/2-1.jpg?raw=true)
c. lakukan `service bind9 restart` 

### 3.  
memiliki subdomain
http://penanjakan.semeruyyy.pw/
 ​yang diatur DNS-nya pada ​MALANG ​dan mengarah ke IP
Server ​PROBOLINGGO

a. lakukan  `nano /etc/bind/jarkom/semerua01.pw`
b. tambahkan dibawahnya 
  seperti pada gambar dibawah ini (sudah ditambah sebelumnya)
    ![3-1](https://github.com/wisnugrohoworks/Lapres_Modul2_JA01/blob/main/img/3-1.jpg?raw=true)
c. lakukan `service bind9 restart` 

### 4.  
membuat reverse domain untuk domain utama
a. jalankan  `nano /etc/bind/named.conf.local`
b. Lalu tambahkan konfigurasi berikut 

![4-1](https://github.com/wisnugrohoworks/Lapres_Modul2_JA01/blob/main/img/4-1.jpg?raw=true)


### 5.  
membuat DNS Server Slave pada ​MOJOKERTO​

#### Konfigurasi pada server MALANG

a. Edit file  `nano /etc/bind/named.conf.local`
    ![5-1](https://github.com/wisnugrohoworks/Lapres_Modul2_JA01/blob/main/img/5-1.jpg?raw=true)
b. service bind9 restart

#### Konfigurasi pada server MOJOKERTO

a)  update package lists dengan menjalankan `apt-get update`
b)  install  bind9 pada MOJOKERTO dengan perintah `apt-get install bind9 -y`
c)  Edit file  `nano /etc/bind/named.conf.local` pada MOJOKERTO 
    ![5-2](https://github.com/wisnugrohoworks/Lapres_Modul2_JA01/blob/main/img/5-2.jpg?raw=true)
d)  service bind9 restart


#### Testing
a. Pada server MALANG silahkan matikan service bind9
  `service bind9 stop`
  
  ![5-3](https://github.com/wisnugrohoworks/Lapres_Modul2_JA01/blob/main/img/5-3.jpg?raw=true)

b. Pada client GRESIK pastikan pengaturan nameserver mengarah ke IP MALANG dan IP MOJOKERTO

c. Lakukan ping semerua01.pw pada client GRESIK. Jika ping berhasil maka konfigurasi DNS slave telah berhasil

![5-4](https://github.com/wisnugrohoworks/Lapres_Modul2_JA01/blob/main/img/5-4.jpg?raw=true)


### 6. 
Selain website utama Bibah juga meminta
dibuatkan (6) subdomain dengan alamat ​http://gunung.semeruyyy.pw​ yang didelegasikan pada server
MOJOKERTO ​dan mengarah ke IP Server ​PROBOLINGGO

#### Konfigurasi pada server MALANG
a. Pada MALANG, edit file /etc/bind/jarkom/semerua01.pw dan ubah menjadi seperti di bawah ini sesuai 
` nano /etc/bind/jarkom/semerua01.pw`

b. edit file nano /etc/bind/named.conf.options

c. comment dnssec-validation auto; dan tambahkan baris berikut pada /etc/bind/named.conf.options
  allow-query{any;};
  
  ![6-1](https://github.com/wisnugrohoworks/Lapres_Modul2_JA01/blob/main/img/6-1.jpg?raw=true)
 
   nano /etc/bind/named.conf.local
  ![6-2](https://github.com/wisnugrohoworks/Lapres_Modul2_JA01/blob/main/img/6-2.jpg?raw=true)

d. service bind9 restart


#### Konfigurasi pada server MOJOKERTO


a. nano /etc/bind/named.conf.options
b. comment dnssec-validation auto; dan tambahkan baris berikut pada /etc/bind/named.conf.options
    allow-query{any;};
 ![6-3](https://github.com/wisnugrohoworks/Lapres_Modul2_JA01/blob/main/img/6-3.jpg?raw=true)

   nano /etc/bind/named.conf.local
  ![6-4](https://github.com/wisnugrohoworks/Lapres_Modul2_JA01/blob/main/img/6-4.jpg?raw=true)


### 7.  
Bibah juga ingin memberi petunjuk mendaki gunung semeru kepada anggota komunitas sehingga dia meminta dibuatkan (7) subdomain dengan nama ​http://naik.gunung.semeruyyy.pw​, domain ini diarahkan ke IP Server ​PROBOLINGGO.

a.  buka /etc/bind/delegasi/gunung.semerua01.pw dan edit file hingga menjadi seperti digambar gambar /etc/bind/delegasi/gunung.semerua01.pw

![7-1](https://github.com/wisnugrohoworks/Lapres_Modul2_JA01/blob/main/img/7-1.jpg?raw=true)


### 8.
Setelah selesai membuat keseluruhan domain, kamu diminta untuk segera mengatur web server. (8) Domain ​http://semeruyyy.pw ​memiliki ​DocumentRoot​ pada ​/var/www/semeruyyy.pw​.

a. Install apache di PROBOLINGGO (apt-get install apache2)

b. Install php di PROBOLINGGO (apt-get install php5)

c. Pindah ke directory /etc/apache2/sites-available

ServerName semerua01.pw 

ServerAlias www.semerua01.pw 

Ubah DocumentRoot menjadi /var/www/semerua01.pw

![8-1](https://github.com/wisnugrohoworks/Lapres_Modul2_JA01/blob/main/img/8-1.jpg?raw=true)

f. Aktifkan konfigurasi semerua01 Gunakan perintah a2ensites semerua01.pw

g. service apache2 restart

h. Pindah ke directory /var/www. lalu unzip file hasil download dari wget dan ubah nama menjadi semerua01.com

![8-2](https://github.com/wisnugrohoworks/Lapres_Modul2_JA01/blob/main/img/8-2.jpg?raw=true)

### 9.
Awalnya web dapat diakses menggunakan alamat http://semeruyyy.pw/index.php/home. Karena dirasa alamat urlnya kurang bagus, maka (9) diaktifkan mod rewrite agar urlnya menjadi http://semeruyyy.pw/home.

a. Menjalankan perintah `a2enmod rewrite` untuk mengaktifkan module rewrite.

b. Restart apache dengan perintah `service apache2 restart`

c. Pindah ke directory /var/www/semerua01.pw dan buat file .htaccess dengan isi file

![9-1](https://github.com/wisnugrohoworks/Lapres_Modul2_JA01/blob/main/img/9-1.jpg?raw=true)

d. Restart apache dengan perintah `service apache2 restart`

Berikut ini adalah screenshot apabila kami membuka `semerua01.pw/home`

![9-2](https://github.com/wisnugrohoworks/Lapres_Modul2_JA01/blob/main/img/9-2.jpg?raw=true)


### 10.
Web http://penanjakan.semeruyyy.pw akan digunakan untuk menyimpan assets file yang memiliki DocumentRoot pada /var/www/penanjakan.semeruyyy.pw dan memiliki struktur folder sebagai berikut:

```
/var/www/penanjakan.semeruyyy.pw
                                /public/javascripts
                                /public/css
                                /public/images
                                /errors
```

a.  Jalankan `wget 10.151.36.202/penanjakan.semeru.pw.zip` pada folder `/var/www`

b.  Ekstrak file `semeru.pw.zip` dengan perintah `unzip penanjakan.semeru.pw.zip`

c.  Rename folder `penanjakan.semeru.pw` menjadi `penanjakan.semerua01.pw` dengan perintah `mv penanjakan.semerua01.pw penanjakan.semerua01.pw`

d.  Pindah ke `/etc/apache2/sites-available` dan copy file `default` menjadi `penanjakan.semerua01.pw` dengan perintah `cp default penanjakan.semerua01.pw`

e.  Edit file `penanjakan.semerua01.pw`, dan tambah line berikut ini:

```
ServerName penanjakan.semerua01.pw
        ServerAlias www.penanjakan.semerua01.pw
        DocumentRoot /var/www/penanjakan.semerua01.pw
        <Directory />
                Options FollowSymLinks
                AllowOverride None
        </Directory>
        <Directory /var/www/html>
                Options Indexes FollowSymLinks MultiViews
                AllowOverride None
                Order allow,deny
                allow from all
        </Directory>

        <Directory /var/www/penanjakan.semerua01.pw/public>
            Options +Indexes
        </Directory>

        <Directory /var/www/penanjakan.semerua01.pw/errors>
            Options +Indexes
        </Directory>

        <Directory /var/www/penanjakan.semerua01.pw/public/javascripts>
            Options -Indexes
        </Directory>
        
        <Directory /var/www/penanjakan.semerua01.pw/public/css>
            Options -Indexes
        </Directory>

        <Directory /var/www/penanjakan.semerua01.pw/public/images>
            Options -Indexes
        </Directory>

        <Directory /var/www/penanjakan.semerua01.pw>
                Options +FollowSymLinks -Multiviews
                AllowOverride All
        </Directory>
```

![10-1](https://github.com/wisnugrohoworks/Lapres_Modul2_JA01/blob/main/img/10-1.jpg?raw=true)


### 11.
Pada folder /public dibolehkan directory listing namun untuk folder yang berada di dalamnya tidak dibolehkan.

a.  Edit file `penanjakan.semerua01.pw`, dan edit line berikut ini:

```
<Directory /var/www/penanjakan.semerua01.pw/public>
    Options +Indexes
</Directory>
<Directory /var/www/penanjakan.semerua01.pw/public/javascripts>
    Options -Indexes
</Directory>
<Directory /var/www/penanjakan.semerua01.pw/public/css>
    Options -Indexes
</Directory>
<Directory /var/www/penanjakan.semerua01.pw/public/images>
    Options -Indexes
</Directory>
```

b.  Situs penanjakan.semerua01.pw diaktifkan dengan perintah `a2ensite penanjakan.semerua01.pw`

c.  Berikut ini adalah gambar kami mengakses penanjakan.semerua01.pw pada setiap folder:

![11-1](https://github.com/wisnugrohoworks/Lapres_Modul2_JA01/blob/main/img/11-1.jpg?raw=true)

![11-2](https://github.com/wisnugrohoworks/Lapres_Modul2_JA01/blob/main/img/11-2.jpg?raw=true)

![11-3](https://github.com/wisnugrohoworks/Lapres_Modul2_JA01/blob/main/img/11-3.jpg?raw=true)

![11-4](https://github.com/wisnugrohoworks/Lapres_Modul2_JA01/blob/main/img/11-4.jpg?raw=true)


### 12.
Untuk mengatasi HTTP Error code 404, disediakan file 404.html pada folder /errors untuk mengganti error default 404 dari Apache.

a.  Pindah ke folder `/var/www/penanjakan.semerua01.pw`. Kemudian `nano .htaccess`, dan menulis syntax ini:

`ErrorDocument 404 http://penanjakan.semerua01.pw/errors/404.html`

![12-1](https://github.com/wisnugrohoworks/Lapres_Modul2_JA01/blob/main/img/12-1.jpg?raw=true)

b.  Restart server Apache dengan perintah `service apache2 restart`

Berikut ini adalah bukti redirect ke 404.html apabila kami mengakses `penanjakan.semerua01.pw/oke`:

![12-2](https://github.com/wisnugrohoworks/Lapres_Modul2_JA01/blob/main/img/12-2.jpg?raw=true)


### 13.
Untuk mengakses file assets javascript awalnya harus menggunakan url http://penanjakan.semeruyyy.pw/public/javascripts. Karena terlalu panjang maka dibuatkan konfigurasi virtual host agar ketika mengakses file assets menjadi http://penanjakan.semeruyyy.pw/js.

a.  Edit file `penanjakan.semerua01.pw` dengan perintah `nano /etc/apache2/sites-available/penanjakan.semerua01.pw`

b.  Tambah perintah `Alias "/js" "/var/www/penanjakan.semerua01.pw/public/javascripts"` dibawah directory Javascript

![13-1](https://github.com/wisnugrohoworks/Lapres_Modul2_JA01/blob/main/img/13-1.jpg?raw=true)

Berikut ini adalah screenshot apabila kami mengakses `penanjakan.semeru.a01.pw/js`:

![13-2](https://github.com/wisnugrohoworks/Lapres_Modul2_JA01/blob/main/img/13-2.jpg?raw=true)


### 14.
Sedangkan web http://naik.gunung.semeruyyy.pw sudah bisa diakses hanya dengan menggunakan port 8888. DocumentRoot web berada pada /var/www/naik.gunung.semeruyyy.pw. 

a.  Pindah ke folder `/var/www`, lalu jalankan perintah `wget 10.151.36.202/naik.gunung.semeru.pw.zip`

b.  Setelah file zip terdownload, ekstrak file tersebut dengan perintah `unzip naik.gunung.semeru.pw.zip`

c.  Rename folder `naik.gunung.semeru.pw` menjadi `naik.gunung.semerua01.pw` dengan perintah `mv naik.gunung.semeru.pw naik.gunung.semerua01.pw`

d.  Pindah ke `/etc/apache2/sites-available` dan copy file `default` menjadi `naik.gunung.semerua01.pw` dengan perintah `cp default naik.gunung.semerua01.pw-8888`

e.  Edit file `naik.gunung.semerua01.pw-8888`, dan pada VirtualHost, angka 80 diganti menjadi 8888. Sehingga isi dari file `naik.gunung.semerua01.pw-8888` menjadi seperti berikut:

![14-1](https://github.com/wisnugrohoworks/Lapres_Modul2_JA01/blob/main/img/14-1.jpg?raw=true)

f.  Pindah ke `/etc/apache2`, kemudian edit file `ports.conf`, dan tambahkan `Listen 8888` dibawah `Listen 80`

![14-2](https://github.com/wisnugrohoworks/Lapres_Modul2_JA01/blob/main/img/14-2.jpg?raw=true)

g.  Aktifkan website naik.gunung.semerua01.pw dengan perintah `a2ensite naik.gunung.semerua01.pw`

h.  Restart server Apache dengan perintah `service apache2 restart`

Berikut ini adalah screenshot apabila kami mengakses `naik.gunung.semerua01.pw:8888`

![14-3](https://github.com/wisnugrohoworks/Lapres_Modul2_JA01/blob/main/img/14-3.jpg?raw=true)


### 15.
Bibah meminta kamu membuat web http://naik.gunung.semeruyyy.pw agar diberi autentikasi password dengan username “semeru” dan password “kuynaikgunung” supaya aman dan tidak sembarang orang bisa mengaksesnya. Saat Bibah mengunjungi IP PROBOLINGGO, yang muncul bukan web utama http://semeruyyy.pw melainkan laman default Apache yang bertuliskan “It works!”

a.  Jalankan `htpasswd -c /etc/apache2/.htpasswd semeru` untuk membuat user `semeru` pada Apache

b.  Akan muncul `Enter Password`, dan tulis kuynaikgunung

c.  Setelah selesai, pindah ke folder `/var/www/naik.gunung.semerua01.pw`, dan buat file `.htaccess` dengan cara `nano .htaccess`, dan tulis perintah dibawah

```
AuthType Basic
AuthName "Restricted Content"
AuthUserFile /etc/apache2/.htpasswd
Require valid-user
```

![15-1](https://github.com/wisnugrohoworks/Lapres_Modul2_JA01/blob/main/img/15-1.jpg?raw=true)

**Keterangan:**

1. `AuthType`: Digunakan untuk tipe autentikasi Basic

2. `AuthName` : Pilih teks yang akan ditampilkan kepada pengguna saat login.

3. `AuthUserFile` : Merupakan lokasi dari credential yang telah dibuat pada saat menjalankan perintah `htpasswd`

4. `Require valid-user` : Digunakan agar pengguna yang bisa masuk ke naik.gunung.semerua01pw adalah user yang valid berdasarkan file `.htpasswd` di `/etc/apache2`

d. Kemudian, pindah ke folder `/etc/apache2/sites-available/` dan edit file naik.gunung.semerua01.pw dengan ditambah perintah berikut:

```
<Directory /var/www/naik.gunung.semerua01.pw>
        AuthType Basic
        AuthName "Restricted Content"
        AuthUserFile /etc/apache2/.htpasswd
        Require valid-user
</Directory>
```

e. Restart server Apache dengan perintah `service apache2 restart`

Berikut ini adalah screenshot pada saat naik.gunung.semerua01.pw:8888 diakses

![15-2](https://github.com/wisnugrohoworks/Lapres_Modul2_JA01/blob/main/img/15-2.jpg?raw=true)


### 16.
Karena dirasa kurang profesional, maka setiap Bibah mengunjungi IP PROBOLINGGO akan dialihkan secara otomatis ke http://semeruyyy.pw.

a.  Edit file `default` pada `/etc/apache2/sites-available` dan edit DocumentRoot serta Directory ke `/var/www/semerua01.pw`. Kemudian untuk dapat Redirect menuju semerua01.pw, maka ditambahkan perintah berikut:

```
Redirect permanent / http://semerua01.pw
```

![16-1](https://github.com/wisnugrohoworks/Lapres_Modul2_JA01/blob/main/img/16-1.jpg?raw=true)

b.  Restart server Apache dengan perintah `service apache2 restart`


### 17.
Karena pengunjung pada /var/www/penanjakan.semeruyyy.pw/public/images sangat banyak maka semua request gambar yang memiliki substring “semeru” akan diarahkan menuju semeru.jpg

a.  Pindah ke folder `/var/www/penanjakan.semerua01.pw`, kemudian edit file .htaccess

b.  Tambahkan syntax Regex berikut:

```
RewriteEngine On
RewriteCond %{REQUEST_FILENAME} !-f
RewriteRule ^/?(.*)semeru(.*)\.jpg$ /public/images/semeru.jpg [R=301,L]
```

![17-1](https://github.com/wisnugrohoworks/Lapres_Modul2_JA01/blob/main/img/17-1.jpg?raw=true)

**Keterangan:**

1.  `^` digunakan untuk menyocokkan dengan string apapun yang dimulai dengan string setelah ^

2.  `/?(.*)semeru(.*)` digunakan untuk mencari alamat string setelah `/` dengan semua string sebelum dan setelah kata "semeru"

3.  `\.jpg$` digunakan untuk mencari akhiran alamat string berupa ekstensi ".jpg"


c. Restart server Apache dengan perintah `service apache2 restart`

Berikut ini adalah screenshot apabila kami mengakses `penanjakan.semerua01.pw/public/images/semeruwww.jpg`, maka akan redirect ke `penanjakan.semerua01.pw/public/images/semeru.jpg`

![17-2](https://github.com/wisnugrohoworks/Lapres_Modul2_JA01/blob/main/img/17-2.jpg?raw=true)

