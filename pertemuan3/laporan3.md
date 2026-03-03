# Laporan Pertemuan 3 Sistem Operasi

<h4>Nama : Deswita Khansa Rafifah<h4>
<h4>NIM : 254107020151<h4>
<h4>Kelas : TI-1G<h4>

## 1.11 Latihan

### Latihan 3.1
#### Pertanyaan Latihan 3.1
Buatlah script yang:
1. Menampilkan daftar 10 file terbesar di direktori /var/log/
2. Menyimpan hasilnya ke file large-logs.txt
3. Menampilkan output juga di terminal menggunakan tee
4. Menangani error dengan redirect ke error.log

#### Jawaban Latihan 3.1
<img src="Screenshot (379).png" width="100%">
Perintah yang digunakan: find /var/log/ -type f -exec ls -lh {} \; 2>error.log | sort -k5 -rh | head -10 | tee large-logs.txt

Penjelasan:
- find /var/log/ -type f → mencari hanya file (bukan folder) di /var/log/
- 2>error.log → error Permission denied disimpan ke error.log
- sort -k5 -rh → urutkan berdasarkan ukuran, terbesar ke terkecil
- head -10 → ambil 10 file terbesar
- tee large-logs.txt → tampilkan di terminal DAN simpan ke file

Hasil: Menampilkan 10 file .journal terbesar (8.0M). Error dari /var/log/private tersimpan di error.log.

### Latihan 3.2
#### Pertanyaan Latihan 3.2
Buat pipeline yang:
1. Membaca /etc/passwd
2. Mengekstrak username (kolom pertama)
3. Mengurutkan alfabetis
4. Menyimpan ke file sorted-users.txt
Hint: Gunakan cut, sort, dan operator redirect.

#### Jawaban Latihan 3.2
<img src="Screenshot (380).png" width="100%">
Perintah yang digunakan: cat /etc/passwd | cut -d: -f1 | sort > sorted-users.txt

Penjelasan:
- cat /etc/passwd → baca file daftar user sistem
- cut -d: -f1 → ambil kolom ke-1 (username) dengan delimiter ':'
- sort → urutkan alfabetis A-Z
- > sorted-users.txt → simpan ke file

Hasil: Daftar username urut alfabetis dari _apt sampai www-data tersimpan di sorted-users.txt.

### Latihan 3.3
#### Pertanyaan Latihan 3.3
Tulis script monitoring yang:
1. Mencatat penggunaan CPU dan memory setiap 5 detik
2. Menyimpan log dengan timestamp
3. Berjalan selama 1 menit (12 iterasi)
4. Output ditampilkan di terminal DAN disimpan ke file

#### Jawaban Latihan 3.3
<img src="Screenshot (384).png" width="100%">
Perintah yang digunakan: for i in $(seq 1 12); do echo "$(date): CPU: $(top -bn1 | grep 'Cpu(s)' | awk '{print $2}')% | MEM: $(free -h | awk '/Mem:/{print $3"/"$2}')"; sleep 5; done | tee -a monitoring.log

Penjelasan:
- seq 1 12 → ulangi 12 kali
- $(date) → timestamp setiap iterasi
- top -bn1 → ambil info CPU
- free -h → ambil info memory
- sleep 5 → tunggu 5 detik
- tee -a monitoring.log → tampil di terminal DAN append ke file

Hasil: 12 baris log selama 1 menit, contoh: Tue Mar 3 01:51:43 PM UTC 2026: CPU: 0.0% | MEM: 312Mi/1.9Gi

### Latihan 3.4
#### Pertanyaan Latihan 3.4
Buat perintah yang:
1. Mencari semua file .conf di sistem
2. Membuang pesan "Permission denied"
3. Menghitung jumlah file yang ditemukan
4. Menyimpan daftar path lengkap ke file

#### Jawaban Latihan 3.4
<img src="Screenshot (386).png" width="100%">
<img src="Screenshot (385).png" width="100%">
Perintah yang digunakan: find / -type f -name "*.conf" 2>/dev/null | tee conf-files.txt | wc -l

Penjelasan:
- find / → cari dari root (seluruh sistem)
- -name "*.conf" → filter ekstensi .conf
- 2>/dev/null → buang error Permission denied
- tee conf-files.txt → simpan path ke file DAN teruskan ke pipe
- wc -l → hitung jumlah file

Hasil: Ditemukan 352 file .conf di seluruh sistem, tersimpan di conf-files.txt.

### Latihan 3.5
#### Pertanyaan Latihan 3.5
Implementasikan script backup yang:
1. Menggunakan tar untuk backup direktori
2. Menampilkan progress dengan tee
3. Mencatat stdout ke backup-success.log
4. Mencatat stderr ke backup-error.log
5. Menambahkan timestamp di setiap log entry

#### Jawaban Latihan 3.5
<img src="Screenshot (389).png" width="100%">
<img src="Screenshot (387).png" width="100%">
<img src="Screenshot (388).png" width="100%">
Perintah yang digunakan: tar -czvf backup.tar.gz ~/ 2>>backup-error.log | tee backup-success.log

Penjelasan:
- tar -czvf → buat backup terkompresi, -v=verbose (tampilkan progress)
- ~/ → backup home directory
- 2>>backup-error.log → error/warning di-append ke backup-error.log
- tee backup-success.log → tampil progress di terminal DAN simpan ke backup-success.log

Hasil: Backup berhasil. backup-error.log berisi 2 peringatan wajar dari tar