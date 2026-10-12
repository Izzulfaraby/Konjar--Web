# PRD — Konjar
**Versi:** 1.1  
**Tanggal:** 12 Oktober 2026  
**Status:** Revisi berdasarkan Daftar Verifikasi PRD Konjar v1.0

## 1. Ringkasan Produk

**Konjar** adalah platform web pembelajaran jaringan komputer dari tingkat dasar hingga profesional. Platform ini dirancang untuk membantu pengguna mempelajari teori, mengikuti panduan praktik, memahami simulasi dan troubleshooting, mengerjakan kuis, serta memantau progres belajar.

Admin dan pengguna memakai satu tabel `users` dengan kolom `role`, tetapi memiliki halaman login dan dashboard yang terpisah. Satu browser hanya boleh memiliki satu sesi aktif pada satu waktu: login sebagai admin akan mengakhiri sesi pengguna yang sedang aktif, dan sebaliknya. Admin bertanggung jawab mengelola konten pembelajaran, sedangkan pengguna menggunakan konten tersebut untuk belajar.

## 2. Latar Belakang dan Masalah

Pembelajaran jaringan komputer sering tersebar di berbagai sumber. Pemula dapat kesulitan menentukan urutan belajar, menghubungkan teori dengan praktik, dan mengetahui kemajuan belajarnya. Materi praktik dan kuis juga perlu dikelola dengan mudah agar konten dapat diperbarui.

Konjar menyatukan materi, lab, kuis, dan progres dalam satu platform yang terstruktur.

## 3. Tujuan Produk

1. Menyediakan jalur belajar jaringan komputer dari dasar hingga tingkat lanjut.
2. Menghubungkan teori dengan praktik dan troubleshooting.
3. Memungkinkan admin mengelola level, materi, lab, dan kuis melalui dashboard.
4. Memisahkan akses admin dan pengguna berdasarkan peran.
5. Menyimpan hasil kuis dan progres belajar pengguna.
6. Menjadi proyek belajar pribadi sekaligus portofolio pengembangan web.

### 3.1 Indikator Keberhasilan

- Admin dapat membuat, membaca, memperbarui, dan menghapus level, materi, lab, serta kuis.
- Pengguna dapat mendaftar, login, membuka materi, mengerjakan kuis, dan melihat hasilnya.
- Hasil kuis dihitung dan disimpan dengan benar.
- Pengguna tidak dapat membuka halaman admin tanpa hak akses.
- Data tetap tersimpan setelah pengguna logout atau menutup browser.

## 4. Target Pengguna

### 4.1 Pengguna Pembelajar
- Mahasiswa atau pelajar TI.
- Pemula yang ingin memahami jaringan komputer.
- Pembelajar mandiri yang ingin berlatih dan menguji pemahaman.

### 4.2 Admin
- Pengelola platform.
- Bertugas menambah, mengedit, menerbitkan, dan menghapus konten pembelajaran.

## 5. Ruang Lingkup

### 5.1 Termasuk dalam Versi Awal (MVP)
- Autentikasi admin dan pengguna dengan satu tabel `users`, kolom `role`, serta halaman login yang terpisah; satu sesi aktif per browser.
- Dashboard admin dan dashboard pengguna.
- CRUD level pembelajaran.
- CRUD materi.
- CRUD lab/praktik.
- CRUD kuis dan pertanyaan pilihan ganda A–D.
- Kunci jawaban dan pembahasan.
- Penilaian kuis otomatis.
- Penyimpanan riwayat hasil kuis.
- Learning Path berdasarkan urutan level.
- Progres belajar dasar dengan tabel `material_progress` dan `lab_progress` yang terpisah.
- Validasi input dan pembatasan akses berdasarkan peran.

### 5.2 Belum Termasuk dalam MVP
- Reset kata sandi mandiri (direncanakan setelah MVP; pada MVP pengguna menghubungi admin melalui prosedur manual yang ditentukan pengelola).
- Video conference atau kelas langsung.
- Forum diskusi dan pesan pribadi.
- Sertifikat resmi dengan verifikasi publik.
- Editor simulasi jaringan interaktif buatan sendiri.
- Integrasi otomatis dengan Cisco Packet Tracer atau perangkat jaringan.
- Pembayaran, langganan, atau fitur marketplace.
- Aplikasi Android/iOS native.
- Reset kata sandi mandiri.

