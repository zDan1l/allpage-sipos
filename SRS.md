


SOFTWARE REQUIREMENT SPECIFICATION
(SRS)

SiPosya
Sistem Informasi Posyandu Digital


Dipersiapkan oleh:
Kelompok 12 TI-C1

Brillian Arhaburrizqi Kusuma   –   434241002
Ziyaa Danil Mubarok   –   434241034
Juanne Meilanie Raya M   –   434241026
Rafael Anandi Bagus Sadewo   –   434241025
Muhammad Javier Rakha Abhista   –   434241021


Program Studi D4 Teknik Informatika
Fakultas Vokasi – Universitas Airlangga
Surabaya, 2026



Versi 1.0   |   Oktober 2026


RIWAYAT REVISI DOKUMEN

Versi	Tanggal	Deskripsi Perubahan	Penulis
1.0	Oktober 2026	Draft awal SRS – mencakup seluruh kebutuhan MVP SiPosya	Kelompok 12 TI-C1


DAFTAR ISI

1.  Pendahuluan	4
  1.1  Tujuan Dokumen	4
  1.2  Ruang Lingkup Sistem	4
  1.3  Definisi, Akronim, dan Singkatan	5
  1.4  Referensi	5
  1.5  Gambaran Umum Dokumen	5
2.  Deskripsi Umum Sistem	6
  2.1  Perspektif Produk	6
  2.2  Fungsi Utama Sistem	6
  2.3  Karakteristik Pengguna	7
  2.4  Batasan Sistem	7
  2.5  Asumsi dan Dependensi	8
3.  Kebutuhan Fungsional	8
  3.1  Modul Autentikasi	8
  3.2  Modul Dashboard Kader (Input Data)	9
  3.3  Modul Riwayat Kesehatan Anak Digital	11
  3.4  Modul Pengingat Jadwal Otomatis	12
  3.5  Modul Grafik Pertumbuhan & Status	13
  3.6  Modul Pemantauan Kehadiran	14
  3.7  Modul Rekap & Laporan Bulanan	14
4.  Kebutuhan Non-Fungsional	15
  4.1  Performa	15
  4.2  Keamanan	15
  4.3  Kegunaan (Usability)	16
  4.4  Ketersediaan (Availability)	16
  4.5  Skalabilitas	16
  4.6  Kompatibilitas	16
5.  Kebutuhan Antarmuka Eksternal	17
  5.1  Antarmuka Pengguna	17
  5.2  Antarmuka Perangkat Keras	17
  5.3  Antarmuka Perangkat Lunak	17
  5.4  Antarmuka Komunikasi	17
6.  Batasan Perancangan	18
7.  Prioritas dan Tahapan Implementasi (MVP)	18
8.  Lampiran	19


1.  PENDAHULUAN
1.1  Tujuan Dokumen
Dokumen Software Requirement Specification (SRS) ini mendeskripsikan secara lengkap kebutuhan fungsional dan non-fungsional dari sistem SiPosya (Sistem Informasi Posyandu Digital). Dokumen ini ditujukan kepada tim pengembang, pemangku kepentingan, dan penguji sistem sebagai acuan dalam proses perancangan, implementasi, dan validasi perangkat lunak.
SiPosya adalah aplikasi web responsif yang dirancang untuk mendigitalisasi layanan Posyandu Kartini IV A. Sistem ini menggantikan proses pencatatan manual berbasis dokumen fisik dengan solusi digital terintegrasi yang dapat diakses melalui peramban web di komputer maupun perangkat seluler.
1.2  Ruang Lingkup Sistem
SiPosya merupakan sistem informasi berbasis web responsif yang mencakup dua peran pengguna utama:
•  Kader Posyandu – mengelola data peserta, mencatat hasil pengukuran, memantau kehadiran, dan menghasilkan laporan bulanan.
•  Peserta Posyandu (orang tua/wali balita) – mengakses riwayat kesehatan anak, melihat grafik pertumbuhan, dan menerima pengingat jadwal kunjungan.

Sistem ini bertujuan untuk:
•  Mengurangi beban administrasi manual kader yang saat ini membutuhkan 1–5 jam per kegiatan.
•  Memastikan riwayat kesehatan anak tersimpan aman secara digital sehingga tidak bergantung pada Buku KIA fisik.
•  Memberikan notifikasi jadwal otomatis kepada peserta untuk mengurangi absensi yang tidak terencana.
•  Menyajikan grafik pertumbuhan anak yang mudah dipahami oleh orang tua.
•  Menghasilkan laporan bulanan ke Puskesmas secara otomatis.

