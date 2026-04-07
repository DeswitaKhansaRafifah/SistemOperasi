# Laporan Pertemuan 6 Sistem Operasi

<h4>Nama : Deswita Khansa Rafifah<h4>
<h4>NIM : 254107020151<h4>
<h4>Kelas : TI-1G<h4>

## Praktikum
### Praktikum 6.1 — Melihat Proses dan Thread
1. Tampilkan semua proses yang berjalan
<img src="Screenshot 2026-04-06 101908.png" width="100%">

2. Tampilkan proses beserta thread-nya, dapat dilihat pada kolom LWP (LightWeight Process ID)
<img src="Screenshot 2026-04-06 103157.png" width="100%">

3. Lihat PID shell aktif dan detail prosesnya
<img src="Screenshot 2026-04-06 104226.png" width="100%">

4. Lihat hierarki proses secara visual
<img src="Screenshot 2026-04-06 104648.png" width="100%">

#### Pertanyaan Praktikum 6.1 (Latihan 6.1)
Jalankan ps aux dan amati outputnya:
1. Berapa total proses yang berjalan? Proses apa yang memiliki PID terkecil?
2. Jalankan pstree -p dan temukan proses bash Anda. Proses apa yang menjadi induk (PPID) dari bash tersebut?
3. Bandingkan output ps aux dan ps aux -L. Apa perbedaan yang Anda lihat?

#### Jawaban Praktikum 6.1 (Latihan 6.1)
1. Total proses yang berjalan, proses yang memiliki PID terkecil
<img src="Screenshot 2026-04-06 102811.png" width="100%">
<img src="Screenshot 2026-04-06 102921.png" width="100%">

- Total proses = 101 proses
- PID terkecil = PID 1 yaitu /sbin/init (systemd) — Proses pertama yang dijalankan kernel saat booting, dan menjadi induk dari semua proses di sistem

2. Proses bash dan proses yang menjadi induk (PPID) dari bash
- PID bash = 1007
- PPID = 737 → artinya proses induk bash adalah PID 737

3. Perbedaan ps aux dan ps aux -L:
- ps aux → 1 baris per proses
- ps aux -L → bisa beberapa baris per proses tergantung jumlah thread-nya
- ps aux -L menambahkan kolom LWP (ID thread) dan NLWP (jumlah thread)
Contoh: polkitd PID 660 muncul 4 baris karena punya 4 thread

### Praktikum 6.2 — Mengamati Siklus Hidup Proses
1. Buat proses di background dan amati kondisinya
<img src="Screenshot 2026-04-06 105419.png" width="100%">

2. Amati perubahan exit code dari perintah yang berhasil dan gagal
<img src="Screenshot 2026-04-06 110022.png" width="100%">

#### Pertanyaan Praktikum 6.2 (Latihan 6.2)
1. Jalankan sleep 120 & dan amati kolom STAT pada ps aux. Kondisi apa yang ditampilkan? Mengapa proses sleep berada di kondisi tersebut?
2. Jalankan beberapa perintah yang berhasil dan yang gagal, lalu catat exit code masing-masing. Pola apa yang Anda temukan?

#### Jawaban Praktikum 6.2 (Latihan 6.2)
1. <img src="Screenshot 2026-04-06 110541.png" width="100%">
Kondisi yang ditampilkan adalah S (Sleeping) karena proses sleep sedang menunggu timer 120 detik habis. Proses ini tidak melakukan komputasi apapun sehingga tidak perlu menggunakan CPU — kernel menaruhnya di kondisi Sleeping dan akan membangunkannya kembali ketika waktunya habis.

2. <img src="Screenshot 2026-04-06 110806.png" width="100%">
Pola yang ditemukan dari exit code:
- Exit code 0 = perintah berhasil dieksekusi tanpa error (contoh: ls /etc menghasilkan exit code 0)
- Exit code bukan 0 = perintah gagal dieksekusi (contoh: ls /direktori-tidak-ada menghasilkan exit code 2, dan cat /file-tidak-ada menghasilkan exit code 1)
- Angka exit code yang berbeda menunjukkan jenis error yang berbeda, namun intinya semua nilai selain 0 menandakan kegagalan.

### Praktikum 6.3 — Mengatur Prioritas Proses
1. Jalankan proses dengan prioritas rendah
<img src="Screenshot 2026-04-06 111133.png" width="100%">

2. Verifikasi nilai nice pada kolom NI
<img src="Screenshot 2026-04-06 111433.png" width="100%">

3. Ubah nilai nice proses yang sudah berjalan
<img src="Screenshot 2026-04-06 111923.png" width="100%">

4. Bersihkan proses percobaan
<img src="Screenshot 2026-04-06 1114330.png" width="100%">