Fitur di luar MVP dapat dipertimbangkan setelah fungsi utama stabil.

## 6. Peran dan Hak Akses

| Fitur | Pengunjung | Pengguna | Admin |
|---|---:|---:|---:|
| Melihat halaman beranda | Ya | Ya | Ya |
| Registrasi pengguna | Ya | Tidak perlu | Tidak |
| Login pengguna | Ya | Ya | Tidak |
| Login admin | Ya | Tidak | Ya |
| Melihat daftar level dan ringkasan | Ya | Ya | Ya |
| Membaca materi lengkap | Tidak | Ya | Ya |
| Mengerjakan lab dan kuis | Tidak | Ya | Ya, pratinjau kuis tidak disimpan |
| Melihat progres dan riwayat nilai | Tidak | Milik sendiri | Sesuai kebutuhan administrasi |
| Mengelola level, materi, lab, kuis | Tidak | Tidak | Ya |
| Mengelola akun pengguna | Tidak | Tidak | Fitur lanjutan/opsional |

**Aturan penting:** halaman admin dan pengguna dipisahkan, tetapi otorisasi tetap harus diperiksa di sisi server pada setiap halaman dan aksi. Menyembunyikan menu saja tidak cukup.

## 7. Struktur Halaman

### 7.1 Halaman Publik
- Beranda
- Tentang Konjar
- Daftar level atau Learning Path (opsional menampilkan ringkasan)
- Login pengguna
- Registrasi pengguna
- Login admin

### 7.2 Halaman Pengguna
- Dashboard pengguna
- Learning Path
- Daftar level
- Detail level
- Daftar materi
- Detail materi
- Detail lab/praktik
- Halaman pengerjaan kuis
- Hasil kuis
- Riwayat kuis
- Progres belajar
- Profil
- Logout

### 7.3 Halaman Admin
- Dashboard admin
- Kelola level
- Form tambah/edit level
- Kelola materi
- Form tambah/edit materi
- Kelola lab
- Form tambah/edit lab
- Kelola kuis
- Form tambah/edit kuis
- Kelola pertanyaan dan pilihan jawaban
- Pratinjau konten
- Logout

## 8. Kebutuhan Fungsional

### FR-01 — Autentikasi dan Sesi
1. Pengguna dapat mendaftar dengan nama, email, dan kata sandi.
2. Sistem memvalidasi email dan memastikan email tidak digunakan akun lain.
3. Kata sandi disimpan menggunakan hashing yang aman, bukan teks biasa.
4. Admin login melalui halaman khusus admin.
5. Sistem memeriksa peran sebelum mengizinkan akses ke halaman admin.
6. Pengguna yang belum login diarahkan ke halaman login.
7. Sistem menyediakan logout dan mengakhiri sesi.
8. Setelah login, admin dan pengguna diarahkan ke dashboard masing-masing.
9. Satu browser hanya memiliki satu sesi aktif; login dengan peran lain mengakhiri sesi sebelumnya.
10. Admin pertama dibuat melalui seed SQL atau skrip CLI di luar web root, bukan melalui `create_admin.php` yang dapat diakses web.
11. Login gagal dibatasi dengan mekanisme rate limit/penundaan sementara setelah percobaan berulang; detail kebijakan dikonfigurasi dan diterapkan di server.
12. Cookie sesi memakai `HttpOnly`, `SameSite` yang sesuai, dan `Secure` saat berjalan melalui HTTPS.

### FR-02 — Dashboard Admin
Dashboard menampilkan ringkasan jumlah level, materi, lab, kuis, dan—jika tersedia—jumlah pengguna. Tersedia navigasi yang jelas ke setiap modul pengelolaan.

### FR-03 — Kelola Level
Admin dapat:
- Menambah level.
- Mengedit level.
- Melihat daftar dan detail level.
- Menghapus level hanya jika belum memiliki konten maupun progres terkait; jika sudah digunakan, penghapusan dilarang dan admin harus menggunakan unpublish.
- Mengatur urutan (`sort_order`), nama, tingkat kesulitan, deskripsi, dan status publikasi.