Sistem ini tidak mencakup: integrasi langsung dengan sistem informasi Puskesmas, fitur telemedisin, dan pengelolaan keuangan Posyandu.
1.3  Definisi, Akronim, dan Singkatan
Istilah	Definisi
SiPosya	Sistem Informasi Posyandu Digital – nama aplikasi yang dikembangkan
SRS	Software Requirement Specification – dokumen spesifikasi kebutuhan perangkat lunak
Posyandu	Pos Pelayanan Terpadu – layanan kesehatan dasar tingkat kelurahan/RT/RW
Kader	Pengurus/petugas Posyandu yang mengelola pelayanan dan administrasi data
Peserta	Orang tua/wali balita yang membawa anak untuk pemantauan di Posyandu
Buku KIA	Buku Kesehatan Ibu dan Anak – dokumen fisik pencatatan kesehatan anak
KMS	Kartu Menuju Sehat – kartu pemantauan pertumbuhan balita
MVP	Minimum Viable Product – versi produk dengan fitur minimal yang fungsional
UI	User Interface – antarmuka pengguna
API	Application Programming Interface – antarmuka pemrograman aplikasi
CRUD	Create, Read, Update, Delete – operasi dasar pengelolaan data
WHO	World Health Organization – digunakan sebagai referensi standar pertumbuhan anak
1.4  Referensi
•  Laporan Proyek Design Thinking – Studi Kasus: Digitalisasi Layanan Posyandu, Kelompok 12 TI-C1, Universitas Airlangga, 2026.
•  Kementerian Kesehatan RI. (2011). Pedoman Umum Pengelolaan Posyandu.
•  Kementerian Kesehatan RI. (2023). Profil Kesehatan Indonesia Tahun 2022.
•  Plattner, H., Meinel, C., & Leifer, L. (2009). Design Thinking: Understand – Improve – Apply. Springer.
•  Standar pertumbuhan anak WHO (WHO Child Growth Standards).
1.5  Gambaran Umum Dokumen
Dokumen ini disusun dalam delapan bab. Bab 1 memuat pendahuluan dan konteks sistem. Bab 2 mendeskripsikan gambaran umum produk. Bab 3 merinci seluruh kebutuhan fungsional per modul. Bab 4 memuat kebutuhan non-fungsional. Bab 5 menjelaskan antarmuka eksternal. Bab 6 memuat batasan perancangan. Bab 7 menetapkan prioritas dan tahapan implementasi MVP. Bab 8 adalah lampiran pendukung.


2.  DESKRIPSI UMUM SISTEM
2.1  Perspektif Produk
SiPosya adalah sistem baru yang berdiri sendiri (stand-alone) dan dibangun untuk menggantikan proses administrasi manual di Posyandu. Sistem ini terdiri dari satu aplikasi web responsif yang dapat diakses melalui peramban modern di komputer desktop maupun perangkat seluler tanpa memerlukan instalasi aplikasi tambahan.
Arsitektur sistem menggunakan pendekatan client-server dengan komponen utama sebagai berikut:
•  Front-end Web (Responsive) – antarmuka yang dapat diakses kader dan peserta melalui peramban web.
•  Back-end Server – logika bisnis, manajemen sesi, dan pemrosesan data.
•  Database Terintegrasi (Cloud) – penyimpanan terpusat yang menjamin data kader dan peserta saling terhubung secara real-time.
•  Notification Engine – sistem pengiriman notifikasi melalui push notification dan WhatsApp sebagai jalur cadangan.
2.2  Fungsi Utama Sistem
SiPosya menyediakan tujuh modul fungsional utama yang terbagi dalam dua prioritas implementasi:

Prioritas 1 – MVP (Rilis Pertama):
•  Modul Autentikasi – registrasi, login, dan manajemen dua peran (kader dan peserta).
•  Modul Dashboard Kader (I-4) – pencatatan data pengukuran peserta secara digital menggunakan form berbasis dropdown.
•  Modul Riwayat Kesehatan Anak Digital (I-1) – penyimpanan dan tampilan riwayat timbang, ukur, dan imunisasi anak secara digital.
•  Modul Pengingat Jadwal Otomatis (I-2) – notifikasi bertingkat H-3, H-1, dan hari-H dengan WhatsApp sebagai jalur cadangan.
•  Modul Grafik Pertumbuhan & Status (I-3) – visualisasi perkembangan berat dan tinggi badan anak dengan indikator normal/perlu perhatian.

