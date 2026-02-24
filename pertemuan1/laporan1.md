# Laporan Pertemuan 1 Sistem Operasi

<h4>Nama : Deswita Khansa Rafifah<h4>
<h4>NIM : 254107020151<h4>
<h4>Kelas : TI-1G<h4>

## 1.10. Latihan

### 1.10.1. Latihan Konseptual

#### Latihan 1.1
##### Pertanyaan Latihan 1.1
Jelaskan 5 fungsi utama sistem operasi dengan contoh konkret dari minimal 2 OS berbeda (Windows, macOS, atau Linux).

##### Jawaban Latihan 1.1
Sistem operasi modern memiliki lima fungsi utama, yaitu:

**1. Process Management**
Sistem operasi bertanggung jawab mengatur proses yang berjalan di komputer, mulai dari penjadwalan, pembuatan, hingga penghentian proses. Di Windows, pengguna dapat memantau proses melalui Task Manager, sedangkan di Linux menggunakan perintah `ps`, `top`, atau `htop` untuk melihat proses yang sedang berjalan.

**2. Memory Management**
Sistem operasi mengalokasikan memori ke setiap proses dan mengelola virtual memory ketika RAM penuh. Di Windows, virtual memory disebut pagefile, sedangkan di Linux disebut swap space. Ketika RAM penuh, data yang tidak aktif dipindahkan ke disk agar aplikasi tetap dapat berjalan.

**3. File Management**
Sistem operasi menyediakan struktur hierarkis untuk menyimpan dan mengakses file. Windows menggunakan filesystem NTFS dengan struktur folder seperti C:\Users\, sedangkan Linux menggunakan ext4 dengan struktur direktori seperti /home/. Keduanya menyediakan kontrol akses(permissions) untuk keamanan file.

**4. I/O Management**
Sistem operasi mengelola komunikasi antara perangkat keras dan perangkat lunak melalui device drivers. Di Windows, driver perangkat diinstal melalui Device Manager, sedangkan di Linux driver sudah terintegrasi di dalam kernel sehingga sebagian besar perangkat langsung dikenali secara otomatis.

**5. Security dan Protection**
Sistem operasi menyediakan mekanisme keamanan seperti autentikasi pengguna dan enkripsi data. Windows menggunakan BitLocker untuk enkripsi disk dan password login untuk autentikasi, sedangkan Linux menggunakan sistem permissions (read, write, execute) dan enkripsi berbasis LUKS untuk melindungi data pengguna.

#### Latihan 1.2
##### Pertanyaan Latihan 1.2
Kapan sebaiknya menggunakan Windows vs Linux vs macOS? Analisis berdasarkan use case: gaming, development, server, creative work, dan enterprise.

##### Jawaban Latihan 1.2
Pemilihan sistem operasi sangat bergantung pada kebutuhan dan use case pengguna. Berikut analisis penggunaan Windows, Linux, dan macOS berdasarkan berbagai skenario:

**1. Gaming**
Windows adalah pilihan terbaik untuk gaming karena memiliki kompatibilitas terluas dengan game-game populer. Sebagian besar game dirilis untuk Windows terlebih dahulu, dan dukungan DirectX hanya tersedia di Windows. Linux memiliki dukungan gaming yang terus berkembang melalui Steam Proton, namun masih terbatas. macOS kurang cocok untuk gaming karena pilihan game yang sangat terbatas.

**2. Development (Pengembangan Software)**
Linux dan macOS adalah pilihan utama untuk pengembangan software karena keduanya berbasis Unix dan mendukung tools pengembangan seperti bash, git, dan berbagai bahasa pemrograman secara native. Linux lebih fleksibel dan gratis, sedangkan macOS menawarkan kombinasi lingkungan Unix dengan antarmuka yang nyaman. Windows juga bisa digunakan terutama untuk pengembangan aplikasi .NET dan dengan dukungan WSL (Windows Subsystem for Linux).

**3. Server**
Linux adalah pilihan utama untuk server karena stabilitas tinggi, keamanan, dan tidak memerlukan biaya lisensi. Linux mendominasi 90% server di cloud seperti AWS, Google Cloud, dan Azure. Windows Server digunakan untuk lingkungan enterprise yang membutuhkan integrasi dengan Active Directory dan layanan Microsoft lainnya.

