# Laporan Pertemuan 4 Sistem Operasi

<h4>Nama : Deswita Khansa Rafifah<h4>
<h4>NIM : 254107020151<h4>
<h4>Kelas : TI-1G<h4>

## Tugas Pendahuluan
### Pertanyaan Tugas Pendahuluan
Jawablah pertanyaan-pertanyaan di bawah ini :
1. Apa yang dimaksud perintah-perintah direktory : pwd, cd, mkdir, rmdir.
2. Apa yang dimaksud perintah-perintah manipulasi file : cp, mv dan rm (sertakan format yang digunakan)
3. Jelaskan perbedaan Symbolic link menggunakan hard link (direct) dan soft link (indirect).
4. Tuliskan maksud perintah-perintah : file, find, which, locate dan grep.

### Jawaban Tugas Pendahuluan
1. Perintah-perintah direktory : pwd, cd, mkdir, rmdir.
- pwd (Print Working Directory) → Perintah pwd digunakan untuk menampilkan path direktori kerja (working directory) yang sedang aktif saat ini secara lengkap (absolute path).
- cd (Change Directory) → Perintah cd digunakan untuk berpindah dari satu direktori ke direktori lain.
- mkdir (Make Directory) → Perintah mkdir digunakan untuk membuat direktori baru.
- rmdir (Remove Directory) → Perintah rmdir digunakan untuk menghapus direktori yang kosong (tidak berisi file maupun subdirektori).

2. Perintah-perintah manipulasi file : cp, mv dan rm.
- cp (Copy) → Menyalin file atau direktori dari satu lokasi ke lokasi lain, file asli tetap ada. Format: cp file_sumber file_tujuan
- mv (Move) → Memindahkan file atau direktori ke lokasi lain, atau mengubah nama file. File asli tidak lagi ada di lokasi semula. Format: mv file_sumber file_tujuan
- rm (Remove) → Menghapus file atau direktori. Format: rm [opsi] nama_file — gunakan opsi -r untuk menghapus direktori beserta isinya, -f untuk memaksa hapus tanpa konfirmasi.

3. Perbedaan Symbolic link menggunakan hard link (direct) dan soft link (indirect).
- Hard Link (direct) → Menunjuk langsung ke inode yang sama dengan file asli. Link count file asli bertambah. Jika file asli dihapus, data tetap bisa diakses melalui hard link. Hanya bisa dibuat dalam partisi yang sama dan tidak bisa untuk direktori.
- Soft Link / Symbolic Link (indirect) → Menunjuk ke nama path file asli, bukan inodenya. Link count tidak berubah. Jika file asli dihapus, link menjadi rusak (broken link). Bisa lintas partisi dan bisa digunakan untuk direktori.

4. Perintah-perintah : file, find, which, locate dan grep.
- file → Menampilkan jenis/tipe dari sebuah file berdasarkan isinya, bukan ekstensinya.
- find → Mencari file atau direktori di dalam pohon direktori berdasarkan nama atau kriteria lain.
- which → Mengetahui lokasi (path) dari sebuah perintah/program yang dapat dieksekusi.
- locate → Mencari file di seluruh sistem dengan cepat menggunakan database indeks.
- grep (General Regular Expression Print) → Mencari teks atau pola tertentu di dalam file dan menampilkan baris yang cocok.

## Percobaan
### Percobaan 1: Direktory
1. Melihat direktori HOME
<img src="Screenshot (444).png" width="100%">

2. Melihat direktori aktual dan parent direktori
<img src="Screenshot (445).png" width="100%">

3. Membuat satu direktori, lebih dari satu direktori atau sub direktori
<img src="Screenshot (447).png" width="100%">

- Pohon struktur direktori yang terbentuk:
```
/home/khansa/
├── A/
│   ├── D/
│   │   └── A/
│   └── E/
├── B/
│   └── F/
└── C/
```

4. Menghapus satu atau lebih direktori hanya dapat dilakukan pada direktori kosong dan hanya dapat dihapus oleh pemiliknya kecuali bila diberikan ijin aksesnya
<img src="Screenshot (448).png" width="100%">