**Validasi:** slug harus unik bila digunakan; nama wajib diisi; `sort_order` harus berupa angka yang valid dan unik bila aturan aplikasi membutuhkannya. Gunakan hanya `sort_order` sebagai kolom pengurutan; jangan menyimpan kolom duplikat `level_number`. Penghapusan level yang memiliki konten atau progres dilarang; gunakan unpublish.

### FR-04 — Kelola Materi
Admin dapat:
- Membuat, melihat, mengedit, dan menghapus materi.
- Memilih level terkait.
- Mengisi judul, ringkasan, isi materi, estimasi waktu, urutan, dan status publikasi.
- Menyimpan materi sebagai draf sebelum diterbitkan.

Isi materi menggunakan Markdown. Server harus memproses dan merender Markdown dengan aman serta melakukan sanitasi/escape untuk mencegah XSS. Admin boleh mengunggah gambar JPG/PNG maksimal 2 MB per file; lampiran umum dan file `.pkt` tidak termasuk MVP. **Validasi:** judul, level, dan isi materi wajib diisi; estimasi waktu tidak boleh negatif. Konten yang belum diterbitkan tidak tampil pada Learning Path pengguna.

### FR-05 — Kelola Lab dan Praktik
Admin dapat membuat, melihat, mengedit, menerbitkan, membatalkan publikasi, dan menghapus lab. Data lab minimal meliputi judul, level, deskripsi, tujuan, alat/perangkat yang diperlukan, langkah pengerjaan, hasil yang diharapkan, dan catatan troubleshooting. `material_id` bersifat opsional untuk menghubungkan lab ke materi. Simulasi dan troubleshooting merupakan bagian dari lab. Penyelesaian lab dicatat berdasarkan klaim pengguna sendiri melalui tombol “Tandai selesai”; MVP tidak memverifikasi hasil praktik secara otomatis.

Lab dapat berupa panduan praktik manual atau simulasi berbasis instruksi. Integrasi dengan simulator eksternal dan lampiran file `.pkt` tidak termasuk MVP. Penghapusan lab yang masih memiliki progres dilarang; admin dapat menggunakan unpublish.

### FR-06 — Kelola Kuis
Admin dapat:
- Membuat dan mengedit kuis.
- Menghubungkan kuis ke level atau materi.
- Menentukan judul, instruksi, nilai kelulusan, batas waktu (opsional), dan status publikasi.
- Menambahkan pertanyaan pilihan ganda A–D.
- Menentukan satu jawaban benar untuk setiap pertanyaan.
- Menulis pembahasan untuk setiap pertanyaan.
- Mengatur urutan pertanyaan.
- Melihat pratinjau kuis.

**Validasi:** setiap pertanyaan memiliki teks dan pilihan jawaban yang valid serta tepat satu kunci jawaban. Kuis yang diterbitkan harus memiliki minimal satu pertanyaan.

### FR-07 — Pengerjaan dan Penilaian Kuis
1. Pengguna yang login dapat memulai kuis yang diterbitkan.
2. Sistem menampilkan pertanyaan dan pilihan jawaban.
3. Sistem memeriksa jawaban di sisi server.
4. Sistem menghitung nilai secara konsisten.
5. Sistem menyimpan pengguna, kuis, jawaban, nilai, waktu pengerjaan, dan status lulus.
6. Sistem menampilkan hasil setelah kuis dikirim.
7. Pembahasan selalu ditampilkan setelah pengiriman.
8. Pengguna dapat mengulang kuis tanpa batas; sistem menyimpan setiap percobaan dan menampilkan nilai tertinggi sebagai nilai utama.
9. Batas waktu diperiksa di server. Ketika waktu habis, jawaban yang sudah tersimpan/dikirimkan pengguna dikumpulkan otomatis.
10. Nilai dibulatkan ke bilangan bulat terdekat; pertanyaan yang tidak dijawab dihitung salah.
11. Setelah kuis memiliki percobaan pengguna, isi kuis dikunci dari pengeditan. Admin harus membatalkan publikasi kuis lama lalu membuat kuis baru.
12. Percobaan saat admin melakukan pratinjau tidak disimpan.