**4. Creative Work (Pekerjaan Kreatif)**
macOS adalah pilihan terbaik untuk pekerjaan kreatif seperti desain grafis, editing video, dan produksi musik karena menjadi standar industri kreatif. Aplikasi seperti Final Cut Pro dan Logic Pro hanya tersedia di macOS.Windows juga bisa digunakan dengan Adobe Creative Suite, namun macOS dianggap lebih optimal untuk workflow kreatif.

**5. Enterprise (Bisnis)**
Windows adalah pilihan dominan untuk lingkungan enterprise karena integrasi yang baik dengan Active Directory, Group Policy, dan ekosistem Microsoft Office. Namun Linux juga banyak digunakan di sisi server enterprise, dan macOS semakin populer di perusahaan teknologi untuk kebutuhan developer.

**Kesimpulan:**
- **Gaming** → Windows
- **Development** → Linux atau macOS
- **Server** → Linux
- **Creative Work** → macOS
- **Enterprise** → Windows (desktop), Linux (server)

### 1.10.2. Latihan Praktikal

#### Latihan 1.3
##### Pertanyaan Latihan 1.3
Install Ubuntu Server 22.04 LTS di VirtualBox dengan langkah berikut:
1. Download Ubuntu Server ISO dari website resmi
2. Create VM baru di VirtualBox (RAM: 2GB, Disk: 25GB)
3. Install dengan automatic partitioning (guided)
4. Buat user account dengan password yang kuat
5. Reboot dan login ke sistem
6. Dokumentasikan proses instalasi dengan screenshot key steps

##### Jawaban Latihan 1.3
###### 1. Create Virtual Machine
<img src="Screenshot (88).png" width="100%">

###### 2. Configure VM Settings
<img src="Screenshot (90).png" width="100%">

###### 3. Boot and Install
<img src="Screenshot (91).png" width="100%">

###### 4. Partitioning
<img src="Screenshot (99).png" width="100%">
<img src="Screenshot (100).png" width="100%">

###### 5. Profile Setup
<img src="Screenshot (102).png" width="100%">

###### 6. SSH Setup
<img src="Screenshot (105).png" width="100%">

###### 7. Featured Server Snaps
<img src="Screenshot (106).png" width="100%">

###### 8. Installation Progress
<img src="Screenshot (108).png" width="100%">

###### 9. First Login
<img src="Screenshot (113).png" width="100%">

#### Latihan 1.4
##### Pertanyaan Latihan 1.4
Setelah instalasi Ubuntu Server, lakukan tasks berikut:
1. Update package list: sudo apt update
2. Upgrade packages: sudo apt upgrade
3. Install neofetch: sudo apt install neofetch
4. Jalankan neofetch dan screenshot hasilnya
5. Check disk usage dengan df -h
6. Check memory dengan free -h
7. Dokumentasikan output dari setiap command

##### Jawaban Latihan 1.4
1. Update package list: sudo apt update
<img src="Screenshot (136).png" width="100%">

2. Upgrade packages: sudo apt upgrade
<img src="Screenshot (137).png" width="100%">

3. Install neofetch: sudo apt install neofetch
<img src="Screenshot (138).png" width="100%">

4. Jalankan neofetch dan screenshot hasilnya
<img src="Screenshot (139).png" width="100%">

5. Check disk usage dengan df -h
<img src="Screenshot (140).png" width="100%">

6. Check memory dengan free -h
<img src="Screenshot (141).png" width="100%">

7. Dokumentasikan output dari setiap command

#### Latihan 1.5
##### Pertanyaan Latihan 1.5
Eksplorasi sistem yang baru diinstall:
1. Tampilkan informasi OS: cat /etc/os-release
2. Tampilkan versi kernel: uname -r
3. List partisi: lsblk
4. Check network connectivity: ping -c 4 google.com
5. Install dan jalankan htop untuk melihat resource usage
6. Buat laporan singkat tentang konfigurasi sistem Anda

##### Jawaban Latihan 1.5
1. Tampilkan informasi OS: cat /etc/os-release
<img src="Screenshot (142).png" width="100%">

2. Tampilkan versi kernel: uname -r
<img src="Screenshot (143).png" width="100%">

3. List partisi: lsblk
<img src="Screenshot (144).png" width="100%">

4. Check network connectivity: ping -c 4 google.com
<img src="Screenshot (145).png" width="100%">