- rmdir B menghasilkan error "Directory not empty" karena direktori B masih berisi subdirektori F. Perintah rmdir hanya dapat menghapus direktori yang kosong.
- rmdir B/F B berhasil karena pertama menghapus B/F (yang sudah kosong) terlebih dahulu, kemudian menghapus B yang kini sudah kosong.
- ls -l B setelah penghapusan menghasilkan error "No such file or directory" karena direktori B sudah berhasil dihapus sebelumnya.

5. Navigasi direktori dengan instruksi cd untuk pindah dari satu direktori ke direktori lain.
<img src="Screenshot (451).png" width="100%">

- cd /khansa/C menghasilkan error "No such file or directory" karena path /khansa/C tidak ada. Direktori khansa tidak berada langsung di root /, melainkan di dalam /home/.

### Percobaan 2 : Manipulasi File
1. Perintah cp untuk mengkopi file atau seluruh direktori
<img src="Screenshot (457).png" width="100%">

2. Perintah mv untuk memindah file
<img src="Screenshot (460).png" width="100%">

- mv contoh contoh2 → berhasil, file contoh diganti nama menjadi contoh2
- mv contoh1 contoh2 A/D → berhasil, file contoh1 dan contoh2 dipindahkan ke direktori A/D
- mv contoh contoh1 C → error karena file contoh dan contoh1 sudah tidak ada di direktori home, sudah dipindahkan ke A/D sebelumnya

3. Perintah rm untuk menghapus file
<img src="Screenshot (461).png" width="100%">

- rm -i contoh → error "No such file or directory" karena file contoh sudah tidak ada di direktori home, sudah dipindahkan ke A/D sebelumnya oleh perintah mv.
- rm -rf A C → berhasil, direktori A dan C beserta seluruh isinya terhapus.

### Percobaan 3 : Symbolic Link
1. Membuat shortcut (file link)
<img src="Screenshot (462).png" width="100%">
<img src="Screenshot (464).png" width="100%">

- ln halo.txt z → membuat hard link z, link count halo.txt bertambah menjadi 2
- ln z mydir/halo.juga → membuat hard link halo.juga di dalam direktori mydir
- ln -s z bye.txt → membuat symbolic link bye.txt yang menunjuk ke file z (bye.txt -> z)
- cat z dan cat bye.txt → keduanya menampilkan isi yang sama "Hallo apa kabar"

### Percobaan 4 : Melihat Isi File
<img src="Screenshot (465).png" width="100%">

- file halo.txt → hasilnya ASCII text, artinya file biasa berisi teks
- file bye.txt → hasilnya symbolic link to z, artinya bye.txt adalah symbolic link yang menunjuk ke file z

### Percobaan 5 : Mencari File
1. Perintah find
<img src="Screenshot (466).png" width="100%">

2. Perintah which
<img src="Screenshot (467).png" width="100%">

3. Perintah locate
<img src="Screenshot (468).png" width="100%">

- locate "*.txt" → error "Command 'locate' not found" karena paket locate belum terinstall di sistem.

### Percobaan 6 : Mencari Text Pada File
<img src="Screenshot (469).png" width="100%">

- grep Hallo *.txt → menemukan kata "Hallo" di dua file yaitu bye.txt dan halo.txt, keduanya menampilkan baris "Hallo apa kabar"

## LATIHAN
1. Cobalah urutan perintah berikut :
- $ cd
- $ pwd
- $ ls –al
- $ cd .
- $ pwd
- $ cd ..
- $ pwd
- $ ls -al
- $ cd ..
- $ pwd
- $ ls -al
- $ cd /etc
- $ ls –al | more
- $ cat passwd
- $ cd –
- $ pwd
<img src="Screenshot (470).png" width="100%">
<img src="Screenshot (471).png" width="100%">
<img src="Screenshot (472).png" width="100%">
<img src="Screenshot (474).png" width="100%">

- cd - → kembali ke direktori sebelumnya yaitu /etc, sehingga pwd menampilkan /

2. Lanjutkan penelusuran pohon pada sistem file menggunakan cd, ls, pwd dan cat. Telusuri direktory /bin, /usr/bin, /sbin, /tmp dan /boot.
<img src="Screenshot (475).png" width="100%">
<img src="Screenshot (476).png" width="100%">
<img src="Screenshot (478).png" width="100%">

