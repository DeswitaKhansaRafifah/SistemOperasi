# Laporan Pertemuan 12 Sistem Operasi

<h4>Nama : Deswita Khansa Rafifah<h4>
<h4>NIM : 254107020151<h4>
<h4>Kelas : TI-1G<h4>

## Praktikum
### Praktikum 10.1: Amati Layanan Aktif Saat Boot
1. Lihat semua layanan yang sedang berjalan.
<img src="Screenshot12 (1).png" width="100%">
Terdapat 17 layanan aktif yang sedang berjalan. Setiap baris menampilkan kolom UNIT (nama service), LOAD (status loaded), ACTIVE (active), SUB (running), dan DESCRIPTION (deskripsi singkat fungsi layanan).

2. Lihat semua unit service yang ada (aktif maupun tidak).
<img src="Screenshot12 (2).png" width="100%">
Daftar menampilkan semua unit service beserta STATE-nya. Service seperti cron.service dan apparmor.service berstatus enabled (otomatis start saat boot), console-getty.service berstatus disabled, sedangkan apport-autoreport.service berstatus static (hanya dipanggil layanan lain).

3. Analisis waktu boot dan temukan layanan paling lambat.
<img src="Screenshot12 (3).png" width="100%">
Output menampilkan daftar layanan diurutkan dari waktu inisialisasi terlama. Layanan systemd-networkd-wait-online.service membutuhkan waktu paling lama yaitu 1 menit 17 detik.

### Tantangan
Identifikasi tiga layanan dengan waktu inisialisasi terlama menggunakan systemd-analyze blame. Gunakan pipeline dari Bab 3 (| sort -rh | head -3) untuk mempercepat pencariannya. Untuk setiap layanan, cari tahu fungsinya dengan systemctl cat nama-layanan. Tuliskan nama layanan, waktu inisialisasinya, dan penjelasan singkat fungsinya.
<img src="Screenshot12 (3).png" width="100%">
<img src="Screenshot12 (4).png" width="100%">
<img src="Screenshot12 (5).png" width="100%">
<img src="Screenshot12 (6).png" width="100%">
<img src="Screenshot12 (06).png" width="100%">
Tiga layanan dengan waktu inisialisasi terlama adalah:
    1. systemd-networkd-wait-online.service — waktu inisialisasi 1 menit 17.090 detik. Fungsinya adalah menunggu jaringan benar-benar terkonfigurasi sebelum layanan lain dilanjutkan (Wait for Network to be Configured).
    2. snapd.seeded.service — waktu inisialisasi 3.017 detik. Fungsinya adalah menunggu hingga snapd selesai melakukan inisialisasi awal setelah instalasi (Wait until snapd is fully seeded).
    3. snapd.service — waktu inisialisasi 2.864 detik. Fungsinya adalah daemon utama yang bertanggung jawab mengelola paket-paket berbasis Snap di sistem (Snap Daemon).

### Praktikum 10.2: Kelola Layanan SSH
1. Periksa status SSH secara menyeluruh.
<img src="Screenshot12 (7).png" width="100%">
Output systemctl status ssh menampilkan banyak informasi meliputi status active (running), Main PID 1221, waktu mulai layanan, penggunaan memori 2.1M, serta beberapa baris log terbaru yang menunjukkan SSH server listening di port 22. is-active menghasilkan active dan is-enabled menghasilkan enabled. Perintah systemctl status adalah perintah pertama yang harus dijalankan ketika ada masalah layanan.

2. Lakukan restart dan pantau perubahannya.
<img src="Screenshot12 (8).png" width="100%">
Setelah sudo systemctl restart ssh, layanan SSH berhasil di-restart. Main PID berubah dari 1221 menjadi 1260, menandakan proses baru dijalankan. Waktu aktif juga berubah menjadi 13 detik yang lalu, membuktikan restart berhasil.

3. Lihat dependensi SSH.
<img src="Screenshot12 (9).png" width="100%">
Output systemctl list-dependencies ssh menampilkan pohon dependensi SSH. SSH membutuhkan banyak unit lain sebelum bisa berjalan, diantaranya ssh.socket, sysinit.target, apparmor.service, systemd-journald.service, systemd-resolved.service, dan berbagai layanan sistem lainnya.