#### Pertanyaan Praktikum 6.3 (Latihan 6.3)
1. Jalankan nice -n 5 sleep 200 & dan verifikasi nilai NI-nya dengan ps.
2. Ubah nilai nice menjadi 10 menggunakan renice, lalu verifikasi kembali.
3. Coba ubah nilai nice menjadi -5 tanpa sudo. Apa yang terjadi? Mengapa Linux membatasi hal ini untuk user biasa?

#### Jawaban Praktikum 6.3 (Latihan 6.3)
1. <img src="Screenshot 2026-04-06 112038.png" width="100%">
Setelah menjalankan nice -n 5 sleep 200 & dengan PID 1259, verifikasi dengan ps menunjukkan kolom NI = 5 dan kolom STAT = SN (huruf N menandakan nice value positif).

2. <img src="Screenshot 2026-04-06 112059.png" width="100%">
Setelah menjalankan renice -n 10 -p 1259, output menunjukkan: 1259 (process ID) old priority 5, new priority 10. Verifikasi dengan ps -p 1259 -o pid,ni,cmd menampilkan NI = 10, berhasil diubah dari 5 → 10.

3. <img src="Screenshot 2026-04-06 112112.png" width="100%">
Saat mencoba renice -n -5 -p 1259 tanpa sudo, muncul error: renice: failed to set priority for 1259 (process ID): Permission denied. Linux membatasi hal ini karena nice negatif berarti menaikkan prioritas proses melebihi default, yang dapat mengganggu proses sistem penting. Hanya root yang diizinkan melakukan ini.

### Praktikum 6.4 — Mengirim Sinyal ke Proses
1. Buat proses percobaan
<img src="Screenshot 2026-04-06 112259.png" width="100%">

2. Hentikan satu proses dengan SIGTERM dan verifikasi
<img src="Screenshot 2026-04-06 112434.png" width="100%">

3. Jeda dan lanjutkan proses dengan SIGSTOP/SIGCONT
<img src="Screenshot 2026-04-06 112617.png" width="100%">
<img src="Screenshot 2026-04-06 112758.png" width="100%">

4. Hentikan semua proses sleep sekaligus
<img src="Screenshot 2026-04-06 1114330.png" width="100%">

#### Pertanyaan Praktikum 6.4 (Latihan 6.4)
1. Jalankan sleep 400 &, kirim SIGSTOP, dan amati perubahan kolom STAT. Kondisi apa yang muncul?
2. Kirim SIGCONT dan verifikasi proses kembali berjalan.
3. Hentikan proses dengan SIGTERM lalu verifikasi sudah tidak ada. Kapan Anda memilih SIGKILL daripada SIGTERM?

#### Jawaban Praktikum 6.4 (Latihan 6.4)
1. <img src="Screenshot 2026-04-06 112954.png" width="100%">
Setelah menjalankan sleep 400 & dengan PID 1290 dan mengirim SIGSTOP, kolom STAT berubah menjadi T (Stopped). Shell juga menampilkan pesan [1]+ Stopped sleep 400.

2. <img src="Screenshot 2026-04-06 113055.png" width="100%">
Setelah mengirim SIGCONT ke PID 1290, kolom STAT kembali berubah menjadi S (Sleeping), menandakan proses kembali berjalan normal.

3. <img src="Screenshot 2026-04-06 113157.png" width="100%">
Setelah mengirim SIGTERM, proses tidak ditemukan lagi di output ps. SIGKILL dipilih daripada SIGTERM ketika proses tidak merespons SIGTERM (proses hang/frozen), karena SIGKILL mematikan proses secara paksa tanpa cleanup. Namun SIGKILL berisiko menyebabkan data korup atau file lock yang tidak terlepas, sehingga harus selalu mencoba SIGTERM terlebih dahulu.

### Praktikum 6.5 — Manajemen Job Foreground dan Background
1. Jalankan tiga job di background
<img src="Screenshot 2026-04-06 113316.png" width="100%">

2. Bawa job pertama ke foreground, jeda, lalu kembalikan ke background
<img src="Screenshot 2026-04-06 113505.png" width="100%">

3. Hentikan semua job
<img src="Screenshot 2026-04-06 113555.png" width="100%">

#### Pertanyaan Praktikum 6.5 (Latihan 6.5)
1. Jalankan top di foreground. Apa yang terjadi di terminal?
2. Tekan Ctrl+Z dan cek statusnya dengan jobs. Kondisi apa yang ditampilkan?
3. Pindahkan ke background dengan bg. Apakah top dapat berjalan dengan baik di background? Mengapa?
4. Kembalikan ke foreground dengan fg, lalu keluar dengan q.