3. Telusuri direktory /dev. Identifikasi perangkat yang tersedia. Identifikasi tty (termninal) Anda (ketik who am i); siapa pemilih tty Anda (gunakan ls –l).
<img src="Screenshot (479).png" width="100%">
<img src="Screenshot (480).png" width="100%">

- Berdasarkan hasil who am i, user khansa menggunakan terminal tty1.
- Berdasarkan ls -l tty, pemilik tty adalah root dengan group tty.

4. Telusuri derectory /proc. Tampilkan isi file interrupts, devices, cpuinfo, meminfo dan uptime menggunakan perintah cat. Dapatkah Anda melihat mengapa directory /proc disebut pseudo -filesystem yang memungkinkan akses ke struktur data kernel ?
<img src="Screenshot (481).png" width="100%">
<img src="Screenshot (482).png" width="100%">
<img src="Screenshot (483).png" width="100%">
<img src="Screenshot (485).png" width="100%">

- Direktori /proc disebut pseudo-filesystem karena isinya bukan file sungguhan di disk, melainkan informasi kernel yang dibuat secara dinamis di RAM setiap kali diakses.

5. Ubahlah direktory home ke user lain secara langsung menggunakan cd ~username.
<img src="Screenshot (486).png" width="100%">

- cd ~root → error "Permission denied" karena user khansa tidak memiliki izin akses ke direktori home milik root (/root).

6. Ubah kembali ke direktory home Anda.
<img src="Screenshot (487).png" width="100%">

7. Buat subdirektory work dan play.
<img src="Screenshot (488).png" width="100%">

8. Hapus subdirektory work.
<img src="Screenshot (489).png" width="100%">

9. Copy file /etc/passwd ke direktory home Anda.
<img src="Screenshot (491).png" width="100%">

10. Pindahkan ke subirectory play.
<img src="Screenshot (492).png" width="100%">

11. Ubahlah ke subdirektory play dan buat symbolic link dengan nama terminal yang menunjuk ke perangkat tty. Apa yang terjadi jika melakukan hard link ke perangkat tty ?
<img src="Screenshot (493).png" width="100%">

- ln -s /dev/tty terminal → berhasil membuat symbolic link terminal -> /dev/tty.
- Hard link ke perangkat tty tidak bisa dilakukan karena /dev/tty adalah character device, bukan file biasa.

12. Buatlah file bernama hello.txt yang berisi kata ”hello word”. Dapatkah Anda gunakan ”cp” menggunakan ”terminal” sebagai file asal untuk menghasilkan efek yang sama ?
<img src="Screenshot (494).png" width="100%">

- Ya, bisa. cp terminal hello.txt akan menghasilkan efek yang sama karena terminal adalah symbolic link ke /dev/tty yang membaca input dari keyboard, namun hasilnya tergantung input yang diketik user.

13. Copy hello.txt ke terminal. Apa yang terjadi ?
<img src="Screenshot (495).png" width="100%">

- cp hello.txt terminal → karena terminal adalah symbolic link ke /dev/tty, isi file hello.txt yaitu hello word langsung ditampilkan di layar terminal, bukan disalin ke file baru.

14. Masih direktory home, copy keseluruhan direktory play ke direktory bernama workmenggunakan symbolic link.
<img src="Screenshot (496).png" width="100%">

15. Hapus direktory work dan isinya dengan satu perintah
<img src="Screenshot (497).png" width="100%">

## Kesimpulan
- Sistem file Linux tersusun secara hierarki dimulai dari root (/) dengan direktori-direktori standar yang memiliki fungsi masing-masing.
- Perintah cd, pwd, mkdir, dan rmdir digunakan untuk navigasi dan manajemen direktori.
- Perintah cp, mv, dan rm digunakan untuk manipulasi file dan direktori.
- Hard link menunjuk langsung ke inode file asli, sedangkan symbolic link menunjuk ke path file asli.
- Direktori /proc bersifat pseudo-filesystem yang isinya dibuat secara dinamis oleh kernel di RAM.
- Perintah find, which, locate, dan grep memudahkan pencarian file dan teks di dalam sistem.