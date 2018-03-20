<h5 align="center"><img src="https://camo.githubusercontent.com/316411cdc29cf834af3ba95fdfddd619ef42d58c/687474703a2f2f696d616765732e762d63646e2e6e65742f76616e696c6c612d626c61636b2d6c6f676f2d3430302e737667"></h5>


[Sekilas Tentang](#sekilas-tentang) | [Instalasi](#instalasi) | [Konfigurasi](#konfigurasi) | [Otomatisasi](#otomatisasi) | [Cara Pemakaian](#cara-pemakaian) | [Pembahasan](#pembahasan) | [Referensi](#referensi)
:---:|:---:|:---:|:---:|:---:|:---:|:---:

# Sekilas Tentang
[`^ kembali ke atas ^`](#)

**Vanilla Forum** adalah sebuah perangkat lunak forum diskusi via internet yang didistribusikan secara open-source
di bawah GNU GPL2. Vanilla Forum dirancang sebagai perangkat lunak forum diskusi yang sederhana, <i>powerful</i>,
dan dapat dikustomisasi dengan mudah untuk menjadikannya unik sesuai dengan komunitas si pengguna. Vanilla Forum
memang ditujukan untuk pengguna yang tergabung dalam komunitas tertentu. Vanilla Forum telah banyak digunakan
untuk mendukung berbagai forum komunitas di berbagai penjuru dunia.

# Instalasi
[`^ kembali ke atas ^`](#)

#### Kebutuhan Sistem :
- Virtualbox 2.6
- Ubuntu server 16.04
- Ubuntu LTS 16.04

#### Proses Instalasi :
1. Lakukan update server
```
$ sudo apt update
```
2. Install ssh pada Ubuntu server
```
$ sudo apt install ssh
```

3. Login ke dalam server menggunakan SSH
```
$ ssh student@localhost –p 2222
```

4. Install LAMP (Linux Apache PHP MySQL).
```
$ sudo apt install apache2 
$ sudo apt install mysql-server 
$ sudo apt install php 
$ sudo apt install libapache2-mod-php 
$ sudo apt install php-mysql 
$ sudo apt install php-gd php-mcrypt php-mbstring php-xml php-ssh2 
$ sudo service apache2 restart 
```
5. Install Vanilla Forum dan unzip
```
$ wget https://open.vanillaforums.com/get/vanilla-core.zip 
```
6. Install unzip dan ekstrak Vanilla-core.zip ke /var/www/html/vanilla 
```
$ sudo apt -y install unzip 
$ sudo unzip vanilla-core.zip -d /var/www/html/vanilla 

```
7. Ubah kepemilikan data pada direktori data di atas secara rekursif supaya data dan direktori dapat diakses dari luar (publik).
```
$ sudo chown -R www-data:www-data /var/www/html/vanilla 
```
8. Selanjutnya database baru dapat dibuat dengan terlebih dahulu masuk ke shell MySQL.
```
$ mysql -u root -p 
```
9. Buat password untuk user root. Lalu, jalankan query berikut untuk membuat database dan sebuah user database untuk instalasi Vanilla Forum. 
```
CREATE DATABASE vanilla_data CHARACTER SET utf8 COLLATE utf8_general_ci; 
CREATE USER 'vanilla_user'@'localhost' IDENTIFIED BY 'StrongPassword'; 
GRANT ALL PRIVILEGES ON vanilla_data.* TO 'vanilla_user'@'localhost'; 
FLUSH PRIVILEGES; 
EXIT;

```
*Ganti nama database vanilla_data dan username vanilla_user sesuai dengan keinginan. Jangan lupa untuk mengganti StrongPassword dengan password yang benar-benar kuat

10. Selanjutnya, buat host virtual untuk situs Vanilla Forum yang akan dibuat.
```
$ sudo nano /etc/apache2/sites-available/000-default.conf 
```
11. Populate file host virtual yang sudah dibuat.
```
<VirtualHost *:80> ServerName forum.example.com DocumentRoot /var/www/vanilla <Directory /var/www/vanilla> Options Indexes FollowSymLinks MultiViews AllowOverride All Order allow,deny allow from all </Directory> </VirtualHost> 
```
12. Aktifkan modul rewrite Apache. 
```
$ sudo a2enmod rewrite 

```

13. Jalankan kembali Apache.
```
$ sudo systemctl restart apache2
```

14. Masukkan Address localhost:8888 di Browser untuk mengakses Vanilla.
```
$ https://localhost:8888
```

# Konfigurasi
[`^ kembali ke atas ^`](#)

**Terdapat banyak hal** yang dapat diatur di Vanilla Forum, meliputi <i>branding</i>, registrasi, kategori diskusi, koneksi dengan media
sosial lainnya, statistika forum, dan lain-lain. Pada gambar di bawah, ditampilkan laman pengaturan <i>branding</i>. Di sini, kita dapat
menentukan judul <i>homepage</i>, deskripsi situs, judul dan logo <i>banner</i>, <i>favicon</i>, dan beberapa opsi pengaturan lainnya.

<img src="https://github.com/alifaz/project-komdat-vanilla/blob/screenshot/screenshot-localhost%208888-2018-03-19-17-32-28.png" align="center">


# Otomatisasi
[`^ kembali ke atas ^`](#)

Terdapat cara alternatif yang lebih mudah untuk menginstall Vanilla, yaitu dengan menggunakan layanan web-hosting provider. Salah satu web yang menyediakan layanan tersebut adalah <strong>Installatron</strong> 

Berikut langka-langkah menginstall Vanilla menggunakan Installatron : 
1. Kunjungi website installatron.com lalu cari "Vanilla Forum" di kolom pencarian
2. klik "+ install this application" 
<img src="https://github.com/alifaz/project-komdat-vanilla/blob/master/screenshot-installatron.com-2018-03-19-17-35-46.png" align="center">
3. isi form yang ditampilkan, lalu klik install di pojok kanan bawah
<img src="https://github.com/alifaz/project-komdat-vanilla/blob/master/installaron.png" align="center">

4. Tunggu proses installasi hingga selesai


# Cara Pemakaian
[`^ kembali ke atas ^`](#)
Berikut adalah cara pemakaian <strong>Vanilla Forum</strong>
1. Kunjungi halaman utama Vanilla Forum, lalu klik login
<img src="https://github.com/alifaz/project-komdat-vanilla/blob/master/tampilan%20awal.png" align="center">
2. isikan username/email dan password yang telah terdaftar, lalu klik tombol "Sign In"
<img src="https://github.com/alifaz/project-komdat-vanilla/blob/master/login.png" align="center">
3. Akan ditampilkan halaman home seperti dibawah ini 
<img src="https://github.com/alifaz/project-komdat-vanilla/blob/master/home.png" align="center">
4. Setelah login, kita dapat langsung membuat diskusi baru dengan cara menekan tombol "New Discussion" lalu akan muncul tampilan berikut 
<img src="https://github.com/alifaz/project-komdat-vanilla/blob/master/screenshot-localhost%208888-2018-03-19-17-39-35.png" align="center">
5. Berikut adalah tampilan setelah kita membuat diskusi, kita pun juga dapat memberikan tanggapan di kolom komentar
<img src="https://github.com/alifaz/project-komdat-vanilla/blob/master/screenshot-localhost%208888-2018-03-19-17-41-50.png" align="center">


# Pembahasan
[`^ kembali ke atas ^`](#)

Pendapat kami tentang aplikasi **Vanilla Forum** ini

Kelebihan
- Mass-appeal forum.
- Tema fleksibel
- Impossibly good integration options with single sign-ons and embedding.
- The best tools available for community management.
- Curated features with great plugin options, not the kitchen sink.

Kelemahan :

# Referensi
[`^ kembali ke atas ^`](#)