#### Jawaban Praktikum 6.5 (Latihan 6.5)
1. <img src="Screenshot 2026-04-06 113644.png" width="100%">
Saat menjalankan top di foreground, terminal dikuasai sepenuhnya oleh tampilan real-time top — tidak bisa mengetik perintah lain selama top berjalan.

2. <img src="Screenshot 2026-04-06 113930.png" width="100%">
Setelah menekan Ctrl+Z, output jobs menampilkan [1]+ Stopped top. Kondisi yang ditampilkan adalah Stopped.

3. <img src="Screenshot 2026-04-06 114014.png" width="100%">
Setelah menjalankan bg %1, status top tetap Stopped meskipun sudah dipindah ke background. Top tidak dapat berjalan dengan baik di background karena top adalah program interaktif yang membutuhkan akses terminal untuk menampilkan output secara real-time. Ketika dipindah ke background, top tidak bisa mengakses terminal sehingga langsung berhenti otomatis.

4. <img src="Screenshot 2026-04-06 100102.png" width="100%">
Setelah menjalankan fg %1, top kembali tampil di foreground dan berhasil keluar dengan menekan q.

### Praktikum 6.6 — Pemantauan Proses
1. Temukan proses dengan penggunaan CPU dan memori tertinggi
<img src="Screenshot 2026-04-06 170108.png" width="100%">

2. Jalankan top dan eksplorasi shortcut-nya
<img src="Screenshot 2026-04-06 114428.png" width="100%">

3. Instal dan jalankan htop
<img src="Screenshot 2026-04-06 114803.png" width="100%">

#### Pertanyaan Praktikum 6.6 (Latihan 6.6)
1. Gunakan ps aux –sort=%mem untuk menemukan proses yang menggunakan memori paling banyak di VM Anda. Proses apa itu?
2. Di dalam top, tekan 1 . Apa yang berubah pada tampilan? Mengapa informasi ini berguna?
3. Di dalam htop, navigasikan ke proses sshd menggunakan tombol panah. Tekan F9 dan amati opsi sinyal yang tersedia.

#### Jawaban Praktikum 6.6 (Latihan 6.6)
1. <img src="Screenshot 2026-04-07 170513.png" width="100%">
Proses yang menggunakan memori paling banyak adalah /sbin/multipathd dengan %MEM = 1.3%. Ini adalah daemon untuk manajemen multipath storage di Linux.

2. <img src="Screenshot 2026-04-07 170547.png" width="100%">
Setelah menekan angka 1 di dalam top, tampilan berubah dari %Cpu(s) menjadi %Cpu0 yang menampilkan penggunaan CPU per-core secara terpisah. Informasi ini berguna karena kita dapat melihat apakah beban CPU terdistribusi merata ke semua core, atau menumpuk di satu core saja, sehingga memudahkan deteksi bottleneck.

3. Di dalam htop, setelah menekan F9 pada proses yang dipilih, muncul panel "Send signal" di sebelah kiri yang menampilkan daftar semua sinyal yang tersedia seperti SIGTERM (15), SIGKILL (9), SIGSTOP (19), SIGHUP (1), dan sinyal lainnya. Kita dapat memilih sinyal menggunakan tombol panah lalu Enter untuk mengirimkannya ke proses tersebut.

## 1.8 Latihan

### Latihan 6.A
#### Pertanyaan Latihan 6.A
Eksplorasi Proses Sistem
1. Jalankan ps aux –forest dan temukan proses dengan PID 1. Apa nama dan fungsi proses tersebut dalam sistem Linux modern?
2. Hitung berapa proses yang dimiliki oleh user root dan berapa yang dimiliki oleh user Anda. Mengapa root memiliki lebih banyak proses?
3. Temukan semua proses yang berada dalam kondisi S. Mengapa sebagian besar proses di sistem berada dalam kondisi ini?

#### Jawaban Latihan 6.A
1. Menjalankan `ps aux --forest` untuk melihat hierarki proses, lalu `ps -p 1 -o pid,cmd` untuk mengidentifikasi proses dengan PID 1.
<img src="Screenshot 2026-04-07 192659.png" width="100%">
<img src="Screenshot 2026-04-07 192944.png" width="100%">

    Proses dengan PID 1 adalah `/sbin/init` yang merupakan symlink ke **systemd**. Fungsinya sebagai init process pertama yang dijalankan kernel setelah booting, bertanggung jawab mengelola semua service sistem dan menjadi induk dari semua proses lainnya.

