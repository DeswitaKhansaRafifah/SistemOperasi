# Laporan Pertemuan 2 Sistem Operasi

<h4>Nama : Deswita Khansa Rafifah<h4>
<h4>NIM : 254107020151<h4>
<h4>Kelas : TI-1G<h4>

## Praktikum 2.1 — Identifikasi CPU dan Memori
### Langkah-langkah
1. Tampilkan informasi CPU: lscpu
<img src="Screenshot (181).png" width="100%">

2. Tampilkan ringkasan memori: free -h
<img src="Screenshot (182).png" width="100%">

3. (Opsional) cek informasi hardware dari DMI/BIOS (butuh sudo): sudo dmidecode -t system
<img src="Screenshot (183).png" width="100%">

#### Pertanyaan Praktikum 2.1
1. Jumlah CPU(s), core/thread
2. Total RAM
3. total swap. 
Jelaskan perbedaan RAM vs swap dalam 2–3 kalimat.

#### Jawaban Praktikum 2.1
Berdasarkan output `lscpu` dan `free -h`:
1. **Jumlah CPU(s):** 1 CPU, Thread(s) per core: 1, Core(s) per socket: 1
2. **Total RAM:** 1.9 GiB
3. **Total Swap:** 2.0 GiB

**Perbedaan RAM vs Swap:**
RAM (Random Access Memory) adalah memori fisik yang digunakan langsung oleh sistem untuk menjalankan proses secara cepat. Swap adalah ruang pada disk yang digunakan sebagai perpanjangan RAM ketika RAM sudah penuh. Akses ke swap jauh lebih lambat dibandingkan RAM karena menggunakan media penyimpanan disk.

## Praktikum 2.2 — Identifikasi Perangkat PCI/USB dan Driver
### Langkah-langkah
1. Lihat daftar perangkat PCI: lspci
<img src="Screenshot (184).png" width="100%">

2. Lihat perangkat PCI beserta driver kernel yang digunakan: lspci -nnk
<img src="Screenshot (185).png" width="100%">

3. Fokus pada NIC (Ethernet) untuk mencari modul driver: lspci -nnk | grep -A3 -i ethernet
<img src="Screenshot (186).png" width="100%">

4. Lihat perangkat USB: lsusb
<img src="Screenshot (187).png" width="100%">

5. Lihat topologi USB (tree): lsusb -t
<img src="Screenshot (188).png" width="100%">

#### Pertanyaan Praktikum 2.2
Temukan 1 perangkat PCI (misal NIC) dan tuliskan: Vendor:Device ID (angka heksadesimal), nama driver/modul kernel, dan deskripsi singkat fungsinya.

#### Jawaban Praktikum 2.2
- **Nama Perangkat:** Intel Corporation 82540EM Gigabit Ethernet Controller
- **Vendor:Device ID:** [8086:100e]
- **Kernel Driver in Use:** e1000
- **Kernel Modules:** e1000
**Fungsi:** Perangkat ini adalah Network Interface Card (NIC) yang berfungsi untuk menghubungkan sistem ke jaringan ethernet, memungkinkan komunikasi data antar perangkat dalam jaringan.

## Praktikum 2.3 — Identifikasi Storage dan Filesystem
### Langkah-langkah:
1. Lihat daftar disk/partisi: lsblk -f
<img src="Screenshot (189).png" width="100%">

2. Tampilkan UUID dan tipe filesystem: sudo blkid
<img src="Screenshot (190).png" width="100%">

3. Lihat mount point untuk root filesystem: findmnt /
<img src="Screenshot (191).png" width="100%">

## Praktikum 2.4 — Melihat Modul Aktif dan Informasinya
### Langkah-langkah:
1. Cek versi kernel: uname -r
<img src="Screenshot (192).png" width="100%">

2. Tampilkan daftar modul aktif: lsmod | head
<img src="Screenshot (193).png" width="100%">

3. Lihat detail modul loop: modinfo loop
<img src="Screenshot (194).png" width="100%">

4. Muat modul dan verifikasi: sudo modprobe loop lalu lsmod | grep -i loop
<img src="Screenshot (198).png" width="100%">

5. (Opsional) Lihat pesan kernel terbaru: dmesg -T | tail -n 20
<img src="Screenshot (198).png" width="100%">

## Praktikum 2.5 — Konfigurasi Auto-load dan Blacklist
### Langkah-langkah
1. Buat file auto-load: echo "loop" | sudo tee /etc/modules-load.d/loop.conf
<img src="Screenshot (201).png" width="100%">

2. Verifikasi modul aktif: lsmod | grep -i loop
<img src="Screenshot (201).png" width="100%">

## Praktikum 2.6 — Mengenali Block vs Character Device
### Langkah-langkah
1. Lihat detail disk: ls -l /dev/sda
<img src="Screenshot (202).png" width="100%">

2. Lihat detail terminal: ls -l /dev/tty
<img src="Screenshot (203).png" width="100%">

