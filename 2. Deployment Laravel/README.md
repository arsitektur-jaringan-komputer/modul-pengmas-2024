## Table of Contents

- [1. Pendahuluan](#pendahuluan)
  - [1.1. Deployment In A Nutshell](#deployment-in-a-nutshell)
  - [1.2. Virtual Server vs Physical Server](#virtual-server-vs-physical-server)
  - [1.3 Konsep Elastic Computing](#konsep-elastic-computing)
- [2. Amazon Elastic Compute Cloud](#amazon-elastic-compute-cloud)
  - [2.1 Setup Akun AWS](#setup-akun-aws)
  - [2.2 Pengenalan EC2](#pengenalan-elastic-compute-cloud)
  - [2.3 Membuat Instance EC2](#membuat-instance-ec2)

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