4. Cek semua unit yang gagal di sistem.
<img src="Screenshot12 (10).png" width="100%">
Output systemctl --failed menampilkan 0 loaded units listed, artinya tidak ada layanan yang gagal di sistem. Kondisi sistem dalam keadaan baik.

### Tantangan
Buat skrip Bash (referensi Bab 7) bernama cek-layanan.sh yang memeriksa status daftar layanan dari sebuah berkas teks. Berkas teks daftar-layanan.txt berisi satu nama layanan per baris (isi minimal: ssh, cron, rsyslog). Skrip membaca setiap nama layanan, memeriksa statusnya dengan systemctl is-active, lalu menulis laporan ke berkas laporan-layanan.log dengan format: [TANGGAL] nama-layanan: ACTIVE/INACTIVE. Gunakan date untuk mendapatkan tanggal.
<img src="Screenshot12 (11).png" width="100%">
Skrip cek-layanan.sh berhasil dibuat dan dijalankan. Skrip membaca daftar layanan dari daftar-layanan.txt yang berisi ssh, cron, dan rsyslog, kemudian memeriksa status masing-masing layanan menggunakan systemctl is-active dan mencatat hasilnya ke laporan-layanan.log beserta tanggal dan waktu menggunakan perintah date. Hasil laporan yang tersimpan di laporan-layanan.log: 
- [2026-05-20 03:36:57] ssh: ACTIVE
- [2026-05-20 03:36:57] cron: ACTIVE
- [2026-05-20 03:36:57] rsyslog: ACTIVE. 

Ketiga layanan terpantau dalam kondisi ACTIVE saat skrip dijalankan.

### Praktikum 10.3: Buat Layanan Sederhana dari Skrip Bash
1. Siapkan konten yang akan dilayani.
<img src="Screenshot12 (12).png" width="100%">

2. Buat skrip wrapper untuk server HTTP.
<img src="Screenshot12 (13).png" width="100%">

3. Buat berkas unit systemd untuk layanan ini.
<img src="Screenshot12 (14).png" width="100%">
<img src="Screenshot12 (15).png" width="100%">
Perintah daemon-reload tidak me-restart layanan yang sedang berjalan, hanya memberi tahu systemd untuk membaca ulang definisi unit dari disk. Harus selalu dijalankan setiap kali berkas unit diubah.

4. Jalankan layanan dan verifikasi.
<img src="Screenshot12 (16).png" width="100%">
Setelah sudo systemctl start demo-web, layanan berhasil berjalan dengan status active (running), Main PID 1376. Perintah curl http://localhost:9090 berhasil menampilkan isi file index.html yang berisi teks 'Halo dari layanan systemd kustom!'.

5. Uji fitur restart otomatis.
<img src="Screenshot12 (17).png" width="100%">
Setelah proses dimatikan paksa dengan kill -9, systemd secara otomatis menjalankan ulang layanan setelah beberapa detik. Main PID berubah dari 1376 menjadi 1396, membuktikan fitur Restart=on-failure bekerja dengan baik. Log menunjukkan pesan 'Failed with result signal' lalu 'Started demo-web.service' kembali.

6. Bersihkan layanan uji setelah selesai.
<img src="Screenshot12 (18).png" width="100%">

### Tantangan
Modifikasi berkas unit demo-web.service sebelum menghapusnya: tambahkan RestartSec=10s agar sistemmenunggu 10 detik sebelum mencoba restart, dan tambahkan Environment="PORT=9091" lalu ubah ExecStart agar menggunakan variabel tersebut. Aktifkan layanan dengan enable dan WantedBy=multi-user.target, lalu uji apakah layanan aktif setelah systemctl daemon-reload. Dokumentasikan perbedaan perilaku dibanding versi sebelumnya.
<img src="Screenshot12 (19).png" width="100%">
<img src="Screenshot12 (20).png" width="100%">
Berkas unit demo-web.service dimodifikasi dengan menambahkan dua perubahan yaitu RestartSec=10s dan Environment="PORT=9091", serta mengubah ExecStart agar menggunakan variabel $PORT. Setelah daemon-reload dan systemctl enable --now demo-web, layanan berhasil aktif dengan status active (running), Main PID 1593, dan berjalan di port 9091 (sebelumnya port 9090).
Perbedaan perilaku dibanding versi sebelumnya:
- Port berubah dari 9090 ke 9091 karena menggunakan variabel environment PORT=9091
- Jika terjadi crash, systemd menunggu 10 detik sebelum restart (sebelumnya hanya 3 detik)
- Layanan kini berstatus enabled sehingga akan otomatis start saat boot