**Rumus nilai dasar:**

`Nilai = (Jumlah jawaban benar / Jumlah pertanyaan) × 100`

Status lulus ditentukan dengan membandingkan nilai bulat dengan nilai kelulusan yang ditetapkan admin. Pertanyaan kosong dihitung salah. Pembahasan selalu ditampilkan setelah submit.

### FR-08 — Learning Path
- Menampilkan level berdasarkan urutan.
- Menampilkan materi, lab, dan kuis yang telah diterbitkan.
- Semua level dan konten terbit dapat dibuka bebas; MVP tidak mengunci level berdasarkan penyelesaian level sebelumnya.
- Menampilkan ringkasan dan estimasi waktu bila tersedia.
- Menandai konten yang telah diselesaikan bila fitur progres aktif.
- Menyediakan navigasi ke konten berikutnya.

### FR-09 — Progres Belajar
- Sistem mencatat penyelesaian materi saat pengguna menekan tombol selesai dan penyelesaian lab saat pengguna mengklaim bahwa lab telah selesai.
- Progres materi disimpan di `material_progress`; progres lab disimpan di `lab_progress`.
- Progres ditampilkan pada dashboard pengguna. Pengguna hanya dapat melihat dan mengubah progres miliknya sendiri.
- Persentase progres = (jumlah materi dan lab terbit yang telah selesai ÷ jumlah seluruh materi dan lab terbit) × 100. Kuis tidak masuk penyebut progres; status lulus kuis ditampilkan terpisah.

### FR-10 — Pencarian dan Filter (Prioritas setelah MVP)
Fitur pencarian dan filter berdasarkan judul, level, kategori, atau jenis konten ditunda setelah MVP. Kolom kategori juga ditunda bersama FR-10.

## 9. Alur Pengguna Utama

### 9.1 Alur Pengguna Pembelajar
1. Pengunjung membuka beranda dan dapat melihat daftar level serta ringkasan saja; isi materi lengkap tidak tersedia sebelum login.
2. Pengunjung mendaftar atau login.
3. Sistem membuka dashboard pengguna.
4. Pengguna memilih Learning Path dan level.
5. Pengguna membaca materi.
6. Pengguna mengerjakan lab/praktik.
7. Pengguna mengerjakan kuis.
8. Sistem menampilkan nilai dan status lulus.
9. Pengguna melihat riwayat nilai dan progres.

### 9.2 Alur Admin
1. Admin membuka halaman login admin.
2. Admin memasukkan kredensial.
3. Sistem memverifikasi akun dan peran admin.
4. Admin membuka dashboard.
5. Admin memilih modul level, materi, lab, atau kuis.
6. Admin menambah, mengedit, menerbitkan, membatalkan publikasi, atau menghapus konten jika belum memiliki relasi/progres yang melarang penghapusan. Admin tidak dapat mengedit kuis yang sudah memiliki percobaan; buat kuis baru setelah unpublish kuis lama.
7. Sistem memvalidasi input dan menyimpan perubahan.
8. Konten yang diterbitkan tersedia untuk pengguna.

## 10. Struktur Materi Pembelajaran Awal

Target konten awal adalah level 1–2 lengkap saat peluncuran MVP. Konten harus netral vendor dan tidak bergantung pada satu merek/perangkat tertentu. Daftar berikut adalah rancangan awal dan dapat diubah oleh admin.

| Level | Nama | Contoh cakupan |
|---|---|---|
| 1 | Dasar Jaringan Komputer | Pengertian jaringan, LAN/WAN, topologi, perangkat jaringan |
| 2 | Dasar IP dan Subnetting | IPv4, subnet mask, gateway, subnetting |
| 3 | Switching dan Routing | Ethernet, MAC address, VLAN dasar, routing dasar |
| 4 | Network Services | DHCP, DNS, NTP, HTTP/HTTPS, FTP/SFTP, SSH, proxy, pengantar load balancing |
| 5 | Wireless Networking | Standar 802.11, SSID, channel, frekuensi 2.4/5/6 GHz, WPA2/WPA3, access point, troubleshooting Wi-Fi |
| 6 | Network Security | Firewall, ACL, segmentasi, dasar keamanan jaringan |
| 7 | Network Monitoring dan Troubleshooting | Ping, traceroute, log, pemantauan, analisis gangguan |
| 8 | Jaringan Lanjutan | Desain jaringan, redundansi, VPN, pengantar high availability |

