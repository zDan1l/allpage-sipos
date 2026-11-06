# Daftar Layar (Screen List) — Aplikasi Mobile SiPosya
### Sistem Informasi Posyandu Digital — Android & iOS

> Dokumen ini menguraikan seluruh layar aplikasi mobile SiPosya beserta konten dan komponen di dalamnya. Acuannya adalah SRS SiPosya v1.0 dan daftar halaman versi web.
> Setiap layar dipetakan ke kode kebutuhan fungsional (mis. `AUTH-002`, `KADER-007`) agar bisa ditelusuri ke SRS.

---

## Keterangan & Konvensi

**Asumsi cakupan**
- Satu aplikasi untuk dua peran: **Orang Tua (Peserta)** dan **Kader**. Setelah login, aplikasi menampilkan navigasi sesuai peran (`AUTH-003`).
- **Administrator tetap menggunakan dashboard web.** Pembuatan akun kader dan konfigurasi sistem (`AUTH-006`) tidak dibawa ke mobile.
- Platform: Android 8.0+ dan iOS 13+ (`COMPAT-002`). Bahasa antarmuka: Bahasa Indonesia.

**Label fase**
- 🟢 **MVP**: rilis pertama, sesuai prioritas SRS.
- 🔵 **Iterasi 2**: Kehadiran, Laporan, dan log (sesuai SRS).
- 🟣 **Usulan Mobile**: layar atau fitur yang muncul karena kebutuhan khas aplikasi mobile dan **tidak tertulis eksplisit di SRS**. Perlu disetujui tim sebelum masuk cakupan.

**Pola desain umum (berlaku di semua layar)**
- **Navigasi bawah (bottom tab bar)** menggantikan sidebar/hamburger versi web.
- **Bottom sheet** untuk pilihan cepat (pilih anak, detail titik grafik, filter) menggantikan dropdown/modal web.
- Tombol & area sentuh min. **44×44 pt** (`USE-003`). Teks cukup besar untuk kader usia 33–67 tahun.
- **Loading state** pada setiap aksi simpan, dan tombol dinonaktifkan selama proses (`USE-005`).
- Pesan error dalam bahasa sehari-hari, tanpa kode teknis (`USE-004`).
- **Pull-to-refresh** pada semua daftar data.
- **Push notification native** (FCM untuk Android, APNs untuk iOS) menggantikan Web Push, dengan WhatsApp sebagai cadangan (`NOTIF-001`, `NOTIF-002`).
- Sesi berakhir otomatis setelah 30 menit tidak aktif (`AUTH-005`), dan login ulang saat aplikasi dibuka kembali.

### Struktur Navigasi

**Orang Tua: 5 tab**

| Tab | Layar utama |
|---|---|
| 🏠 Beranda | B1 Beranda |
| 📋 Riwayat | B4 Riwayat Kesehatan |
| 📈 Grafik | B7 Grafik Pertumbuhan |
| 📅 Jadwal | B9 Jadwal & Kalender |
| 👤 Akun | B13 Akun Saya |

Ikon lonceng 🔔 (Notifikasi) ada di header Beranda.

**Kader: 4 tab + tombol aksi tengah**

| Tab | Layar utama |
|---|---|
| 🏠 Beranda | C1 Dashboard Kader |
| 👥 Peserta | C2 Daftar Peserta |
| ➕ (tombol tengah) | C7 Input Pengukuran |
| 📅 Jadwal | C11 Kelola Jadwal |
| 👤 Akun | C19 Akun Kader |

### Ringkasan Jumlah Layar

| Kelompok | Jumlah | Peran |
|---|---|---|
| A. Umum & Autentikasi | 12 | Semua |
| B. Area Orang Tua | 18 | Peserta |
| C. Area Kader | 20 | Kader |
| D. Komponen & Layar Sistem | 9 | Semua |
| **Total** | **59** | |

Rincian fase: 🟢 MVP 54 layar · 🔵 Iterasi 2 2 layar (C17, C18) · 🟣 Usulan Mobile 3 layar penuh (B16, C6, D5). Sisanya berupa fitur 🟣 di dalam layar MVP.

---

# A. UMUM & AUTENTIKASI
*Ref: Modul Autentikasi (AUTH)*

## A1. Splash Screen 🟢
Layar pertama saat aplikasi dibuka.
**Konten:**
- Logo SiPosya di tengah, latar warna brand (teal).
- Tagline singkat: "Pantau tumbuh kembang anak".
- Indikator memuat kecil di bawah.
- **Logika:** cek sesi tersimpan. Jika masih valid, langsung ke Beranda sesuai peran. Jika tidak, ke Onboarding (pengguna baru) atau Login.