5. Install dan jalankan htop untuk melihat resource usage
<img src="Screenshot (146).png" width="100%">
<img src="Screenshot (147).png" width="100%">

6. Buat laporan singkat tentang konfigurasi sistem Anda
Berdasarkan eksplorasi sistem Ubuntu Server yang telah diinstall, 
berikut adalah konfigurasi sistem yang diperoleh:
- **OS:** Ubuntu 24.04.4 LTS (Noble Numbat)
- **Kernel:** 6.8.0-100-generic
- **CPU:** 13th Gen Intel i5-1335U
- **RAM:** Total 1.9GB, digunakan 366MB, tersedia 909MB
- **Disk:** Total 11.5GB, digunakan 4.0GB (45%), tersisa 6.0GB
- **Partisi:** sda (25G) dengan sda1 (1M), sda2 (2G /boot), sda3 (23G)
- **Network:** Terhubung ke internet (ping google.com 0% packet loss)
- **Uptime:** 31 menit
- **Processes:** 22 tasks berjalan

### 1.10.3. Latihan Refleksi
#### Latihan 1.6
##### Pertanyaan Latihan 1.6
Ceritakan pengalaman Anda dengan sistem operasi:
1. Sistem operasi apa yang Anda gunakan sehari-hari? (Windows, macOS, Linux, atau lainnya)
2. Berapa lama Anda menggunakan sistem operasi tersebut?
3. Apa yang Anda sukai dari sistem operasi tersebut?
4. Apa tantangan atau masalah yang pernah Anda hadapi?
5. Apakah Anda pernah menggunakan sistem operasi lain? Bandingkan pengalaman Anda.
6. Setelah mempelajari bab ini, apakah ada sistem operasi lain yang ingin Anda coba? Mengapa? 
Tulis refleksi Anda dalam 300-500 kata disertai dengan dokumentasi.

##### Jawaban Latihan 1.6
Saya adalah pengguna Windows yang sudah menggunakan sistem operasi ini selama kurang lebih 5 tahun. Sejak pertama kali mengenal komputer, Windows menjadi sistem operasi utama yang saya gunakan untuk berbagai keperluan sehari-hari, mulai dari mengerjakan tugas sekolah, browsing internet, hingga hiburan seperti menonton video dan bermain game.
Hal yang saya sukai dari Windows adalah kemudahan penggunaannya. Antarmuka Windows dirancang secara ramah pengguna (user-friendly), sehingga dapat digunakan oleh berbagai kalangan tanpa memerlukan keahlian teknis yang khusus. Selain itu, Windows memiliki tingkat kompatibilitas yang sangat luas dengan berbagai aplikasi dan perangkat keras. Hampir semua perangkat lunak yang saya butuhkan tersedia dan dapat berjalan dengan baik pada sistem operasi ini.
Namun, selama lima tahun menggunakan Windows, saya juga menghadapi beberapa kendala. Salah satu masalah yang sering terjadi adalah penurunan performa sistem seiring waktu, terutama ketika banyak aplikasi dijalankan secara bersamaan. Selain itu, Windows relatif lebih rentan terhadap virus dan malware sehingga memerlukan perlindungan tambahan berupa perangkat lunak antivirus. Pembaruan (update) sistem yang terkadang muncul pada waktu yang kurang tepat juga dapat mengganggu aktivitas yang sedang berlangsung.
Sebelum mempelajari mata kuliah Sistem Operasi, saya belum pernah menggunakan sistem operasi lain secara serius. Namun, setelah mempelajari bab ini dan melakukan praktik instalasi Ubuntu Server, saya mulai memahami perbedaan utama antara Windows dan Linux. Linux terasa lebih kompleks karena banyak menggunakan command line, tetapi saya menyadari bahwa di situlah letak keunggulannya, yaitu memberikan kontrol yang lebih besar dan fleksibilitas terhadap sistem.
Setelah mempelajari bab ini, saya mulai mencoba untuk lebih memahami Linux, khususnya Ubuntu. Meskipun penggunaannya terasa cukup menantang, terutama karena banyaknya penggunaan command line, saya memahami bahwa keterampilan ini penting untuk dikuasai. Penggunaan Linux yang luas pada server cloud dan superkomputer di dunia juga menjadi alasan bagi saya untuk terus mempelajarinya. Oleh karena itu, saya berencana untuk terus berlatih menggunakan Linux melalui VirtualBox, seperti yang telah dilakukan pada praktikum ini.