Verifikasi dengan curl http://localhost:9091 berhasil menampilkan isi index.html.

### Praktikum 10.4: Filter dan Analisis Log Layanan
1. Lihat log SSH dari satu jam terakhir.
<img src="Screenshot12 (21).png" width="100%">
Log SSH dari satu jam terakhir menampilkan aktivitas restart SSH yang terjadi sebelumnya, yaitu proses stopping, stopped, starting, dan started SSH server pada port 22.

2. Filter log berprioritas error ke atas.
<img src="Screenshot12 (22).png" width="100%">
Output journalctl -b -p err menampilkan beberapa error sejak boot, diantaranya error dari kernel terkait vmwgfx (karena berjalan di VirtualBox), serta error PAM terkait modul pam_lastlog.so yang tidak ditemukan. Error-error ini perlu diperhatikan karena bisa mempengaruhi fungsi sistem.

3. Ikuti log secara real-time sambil memicu aktivitas.
<img src="Screenshot12 (23).png" width="100%">
Perintah journalctl -u ssh -f menampilkan log SSH secara real-time dan menunggu log baru masuk. Mode ini berguna untuk memantau aktivitas layanan secara langsung.

4. Ekstrak log ke berkas untuk analisis.
<img src="Screenshot12 (24).png" width="100%">
File log-ssh-hari-ini.txt berisi 12 baris log SSH. Tidak ditemukan baris yang mengandung kata 'error' atau 'failed', menandakan layanan SSH berjalan normal tanpa masalah hari ini.

### Tantangan
Ekstrak semua log dengan prioritas error (-p err) dari 24 jam terakhir untuk layanan SSH, simpan ke berkas error-ssh-24jam.txt. Gunakan pipeline dari Bab 3 untuk menghitung total jumlah baris error dengan wc -l, lalu tampilkan 10 pesan error yang paling sering muncul menggunakan sort | uniq -c | sort -rn | head -10. Tuliskan perintah lengkap yang kamu gunakan.
<img src="Screenshot12 (25).png" width="100%">
File error-ssh-24jam.txt berisi 1 baris yang merupakan header "-- No entries --", artinya tidak ditemukan log dengan prioritas error pada layanan SSH dalam 24 jam terakhir. Hal ini menunjukkan layanan SSH berjalan dengan baik tanpa error selama periode tersebut.

### Praktikum 10.5: Konfigurasi SSH Server
1. Periksa konfigurasi SSH saat ini.
<img src="Screenshot12 (26).png" width="100%">
Hasil grep menunjukkan baris #Port 22 pada baris ke-23, artinya konfigurasi port SSH masih menggunakan nilai default (dikomentari) yaitu port 22. Hasil ss -tlnp mengkonfirmasi SSH mendengarkan di port 22.

2. Buat backup dan ubah port SSH.
<img src="Screenshot12 (27).png" width="100%">
Setelah perintah sed, konfigurasi berubah dari #Port 22 menjadi Port 2222. Verifikasi dengan grep "^Port" menampilkan Port 2222.

3. Validasi konfigurasi dan restart layanan.
<img src="Screenshot12 (28).png" width="100%">
Perintah sshd -t menghasilkan kode keluar 0, artinya sintaks konfigurasi valid. Setelah restart, SSH berhasil berjalan dengan status active (running), Main PID 1760, mendengarkan di port 22.

4. Verifikasi port baru dengan ss.
<img src="Screenshot12 (29).png" width="100%">

5. Kembalikan port SSH ke 22 setelah praktek.
<img src="Screenshot12 (30).png" width="100%">