## A2. Onboarding (3 slide) 🟢
*(Ref: bagian 5.1 SRS — tutorial satu kali)*
**Konten:**
- Slide 1: ilustrasi Buku KIA → ponsel. "Riwayat anak tersimpan aman, tidak takut hilang."
- Slide 2: ilustrasi grafik. "Pahami pertumbuhan anak dengan grafik standar WHO."
- Slide 3: ilustrasi lonceng. "Diingatkan sebelum jadwal Posyandu dan imunisasi."
- Indikator titik halaman, tombol **Lewati** dan **Lanjut**, lalu **Mulai** di slide terakhir.
- Hanya tampil sekali dan bisa dibuka lagi dari menu Bantuan.

## A3. Selamat Datang / Pilih Aksi 🟢
**Konten:**
- Ilustrasi keluarga + logo.
- Tombol utama **Masuk**.
- Tombol sekunder **Daftar sebagai Orang Tua**.
- Teks kecil: "Anda kader? Akun kader dibuat oleh admin Posyandu" (`AUTH-006`).
- Tautan Bantuan.

## A4. Login 🟢
*(Ref: `AUTH-002`, `AUTH-003`, `SEC-007`)*
**Konten:**
- Field **Nomor WhatsApp** dengan prefiks +62 dan keyboard angka.
- Field **Kata Sandi** dengan ikon tampil/sembunyikan.
- Checkbox **Ingat saya di perangkat ini**.
- Tombol **Masuk** (dengan loading state).
- Tautan **Lupa kata sandi?** dan **Belum punya akun? Daftar**.
- Pesan error jelas. Setelah 5 kali gagal, akun dikunci 15 menit dan ditampilkan hitung mundurnya.
- **Logika:** setelah berhasil, diarahkan ke Beranda Orang Tua atau Dashboard Kader.

## A5. Registrasi Orang Tua — Langkah 1: Data Diri 🟢
*(Ref: `AUTH-001`)*
**Konten:**
- Indikator langkah (1 dari 3).
- Field: **Nama Lengkap**, **Nomor WhatsApp**.
- Tombol **Lanjut**.

## A6. Registrasi — Langkah 2: Hubungkan Anak 🟢
*(Ref: `AUTH-001`, `KADER-002`)*
**Konten:**
- Field **Kode ID Anak** (mis. PK-0086).
- Kotak info: "Kode ID diberikan kader saat anak didaftarkan di Posyandu."
- 🟣 Tombol **Pindai QR Kartu Anak** sebagai alternatif mengetik kode (lihat C6).
- Setelah kode valid, tampil **kartu konfirmasi**: nama anak, tanggal lahir, jenis kelamin. Pertanyaan: "Apakah ini anak Anda?" dengan tombol **Ya, benar** / **Bukan**.

## A7. Registrasi — Langkah 3: Buat Kata Sandi 🟢
*(Ref: `AUTH-001`, `SEC-002`)*
**Konten:**
- Field **Kata Sandi** + **Konfirmasi**.
- Indikator kekuatan sandi dan daftar syarat (min. 8 karakter, dsb.) yang tercentang secara real-time.
- Checkbox persetujuan **Syarat & Kebijakan Privasi**.
- Tombol **Daftar** → layar A8.

## A8. Verifikasi OTP WhatsApp 🟢
*(Ref: `AUTH-004`; 🟣 dipakai juga saat registrasi)*
**Konten:**
- Teks: "Kode 6 digit dikirim ke WhatsApp +62 812-xxxx-1234".
- 6 kotak input OTP, dengan dukungan autofill.
- Hitung mundur **Kirim ulang kode (0:59)**.
- Tautan **Ganti nomor**.
- Status: kode salah atau kedaluwarsa.

## A9. Lupa Kata Sandi 🟢
*(Ref: `AUTH-004`)*
**Konten:**
- Langkah 1: field **Nomor WhatsApp terdaftar** → tombol **Kirim kode**.
- Langkah 2: verifikasi OTP (memakai komponen A8).
- Langkah 3: **Kata Sandi Baru** + konfirmasi.
- Layar sukses dengan tombol **Kembali ke Login**.

## A10. Izin Notifikasi 🟢
*(Ref: `NOTIF-001`, `NOTIF-004`)*
Tampil setelah login pertama, **sebelum** dialog izin bawaan sistem muncul.
**Konten:**
- Ilustrasi lonceng + contoh notifikasi "Besok imunisasi MR, 08.00".
- Penjelasan manfaat: pengingat H-3, H-1, dan hari-H.
- Tombol **Izinkan Notifikasi** → memicu dialog izin Android/iOS.
- Tautan **Nanti saja** (bisa diaktifkan di Pengaturan).