Prioritas 2 – Iterasi Berikutnya:
•  Modul Pemantauan Kehadiran (I-6) – penandaan dan pemantauan peserta yang absen berturut-turut.
•  Modul Rekap & Laporan Bulanan (I-5) – pembuatan laporan ke Puskesmas dengan satu klik.
2.3  Karakteristik Pengguna
Peran	Deskripsi	Kemampuan Teknis	Kebutuhan Khusus
Kader Posyandu	Pengurus Posyandu berusia 33–67 tahun, mayoritas ibu rumah tangga dengan beban kerja ganda	Dasar – terbiasa WhatsApp dan form cetak; beberapa belum familiar dengan aplikasi web	Antarmuka sangat sederhana, ukuran teks cukup besar, proses input minimal, tersedia pelatihan awal
Peserta Posyandu	Orang tua/wali balita berusia 28–43 tahun, aktif menggunakan smartphone sehari-hari	Menengah – menggunakan WhatsApp dan media sosial setiap hari	Akses riwayat mudah, tampilan grafik intuitif, notifikasi proaktif
Administrator Sistem	Pengelola teknis sistem (dapat berperan ganda sebagai kader senior atau pengelola IT)	Lanjutan – memahami konsep dasar sistem informasi	Akses manajemen data dan konfigurasi sistem
2.4  Batasan Sistem
Berikut adalah batasan yang berlaku pada sistem SiPosya:
•  Sistem hanya mencakup satu unit Posyandu pada versi MVP (Posyandu Kartini IV A). Fitur multi-Posyandu dapat ditambahkan pada iterasi berikutnya.
•  Standar pertumbuhan yang digunakan adalah standar WHO (Weight-for-Age, Height-for-Age, dan BMI-for-Age) yang telah diadopsi Kementerian Kesehatan RI.
•  Sistem tidak menyimpan foto atau dokumen lampiran pada versi MVP.
•  Notifikasi WhatsApp menggunakan layanan pihak ketiga (misalnya WhatsApp Business API atau Twilio); ketersediaannya bergantung pada konfigurasi integrasi.
•  Sistem memerlukan koneksi internet untuk mengakses dan menyinkronkan data. Mode offline tidak tersedia pada versi MVP.
•  Bahasa antarmuka sistem adalah Bahasa Indonesia.
•  Sistem tidak menggantikan konsultasi medis profesional; seluruh informasi yang ditampilkan bersifat indikatif dan informatif.
2.5  Asumsi dan Dependensi
Asumsi:
•  Seluruh kader Posyandu memiliki akses ke perangkat seluler atau komputer dengan koneksi internet minimal saat pelaksanaan kegiatan bulanan.
•  Peserta Posyandu memiliki nomor WhatsApp aktif yang dapat digunakan sebagai media notifikasi.
•  Data jadwal kegiatan Posyandu dimasukkan oleh kader ke dalam sistem secara manual untuk versi MVP.
Dependensi:
•  Layanan cloud storage dan database untuk penyimpanan data terpusat.
•  Layanan pengiriman notifikasi (push notification web dan/atau WhatsApp Business API).
•  Standar data pertumbuhan WHO yang diadopsi Kemenkes RI sebagai referensi indikator status.


3.  KEBUTUHAN FUNGSIONAL
Setiap kebutuhan fungsional diberi kode unik dengan format [MODUL-XXX] untuk kemudahan penelusuran. Kolom Prioritas menggunakan skala: Tinggi (T), Sedang (S), dan Rendah (R). Kolom MVP menandai apakah fitur termasuk dalam rilis pertama.
3.1  Modul Autentikasi (AUTH)
Modul ini mengelola proses registrasi, login, pengelolaan sesi, dan manajemen dua peran pengguna dalam sistem.