Level bukan batas tetap; admin dapat menambah, mengubah, atau mengurutkannya.

## 11. Model Data dan Database

Nama database dan folder proyek yang digunakan adalah `konjar`. Nama produk final adalah **Konjar**. Database dibuat melalui file SQL `database/konjar.sql`.

### 11.1 Tabel `users`
- `id` — primary key
- `name`
- `email` — unique
- `password_hash`
- `role` — `user` atau `admin`
- `status` — `active` atau `blocked`; pengelolaan status pada MVP dilakukan manual melalui database
- `created_at`
- `updated_at`

Admin dan pengguna berada dalam satu tabel. Halaman login tetap terpisah dan server wajib memeriksa `role`. Akun admin pertama dibuat melalui seed SQL atau skrip CLI di luar web root; jangan menyediakan `create_admin.php` yang dapat dipanggil melalui browser.

### 11.2 Tabel `levels`
- `id` — primary key
- `title`
- `slug` — unique
- `difficulty`
- `description`
- `sort_order` — satu-satunya kolom urutan level
- `status` — `draft`/`published`
- `created_at`
- `updated_at`

Tidak ada kolom `level_number`; urutan level ditentukan oleh `sort_order`.

### 11.3 Tabel `materials`
- `id` — primary key
- `level_id` — foreign key ke `levels`
- `title`
- `slug` — unique sesuai kebijakan aplikasi
- `summary`
- `content` — isi Markdown yang diproses dengan aman di server
- `estimated_minutes`
- `sort_order`
- `status` — `draft`/`published`
- `created_at`
- `updated_at`

Gambar yang diunggah dibatasi ke JPG/PNG maksimal 2 MB per file. File `.pkt` dan lampiran umum tidak termasuk MVP.

### 11.4 Tabel `labs`
- `id` — primary key
- `level_id` — foreign key ke `levels`
- `material_id` — foreign key opsional ke `materials`
- `title`
- `slug` — unique sesuai kebijakan aplikasi
- `description`
- `objectives`
- `requirements`
- `steps`
- `expected_result`
- `troubleshooting_notes`
- `estimated_minutes`
- `sort_order`
- `status` — `draft`/`published`
- `created_at`
- `updated_at`

Simulasi dan troubleshooting merupakan bagian dari lab. Penyelesaian lab dicatat berdasarkan klaim pengguna sendiri, bukan validasi otomatis simulator.

### 11.5 Tabel `quizzes`
- `id` — primary key
- `level_id` — foreign key ke `levels`
- `material_id` — foreign key opsional ke `materials`
- `title`
- `instructions`
- `passing_score`
- `time_limit_minutes` — opsional
- `status` — `draft`/`published`
- `created_at`
- `updated_at`

Pembahasan selalu tampil setelah submit. Kuis yang sudah memiliki percobaan tidak boleh diedit; admin melakukan unpublish lalu membuat kuis baru. Pratinjau kuis oleh admin tidak menghasilkan data percobaan.

### 11.6 Tabel `questions`
- `id` — primary key
- `quiz_id` — foreign key ke `quizzes`
- `question_text`
- `option_a`
- `option_b`
- `option_c`
- `option_d`
- `correct_option` — A/B/C/D
- `explanation`
- `sort_order`

Setiap pertanyaan harus memiliki teks, pilihan yang valid, dan tepat satu kunci jawaban.

### 11.7 Tabel `quiz_attempts`
- `id` — primary key
- `user_id` — foreign key ke `users`
- `quiz_id` — foreign key ke `quizzes`
- `score` — nilai bulat 0–100
- `correct_count`
- `total_questions`
- `is_passed`
- `started_at`
- `submitted_at`