## A11. Registrasi Berhasil 🟢
**Konten:**
- Ilustrasi sukses (centang + konfeti statis).
- "Akun berhasil dibuat. Data Aisyah sudah terhubung."
- Tombol **Masuk ke Beranda**.

## A12. Syarat Penggunaan & Kebijakan Privasi 🟢
*(Ref: `SEC-005` — privasi data kesehatan anak)*
Dibuka dari checkbox persetujuan di A7 dan dari menu Tentang Aplikasi.
**Konten:**
- Tab: **Syarat Penggunaan** | **Kebijakan Privasi**.
- Ringkasan poin penting di atas (bahasa sederhana): data apa yang disimpan, siapa yang bisa melihat (orang tua + kader berwenang), dan cara menghapus akun.
- Isi lengkap yang bisa digulir + tanggal pembaruan terakhir.
- Tombol **Saya Mengerti** (saat dibuka dari registrasi).

---

# B. AREA ORANG TUA (PESERTA)
*Akses hanya ke data anak sendiri (`SEC-004`, `SEC-005`). Ref: Modul Riwayat I-1, Grafik I-3, Notifikasi I-2.*

## B1. Beranda 🟢
*(Ref: `RIWAYAT-005`, `RIWAYAT-007`, `GRAFIK-005`)*
**Konten:**
- **Header:** sapaan "Halo, Bunda Dewi", ikon 🔔 dengan badge jumlah notifikasi belum dibaca.
- **Pemilih anak** (avatar + nama + usia + ikon ▼) → membuka B2.
- **Kartu ringkasan kondisi terkini** (kartu besar berwarna): berat terakhir, tinggi terakhir, tanggal kunjungan terakhir, label status (Normal / Perlu Perhatian / Kritis), dan grafik mini (sparkline).
- **Kartu status naratif**, mis. "Berat badan Aisyah dalam batas normal. Pertahankan pola makan bergizi."
- **Kartu jadwal terdekat:** tanggal, jam, lokasi Posyandu, dengan tombol **Tambah ke Kalender** 🟣.
- **Imunisasi berikutnya:** nama vaksin + tanggal.
- **Catatan kader terbaru** (jika ada).
- **Pintasan cepat** (grid 4 ikon): Riwayat, Grafik, Imunisasi, Kartu Anak.

## B2. Pilih Anak (Bottom Sheet) 🟢
*(Ref: `RIWAYAT-008`)*
**Konten:**
- Daftar anak terhubung: avatar inisial, nama, usia, label status. Anak aktif diberi tanda centang.
- Tombol **+ Hubungkan anak lain** → B3.

## B3. Hubungkan Anak Baru 🟢
*(Ref: `RIWAYAT-008`, `KADER-002`)*
**Konten:**
- Field **Kode ID Anak** atau 🟣 **Pindai QR**.
- Kartu konfirmasi data anak (nama, tanggal lahir).
- Tombol **Hubungkan**.

## B4. Riwayat Kesehatan 🟢
*(Ref: `RIWAYAT-001`, `RIWAYAT-003`, `RIWAYAT-006`, `RIWAYAT-007`)*
**Konten:**
- Segmented control: **Pengukuran** | **Imunisasi** (tab Imunisasi = B6).
- Tombol **Filter** → bottom sheet rentang waktu (bulan/tahun, 3/6/12 bulan terakhir).
- Daftar kunjungan **terbaru → terlama**, dikelompokkan per tahun.
- Setiap item: tanggal, berat, tinggi, lingkar kepala, label status, dan ikon 📝 jika ada catatan kader.
- Ketuk item → B5.
- Empty state: "Belum ada data kunjungan. Data muncul setelah anak ditimbang di Posyandu."

## B5. Detail Kunjungan 🟢
*(Ref: `RIWAYAT-001`, `RIWAYAT-002`, `RIWAYAT-004`, `RIWAYAT-007`)*
**Konten:**
- Header: tanggal kunjungan + label status.
- Kartu nilai: **Berat**, **Tinggi/Panjang**, **Lingkar Kepala**, masing-masing dengan perubahan dari kunjungan sebelumnya (mis. "+0,4 kg").
- **Imunisasi yang diberikan** pada kunjungan tersebut.
- **Catatan kader** (maks. 200 karakter) + nama kader.
- Tautan **Lihat di grafik** → B7 dengan titik tersorot.

