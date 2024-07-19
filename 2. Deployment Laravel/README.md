## Table of Contents

- [1. Pendahuluan](#pendahuluan)
  - [1.1. Deployment In A Nutshell](#deployment-in-a-nutshell)
  - [1.2. Virtual Server vs Physical Server](#virtual-server-vs-physical-server)
  - [1.3 Konsep Elastic Computing](#konsep-elastic-computing)
- [2. Amazon Elastic Compute Cloud](#amazon-elastic-compute-cloud)
  - [2.1. Pengenalan EC2](#pengenalan-ec2)
  - [2.2. Membuat Penyediaan Shell](#membuat-penyediaan-shell)\
  - [2.3. Upload Projek Laravel](#upload-projek-laravel)
  - [2.4. Menjalankan Projek](#menjalankan-projek)
  - [2.5. Buat Database Baru](#buat-database-baru)
  - [2.6. Tambahkan Application Environment](#tambahkan-application-environment)
    - [2.6.1. Tambahkan debug](#tambahkan-debug)
    - [2.6.2. Edit .env file](#edit-env-file)
  - [2.7. Composer](#composer)
    - [2.7.1. Composer Install](#composer-install)
    - [2.7.2. Composer Update(optional)](#composer-updateoptional)
    - [2.7.3. Upgrade Composer](#upgrade-composer)
  - [2.8. Artisan](#artisan)
  - [2.9. Error yang Mungkin Terjadi](#error-yang-mungkin-terjadi)
    - [2.9.1. Halaman yang Muncul Adalah Nginx Default Page](#halaman-yang-muncul-adalah-nginx-default-page)

### Pendahuluan

### Deployment In A Nutshell

Deployment adalah proses akhir dalam pengembangan perangkat lunak di mana aplikasi yang telah selesai dibuat dan diuji dipindahkan ke tempat di mana pengguna bisa menggunakannya. Tempat ini bisa berupa server, komputer pengguna, atau cloud. Tujuannya adalah memastikan aplikasi berjalan dengan baik dan aman di tempat tujuan.

Lingkungan deployment bisa berupa server, desktop, mobile, atau web. Proses deployment bisa dilakukan secara manual, otomatis, atau kombinasi keduanya. Alat-alat seperti Git, Ansible, Jenkins, dan Docker membantu mempermudah proses deployment dengan menyediakan sistem pengelolaan versi, manajemen konfigurasi, dan platform kontainer.

Stack teknologi yang digunakan dalam deployment termasuk LEMP (Linux, Nginx, MySQL, PHP), LAMP (Linux, Apache, MySQL, PHP), MEAN (MongoDB, Express.js, Angular, Node.js), MERN (MongoDB, Express.js, React, Node.js), dan MEVN (MongoDB, Express.js, Vue.js, Node.js). Masing-masing stack ini memiliki kelebihan tersendiri, sehingga pengembang bisa memilih yang paling cocok untuk aplikasi mereka.

### Virtual Server vs Physical Server

Physical server adalah server perangkat keras yang terdiri dari motherboard, CPU, memori, dan pengontrol IO. Server ini disebut "bare-metal" karena perangkat kerasnya digunakan langsung oleh sistem operasi (OS) seperti Windows atau Linux. Physical server biasanya digunakan untuk menjalankan satu aplikasi saja.

Virtual server atau virtual machine (VM) adalah versi perangkat lunak dari server fisik. Fungsi yang memisahkan CPU, memori, penyimpanan, dan sumber daya jaringan dari perangkat keras asli dan memberikannya ke VM disebut hypervisor. Hypervisor berjalan langsung di perangkat keras server, menggantikan OS. VM memiliki tingkat isolasi tambahan dan dapat menjalankan OS sendiri di atas hypervisor.

Physical server dapat dibagi menjadi beberapa VM, di mana setiap VM dapat menjalankan OS dan aplikasi yang berbeda. Hal ini berbeda dengan server bare-metal yang hanya menjalankan satu layanan saja.

![virtual-vs-physical](assets/virtual-vs-physical)

### Konsep Elastic Computing

Apa pun jenis aplikasi yang kita jalankan, sudah pasti kita akan membutuhkan server. Masalahnya, kebutuhan server kita tidak pasti. Kadang kita butuh yang besar, dan kadang kita butuh yang kecil. Kadang kita cuma butuh sedikit, dan kadang kita mungkin membutuhkan ratusan. 

Jaman dahulu kala, mendapatkan server bisa sangat memakan waktu dan biasanya bisa memakan waktu berminggu-minggu atau bahkan berbulan-bulan. Kita harus melakukan penelitian tentang jenis perangkat keras yang tepat untuk dibeli, mungkin mendapatkan persetujuan anggaran dan kemudian membeli perangkat kerasnya, menyusunnya, dan akhirnya mendapatkan akses ke server kita. Lalu, setelah membelinya, kita terjebak dengan server tersebut. Meskipun ternyata kebutuhan server kita menjadi lebih besar, kita harus bertahan dengan server tersebut, atau membeli server baru yang lebih besar. Seiring bertambah besarnya aplikasi kita, kita perlu terus membeli server baru. Hal ini sangat tidak efisien dari segi ekonomi, bukan?

Solusi dari permasalahan di atas yaitu elastic computing. Elastic computing adalah kemampuan untuk dengan cepat memperluas atau mengurangi sumber daya pemrosesan, memori, dan penyimpanan komputer untuk memenuhi permintaan yang berubah-ubah tanpa perlu mengkhawatirkan perencanaan kapasitas dan rekayasa untuk penggunaan tertinggi. 

![elastic-computing](assets/elastic-computing-webp)

## Amazon Elastic Compute Cloud

### Pengenalan EC2

Elastic Compute Cloud (EC2) adalah server virtual yang bisa kita "rental" di AWS. Dalam Cloud Computing, server virtual ini dikenal sebagai compute instance. Dengan EC2, kita bisa dengan mudah dan murah memilih tipe instance, template, sistem operasi, dan kuantitas yang kita perlukan hanya dengan beberapa klik di console AWS.

Setelah melakukan setup, instance bisa dijalankan dan kita akan memiliki akses administratif secara penuh, seperti jika kita membeli server pribadi. 


### Masuk ke Dalam Server

Untuk melakukan deployment, kita akan menggunakna server EC2 dari AWS. Buka powershell lalu masukkan perintah berikut:

```sh
ssh [akun_kalian]@[ip_server] 
```

Lalu apabila diminta password, maka masukkan password sesuai yang tertera di sheet sesuai pada baris mana kalian.

### Upload Projek Laravel 

Pindah ke folder /var/www/app

```sh
sudo mkdir /var/www/app
cd /var/www/app
```

Di folder /var/www/app lakukan cloning projek Laravel dari repositori berikut:

```shell
git clone https://gitlab.com/kuuhaku86/web-penugasan-individu.git
```

### Instalasi dependensi

Supaya kita bisa mendeploy aplikasi berbasis laravel, lakukan instalasi dependensi sebagi berikut:
```shell
#!/bin/bash

#Update
sudo apt-get update -y

#Install dependencies and add PHP8.0 repository
sudo apt-get install  ca-certificates apt-transport-https software-properties-common -y
sudo add-apt-repository ppa:ondrej/php -y

# install nginx
sudo apt-get install nginx -y

# You should install PHP8.0 version to run the Laravel Project
sudo apt-get update -y
sudo apt-get install php8.0-common php8.0-cli -y

# install PHP package
sudo apt-get install php8.0-mbstring php8.0-xml unzip composer -y
sudo apt-get install php8.0-curl php8.0-mysql php8.0-fpm -y

# install MYSQL
sudo apt-get install mysql-server -y

# Set MYSQL password
sudo apt-get install debconf-utils -y
debconf-set-selections <<< 'mysql-server mysql-server/root_password_again password root'
sudo debconf-set-selections <<< "mysql-server mysql-server/root_password_again password root"
```

### Ubah permission storage
Kita perlu mengubah permission pada ``/var/www/app/web-penugasan-individu/storage``, karena aplikasi laravel berjalan dengan user www-data. Aplikasi akan menuliskan log kejadian pada folder tersebut. Dan untuk melakukannya, kita perlu mengubah kepemilikannya ke www-data. Jalankan perintah berikut:
```
sudo chown -R www-data:www-data /var/www/app/web-penugasan-individu/storage
```

### Buat Database Baru

Akses MySQL

```sh
sudo mysql -u root -p
```

Jalankan perintah berikut:

```shell
CREATE DATABASE databaseku;
CREATE USER 'user1'@'%' IDENTIFIED BY 'P4ssW0rdDat4b4seKu';
GRANT ALL PRIVILEGES ON databaseku.* TO 'user1'@'%' WITH GRANT OPTION;
FLUSH PRIVILEGES;
```

### Tambahkan Application Environment

```
sudo cp .env.example .env
sudo nano /var/www/app/web-penugasan-individu/.env
```

#### Tambahkan debug

```
APP_DEBUG=true
LOG_DEBUG=true
```

#### Edit .env file

Lakukan konfigurasi di DB_DATABASE, DB_USERNAME, DB_PASSWORD, dan lainnya.

```shell
APP_NAME=Laravel
APP_ENV=local
APP_KEY=
APP_DEBUG=true
APP_URL=http://localhost

LOG_CHANNEL=stack
LOG_LEVEL=debug

DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=databaseku
DB_USERNAME=user1
DB_PASSWORD=P4ssW0rdDat4b4seKu
```

### Composer

#### Composer Install

```
sudo composer install
```

####  Composer Update(optional)

```
sudo composer update
```

#### Upgrade Composer 

```
sudo which composer
sudo php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
sudo php composer-setup.php --install-dir=/usr/bin --filename=composer
```

### Artisan

```
sudo php artisan key:generate
sudo php artisan migrate
```