Pengguna boleh mengulang kuis tanpa batas. Semua percobaan disimpan; nilai tertinggi ditampilkan sebagai nilai utama. Waktu diperiksa di server dan jawaban yang sudah ada dikirim otomatis saat waktu habis. Pertanyaan kosong dihitung salah.

### 11.8 Tabel `quiz_answers`
- `id` — primary key
- `attempt_id` — foreign key ke `quiz_attempts`
- `question_id` — foreign key ke `questions`
- `selected_option` — nullable jika tidak dijawab
- `is_correct`

### 11.9 Tabel `material_progress`
- `id` — primary key
- `user_id` — foreign key ke `users`
- `material_id` — foreign key ke `materials`
- `status` — `not_started`/`in_progress`/`completed`
- `completed_at`
- `updated_at`

Sediakan unique constraint yang sesuai, misalnya pada pasangan `user_id` dan `material_id`, agar satu pengguna memiliki satu catatan progres per materi.

### 11.10 Tabel `lab_progress`
- `id` — primary key
- `user_id` — foreign key ke `users`
- `lab_id` — foreign key ke `labs`
- `status` — `not_started`/`in_progress`/`completed`
- `completed_at`
- `updated_at`

Sediakan unique constraint yang sesuai pada pasangan `user_id` dan `lab_id`. Penyelesaian lab berdasarkan klaim pengguna.

### 11.11 Relasi dan aturan penghapusan
- Satu level memiliki banyak materi, lab, dan kuis.
- Satu materi dapat memiliki banyak lab terkait secara opsional.
- Satu kuis memiliki banyak pertanyaan dan percobaan.
- Satu pengguna memiliki banyak percobaan kuis, jawaban melalui percobaan, serta catatan progres materi dan lab.
- Gunakan foreign key dan indeks pada kolom relasi.
- Penghapusan level, materi, atau lab dilarang bila masih memiliki konten turunan atau progres terkait. Gunakan unpublish untuk menyembunyikan konten yang sudah dipakai.
- Kategori ditunda bersama fitur pencarian/filter FR-10.

## 12. Kebutuhan Nonfungsional

### Keamanan
- Gunakan `password_hash()` dan `password_verify()` untuk kata sandi.
- Gunakan prepared statements (PDO atau MySQLi) untuk query yang menerima input.
- Validasi dan sanitasi input di sisi server.
- Escape output HTML untuk mencegah XSS.
- Terapkan perlindungan CSRF untuk formulir perubahan data.
- Periksa sesi dan role pada setiap halaman admin dan endpoint aksi.
- Regenerasi ID sesi setelah login.
- Satu sesi aktif per browser; login sebagai peran lain mengakhiri sesi sebelumnya.
- Terapkan pembatasan percobaan login gagal di sisi server.
- Atur cookie sesi dengan `HttpOnly`, `SameSite`, dan `Secure` saat HTTPS.
- Jangan menampilkan kata sandi atau detail koneksi database pada pesan error.
- File konfigurasi sensitif tidak boleh dapat diakses publik.
- Hapus atau nonaktifkan skrip pembuatan admin awal setelah digunakan.

### Kinerja dan Kompatibilitas
- Berjalan pada PHP dan MySQL yang didukung versi XAMPP yang digunakan.
- Antarmuka responsif untuk ponsel, tablet, dan desktop.
- Gunakan pagination pada daftar yang panjang.
- Hindari query berulang yang tidak diperlukan.

### Kemudahan Pemeliharaan
- Pisahkan konfigurasi database, autentikasi, logika, dan tampilan secara wajar.
- Gunakan nama variabel, tabel, dan file yang konsisten.
- Berikan pesan validasi yang mudah dimengerti.
- Dokumentasikan cara instalasi dan struktur database.

### Aksesibilitas dan Usabilitas
- Form memiliki label yang jelas.
- Navigasi konsisten.
- Pesan sukses dan gagal mudah dikenali.
- Tombol hapus meminta konfirmasi.
- Kesalahan input ditampilkan dekat dengan bagian yang perlu diperbaiki.

## 13. Teknologi