ID	Deskripsi Kebutuhan	Prioritas	MVP
AUTH-001	Sistem menyediakan halaman registrasi akun baru untuk peserta Posyandu. Data yang diperlukan: nama lengkap, nomor WhatsApp, kata sandi, serta nomor ID anak yang didaftarkan oleh kader.	T	Ya
AUTH-002	Sistem menyediakan halaman login dengan autentikasi menggunakan nomor WhatsApp dan kata sandi.	T	Ya
AUTH-003	Sistem membedakan dua peran pengguna (kader dan peserta) dan mengarahkan masing-masing ke halaman dashboard yang sesuai setelah login berhasil.	T	Ya
AUTH-004	Sistem menyediakan fitur lupa kata sandi dengan verifikasi melalui nomor WhatsApp terdaftar.	S	Ya
AUTH-005	Sistem secara otomatis mengakhiri sesi (logout) setelah periode tidak aktif selama 30 menit untuk alasan keamanan.	S	Ya
AUTH-006	Akun kader hanya dapat dibuat oleh administrator sistem (bukan melalui registrasi umum) untuk menjaga integritas data.	T	Ya
AUTH-007	Sistem mencatat log aktivitas login termasuk waktu dan perangkat yang digunakan.	R	Tidak
3.2  Modul Dashboard Kader / Input Data (I-4)
Modul ini merupakan fondasi sistem (enabler) yang memungkinkan kader menginput data pengukuran peserta secara digital. Data yang diinput di sini mengalir otomatis ke modul riwayat peserta.
3.2.1  Manajemen Data Peserta
ID	Deskripsi Kebutuhan	Prioritas	MVP
KADER-001	Kader dapat menambahkan data peserta baru (balita) meliputi: nama anak, tanggal lahir, jenis kelamin, nama orang tua/wali, nomor WhatsApp orang tua, dan alamat.	T	Ya
KADER-002	Sistem menghasilkan kode ID unik untuk setiap peserta yang terdaftar. Kode ini digunakan peserta untuk menghubungkan akun mereka ke data anak.	T	Ya
KADER-003	Kader dapat mencari data peserta berdasarkan nama anak, nama orang tua, atau kode ID dengan hasil yang tampil secara instan (pencarian real-time).	T	Ya
KADER-004	Kader dapat memperbarui informasi data peserta yang sudah ada.	T	Ya
KADER-005	Kader dapat melihat daftar seluruh peserta yang terdaftar beserta status kehadiran terakhir.	T	Ya
KADER-006	Sistem menampilkan peringatan apabila peserta belum hadir selama dua bulan berturut-turut.	S	Tidak
3.2.2  Input Hasil Pengukuran
ID	Deskripsi Kebutuhan	Prioritas	MVP
KADER-007	Kader dapat mencatat hasil pengukuran per kunjungan yang mencakup: tanggal kunjungan, berat badan (kg), tinggi/panjang badan (cm), lingkar kepala (cm, opsional), serta status imunisasi yang diberikan pada kunjungan tersebut.	T	Ya
KADER-008	Sistem menyediakan form input berbasis dropdown dan pilihan ganda (bukan teks bebas) untuk meminimalkan kesalahan input dan mempercepat proses pencatatan.	T	Ya
KADER-009	Sistem melakukan validasi otomatis terhadap nilai yang diinput (contoh: berat badan balita tidak boleh melebihi 50 kg; tinggi badan tidak boleh kurang dari 30 cm) dan menampilkan pesan kesalahan yang jelas apabila validasi gagal.	T	Ya
KADER-010	Setelah data pengukuran tersimpan, sistem secara otomatis menghitung dan menampilkan status pertumbuhan anak (Normal, Perlu Perhatian, atau Kritis) berdasarkan tabel standar WHO.	T	Ya
KADER-011	Kader dapat menambahkan catatan teks singkat (maks. 200 karakter) per kunjungan untuk informasi tambahan seperti kondisi anak atau saran gizi.	S	Ya
KADER-012	Sistem mencatat nama kader yang menginput data serta waktu input secara otomatis (audit trail).	S	Ya
KADER-013	Kader dapat mengedit data pengukuran yang sudah diinput dalam batas waktu 24 jam setelah penyimpanan.	S	Ya
3.2.3  Manajemen Jadwal Kegiatan
ID	Deskripsi Kebutuhan	Prioritas	MVP
KADER-014	Kader dapat menetapkan dan mengubah jadwal kegiatan Posyandu bulanan (tanggal dan waktu pelaksanaan).	T	Ya
KADER-015	Kader dapat menetapkan jadwal imunisasi untuk masing-masing peserta berdasarkan rekomendasi program imunisasi nasional.	T	Ya
KADER-016	Sistem menampilkan kalender kegiatan yang memperlihatkan jadwal Posyandu dan jadwal imunisasi peserta dalam satu tampilan.	S	Ya
3.3  Modul Riwayat Kesehatan Anak Digital (I-1)
Modul ini menyediakan akses bagi peserta terhadap riwayat kesehatan anak secara digital, menggantikan ketergantungan pada Buku KIA fisik.
ID	Deskripsi Kebutuhan	Prioritas	MVP
RIWAYAT-001	Peserta dapat melihat riwayat lengkap hasil pengukuran anak (berat badan, tinggi badan, lingkar kepala) yang diinput kader, diurutkan dari kunjungan terbaru ke terlama.	T	Ya
RIWAYAT-002	Sistem menampilkan riwayat imunisasi anak secara lengkap, mencakup: jenis vaksin, tanggal pemberian, dan status (sudah/belum/terjadwal).	T	Ya
RIWAYAT-003	Data riwayat anak tersimpan di cloud dan dapat diakses kapan saja melalui peramban web, bahkan jika Buku KIA fisik hilang atau rusak.	T	Ya
RIWAYAT-004	Peserta dapat melihat catatan kader yang terlampir pada setiap kunjungan.	S	Ya
RIWAYAT-005	Sistem menampilkan ringkasan kondisi terkini anak di halaman utama peserta, mencakup: berat badan terakhir, tinggi badan terakhir, dan tanggal kunjungan terakhir.	T	Ya
RIWAYAT-006	Peserta dapat menyaring (filter) tampilan riwayat berdasarkan rentang waktu (bulan/tahun).	S	Ya
RIWAYAT-007	Sistem menampilkan label status pertumbuhan (Normal / Perlu Perhatian / Kritis) pada setiap entri riwayat dan pada ringkasan kondisi terkini.	T	Ya
RIWAYAT-008	Satu akun peserta dapat mengelola riwayat lebih dari satu anak (untuk peserta yang memiliki beberapa balita).	S	Ya
3.4  Modul Pengingat Jadwal Otomatis (I-2)
Modul ini mengirimkan notifikasi proaktif kepada peserta untuk mengurangi absensi yang tidak terencana dan memastikan jadwal imunisasi tidak terlewat.
ID	Deskripsi Kebutuhan	Prioritas	MVP
NOTIF-001	Sistem mengirimkan notifikasi web push secara otomatis pada H-3 (tiga hari sebelum), H-1 (satu hari sebelum), dan hari-H (pada pagi hari pukul 07.00 WIB) untuk mengingatkan peserta tentang jadwal kunjungan Posyandu.	T	Ya
NOTIF-002	Apabila notifikasi web push tidak terbaca (ditandai tidak dibuka dalam 2 jam), sistem mengirimkan pesan WhatsApp sebagai jalur cadangan melalui layanan WhatsApp Business API.	T	Ya
NOTIF-003	Sistem mengirimkan notifikasi khusus untuk mengingatkan jadwal imunisasi anak dengan mekanisme yang sama (H-3, H-1, hari-H) disertai informasi jenis imunisasi yang akan diberikan.	T	Ya
NOTIF-004	Peserta dapat mengaktifkan atau menonaktifkan notifikasi web push melalui halaman pengaturan akun.	S	Ya
NOTIF-005	Kader dapat mengirimkan notifikasi pengumuman khusus (misalnya perubahan jadwal atau informasi kesehatan) kepada seluruh peserta atau peserta tertentu melalui dashboard kader.	S	Ya
NOTIF-006	Sistem mencatat log pengiriman notifikasi beserta status pengiriman (berhasil/gagal) untuk setiap peserta.	R	Tidak
NOTIF-007	Isi pesan notifikasi ditulis dalam Bahasa Indonesia yang sederhana dan mudah dipahami oleh segala kalangan.	T	Ya
3.5  Modul Grafik Pertumbuhan & Status (I-3)
Modul ini menyajikan visualisasi perkembangan anak secara grafis sehingga orang tua dapat memahami kondisi pertumbuhan anak dari waktu ke waktu tanpa memerlukan keahlian medis khusus.
ID	Deskripsi Kebutuhan	Prioritas	MVP
GRAFIK-001	Sistem menampilkan grafik garis perkembangan berat badan anak dari waktu ke waktu, dilengkapi garis referensi standar WHO (Median, -2 SD, +2 SD) yang divisualisasikan dalam warna berbeda.	T	Ya
GRAFIK-002	Sistem menampilkan grafik garis perkembangan tinggi/panjang badan anak dari waktu ke waktu dengan referensi standar WHO yang serupa.	T	Ya
GRAFIK-003	Setiap titik data pada grafik menampilkan tooltip atau keterangan ketika diklik/disentuh, berisi: tanggal pengukuran, nilai pengukuran, dan status (Normal/Perlu Perhatian/Kritis).	T	Ya
GRAFIK-004	Grafik menyertakan legenda yang jelas dan keterangan sumbu (sumbu X: waktu dalam format Bulan/Tahun; sumbu Y: nilai pengukuran beserta satuannya).	T	Ya
GRAFIK-005	Sistem menampilkan kartu status pertumbuhan yang merangkum kondisi terkini anak dalam format yang mudah dipahami (contoh: "Berat badan Anak dalam batas normal", atau "Tinggi badan Anak perlu diperhatikan – konsultasikan dengan kader").	T	Ya
GRAFIK-006	Grafik dapat ditampilkan sepenuhnya di layar perangkat seluler (responsive) dengan kemampuan pinch-to-zoom atau geser horizontal untuk melihat data historis.	S	Ya
GRAFIK-007	Kader dapat melihat grafik pertumbuhan seluruh peserta melalui dashboard kader sebagai alat pemantauan kolektif.	S	Ya
3.6  Modul Pemantauan Kehadiran (I-6)
Catatan: Modul ini masuk dalam Prioritas 2 (iterasi berikutnya) dan tidak termasuk dalam rilis MVP.
ID	Deskripsi Kebutuhan	Prioritas	MVP
HADIR-001	Kader dapat menandai kehadiran peserta pada setiap sesi kegiatan Posyandu secara digital melalui daftar peserta yang tersedia di dashboard.	T	Tidak
HADIR-002	Sistem secara otomatis menandai dan menampilkan daftar peserta yang absen berturut-turut selama dua bulan atau lebih.	T	Tidak
HADIR-003	Sistem menampilkan persentase tingkat kehadiran per peserta dalam rentang waktu yang dapat dipilih.	S	Tidak
HADIR-004	Kader dapat mengekspor data kehadiran dalam format yang dapat dicetak atau disimpan.	R	Tidak
3.7  Modul Rekap & Laporan Bulanan (I-5)
Catatan: Modul ini masuk dalam Prioritas 2 (iterasi berikutnya) dan tidak termasuk dalam rilis MVP.
ID	Deskripsi Kebutuhan	Prioritas	MVP
LAPORAN-001	Sistem menghasilkan laporan bulanan secara otomatis berdasarkan data yang telah diinput kader selama periode satu bulan, mencakup: rekapitulasi jumlah peserta hadir, rata-rata berat dan tinggi badan, serta status pertumbuhan kolektif.	T	Tidak
LAPORAN-002	Kader dapat mengunduh laporan bulanan dalam format PDF dan/atau spreadsheet (.xlsx) dengan satu klik.	T	Tidak
LAPORAN-003	Sistem menyediakan rangkuman statistik bulanan dalam bentuk visual (kartu angka dan grafik batang) yang dapat dilihat langsung di dashboard kader.	S	Tidak
LAPORAN-004	Kader dapat menyesuaikan periode laporan (misalnya laporan tiga bulan atau kuartal).	R	Tidak