### Tantangan
Ubah konfigurasi SSH untuk menambahkan dua pengaturan keamanan: PermitRootLogin no (larang login root langsung) dan MaxAuthTries 3 (maksimal tiga kali percobaan). Lakukan dengan urutan yang aman: backup, edit, validasi dengan sshd -t, reload. Verifikasi perubahan dengan grep -E "PermitRoot|MaxAuth" /etc/ssh/sshd_config. Kemudian periksa log SSH untuk memastikan tidak ada error setelah perubahan dengan journalctl -u ssh -n 20. Referensi Bab 2 untuk penggunaan ss dan Bab 9 untuk keamanan pengguna.
<img src="Screenshot12 (31).png" width="100%">
<img src="Screenshot12 (32).png" width="100%">
<img src="Screenshot12 (33).png" width="100%">
Dua pengaturan keamanan berhasil ditambahkan ke /etc/ssh/sshd_config dengan urutan yang aman: backup, edit, validasi dengan sshd -t (kode keluar 0 = valid), lalu reload.
Hasil verifikasi grep -E "PermitRoot|MaxAuth" menampilkan:
- PermitRootLogin no → login langsung sebagai root dilarang
- MaxAuthTries 3 → maksimal 3 kali percobaan login sebelum koneksi ditolak

Hasil systemctl status ssh menunjukkan layanan tetap active (running) dengan Main PID 1786 setelah reload, membuktikan perubahan konfigurasi tidak mengganggu layanan yang berjalan.

Hasil journalctl -u ssh -n 20 menampilkan proses reload berhasil dengan pesan "Received SIGHUP: restarting" dan "Reloaded ssh.service" tanpa ada error, mengkonfirmasi konfigurasi baru terbaca dengan baik.

## Latihan
### Latihan 10.1 Audit Layanan dan Analisis Boot
Lakukan audit menyeluruh terhadap layanan yang berjalan di sistem.
1. Jalankan systemctl list-units –type=service –state=running dan catat semua layanan aktif. Pilih tiga layanan yang kamu kenal, periksa status masing-masing dengan systemctl status, dan jelaskan fungsinya.
<img src="Screenshot12 (34).png" width="100%">
<img src="Screenshot12 (35).png" width="100%">
<img src="Screenshot12 (36).png" width="100%">
Tiga layanan yang diperiksa:
    1. ssh.service — status active (running), Main PID 1786. Fungsinya adalah menyediakan layanan remote login yang aman melalui protokol SSH (Secure Shell), memungkinkan administrator mengelola server dari jarak jauh melalui koneksi terenkripsi.
    2. cron.service — status active (running), Main PID 870. Fungsinya adalah menjalankan tugas-tugas terjadwal secara otomatis pada waktu yang ditentukan, seperti backup rutin, pembersihan log, dan perintah berkala lainnya.
    3. nginx.service — status active (running), Main PID 879. Fungsinya adalah menyediakan layanan web server berkinerja tinggi yang melayani permintaan HTTP/HTTPS dan bisa berfungsi sebagai reverse proxy server.

2. Jalankan systemd-analyze blame dan identifikasi lima layanan dengan waktu inisialisasi terlama. Tampilkan hasilnya menggunakan pipeline: systemd-analyze blame | head -5.
<img src="Screenshot12 (37).png" width="100%">
Lima layanan dengan waktu inisialisasi terlama saat boot adalah systemd-networkd-wait-online.service (1 menit 17.090 detik) yang menunggu jaringan terkonfigurasi, snapd.seeded.service (3.017 detik) yang menunggu snapd selesai inisialisasi, snapd.service (2.864 detik) sebagai daemon manajemen paket Snap, dpkg-db-backup.service (2.553 detik) yang melakukan backup database dpkg, dan dev-mapper-ubuntu (2.284 detik) yang mengelola device mapper untuk storage.

3. Jalankan systemctl –failed dan dokumentasikan hasilnya. Jika ada layanan yang gagal, cari tahu penyebabnya dengan journalctl -u nama-layanan -n 30.
<img src="Screenshot12 (37).png" width="100%">
Hasil systemctl --failed menampilkan 0 loaded units listed, artinya tidak ada layanan yang gagal di sistem. Semua layanan berjalan dalam kondisi normal dan tidak memerlukan penanganan lebih lanjut.

### Latihan 10.2 Layanan Kustom dengan Restart Otomatis
Buat layanan systemd kustom yang mendemonstrasikan fitur restart otomatis.
1. Buat skrip Bash (referensi Bab 7) bernama monitor-disk.sh yang setiap 30 detik menuliskan penggunaan disk ke berkas log. Gunakan df -h dan date.
<img src="Screenshot12 (38).png" width="100%">
Skrip monitor-disk.sh berhasil dibuat. Skrip berjalan dalam loop, setiap 30 detik mencatat tanggal dan waktu menggunakan date serta penggunaan disk menggunakan df -h ke file monitor-disk.log.