## B6. Imunisasi 🟢
*(Ref: `RIWAYAT-002`, `NOTIF-003`)*
**Konten:**
- Ringkasan progres: "8 dari 12 imunisasi dasar selesai" + progress bar.
- Timeline berdasarkan usia (0 bulan, 1 bulan, 2–4 bulan, 9 bulan, 18 bulan).
- Setiap vaksin: nama, tanggal, status **Sudah / Berikutnya / Terjadwal / Belum**.
- Ketuk vaksin → bottom sheet penjelasan singkat dalam bahasa awam.
- Catatan: jadwal mengikuti program imunisasi nasional dan petugas kesehatan.

## B7. Grafik Pertumbuhan 🟢
*(Ref: `GRAFIK-001` s/d `GRAFIK-006`)*
**Konten:**
- Tab: **Berat Badan** | **Tinggi Badan** (dan IMT jika tersedia).
- Grafik garis anak + **garis referensi WHO** (Median, −2 SD, +2 SD) dalam warna berbeda, dengan zona warna latar (Normal / Perlu Perhatian / Kritis).
- Sumbu X: Bulan/Tahun. Sumbu Y: nilai + satuan. Legenda di bawah grafik.
- **Geser horizontal** dan **pinch-to-zoom** untuk data historis (`GRAFIK-006`).
- Ketuk titik → B8.
- Tombol **⤢ Layar penuh** → mode landscape 🟣.
- **Kartu status pertumbuhan** naratif di bawah grafik (`GRAFIK-005`).

## B8. Detail Titik Grafik (Bottom Sheet) 🟢
*(Ref: `GRAFIK-003`)*
**Konten:**
- Tanggal pengukuran, nilai, status.
- Posisi relatif terhadap standar, mis. "Di antara Median dan +2 SD".
- Tautan **Lihat detail kunjungan** → B5.

## B9. Jadwal & Kalender 🟢
*(Ref: `KADER-016`, `NOTIF-001`, `NOTIF-003`)*
**Konten:**
- Kalender bulanan. Tanggal kegiatan diberi titik warna (hijau = Posyandu, oranye = imunisasi).
- Daftar **Jadwal Mendatang** di bawah kalender.
- Ketuk jadwal → B10.

## B10. Detail Jadwal 🟢
**Konten:**
- Jenis kegiatan (Penimbangan / Imunisasi), tanggal, jam, lokasi.
- Daftar layanan: penimbangan, ukur tinggi, vitamin A, imunisasi (jenis vaksin untuk anak ini).
- Checklist **yang perlu dibawa**: Buku KIA, kartu ID anak.
- Status pengingat: "Anda akan diingatkan H-3, H-1, dan hari-H pukul 07.00."
- Tombol 🟣 **Tambah ke Kalender Ponsel** dan 🟣 **Buka di Peta**.

## B11. Notifikasi 🟢
*(Ref: `NOTIF-001` s/d `NOTIF-005`, `NOTIF-007`)*
**Konten:**
- Filter chip: **Semua** | **Pengingat** | **Pengumuman**.
- Daftar notifikasi dengan ikon jenis (H-3 / H-1 / Hari-H / Imunisasi / Pengumuman kader), judul, potongan isi, dan waktu relatif.
- Penanda belum dibaca (titik + latar tebal). Aksi **Tandai semua dibaca**.
- Ketuk pengingat → B10. Ketuk pengumuman → B12.

## B12. Detail Pengumuman 🟢
*(Ref: `NOTIF-005`)*
**Konten:**
- Judul, nama kader pengirim, tanggal.
- Isi pengumuman lengkap dalam Bahasa Indonesia sederhana.
- Tautan ke jadwal terkait (jika ada).

## B13. Akun Saya 🟢
*(Ref: `RIWAYAT-008`, `NOTIF-004`)*
**Konten:**
- Kartu profil: nama orang tua, nomor WhatsApp, tombol **Edit**.
- Menu: **Anak Saya**, **Kartu Anak Digital** 🟣, **Pengaturan Notifikasi**, **Ubah Kata Sandi**, **Keamanan** 🟣, **Bantuan & FAQ**, **Tentang Aplikasi**.
- Tombol **Keluar** (dengan dialog konfirmasi).

## B14. Edit Profil 🟢
**Konten:**
- Field nama lengkap dan nomor WhatsApp. Perubahan nomor membutuhkan verifikasi OTP (A8).
- Tombol **Simpan**.

## B15. Pengaturan Notifikasi 🟢
*(Ref: `NOTIF-004`)*
**Konten:**
- Toggle utama **Notifikasi Push**.
- Toggle per jenis: Pengingat Posyandu, Pengingat Imunisasi, Pengumuman Kader.
- Info: "WhatsApp tetap dikirim sebagai cadangan jika notifikasi tidak dibuka dalam 2 jam."
- Jika izin sistem dimatikan: banner + tombol **Buka Pengaturan Ponsel**.