4.  KEBUTUHAN NON-FUNGSIONAL
4.1  Performa
ID	Deskripsi Kebutuhan	Target
PERF-001	Waktu muat halaman utama (first contentful paint) pada koneksi jaringan 4G atau lebih cepat.	Maks. 3 detik
PERF-002	Waktu respons penyimpanan data pengukuran oleh kader setelah tombol simpan ditekan.	Maks. 2 detik
PERF-003	Waktu muat halaman grafik pertumbuhan termasuk rendering grafis.	Maks. 4 detik
PERF-004	Sistem mampu melayani pengguna bersamaan tanpa penurunan performa yang signifikan.	Min. 50 pengguna bersamaan
PERF-005	Waktu pengiriman notifikasi push setelah waktu yang dijadwalkan tercapai.	Maks. 5 menit
4.2  Keamanan
ID	Deskripsi Kebutuhan	Keterangan
SEC-001	Seluruh komunikasi antara klien dan server menggunakan protokol HTTPS/TLS.	Wajib
SEC-002	Kata sandi pengguna disimpan dalam bentuk hash menggunakan algoritma bcrypt (salt rounds ≥ 10) dan tidak pernah disimpan dalam bentuk teks biasa.	Wajib
SEC-003	Sesi pengguna menggunakan JSON Web Token (JWT) atau mekanisme sesi yang setara dengan masa berlaku token yang terbatas.	Wajib
SEC-004	Sistem menerapkan pembatasan akses berbasis peran (Role-Based Access Control) sehingga peserta tidak dapat mengakses data peserta lain atau fitur khusus kader.	Wajib
SEC-005	Sistem melindungi data kesehatan sesuai prinsip privasi data (data anak hanya dapat diakses oleh orang tua/wali yang terdaftar dan kader yang berwenang).	Wajib
SEC-006	Sistem menerapkan proteksi terhadap serangan umum web: SQL Injection, Cross-Site Scripting (XSS), dan Cross-Site Request Forgery (CSRF).	Wajib
SEC-007	Sistem membatasi jumlah percobaan login yang gagal (maks. 5 kali sebelum akun dikunci sementara selama 15 menit).	Disarankan
4.3  Kegunaan (Usability)
ID	Deskripsi Kebutuhan	Target
USE-001	Antarmuka dirancang dengan prinsip "mobile-first responsive design" sehingga seluruh fitur dapat digunakan dengan baik di layar perangkat seluler (lebar layar min. 320px) maupun komputer desktop.	Semua resolusi umum
USE-002	Kader yang belum pernah menggunakan sistem mampu menyelesaikan proses input data pengukuran satu peserta tanpa bantuan setelah mendapat pelatihan singkat (maks. 30 menit).	Usability test
USE-003	Ukuran elemen interaktif (tombol, tautan, input form) memenuhi standar aksesibilitas sentuh minimal 44×44 piksel CSS.	WCAG 2.1 AA
USE-004	Pesan kesalahan dan konfirmasi ditulis dalam Bahasa Indonesia yang jelas dan tidak menggunakan kode teknis yang membingungkan pengguna awam.	Plain language
USE-005	Sistem menyediakan indikator visual yang jelas saat proses penyimpanan data sedang berlangsung (loading state) untuk mencegah pengguna menekan tombol berulang kali.	UX requirement
4.4  Ketersediaan (Availability)
ID	Deskripsi Kebutuhan	Target
AVAIL-001	Sistem tersedia dan dapat diakses tanpa gangguan selama jam operasional utama, terutama pada hari pelaksanaan kegiatan Posyandu.	Min. 99% uptime/bulan
AVAIL-002	Pemeliharaan terjadwal (maintenance) dilaksanakan di luar jam operasional (pukul 22.00–05.00 WIB) dan diumumkan minimal 24 jam sebelumnya.	Prosedur operasional
4.5  Skalabilitas
ID	Deskripsi Kebutuhan	Keterangan
SCAL-001	Arsitektur sistem dirancang agar dapat diperluas untuk mendukung lebih dari satu unit Posyandu di masa mendatang tanpa perubahan arsitektur yang fundamental.	Multi-Posyandu
SCAL-002	Database dirancang untuk dapat menyimpan data historis minimal lima tahun untuk setiap peserta tanpa penurunan performa.	Retensi data jangka panjang
4.6  Kompatibilitas
ID	Deskripsi Kebutuhan	Target
COMPAT-001	Sistem kompatibel dengan peramban web modern: Google Chrome (versi 90+), Mozilla Firefox (versi 88+), Safari (versi 14+), dan Microsoft Edge (versi 90+).	Cross-browser
COMPAT-002	Sistem berfungsi dengan baik pada sistem operasi Android 8.0+ dan iOS 13+ saat diakses melalui peramban bawaan maupun Chrome/Safari.	Cross-platform mobile
COMPAT-003	Sistem tidak memerlukan instalasi plugin atau ekstensi peramban tambahan untuk menjalankan seluruh fungsionalitas.	Zero-plugin