| Lapisan | Teknologi |
|---|---|
| Backend | PHP |
| Database | MySQL/MariaDB |
| Struktur halaman | HTML |
| Tampilan | CSS |
| Interaksi sisi klien | JavaScript |
| Lingkungan pengembangan | XAMPP |
| Pengelolaan database | phpMyAdmin |
| Kontrol versi (disarankan) | Git |

Gunakan JavaScript untuk meningkatkan pengalaman pengguna, tetapi validasi, penilaian kuis, dan pemeriksaan hak akses tetap dilakukan di server.

## 14. Struktur Folder yang Disarankan

```text
konjar/
├── index.php
├── config/
│   └── database.php
├── includes/
│   ├── auth.php
│   ├── functions.php
│   ├── header.php
│   └── footer.php
├── assets/
│   ├── css/
│   ├── js/
│   └── images/
├── auth/
│   ├── login.php
│   ├── register.php
│   └── logout.php
├── user/
│   ├── dashboard.php
│   ├── learning_path.php
│   ├── material.php
│   ├── lab.php
│   ├── quiz.php
│   ├── quiz_result.php
│   ├── history.php
│   └── progress.php
├── admin/
│   ├── login.php
│   ├── dashboard.php
│   ├── levels/
│   ├── materials/
│   ├── labs/
│   ├── quizzes/
│   └── (tidak ada skrip pembuatan admin yang dapat diakses melalui web)
├── database/
│   └── konjar.sql
└── README.md
```

Struktur ini adalah rekomendasi, bukan kewajiban. Jika kode yang sudah ada memiliki struktur berbeda, perubahan sebaiknya mengikuti struktur proyek tersebut dan tidak mengganti nama file secara sembarangan.

## 15. Kriteria Penerimaan (Acceptance Criteria)

### Autentikasi
- [ ] Registrasi menolak email duplikat.
- [ ] Login dengan kredensial salah menampilkan pesan yang aman.
- [ ] Admin dan pengguna diarahkan ke dashboard masing-masing.
- [ ] Pengguna biasa tidak dapat membuka URL admin secara langsung.
- [ ] Logout mengakhiri sesi.

### CRUD Admin
- [ ] Admin dapat menambah, melihat, mengedit, dan menghapus level.
- [ ] Admin dapat menambah, melihat, mengedit, dan menghapus materi.
- [ ] Admin dapat menambah, melihat, mengedit, dan menghapus lab.
- [ ] Admin dapat membuat kuis dan mengelola pertanyaan A–D.
- [ ] Input wajib dan relasi database divalidasi.
- [ ] Konten draf tidak terlihat pada halaman belajar pengguna.
- [ ] Konten terbit tampil pada Learning Path sesuai levelnya.

### Kuis dan Progres
- [ ] Jawaban dinilai di server dan nilai sesuai dengan kunci jawaban.
- [ ] Nilai dan status kelulusan disimpan.
- [ ] Pengguna hanya dapat melihat riwayat kuis miliknya.
- [ ] Progres tersimpan dan tampil konsisten setelah login kembali.

### Antarmuka
- [ ] Halaman utama dapat digunakan pada layar ponsel dan desktop.
- [ ] Navigasi admin dan pengguna jelas dan terpisah.
- [ ] Form menampilkan pesan validasi yang dapat dipahami.

## 16. Prioritas Pengembangan

### Tahap 1 — Fondasi
- Struktur folder.
- Database dan koneksi.
- Registrasi/login pengguna.
- Login admin dan kontrol role.
- Dashboard terpisah.

### Tahap 2 — CMS Admin
- CRUD level.
- CRUD materi.
- CRUD lab.
- CRUD kuis, pertanyaan, dan pembahasan.
- Status draf dan publikasi.

### Tahap 3 — Pembelajaran Pengguna
- Learning Path.
- Halaman detail materi dan lab.
- Pengerjaan kuis.
- Penilaian dan riwayat nilai.

### Tahap 4 — Progres dan Penyempurnaan
- Pelacakan progres materi dan lab.
- Perbaikan responsivitas dan aksesibilitas.
- Pengujian keamanan, integrasi, dan penggunaan.
- Pencarian/filter dan kategori tetap di luar MVP; dapat dikerjakan setelah MVP stabil.

## 17. Risiko dan Mitigasi