## B16. Kartu Anak Digital 🟣 *(Usulan Mobile)*
**Konten:**
- Kartu berisi nama anak, tanggal lahir, **Kode ID**, dan **QR Code** dari Kode ID.
- Tujuan: kader cukup memindai QR di meja pendaftaran untuk langsung membuka data anak (lihat C6).
- Tombol **Simpan ke Galeri** / **Bagikan**.

## B17. Ubah Kata Sandi & Keamanan 🟢 / 🟣
*(Ref: `SEC-002`, `AUTH-005`)*
**Konten:**
- Form sandi lama, sandi baru, dan konfirmasi.
- 🟣 Toggle **Buka dengan sidik jari / Face ID**.
- 🟣 Daftar perangkat yang sedang login (berkaitan dengan `AUTH-007`, Iterasi 2).

## B18. Anak Saya 🟢
*(Ref: `RIWAYAT-008`)*
Dibuka dari menu Akun Saya (B13).
**Konten:**
- Daftar semua anak yang terhubung: avatar, nama, usia, Kode ID, label status terakhir.
- Ketuk anak → **profil anak** (hanya-baca): nama, tanggal lahir, jenis kelamin, Posyandu terdaftar, tanggal didaftarkan. Data hanya bisa diubah kader. Ada tombol **Minta koreksi data** 🟣 yang membuka chat WhatsApp ke kader.
- Tombol **+ Hubungkan anak lain** → B3.
- Aksi **Lepas hubungan** dengan dialog konfirmasi, untuk anak yang salah terhubung.

---

# C. AREA KADER
*Enabler utama: seluruh data bersumber dari sini. Ref: Modul I-4 (KADER).*

## C1. Dashboard Kader 🟢
*(Ref: `KADER-005`, `KADER-016`, `GRAFIK-007`)*
**Konten:**
- Header: sapaan "Halo, Bu Sri", nama Posyandu, ikon 🔔.
- **Kartu kegiatan hari ini / terdekat:** tanggal + progres "32 dari 86 balita sudah ditimbang" dengan progress bar.
- **Kartu statistik** (geser horizontal): Total Peserta, Hadir Bulan Ini, Status Normal, Perlu Perhatian, Kritis.
- **Aksi cepat** (grid): Input Pengukuran, Tambah Peserta, Pindai QR 🟣, Kirim Pengumuman.
- **Perlu ditindaklanjuti:** daftar anak berstatus Kritis / Perlu Perhatian.
- **Aktivitas terbaru:** input terakhir, peserta baru, pengumuman terkirim.
- 🔵 Kartu peringatan peserta absen 2 bulan berturut-turut (`KADER-006`).

## C2. Daftar Peserta 🟢
*(Ref: `KADER-003`, `KADER-005`, `KADER-006`)*
**Konten:**
- **Kolom pencarian** di atas, dengan hasil real-time berdasarkan nama anak, nama orang tua, atau Kode ID.
- Filter chip: Semua, Normal, Perlu Perhatian, Kritis, Belum Ditimbang Bulan Ini.
- Setiap item: avatar, nama anak, usia, nama orang tua, label status, dan tanggal kunjungan terakhir.
- **Swipe** item untuk aksi cepat: Input Pengukuran / Edit 🟣.
- Tombol mengambang **+ Tambah Peserta**.

## C3. Detail Peserta 🟢
*(Ref: `KADER-004`, `RIWAYAT-001`, `GRAFIK-007`)*
**Konten:**
- Header profil anak: nama, usia, jenis kelamin, Kode ID (dengan tombol salin), label status.
- Info orang tua: nama, nomor WhatsApp, alamat, tombol 🟣 **Chat WhatsApp**.
- Tab: **Riwayat** | **Grafik** | **Imunisasi**.
- Tombol bawah: **Input Pengukuran** (utama), **Edit Data**, **Atur Imunisasi**.

## C4. Tambah / Edit Peserta 🟢
*(Ref: `KADER-001`, `KADER-004`)*
**Konten (form bertahap):**
- Langkah 1 — Data Anak: nama, tanggal lahir (date picker), jenis kelamin (pilihan tombol L/P).
- Langkah 2 — Data Orang Tua: nama orang tua/wali, nomor WhatsApp, alamat.
- Langkah 3 — Tinjau: ringkasan semua data sebelum disimpan.
- Validasi wajib isi + pesan error jelas. Loading state saat menyimpan.