5.  KEBUTUHAN ANTARMUKA EKSTERNAL
5.1  Antarmuka Pengguna
Antarmuka pengguna SiPosya dirancang dengan pendekatan web responsif menggunakan tata letak yang bersih dan konsisten. Ketentuan desain antarmuka adalah sebagai berikut:
•  Palet warna utama menggunakan skema yang ramah pengguna dengan kontras cukup untuk keterbacaan.
•  Tipografi menggunakan font sans-serif yang terbaca baik di layar kecil.
•  Navigasi utama menggunakan menu hamburger untuk tampilan seluler dan sidebar untuk tampilan desktop.
•  Sistem menyediakan halaman onboarding singkat (tutorial satu kali) untuk pengguna baru.
•  Seluruh form input menyediakan placeholder yang informatif dan validasi real-time.
5.2  Antarmuka Perangkat Keras
•  Sistem dapat diakses dari perangkat seluler (smartphone/tablet) maupun komputer desktop/laptop.
•  Tidak ada perangkat keras khusus yang diperlukan selain perangkat dengan peramban web dan koneksi internet.
•  Sistem mendukung akses kamera perangkat (opsional, untuk fitur upload foto pada iterasi mendatang).
5.3  Antarmuka Perangkat Lunak
Komponen	Teknologi/Layanan	Fungsi
Database	PostgreSQL / MySQL atau layanan database cloud (misalnya Supabase, PlanetScale)	Penyimpanan data terpusat
Notifikasi Push	Web Push API (standar browser) + Service Worker	Notifikasi di peramban web
Notifikasi WhatsApp	WhatsApp Business API (Twilio / Fonnte / WA Gateway)	Notifikasi jalur cadangan
Grafik	Library JavaScript (Chart.js / Recharts / ApexCharts)	Visualisasi data pertumbuhan
Autentikasi	JWT (JSON Web Token)	Manajemen sesi pengguna
Hosting	Layanan cloud (Vercel / Railway / VPS)	Hosting aplikasi web
5.4  Antarmuka Komunikasi
•  Seluruh komunikasi data antara klien (peramban) dan server menggunakan protokol HTTPS dengan enkripsi TLS 1.2 atau lebih baru.
•  API back-end menggunakan arsitektur RESTful dengan format data JSON.
•  Notifikasi push web menggunakan Web Push Protocol (RFC 8030).
•  Integrasi WhatsApp menggunakan webhook atau API HTTP dari penyedia layanan yang dipilih.


