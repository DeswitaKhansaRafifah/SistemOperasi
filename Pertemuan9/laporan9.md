# Laporan Pertemuan 9 Sistem Operasi

<h4>Nama : Deswita Khansa Rafifah<h4>
<h4>NIM : 254107020151<h4>
<h4>Kelas : TI-1G<h4>

## Praktikum
### Praktikum 7.1 Script Pertama: Laporan Sistem
1. Buat workspace praktikum:
<img src="Screenshot (866).png" width="100%">

2. Buat script dengan nano:
<img src="Screenshot (867).png" width="100%">

3. Ketik isi berikut, simpan ( Ctrl+O Enter ), lalu keluar ( Ctrl+X ):
<img src="Screenshot (868).png" width="100%">

4. Beri izin dan jalankan:
<img src="Screenshot (870).png" width="100%">

### Latihan 9.1
Modifikasi laporan-sistem.sh agar menyimpan output ke file laporan-YYYY-MM-DD.txt sekaligus menampilkannya di terminal. Petunjuk:gunakan tee yang sudah dipelajari di bab sebelumnya.

<img src="Screenshot (871).png" width="100%">
<img src="Screenshot (873).png" width="100%">

### Praktikum 7.2 Script Info Sistem dengan Argumen
1. Buat script:
<img src="Screenshot (874).png" width="100%">

2. Ketik isi berikut:
<img src="Screenshot (875).png" width="100%">

3. Simpan, beri izin, uji dengan berbagai kombinasi argumen:
<img src="Screenshot (876).png" width="100%">

### Latihan 9.2
Buat script kalkulator.sh yang menerima tiga argumen: <angka1> <operator> <angka2> dengan operator +, -, *, atau /. Contoh: ./kalkulator.sh 20 + 5 menghasilkan 25. Gunakan case untuk memilih operasi, dan validasi jika argumen tidak lengkap

<img src="Screenshot (884).png" width="100%">
<img src="Screenshot (885).png" width="100%">

### Praktikum 7.3 Script Grading dan Menu Interaktif
1. Buat script grading (menggunakan if dan for):
<img src="Screenshot (887).png" width="100%">

2. Ketik isi berikut:
<img src="Screenshot (888).png" width="100%">

3. Simpan, beri izin, dan jalankan:
<img src="Screenshot (889).png" width="100%">

4. Buat script menu interaktif (while + case):
<img src="Screenshot (890).png" width="100%">

5. Ketik isi berikut:
<img src="Screenshot (890).png" width="100%">

6. Beri izin dan jalankan, coba setiap opsi:
<img src="Screenshot (891).png" width="100%">


### Latihan 9.3
Tambahkan ke script grading-batch.sh sebuah ringkasan di bagian bawah yang menampilkan: jumlah mahasiswa per grade (A, B, C, D, E) menggunakan perulangan for kedua yang mengiterasi array MAHASISWA.

<img src="Screenshot (911).png" width="100%">
<img src="Screenshot (916).png" width="100%">

### Praktikum 7.4 Library Fungsi Validasi
1. Buat file library:
<img src="Screenshot (917).png" width="100%">

2. Ketik isi berikut:
<img src="Screenshot (918).png" width="100%">

3. Buat script yang menggunakan library:
<img src="Screenshot (919).png" width="100%">

4. Ketik isi berikut:
<img src="Screenshot (919).png" width="100%">

5. Beri izin dan uji semua skenario:
<img src="Screenshot (920).png" width="100%">

### Latihan 9.4
Tambahkan fungsi konfirmasi() ke lib-validasi.sh. Fungsi ini menampilkan pertanyaan, membaca input Y/N dari user, mengembalikan 0 jika Y dan 1 jika N. Buat script demo yang memanggil fungsi ini sebelum menghapus sebuah file.

<img src="Screenshot (921).png" width="100%">
<img src="Screenshot (925).png" width="100%">

### Praktikum 7.5 Script Backup dengan Opsi
1. Buat script:
<img src="Screenshot (926).png" width="100%">

2. Ketik isi berikut:
<img src="Screenshot (926).png" width="100%">

3. Beri izin dan uji:
<img src="Screenshot (927).png" width="100%">

### Praktikum 7.6 Debugging Script
1. Buat script untuk dianalisis:
<img src="Screenshot (928).png" width="100%">

2. Ketik isi berikut:
<img src="Screenshot (928).png" width="100%">

3. Cek sintaks, lalu jalankan dengan tracing:
<img src="Screenshot (929).png" width="100%">

### Latihan 9.5
Script debug-latihan.sh tidak menangani direktori yang tidak ada. Perbaiki dengan menambahkan:
- set -e di baris kedua
- Pengecekan -d "$DIREKTORI" sebelum memanggil du
- Pesan error yang informatif jika direktori tidak ditemukan
Uji dengan direktori yang tidak ada.

<img src="Screenshot (930).png" width="100%">
<img src="Screenshot (931).png" width="100%">


## Tugas Praktikum
### Tugas 1 Script Absensi Kelas
Konteks: instruktur mencatat kehadiran mahasiswa dari command line.
Instruksi:
1. Buat script absensi.sh yang:
- Menerima argumen nama mahasiswa dan status (hadir/izin/alpha)
- Menyimpan entri ke absensi-YYYY-MM-DD.txt dengan format [HH:MM] NAMA - STATUS
- Opsi -r: tampilkan rekapitulasi (jumlah per status)
- Opsi -h: tampilkan bantuan
2. Rekam minimal 5 entri dan tampilkan rekapitulasinya.
Konsep wajib: variabel, parameter posisional, getopts, if, for, fungsi, dan redirection ke file.

<img src="Screenshot (932).png" width="100%">
<img src="Screenshot (933).png" width="100%">

### Tugas 2 Script Health Check Sistem
Konteks: administrator membuat pemeriksaan kondisi server sebelum maintenance.
Instruksi:
1. Buat script healthcheck.sh menggunakan template profesional dari bagian
Best Practices.
2. Script menampilkan: tanggal/waktu, hostname, uptime, penggunaan CPU,
memori, dan disk untuk setiap filesystem yang terpasang.
3. Jika penggunaan disk mana pun melebihi 80%, tampilkan peringatan.
4. Simpan hasil ke healthcheck-YYYY-MM-DD.log dan tampilkan ke terminal
sekaligus menggunakan tee.
5. Opsi -t <persen> mengubah batas peringatan disk (default 80).
Konsep wajib: set -euo pipefail, trap, getopts, fungsi dengan local, for, if, dan tee.

<img src="Screenshot (934).png" width="100%">
<img src="Screenshot (935).png" width="100%">