## C5. Peserta Berhasil Didaftarkan 🟢
*(Ref: `KADER-002`)*
**Konten:**
- Ilustrasi sukses.
- **Kode ID unik** dalam ukuran besar + QR Code.
- Tombol **Kirim ke WhatsApp Orang Tua** 🟣 (berisi Kode ID + tautan unduh aplikasi).
- Tombol **Salin Kode**, **Input Pengukuran Sekarang**, dan **Selesai**.

## C6. Pindai QR Kartu Anak 🟣 *(Usulan Mobile)*
*(Terkait catatan SRS 5.2 tentang akses kamera)*
**Konten:**
- Tampilan kamera dengan bingkai pemindai.
- Tombol senter dan **Ketik Kode ID manual**.
- Setelah terpindai, langsung membuka C3 atau C7 untuk anak tersebut.

## C7. Input Pengukuran — Pilih Peserta 🟢
*(Ref: `KADER-007`)*
Dibuka dari tombol ➕ di tengah tab bar.
**Konten:**
- Pencarian peserta + daftar **Belum ditimbang bulan ini** di bagian atas.
- Tombol 🟣 **Pindai QR**.
- Ketuk peserta → C8.

## C8. Input Pengukuran — Form 🟢
*(Ref: `KADER-007` s/d `KADER-009`, `KADER-011`)*
**Konten:**
- Header: nama anak, usia, data terakhir sebagai pembanding.
- **Tanggal kunjungan** (default hari ini).
- **Berat badan (kg):** stepper / roda angka (wheel picker), bukan ketik bebas.
- **Tinggi/panjang badan (cm):** stepper / wheel picker.
- **Lingkar kepala (cm, opsional).**
- **Imunisasi hari ini:** chip pilihan ganda berisi daftar vaksin.
- **Catatan** (maks. 200 karakter, dengan penghitung).
- **Validasi real-time** (mis. berat > 50 kg atau tinggi < 30 cm langsung ditandai merah).
- Peringatan lunak jika berbeda jauh dari data sebelumnya, mis. "Turun 2 kg dari bulan lalu, sudah benar?" 🟣.
- Tombol **Simpan** (loading state, maks. 2 detik — `PERF-002`).

## C9. Hasil Pengukuran 🟢
*(Ref: `KADER-010`, `KADER-012`)*
**Konten:**
- Label status besar: **Normal / Perlu Perhatian / Kritis**, otomatis berdasarkan WHO.
- Ringkasan nilai + perubahan dari bulan lalu.
- Grafik mini posisi anak terhadap standar WHO.
- Saran tindak lanjut untuk status Perlu Perhatian / Kritis (mis. "Sarankan konsultasi ke Puskesmas").
- Info audit: "Dicatat oleh Sri Rahayu, 09.41".
- Tombol **Input Peserta Berikutnya** (alur cepat), **Lihat Detail**, dan **Selesai**.

## C10. Edit Pengukuran 🟢
*(Ref: `KADER-013`)*
**Konten:**
- Form sama seperti C8 dengan nilai terisi.
- Banner: "Data hanya bisa diubah hingga 24 jam setelah disimpan (sisa 18 jam)."
- Jika lewat 24 jam: tampilan hanya-baca + penjelasan.

## C11. Kelola Jadwal 🟢
*(Ref: `KADER-014`, `KADER-016`)*
**Konten:**
- Kalender gabungan: jadwal Posyandu + imunisasi peserta.
- Daftar jadwal mendatang & riwayat kegiatan.
- Tombol **+ Jadwal Kegiatan** → C12.

## C12. Tambah / Ubah Jadwal Kegiatan 🟢
*(Ref: `KADER-014`)*
**Konten:**
- Jenis kegiatan, tanggal (date picker), jam mulai–selesai (time picker), lokasi, dan layanan yang tersedia.
- Toggle **Beritahu semua orang tua** (memicu pengumuman perubahan jadwal).
- Tombol **Simpan**.

## C13. Atur Jadwal Imunisasi Peserta 🟢
*(Ref: `KADER-015`, `NOTIF-003`)*
**Konten:**
- Pilih peserta (atau dibuka dari C3).
- Rekomendasi otomatis sesuai usia anak berdasarkan program imunisasi nasional.
- Daftar vaksin: tanggal rencana dan status. Bisa diubah satu per satu.
- Tombol **Simpan Jadwal**, dengan info bahwa pengingat otomatis aktif.