| Risiko | Mitigasi |
|---|---|
| Pengguna biasa mengakses URL admin | Pemeriksaan role di sisi server pada setiap halaman dan aksi |
| SQL injection | Prepared statements |
| XSS pada konten materi | Escape output dan kebijakan format konten |
| Nilai kuis dimanipulasi dari browser | Hitung nilai di server dan simpan hasil dari proses server |
| Konten hilang saat level dihapus | Periksa relasi dan larang penghapusan jika masih dipakai, atau sediakan proses pemindahan |
| Konten draf terlihat oleh pengguna | Filter status publikasi pada query pengguna |
| Struktur proyek berkembang tidak konsisten | Dokumentasi struktur dan konvensi penamaan |

## 18. Asumsi dan Keputusan yang Ditetapkan untuk v1.1

Keputusan berikut mengikuti saran default pada Daftar Verifikasi PRD Konjar v1.0. Jika pemilik produk mengubah keputusan, revisi PRD dan skema database sebelum implementasi terkait dimulai.

- Nama produk, folder proyek, dan database: `Konjar`, `konjar/`, dan `konjar`.
- Admin dan pengguna menggunakan satu tabel `users` dengan kolom `role`; halaman login tetap terpisah.
- Akun admin pertama dibuat dengan seed SQL atau skrip CLI di luar web root.
- Hanya satu sesi aktif per browser; login lintas peran mengakhiri sesi sebelumnya.
- Konten materi menggunakan Markdown yang diproses aman di server.
- Unggahan MVP hanya gambar JPG/PNG maksimal 2 MB; file `.pkt` dan lampiran umum tidak termasuk.
- Penghapusan level/konten yang masih memiliki konten turunan atau progres dilarang; gunakan unpublish.
- Progres materi dan lab disimpan di tabel berbeda.
- `sort_order` adalah satu-satunya kolom pengurutan level; tidak ada `level_number`.
- Reset kata sandi bukan bagian MVP.
- Kuis dapat diulang tanpa batas; nilai tertinggi menjadi nilai utama.
- Batas waktu diperiksa di server dan jawaban yang tersedia dikirim otomatis saat waktu habis.
- Nilai dibulatkan ke bilangan bulat terdekat; jawaban kosong dihitung salah; pembahasan selalu ditampilkan setelah submit.
- Learning Path tidak mengunci level.
- Progres = (materi dan lab terbit yang selesai) ÷ (seluruh materi dan lab terbit); status lulus kuis ditampilkan terpisah.
- Kuis yang sudah memiliki percobaan tidak dapat diedit; unpublish kuis lama dan buat kuis baru.
- Lab dapat terhubung ke materi melalui `material_id` opsional.
- Pratinjau kuis admin tidak disimpan.
- Pengunjung hanya melihat daftar level dan ringkasan, bukan isi materi lengkap.
- `users.status` menggunakan `active` atau `blocked`; pengelolaan dilakukan manual melalui database untuk MVP.
- Simulasi dan troubleshooting termasuk bagian lab; penyelesaian lab menggunakan klaim pengguna.
- Laporan admin berada di luar MVP.
- Deployment awal lokal menggunakan XAMPP; hosting dibahas setelah Tahap 4.
- Target awal adalah level 1–2 lengkap dan materi netral vendor.
- Metrik keberhasilan, rencana uji, dan jadwal disusun saat evaluasi pengembangan v1.1 dan sebelum implementasi final.

## 19. Definisi Selesai (Definition of Done)

Sebuah fitur dianggap selesai jika:
1. Alur utama berjalan sesuai kebutuhan.
2. Input divalidasi di sisi server.
3. Hak akses diperiksa.
4. Data disimpan atau dibaca dari database dengan benar.
5. Pesan sukses dan gagal tersedia.
6. Tampilan dapat digunakan di ponsel dan desktop.
7. Pengujian dasar fitur dan kasus gagal dilakukan.
8. Petunjuk instalasi atau penggunaan diperbarui bila diperlukan.

---

**Dokumen terkait:** `README.md` untuk cara instalasi dan penggunaan proyek; `database/konjar.sql` untuk skema database dan data awal.