2. Buat berkas unit /etc/systemd/system/monitor-disk.service untuk menjalankan skrip tersebut dengan konfigurasi: Restart=always, RestartSec=5s, dan berjalan sebagai pengguna kamu sendiri.
<img src="Screenshot12 (39).png" width="100%">
Berkas unit monitor-disk.service berhasil dibuat di /etc/systemd/system/ dengan konfigurasi Restart=always, RestartSec=5s, dan berjalan sebagai user khansa.

3. Aktifkan dan jalankan layanan. Verifikasi dengan systemctl status dan pastikan log masuk ke journal.
<img src="Screenshot12 (40).png" width="100%">
Verifikasi: Layanan berhasil aktif dengan status active (running), Main PID 1943. Log masuk ke journal dengan pesan "Started monitor-disk.service".

4. Simulasikan crash dengan membunuh proses secara paksa (kill -9), tunggu 10 detik, dan verifikasi bahwa layanan hidup kembali secara otomatis.
<img src="Screenshot12 (41).png" width="100%">
Setelah proses dimatikan paksa dengan kill -9, systemd menampilkan pesan "Failed with result 'signal'" lalu secara otomatis menjalankan ulang layanan setelah 5 detik. Main PID berubah dari 1943 menjadi 1975, membuktikan Restart=always bekerja dengan baik.

5. Bersihkan: nonaktifkan layanan dan hapus berkas unit setelah selesai.
<img src="Screenshot12 (42).png" width="100%">

### Latihan 10.3 Investigasi Log dan Keamanan SSH
Analisis log sistem dan tingkatkan keamanan konfigurasi SSH.
1. Gunakan journalctl -b -p err untuk menemukan semua error sejak boot terakhir. Simpan hasilnya ke berkas dan hitung jumlah baris dengan wc -l.
<img src="Screenshot12 (43).png" width="100%">
File error-boot.txt berisi 6 baris error sejak boot, diantaranya error kernel vmwgfx karena berjalan di VirtualBox dan error PAM terkait modul pam_lastlog.so yang tidak ditemukan.

2. Lakukan tiga perubahan keamanan pada /etc/ssh/sshd_config: tambahkan PermitRootLogin no, MaxAuthTries 3, dan LoginGraceTime 30. Ikuti alur aman: backup, edit, validasi sshd -t, reload.
<img src="Screenshot12 (44).png" width="100%">
Tiga pengaturan keamanan berhasil ditambahkan ke sshd_config yaitu PermitRootLogin no, MaxAuthTries 3, dan LoginGraceTime 30 dengan urutan aman: backup, edit, validasi sshd -t, reload.

3. Setelah reload, verifikasi tiga hal: layanan masih berjalan (systemctl status ssh), port masih mendengarkan (ss -tlnp | grep ssh), dan konfigurasi baru terbaca (grep -E "PermitRoot|MaxAuth|GraceTime" /etc/ssh/sshd_config).
<img src="Screenshot12 (45).png" width="100%">
    1. systemctl status ssh menunjukkan layanan tetap active (running) dengan Main PID 1786 setelah reload, membuktikan perubahan konfigurasi tidak mengganggu layanan.
    2. ss -tlnp mengkonfirmasi SSH tetap mendengarkan di port 22, layanan berjalan normal.
    3. Ketiga, grep -E "PermitRoot|MaxAuth|GraceTime" menampilkan ketiga konfigurasi keamanan terbaca dengan benar yaitu LoginGraceTime 30, PermitRootLogin no, dan MaxAuthTries 3.

4. Kembalikan konfigurasi SSH ke kondisi semula menggunakan berkas backup.
<img src="Screenshot12 (46).png" width="100%">
Konfigurasi SSH berhasil dikembalikan ke semula menggunakan file backup sshd_config.backup.latihan3. Validasi sshd -t berhasil tanpa error, reload berhasil dengan pesan 'Reloaded ssh.service', dan layanan tetap active (running) dengan Main PID 1786 mendengarkan di port 22.