2. Menghitung jumlah proses milik root dan user khansa menggunakan `ps aux` dikombinasikan dengan `awk` dan `wc -l`.
<img src="Screenshot 2026-04-07 193501.png" width="100%">

    Root memiliki **89 proses** sedangkan user khansa hanya memiliki **6 proses**. Root memiliki lebih banyak proses karena root menjalankan semua service sistem seperti systemd, sshd, cron, dan journald yang membutuhkan hak akses penuh untuk mengelola hardware dan konfigurasi sistem.

3. Menampilkan semua proses dalam kondisi S menggunakan `ps aux | awk '$8 ~ /^S/'`.
<img src="Screenshot 2026-04-07 193727.png" width="100%">

    Sebagian besar proses berada dalam kondisi **S (Sleeping)** karena sedang menunggu event seperti input user, data jaringan, atau timer. Kondisi ini normal dan efisien karena proses yang menunggu tidak menggunakan CPU, sehingga CPU bebas melayani proses lain yang aktif.

### Latihan 6.B
#### Pertanyaan Latihan 6.B
Simulasi Manajemen Job
1. Jalankan tiga perintah sleep dengan durasi 100, 200, dan 300 detik di background. Verifikasi ketiganya dengan jobs.
2. Bawa job kedua ke foreground, jeda dengan Ctrl+Z , lalu kembalikan ke background dengan bg.
3. Hentikan job pertama dengan kill %1. Tampilkan kembali daftar job. Berapa job yang tersisa?

#### Jawaban Latihan 6.B
1. Menjalankan tiga perintah sleep di background dan memverifikasi dengan `jobs`.
<img src="Screenshot 2026-04-07 193918.png" width="100%">

    Ketiga job berhasil berjalan di background dengan status Running: [1] sleep 100, [2] sleep 200, dan [3] sleep 300.

2. Membawa job kedua ke foreground dengan `fg %2`, menjeda dengan Ctrl+Z, lalu melanjutkan di background dengan `bg %2`.
<img src="Screenshot 2026-04-07 194030.png" width="100%">

    Job kedua (sleep 200) berhasil dipindah ke foreground, dijeda (status Stopped), lalu dilanjutkan kembali di background (status Running).

3. Menghentikan job pertama dengan `kill %1` dan memverifikasi sisa job dengan `jobs`.
<img src="Screenshot 2026-04-07 194113.png" width="100%">

    Setelah `kill %1`, job pertama (sleep 100) berstatus Done dan dihapus dari daftar. Tersisa **2 job** yaitu sleep 200 dan sleep 300.

### Latihan 6.C
#### Pertanyaan Latihan 6.C
Prioritas dan Sinyal
1. Jalankan dua proses sleep: satu dengan nice +5 dan satu dengan nice +15. Verifikasi nilai NI keduanya dengan ps.
2. Gunakan renice untuk mengubah nice proses pertama menjadi +10. Proses mana yang kini lebih diprioritaskan scheduler?
3. Kirim SIGSTOP ke salah satu proses, verifikasi kondisi T-nya, lalu kirim SIGCONT. Akhiri semua proses percobaan dengan pkill sleep.

#### Jawaban Latihan 6.C
1. Menjalankan dua proses sleep dengan nice +5 dan nice +15, lalu memverifikasi nilai NI dengan `ps -p <PID> -o pid,ni,cmd`.
<img src="Screenshot 2026-04-07 194422.png" width="100%">
<img src="Screenshot 2026-04-07 194512.png" width="100%">

    Kedua proses berhasil berjalan dengan nilai NI **5** dan **15** sesuai yang ditentukan.

2. Mengubah nilai nice proses pertama dari +5 menjadi +10 menggunakan `renice`, lalu memverifikasi kembali.
<img src="Screenshot 2026-04-07 194707.png" width="100%">

    Nilai nice proses pertama berhasil diubah menjadi **10**. Proses pertama (NI=10) kini lebih diprioritaskan oleh scheduler dibanding proses kedua (NI=15), karena semakin kecil nilai nice maka semakin tinggi prioritasnya.

3. Mengirim SIGSTOP, memverifikasi kondisi T, mengirim SIGCONT, lalu mengakhiri semua proses dengan `pkill sleep`.
    
    <img src="Screenshot 2026-04-07 194827.png" width="100%">
     Setelah SIGSTOP, kolom STAT proses berubah menjadi **TN** yang menandakan proses dalam kondisi Stopped.

    <img src="Screenshot 2026-04-07 194919.png" width="100%">
    Setelah SIGCONT, kolom STAT kembali menjadi **SN** yang menandakan proses berjalan kembali.

    <img src="Screenshot 2026-04-07 194957.png" width="100%">
    Semua proses sleep berhasil dihentikan dengan `pkill sleep`, ditandai dengan status Terminated pada kedua job.