## C14. Kirim Pengumuman 🟢
*(Ref: `NOTIF-005`, `NOTIF-007`)*
**Konten:**
- Penerima: **Semua orang tua** / **Pilih peserta** (daftar dengan checkbox) / 🟣 filter cepat (mis. "Anak usia 9 bulan").
- Template cepat 🟣: Perubahan Jadwal, Info Kesehatan, Pengingat Umum.
- Field judul + isi pesan.
- **Pratinjau** tampilan notifikasi di ponsel orang tua.
- Tombol **Kirim** dengan dialog konfirmasi jumlah penerima.

## C15. Riwayat Pengumuman 🟢 / 🔵
*(Ref: `NOTIF-005`, `NOTIF-006`)*
**Konten:**
- Daftar pengumuman terkirim: judul, tanggal, jumlah penerima.
- 🔵 Status pengiriman per penerima (berhasil / gagal / dibaca).

## C16. Pemantauan Pertumbuhan Kolektif 🟢
*(Ref: `GRAFIK-007`)*
**Konten:**
- Ringkasan status seluruh peserta (diagram batang / donat: Normal, Perlu Perhatian, Kritis).
- Tren rata-rata berat dan tinggi per bulan.
- Daftar peserta per kategori status, dan ketuk peserta → C3.

## C17. Kehadiran 🔵 *(Iterasi 2)*
*(Ref: `HADIR-001` s/d `HADIR-004`)*
**Konten:**
- Pilih sesi kegiatan.
- Daftar peserta dengan **centang hadir** (atau otomatis hadir saat pengukuran diinput 🟣).
- Tab **Absen ≥ 2 bulan** dengan tombol **Kirim pengingat WhatsApp**.
- Persentase kehadiran per peserta (rentang waktu bisa dipilih).
- Tombol **Ekspor**.

## C18. Laporan Bulanan 🔵 *(Iterasi 2)*
*(Ref: `LAPORAN-001` s/d `LAPORAN-004`)*
**Konten:**
- Pilih periode (bulan / kuartal).
- Kartu angka: jumlah hadir, rata-rata berat dan tinggi, status kolektif.
- Grafik batang statistik bulanan.
- Tombol **Unduh PDF** / **Unduh Excel** + **Bagikan** (share sheet ponsel).

## C19. Akun Kader 🟢
**Konten:**
- Profil kader: nama, nomor WhatsApp, Posyandu, peran.
- Menu: Edit Profil, Ubah Kata Sandi, Pengaturan Notifikasi, Bantuan & Panduan Kader, Tentang Aplikasi.
- Edit Profil dan Ubah Kata Sandi memakai layar yang sama dengan B14 dan B17.
- Tombol **Keluar**.

## C20. Notifikasi Kader 🟢
Dibuka dari ikon 🔔 di Dashboard Kader.
**Konten:**
- Pengingat kegiatan untuk kader: "Besok Posyandu, 08.00 · 86 peserta terdaftar".
- Info dari admin, mis. perubahan akun atau pemeliharaan sistem.
- Pemberitahuan data: "3 pengukuran masih bisa diedit (batas 24 jam)" (`KADER-013`).
- 🔵 Ringkasan peserta absen 2 bulan berturut-turut (`KADER-006`, `HADIR-002`).
- Penanda belum dibaca + **Tandai semua dibaca**.


---

# D. KOMPONEN & LAYAR SISTEM
*Berlaku lintas peran.*

## D1. Tidak Ada Koneksi Internet 🟢
*(Ref: batasan 2.4 — belum ada mode offline)*
- Ilustrasi sinyal terputus, pesan "Periksa koneksi internet Anda", dan tombol **Coba Lagi**.
- 🟣 Data terakhir yang sudah dimuat tetap bisa dilihat (hanya-baca).

## D2. Sesi Berakhir 🟢
*(Ref: `AUTH-005`)*
- Dialog "Sesi Anda berakhir karena tidak aktif 30 menit" + tombol **Masuk Kembali**.

## D3. Akses Ditolak 🟢
*(Ref: `SEC-004`)*
- Pesan saat membuka data di luar hak akses (mis. tautan notifikasi anak lain).

## D4. Pemeliharaan Sistem 🟢
*(Ref: `AVAIL-002`)*
- Ilustrasi + pesan jadwal pemeliharaan (22.00–05.00 WIB) dan perkiraan selesai.

## D5. Pembaruan Aplikasi Wajib 🟣
- Pesan "Versi baru tersedia" + tombol **Perbarui di App Store / Google Play**.

## D6. Dialog Konfirmasi (komponen) 🟢
- Dipakai untuk: Keluar, Kirim Pengumuman, Hapus jadwal, Batal isi form.
- Judul, penjelasan singkat, tombol utama dan sekunder.