6.  BATASAN PERANCANGAN
Berikut adalah batasan teknis dan non-teknis yang harus diperhatikan selama proses perancangan dan pengembangan SiPosya:
•  Sistem dibangun sebagai aplikasi web responsif (bukan aplikasi mobile native Android/iOS) untuk efisiensi pengembangan dan kemudahan akses tanpa instalasi.
•  Seluruh antarmuka dan konten sistem menggunakan Bahasa Indonesia sebagai bahasa primer.
•  Standar perhitungan status pertumbuhan mengacu pada tabel WHO yang diterbitkan dalam Permenkes No. 2 Tahun 2020 tentang Standar Antropometri Anak.
•  Sistem harus dapat berjalan dengan baik pada koneksi internet dengan kecepatan minimal 1 Mbps (setara koneksi 3G yang stabil).
•  Fitur yang memerlukan integrasi dengan sistem eksternal (misalnya sistem informasi Puskesmas) tidak termasuk dalam cakupan MVP dan akan dievaluasi pada iterasi berikutnya.
•  Anggaran hosting dan infrastruktur pada MVP mengutamakan solusi berbiaya rendah tanpa mengorbankan keamanan dan ketersediaan.
•  Keseluruhan sistem harus dapat dioperasikan dan dipelihara oleh tim non-teknis (kader) tanpa memerlukan intervensi pengembang untuk kegiatan operasional rutin.


7.  PRIORITAS DAN TAHAPAN IMPLEMENTASI (MVP)
Berdasarkan hasil analisis Impact-Effort Matrix pada tahap Ideate, implementasi SiPosya dibagi menjadi dua tahap utama:

7.1  Tahap 1 – MVP (Minimum Viable Product)
Tahap ini mencakup fitur-fitur yang paling kritis dan memberikan nilai tertinggi bagi kedua kelompok pengguna dalam waktu pengembangan yang efisien.
No	Modul	ID Fitur	Justifikasi Prioritas
1	Autentikasi	AUTH-001 s/d AUTH-006	Fondasi sistem; tidak ada modul lain yang dapat berjalan tanpanya
2	Dashboard Kader – Input Data (I-4)	KADER-001 s/d KADER-016	Enabler utama: seluruh data di sistem bersumber dari modul ini
3	Riwayat Kesehatan Anak Digital (I-1)	RIWAYAT-001 s/d RIWAYAT-008	Menjawab pain point utama peserta; menggantikan ketergantungan pada Buku KIA fisik
4	Grafik Pertumbuhan & Status (I-3)	GRAFIK-001 s/d GRAFIK-007	Diserap ke dalam I-1 sebagai fitur visualisasi; meningkatkan nilai riwayat digital
5	Pengingat Jadwal Otomatis (I-2)	NOTIF-001 s/d NOTIF-005, NOTIF-007	Quick win: dampak tinggi, upaya implementasi rendah
7.2  Tahap 2 – Iterasi Berikutnya
Fitur-fitur berikut ditunda dari rilis MVP, namun arsitektur sistem pada Tahap 1 dirancang untuk mengakomodasi penambahan modul-modul ini tanpa perombakan besar.
No	Modul	ID Fitur	Justifikasi Penundaan
1	Pemantauan Kehadiran (I-6)	HADIR-001 s/d HADIR-004	Fungsionalitas penting namun tidak menghalangi manfaat inti MVP; kehadiran masih dapat dicatat manual sambil menunggu
2	Rekap & Laporan Bulanan (I-5)	LAPORAN-001 s/d LAPORAN-004	Kompleksitas implementasi lebih tinggi; kader masih dapat merekap dari data digital yang sudah ada di Tahap 1
3	Log aktivitas login (AUTH-007)	AUTH-007	Fitur administratif pendukung; tidak kritis untuk fungsionalitas utama
4	Log pengiriman notifikasi (NOTIF-006)	NOTIF-006	Fitur monitoring; dapat ditambahkan setelah notifikasi dasar berjalan stabil
7.3  Matriks Keterlacakan Kebutuhan (Traceability Matrix)
Tabel berikut menghubungkan problem statement dan HMW Questions dari tahap Define dengan fitur-fitur yang dikembangkan dalam SRS ini.
Problem Statement / HMW	Modul yang Menjawab	ID Kebutuhan Utama
Pencatatan manual menyita waktu kader (1–5 jam/kegiatan)	Dashboard Kader (I-4)	KADER-007, KADER-008, KADER-009
Kader sulit memantau peserta yang tidak hadir rutin	Pemantauan Kehadiran (I-6)	HADIR-001, HADIR-002
Laporan bulanan ke Puskesmas membutuhkan waktu tambahan	Rekap & Laporan Bulanan (I-5)	LAPORAN-001, LAPORAN-002
Buku KIA mudah hilang, rusak, atau tertinggal	Riwayat Kesehatan Digital (I-1)	RIWAYAT-001, RIWAYAT-002, RIWAYAT-003
Peserta lupa jadwal kunjungan dan imunisasi	Pengingat Jadwal Otomatis (I-2)	NOTIF-001, NOTIF-002, NOTIF-003
Informasi perkembangan anak sulit dipahami dari dokumen fisik	Grafik Pertumbuhan & Status (I-3)	GRAFIK-001, GRAFIK-002, GRAFIK-005


8.  LAMPIRAN
8.1  Daftar Seluruh Kebutuhan Fungsional (Ringkasan)
ID	Modul	Jumlah Kebutuhan	Status MVP
AUTH	Autentikasi	7	MVP: 6 / Iterasi: 1
KADER	Dashboard Kader / Input Data (I-4)	16	MVP: 16 / Iterasi: 0
RIWAYAT	Riwayat Kesehatan Anak Digital (I-1)	8	MVP: 8 / Iterasi: 0
NOTIF	Pengingat Jadwal Otomatis (I-2)	7	MVP: 6 / Iterasi: 1
GRAFIK	Grafik Pertumbuhan & Status (I-3)	7	MVP: 7 / Iterasi: 0
HADIR	Pemantauan Kehadiran (I-6)	4	MVP: 0 / Iterasi: 4
LAPORAN	Rekap & Laporan Bulanan (I-5)	4	MVP: 0 / Iterasi: 4
TOTAL	–	53	MVP: 43 / Iterasi: 10

8.2  Daftar Aktor dan Hak Akses
Fitur / Modul	Administrator	Kader	Peserta
Registrasi & Login	Ya	Ya (dibuat admin)	Ya
Tambah/Edit Data Peserta	Ya	Ya	Tidak
Input Hasil Pengukuran	Ya	Ya	Tidak
Lihat Riwayat Anak (milik sendiri)	Ya	Ya (semua peserta)	Ya (anak sendiri)
Lihat Grafik Pertumbuhan	Ya	Ya (semua peserta)	Ya (anak sendiri)
Kelola Jadwal Kegiatan	Ya	Ya	Tidak
Terima Notifikasi Jadwal	Ya	Tidak	Ya
Kirim Pengumuman	Ya	Ya	Tidak
Pemantauan Kehadiran	Ya	Ya	Tidak
Unduh Laporan Bulanan	Ya	Ya	Tidak
Manajemen Akun Kader	Ya	Tidak	Tidak

8.3  Sumber Data Penelitian
SRS ini disusun berdasarkan data primer yang dikumpulkan melalui:
•  Observasi lapangan di Posyandu Kartini IV A pada tanggal 30 Agustus 2026.
•  Kuesioner yang diisi oleh 5 kader dan 5 peserta Posyandu (30 Agustus – 3 September 2026).
•  Wawancara langsung dengan pengurus Posyandu dan Ibu RT setempat.
•  Simulasi immersive experience pencatatan manual oleh tim peneliti.
•  Analisis Design Thinking: Empathize, Define, dan Ideate (Kelompok 12 TI-C1, 2026).

Dokumen ini disahkan oleh:


Surabaya, Oktober 2026

Tim Pengembang Kelompok 12 TI-C1



Program Studi D4 Teknik Informatika – Fakultas Vokasi – Universitas Airlangga