3. Mapping disk/partisi: lsblk
<img src="Screenshot (204).png" width="100%">

#### Pertanyaan Praktikum 2.6
Dari output ls -l, jelaskan perbedaan penanda file untuk block device dan character device. (Hint: karakter pertama pada permission string)

#### Jawaban Praktikum 2.6
- **Block Device (/dev/sda):** ditandai dengan huruf **`b`** di awal permission string → `brw-rw----`
- **Character Device (/dev/tty):** ditandai dengan huruf **`c`** di awal permission string → `crw-rw-rw-`

Block device mengakses data dalam bentuk blok (cocok untuk disk), sedangkan character device mengakses data sebagai aliran karakter satu per satu (cocok untuk terminal/serial).

## Praktikum 2.7 — Melihat Informasi udev
### Langkah-langkah
1. Cek atribut udev untuk disk: udevadm info --query=all --name=/dev/sda | head -n 30
<img src="Screenshot (205).png" width="100%">


## Praktikum 2.8 — Membuat Workspace Praktikum
### Langkah-langkah 
1. Buat direktori praktikum: mkdir -p ~/praktikum-os/week02 lalu cd ~/praktikum-os/week02 lalu pwd
<img src="Screenshot (206).png" width="100%">

2. Buat file contoh: touch notes.txt data.log config.txt lalu ls -lah
<img src="Screenshot (207).png" width="100%">

3. Isi file log contoh:
bashecho "INFO: service started" >> data.log
echo "WARN: disk usage high" >> data.log
echo "ERROR: failed to connect" >> data.log
cat data.log
<img src="Screenshot (209).png" width="100%">

4. Baca file dengan less: less data.log
<img src="Screenshot (210).png" width="100%">

## Praktikum 2.9 — Pencarian Pola dengan grep
### Langkah-langkah
1. Cari baris ERROR: grep "ERROR" data.log
<img src="Screenshot (211).png" width="100%">

2. Cari tanpa memperhatikan huruf besar/kecil: grep -i "error" data.log
<img src="Screenshot (212).png" width="100%">

3. Tampilkan nomor baris: grep -n "WARN" data.log
<img src="Screenshot (212).png" width="100%">

4. Tampilkan baris yang tidak cocok: grep -v "INFO" data.log
<img src="Screenshot (212).png" width="100%">

### Pertanyaan Praktikum 2.9
Gunakan grep untuk menampilkan hanya baris yang mengandung INFO atau WARN dari data.log. (Hint: gunakan grep -E dengan pola alternatif)

### Jawaban Praktikum 2.9
Perintah yang digunakan:
```bash
grep -E "INFO|WARN" data.log
```

Output:
```
INFO: service started
WARN: disk usage high
```

Perintah `grep -E` menggunakan extended regex dengan `|` sebagai operator OR untuk menampilkan baris yang mengandung INFO atau WARN.

## Praktikum 2.10 — Substitusi dengan sed
### Langkah-langkah
1. Buat file config latihan
<img src="Screenshot (216).png" width="100%">

2. Ganti dev menjadi prod (tanpa mengubah file): sed 's/MODE=dev/MODE=prod/' config.txt
<img src="Screenshot (217).png" width="100%">

3. Terapkan perubahan langsung ke file: sed -i 's/MODE=dev/MODE=prod/' config.txt lalu cat config.txt
<img src="Screenshot (218).png" width="100%">

4. Ganti semua kemunculan: sed -i 's/myserver/node/g' config.txt lalu cat config.txt
<img src="Screenshot (219).png" width="100%">

## Praktikum 2.11 — Ekstraksi Kolom dengan awk
### Langkah-langkah
1. Lihat output df -h: df -h
<img src="Screenshot (220).png" width="100%">

2. Ambil kolom filesystem dan persentase: df -h | awk 'NR==1{print $1,$5,$6}NR>1{print $1,$5,$6}'
<img src="Screenshot (223).png" width="100%">

3. Filter pemakaian disk di atas 80%: df -h | awk 'NR==1||($5+0)>80{print $1,$5,$6}'
<img src="Screenshot (223).png" width="100%">

## Praktikum 2.12 — Melihat Proses dengan ps
### Langkah-langkah
1. Tampilkan semua proses: ps aux | head
<img src="Screenshot (224).png" width="100%">

2. Cari proses sshd: ps aux | grep -i sshd
<img src="Screenshot (225).png" width="100%">

## Praktikum 2.13 — Monitoring Real-time dengan top
### Langkah-langkah
1. Jalankan top: top (tekan q untuk keluar)
<img src="Screenshot (227).png" width="100%">

## Praktikum 2.14 — Menghentikan Proses dengan kill
### Langkah-langkah
1. Jalankan proses dummy: sleep 300 &
<img src="Screenshot (230).png" width="100%">

2. Cari PID proses sleep: ps aux | grep -E "sleep 300" | grep -v grep
<img src="Screenshot (230).png" width="100%">