## D7. Toast / Snackbar (komponen) 🟢
- Umpan balik singkat: "Data tersimpan", "Kode disalin", "Pengumuman terkirim ke 86 orang tua".

## D8. Bantuan, FAQ & Tentang Aplikasi 🟢
- FAQ yang bisa dibuka-tutup: Kode ID, notifikasi, keamanan data, status pertumbuhan.
- Kontak kader / Posyandu.
- Tentang: versi aplikasi, kebijakan privasi, syarat penggunaan.
- **Disclaimer:** informasi pertumbuhan bersifat indikatif dan tidak menggantikan pemeriksaan tenaga kesehatan.

## D9. Empty State & Skeleton Loading (komponen) 🟢
*(Ref: `USE-005`, `PERF-001`)*
- **Skeleton loading:** kerangka abu-abu berbentuk kartu/daftar saat data dimuat, agar layar tidak kosong.
- **Empty state** dengan ilustrasi + pesan + aksi untuk setiap daftar, misalnya:
  - Riwayat kosong: "Belum ada data kunjungan."
  - Notifikasi kosong: "Belum ada notifikasi."
  - Pencarian peserta tidak ditemukan: "Tidak ada hasil untuk 'Raka'" + tombol **Tambah Peserta**.
  - Jadwal kosong: "Belum ada jadwal bulan ini."

---

## Lampiran 1 — Matriks Layar × Modul SRS

| Layar | Modul SRS | Fase |
|---|---|---|
| A4–A9 Login, Registrasi, OTP, Lupa Sandi | AUTH | 🟢 |
| A10, B11, B12, B15 Izin & Notifikasi | Notifikasi I-2 | 🟢 |
| B1–B6 Beranda, Riwayat, Imunisasi | Riwayat I-1 | 🟢 |
| B7–B8 Grafik | Grafik I-3 | 🟢 |
| B9–B10 Jadwal | Dashboard Kader I-4 (tampilan peserta) | 🟢 |
| C1–C10 Dashboard, Peserta, Input Pengukuran | Dashboard Kader I-4 | 🟢 |
| C11–C13 Jadwal & Imunisasi | Dashboard Kader I-4 | 🟢 |
| C14–C15 Pengumuman | Notifikasi I-2 | 🟢 / 🔵 |
| C16 Pemantauan kolektif | Grafik I-3 | 🟢 |
| C17 Kehadiran | Pemantauan Kehadiran I-6 | 🔵 |
| C18 Laporan | Rekap & Laporan I-5 | 🔵 |
| A12 Syarat & Privasi | Keamanan (SEC-005) | 🟢 |
| B18 Anak Saya | Riwayat I-1 | 🟢 |
| C19–C20 Akun & Notifikasi Kader | AUTH / Notifikasi I-2 | 🟢 |
| D1–D9 Layar sistem & komponen | Non-fungsional (USE, AVAIL, SEC) | 🟢 |
| B16, C6, D5 Kartu Anak, QR, Update | — | 🟣 |

## Lampiran 2 — Perbedaan Utama Web vs Mobile

| Aspek | Web | Mobile |
|---|---|---|
| Navigasi | Sidebar (desktop) / hamburger | Bottom tab bar + tombol aksi tengah (kader) |
| Notifikasi | Web Push (Service Worker) | Push native FCM/APNs + WhatsApp cadangan |
| Input angka | Dropdown | Stepper / wheel picker, lebih cepat dengan satu tangan |
| Identifikasi anak | Ketik Kode ID | Ketik Kode ID **atau pindai QR** 🟣 |
| Pilihan & detail | Modal / dropdown | Bottom sheet |
| Grafik | Hover tooltip | Ketuk titik, pinch-to-zoom, mode landscape |
| Login ulang | Sandi | Sandi atau 🟣 biometrik |
| Admin | Tersedia | Tidak tersedia (tetap di web) |

## Lampiran 3 — Daftar Usulan Mobile (🟣) yang Perlu Disetujui Tim

1. Kartu Anak Digital dengan QR Code (B16).
2. Pindai QR di sisi kader (C6) dan saat registrasi orang tua (A6, B3).
3. Login biometrik (B17).
4. Tambah jadwal ke kalender ponsel & buka lokasi di peta (B10).
5. Kirim Kode ID + tautan unduh aplikasi via WhatsApp (C5).
6. Peringatan lunak saat nilai berbeda jauh dari bulan sebelumnya (C8).
7. Template & filter cepat pengumuman (C14).
8. Data terakhir tetap bisa dibaca saat offline (D1).
9. Layar wajib perbarui aplikasi (D5).

---

*Disusun berdasarkan SRS SiPosya v1.0 dan daftar halaman versi web.*