3. Hentikan dengan SIGTERM: kill <PID_ANDA>
<img src="Screenshot (230).png" width="100%">

4. Verifikasi proses berhenti: ps aux | grep -E "sleep 300" | grep -v grep
<img src="Screenshot (230).png" width="100%">

## Praktikum 2.15 — Cek Disk, Load, dan Service
### Langkah-langkah
1. Cek penggunaan disk: df -h
<img src="Screenshot (231).png" width="100%">

2. Cari direktori besar: sudo du -sh /var/* 2>/dev/null | sort -h | tail -n 10
<img src="Screenshot (232).png" width="100%">

3. Cek load dan uptime: uptime
<img src="Screenshot (233).png" width="100%">

4. Cek service yang gagal: systemctl --failed
<img src="Screenshot (234).png" width="100%">

5. Ambil log error terbaru: journalctl -xe | tail -n 50
<img src="Screenshot (235).png" width="100%">

## Praktikum 2.16 — Monitoring Port dan Koneksi
### Langkah-langkah
1. Lihat interface dan IP: ip a
<img src="Screenshot (236).png" width="100%">

2. Lihat routing table: ip r
<img src="Screenshot (237).png" width="100%">

3. Lihat port yang sedang listening: sudo ss -tulpn
<img src="Screenshot (238).png" width="100%">

## Pertanyaan Praktikum 2.16
Pilih satu port yang listening dari output ss -tulpn(misal port 22), lalu tuliskan service/proses yang membukanya. Jelaskan kegunaan port tersebut secara singkat.

## Jawaban Praktikum 2.16
- Port yang dipilih: Port 22
- Service: ssh (systemd)
- Kegunaan: Port 22 digunakan untuk protokol SSH (Secure Shell) yaitu untuk koneksi remote terenkripsi ke server agar administrator dapat mengelola server dari jarak jauh secara aman

## Latihan
### Pertanyaan Latihan 2.A
Jalankan lspci -nnk. Pilih 1 perangkat PCI dan tuliskan: nama perangkat, ID vendor:device, dan kernel driver in use.

### Jawaban Latihan 2.A
<img src="Screenshot (239).png" width="100%">
Perangkat yang dipilih: Intel Corporation 82540EM Gigabit Ethernet Controller
Nama perangkat: Intel Corporation 82540EM Gigabit Ethernet Controller
ID Vendor:Device: [8086:100e]
Kernel driver in use: e1000

### Pertanyaan Latihan 2.B
Tentukan device root filesystem dengan findmnt /. Lalu cocokkan dengan lsblk -f dan tuliskan tipe filesystem serta UUID-nya.

### Jawaban Latihan 2.B
<img src="Screenshot (242).png" width="100%">
Device root: /dev/mapper/ubuntu--vg-ubuntu--lv
Filesystem: ext4
UUID: 3d1034c6-00ad-485d-a4c7-337519b9608e

### Pertanyaan Latihan 2.C
Buat file server.log berisi minimal 10 baris dengan variasi kata: INFO, WARN, ERROR. Gunakan grep untuk menampilkan hanya baris ERROR

### Jawaban Latihan 2.C
<img src="Screenshot (244).png" width="100%">
Muncul 3 baris ERROR:
ERROR: failed to connect
ERROR: timeout error
ERROR: database connection failed

### Pertanyaan Latihan 2.D
Gunakan sed untuk mengganti semua kata server menjadi node pada file latihan. Tunjukkan sebelum dan sesudah.

### Jawaban Latihan 2.D
<img src="Screenshot (247).png" width="100%">

### Pertanyaan Latihan 2.E
Gunakan df -h lalu awk untuk menampilkan filesystem yang penggunaan disk di atas 70%.

### Jawaban Latihan 2.E
<img src="Screenshot (248).png" width="100%">
Output hanya menampilkan header karena tidak ada filesystem yang penggunaannya melebihi 70%.

### Pertanyaan Latihan 2.F
Jalankan sleep 600 &. Temukan PID-nya dengan ps. Hentikan dengan SIGTERM. Jelaskan beda SIGTERM vs SIGKILL.

### Jawaban Latihan 2.F
<img src="Screenshot (250).png" width="100%">
SIGTERM (15): Meminta proses berhenti secara baik (graceful), proses bisa menyimpan data dulu sebelum berhenti
SIGKILL (9): Memaksa proses berhenti langsung (force kill), proses tidak sempat menyimpan data dan tidak bisa diabaikan

### Pertanyaan Latihan 2.G
Gunakan systemctl –failed. Jika tidak ada yang gagal, pilih satu service aktif (misal ssh) dan tampilkan status serta 30 baris log terakhirnya.

### Jawaban Latihan 2.G
<img src="Screenshot (252).png" width="100%">
Output -- No entries -- karena ssh dalam kondisi inactive (dead), jadi tidak ada log yang tercatat.