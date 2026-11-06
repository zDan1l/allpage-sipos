# Prototype Flow — PosCare Mobile

**Aplikasi Mobile Sistem Informasi Posyandu Digital — Android & iOS**

> Dokumen ini memetakan alur prototype aplikasi mobile berdasarkan **SRS SiPosya v1.0**, **mobile-page.md (59 layar)**, dan **PROTOTYPE-FLOW.md versi web**. Aplikasi melayani dua peran: **Orang Tua (Peserta)** dan **Kader**. Fungsi Administrator tetap di dashboard web.

---

## 1. Ringkasan Peran & Struktur Prototype

| Kelompok | Halaman Figma | Peran | Jumlah Layar | Fase |
|---|---|---|---:|---|
| Umum & Autentikasi | `01 · Umum` | Semua | 12 | 🟢 MVP |
| Area Orang Tua | `02 · Orang Tua` | Peserta (orang tua/wali) | 18 | 🟢 MVP + 🟣 Usulan |
| Area Kader | `03 · Kader` | Kader Posyandu | 20 | 🟢 MVP + 🔵 Iterasi 2 + 🟣 Usulan |
| Layar Sistem & Komponen | `04 · Sistem` | Semua | 9 | 🟢 MVP + 🟣 Usulan |
| **Total** | — | — | **59 layar** | — |

**Struktur file prototype (Figma), frame 390 × 844 pt:**

```text
PosCare Mobile (Figma)
├─ 00 · Cover & Flow Map               # Ringkasan alur (dokumen ini)
├─ 01 · Umum
│  ├─ A1  Splash
│  ├─ A2  Onboarding (3 slide)
│  ├─ A3  Selamat Datang
│  ├─ A4  Login
│  ├─ A5  Registrasi 1 · Data Diri
│  ├─ A6  Registrasi 2 · Hubungkan Anak
│  ├─ A7  Registrasi 3 · Kata Sandi
│  ├─ A8  Verifikasi OTP WhatsApp
│  ├─ A9  Lupa Kata Sandi
│  ├─ A10 Izin Notifikasi
│  ├─ A11 Registrasi Berhasil
│  └─ A12 Syarat & Kebijakan Privasi
├─ 02 · Orang Tua
│  ├─ B1  Beranda                      # Tab 🏠
│  ├─ B2  Pilih Anak                   # overlay bottom sheet
│  ├─ B3  Hubungkan Anak Baru
│  ├─ B4  Riwayat Kesehatan            # Tab 📋
│  ├─ B5  Detail Kunjungan
│  ├─ B6  Imunisasi
│  ├─ B7  Grafik Pertumbuhan           # Tab 📈
│  ├─ B8  Detail Titik Grafik          # overlay bottom sheet
│  ├─ B9  Jadwal & Kalender            # Tab 📅
│  ├─ B10 Detail Jadwal
│  ├─ B11 Notifikasi
│  ├─ B12 Detail Pengumuman
│  ├─ B13 Akun Saya                    # Tab 👤
│  ├─ B14 Edit Profil
│  ├─ B15 Pengaturan Notifikasi
│  ├─ B16 Kartu Anak Digital           # 🟣
│  ├─ B17 Ubah Sandi & Keamanan
│  └─ B18 Anak Saya
├─ 03 · Kader
│  ├─ C1  Dashboard Kader              # Tab 🏠
│  ├─ C2  Daftar Peserta               # Tab 👥
│  ├─ C3  Detail Peserta
│  ├─ C4  Tambah / Edit Peserta
│  ├─ C5  Peserta Berhasil Didaftarkan
│  ├─ C6  Pindai QR Kartu Anak         # 🟣
│  ├─ C7  Input Pengukuran · Pilih     # Tombol ➕
│  ├─ C8  Input Pengukuran · Form
│  ├─ C9  Hasil Pengukuran
│  ├─ C10 Edit Pengukuran
│  ├─ C11 Kelola Jadwal                # Tab 📅
│  ├─ C12 Tambah / Ubah Jadwal
│  ├─ C13 Atur Jadwal Imunisasi
│  ├─ C14 Kirim Pengumuman
│  ├─ C15 Riwayat Pengumuman
│  ├─ C16 Pemantauan Kolektif
│  ├─ C17 Kehadiran                    # 🔵
│  ├─ C18 Laporan Bulanan              # 🔵
│  ├─ C19 Akun Kader                   # Tab 👤
│  └─ C20 Notifikasi Kader
├─ 04 · Sistem
│  ├─ D1  Tidak Ada Koneksi
│  ├─ D2  Sesi Berakhir
│  ├─ D3  Akses Ditolak
│  ├─ D4  Pemeliharaan
│  ├─ D5  Pembaruan Wajib              # 🟣
│  ├─ D6  Dialog Konfirmasi            # komponen / overlay
│  ├─ D7  Toast / Snackbar             # komponen / overlay
│  ├─ D8  Bantuan, FAQ & Tentang
│  └─ D9  Empty State & Skeleton       # komponen
└─ 05 · Komponen
   ├─ Tab Bar Orang Tua / Tab Bar Kader (variant aktif per tab)
   ├─ Header + Lonceng Notifikasi
   ├─ Bottom Sheet, Dialog, Toast
   └─ Status Pill, Kartu, Input, Stepper, Tombol
```

**Titik mulai prototype (Flow starting points di Figma):**

| Flow | Mulai dari | Alur yang bisa dicoba |
|---|---|---|
| 1. Pengguna Baru | A1 Splash | Onboarding → Registrasi 3 langkah → OTP → Izin Notifikasi → B1 |
| 2. Orang Tua | B1 Beranda | Riwayat, Grafik, Imunisasi, Jadwal, Notifikasi, Akun |
| 3. Kader — Input Pengukuran | C1 Dashboard | ➕ → C7 → C8 → C9 → peserta berikutnya |
| 4. Kader — Peserta Baru | C2 Daftar Peserta | C4 → C5 (Kode ID + QR) |
| 5. Kader — Jadwal & Pengumuman | C11 Kelola Jadwal | C12, C13, C14 → C15 |
| 6. Kondisi Sistem | D1 Tidak Ada Koneksi | D1–D9 |

> **Catatan:** frame berlabel overlay (B2, B8, D6, D7) tidak berdiri sendiri. Di prototype, frame ini dibuka dengan aksi *Open overlay* dari layar induknya.

---

## 2. Peta Layar & Traceability SRS

| Kode | Layar | Frame | Peran | Fase | Referensi SRS |
|---|---|---|---|---|---|
| A1 | Splash Screen | `01 · Umum / A1` | Semua | 🟢 | AUTH-005 |
| A2 | Onboarding | `01 · Umum / A2` | Semua | 🟢 | SRS 5.1 |
| A3 | Selamat Datang | `01 · Umum / A3` | Semua | 🟢 | AUTH-006 |
| A4 | Login | `01 · Umum / A4` | Semua | 🟢 | AUTH-002, AUTH-003, SEC-007 |
| A5 | Registrasi 1 · Data Diri | `01 · Umum / A5` | Orang Tua | 🟢 | AUTH-001 |
| A6 | Registrasi 2 · Hubungkan Anak | `01 · Umum / A6` | Orang Tua | 🟢 | AUTH-001, KADER-002 |
| A7 | Registrasi 3 · Kata Sandi | `01 · Umum / A7` | Orang Tua | 🟢 | AUTH-001, SEC-002 |
| A8 | Verifikasi OTP WhatsApp | `01 · Umum / A8` | Semua | 🟢 | AUTH-004 |
| A9 | Lupa Kata Sandi | `01 · Umum / A9` | Semua | 🟢 | AUTH-004 |
| A10 | Izin Notifikasi | `01 · Umum / A10` | Semua | 🟢 | NOTIF-001, NOTIF-004 |
| A11 | Registrasi Berhasil | `01 · Umum / A11` | Orang Tua | 🟢 | AUTH-001 |
| A12 | Syarat & Kebijakan Privasi | `01 · Umum / A12` | Semua | 🟢 | SEC-005 |
| B1 | Beranda | `02 · Orang Tua / B1` | Orang Tua | 🟢 | RIWAYAT-005, RIWAYAT-007, GRAFIK-005 |
| B2 | Pilih Anak (bottom sheet) | `02 · Orang Tua / B2` | Orang Tua | 🟢 | RIWAYAT-008 |
| B3 | Hubungkan Anak Baru | `02 · Orang Tua / B3` | Orang Tua | 🟢 | RIWAYAT-008, KADER-002 |
| B4 | Riwayat Kesehatan | `02 · Orang Tua / B4` | Orang Tua | 🟢 | RIWAYAT-001, RIWAYAT-003, RIWAYAT-006, RIWAYAT-007 |
| B5 | Detail Kunjungan | `02 · Orang Tua / B5` | Orang Tua | 🟢 | RIWAYAT-001, RIWAYAT-002, RIWAYAT-004, RIWAYAT-007 |
| B6 | Imunisasi | `02 · Orang Tua / B6` | Orang Tua | 🟢 | RIWAYAT-002, NOTIF-003 |
| B7 | Grafik Pertumbuhan | `02 · Orang Tua / B7` | Orang Tua | 🟢 | GRAFIK-001 s.d. GRAFIK-006 |
| B8 | Detail Titik Grafik (bottom sheet) | `02 · Orang Tua / B8` | Orang Tua | 🟢 | GRAFIK-003 |
| B9 | Jadwal & Kalender | `02 · Orang Tua / B9` | Orang Tua | 🟢 | KADER-016, NOTIF-001, NOTIF-003 |
| B10 | Detail Jadwal | `02 · Orang Tua / B10` | Orang Tua | 🟢 | KADER-016, NOTIF-003 |
| B11 | Notifikasi | `02 · Orang Tua / B11` | Orang Tua | 🟢 | NOTIF-001 s.d. NOTIF-005, NOTIF-007 |
| B12 | Detail Pengumuman | `02 · Orang Tua / B12` | Orang Tua | 🟢 | NOTIF-005 |
| B13 | Akun Saya | `02 · Orang Tua / B13` | Orang Tua | 🟢 | RIWAYAT-008, NOTIF-004 |
| B14 | Edit Profil | `02 · Orang Tua / B14` | Semua | 🟢 | AUTH-004 |
| B15 | Pengaturan Notifikasi | `02 · Orang Tua / B15` | Semua | 🟢 | NOTIF-004 |
| B16 | Kartu Anak Digital | `02 · Orang Tua / B16` | Orang Tua | 🟣 | — (usulan mobile) |
| B17 | Ubah Sandi & Keamanan | `02 · Orang Tua / B17` | Semua | 🟢 / 🟣 | SEC-002, AUTH-005, AUTH-007 |
| B18 | Anak Saya | `02 · Orang Tua / B18` | Orang Tua | 🟢 | RIWAYAT-008 |
| C1 | Dashboard Kader | `03 · Kader / C1` | Kader | 🟢 | KADER-005, KADER-016, GRAFIK-007 |
| C2 | Daftar Peserta | `03 · Kader / C2` | Kader | 🟢 | KADER-003, KADER-005, KADER-006 |
| C3 | Detail Peserta | `03 · Kader / C3` | Kader | 🟢 | KADER-004, RIWAYAT-001, GRAFIK-007 |
| C4 | Tambah / Edit Peserta | `03 · Kader / C4` | Kader | 🟢 | KADER-001, KADER-004 |
| C5 | Peserta Berhasil Didaftarkan | `03 · Kader / C5` | Kader | 🟢 | KADER-002 |
| C6 | Pindai QR Kartu Anak | `03 · Kader / C6` | Kader | 🟣 | Perluasan SRS 5.2 (akses kamera) |
| C7 | Input Pengukuran · Pilih Peserta | `03 · Kader / C7` | Kader | 🟢 | KADER-007 |
| C8 | Input Pengukuran · Form | `03 · Kader / C8` | Kader | 🟢 | KADER-007 s.d. KADER-009, KADER-011, PERF-002 |
| C9 | Hasil Pengukuran | `03 · Kader / C9` | Kader | 🟢 | KADER-010, KADER-012 |
| C10 | Edit Pengukuran | `03 · Kader / C10` | Kader | 🟢 | KADER-013 |
| C11 | Kelola Jadwal | `03 · Kader / C11` | Kader | 🟢 | KADER-014, KADER-016 |
| C12 | Tambah / Ubah Jadwal | `03 · Kader / C12` | Kader | 🟢 | KADER-014 |
| C13 | Atur Jadwal Imunisasi | `03 · Kader / C13` | Kader | 🟢 | KADER-015, NOTIF-003 |
| C14 | Kirim Pengumuman | `03 · Kader / C14` | Kader | 🟢 | NOTIF-005, NOTIF-007 |
| C15 | Riwayat Pengumuman | `03 · Kader / C15` | Kader | 🟢 / 🔵 | NOTIF-005, NOTIF-006 |
| C16 | Pemantauan Kolektif | `03 · Kader / C16` | Kader | 🟢 | GRAFIK-007 |
| C17 | Kehadiran | `03 · Kader / C17` | Kader | 🔵 | HADIR-001 s.d. HADIR-004 |
| C18 | Laporan Bulanan | `03 · Kader / C18` | Kader | 🔵 | LAPORAN-001 s.d. LAPORAN-004 |
| C19 | Akun Kader | `03 · Kader / C19` | Kader | 🟢 | AUTH-005 |
| C20 | Notifikasi Kader | `03 · Kader / C20` | Kader | 🟢 | KADER-006, KADER-013 |
| D1 | Tidak Ada Koneksi | `04 · Sistem / D1` | Semua | 🟢 | Batasan 2.4 |
| D2 | Sesi Berakhir | `04 · Sistem / D2` | Semua | 🟢 | AUTH-005 |
| D3 | Akses Ditolak | `04 · Sistem / D3` | Semua | 🟢 | SEC-004, SEC-005 |
| D4 | Pemeliharaan Sistem | `04 · Sistem / D4` | Semua | 🟢 | AVAIL-002 |
| D5 | Pembaruan Aplikasi Wajib | `04 · Sistem / D5` | Semua | 🟣 | — (usulan mobile) |
| D6 | Dialog Konfirmasi | `04 · Sistem / D6` | Semua | 🟢 | USE-004 |
| D7 | Toast / Snackbar | `04 · Sistem / D7` | Semua | 🟢 | USE-005 |
| D8 | Bantuan, FAQ & Tentang | `04 · Sistem / D8` | Semua | 🟢 | Batasan 2.4 |
| D9 | Empty State & Skeleton | `04 · Sistem / D9` | Semua | 🟢 | USE-005, PERF-001 |

**Legenda fase:** 🟢 MVP · 🔵 Iterasi 2 · 🟣 Usulan Mobile (tidak tertulis di SRS, perlu persetujuan tim)
**Legenda diagram:** garis **solid** = alur yang dapat ditelusuri di prototype (tap, swipe, atau tombol); garis **putus-putus** = alur otomatis/backend, aksi ke aplikasi lain di ponsel, atau alur usulan.

---

## 3. Alur Utama Berdasarkan Peran

### 3.1 Routing Awal & Pemilihan Peran

```mermaid
flowchart TD
    OPEN(["Buka aplikasi"]) --> SP["A1 Splash"]
    PUSH(["Ketuk push notification"]) -.->|"deep link"| SP
    SP --> SES{"Sesi tersimpan<br/>masih valid?"}
    SES -->|"Ya, Orang Tua"| B1["B1 Beranda"]
    SES -->|"Ya, Kader"| C1["C1 Dashboard Kader"]
    SES -->|"Tidak"| FIRST{"Pertama kali<br/>membuka aplikasi?"}
    FIRST -->|"Ya"| OB["A2 Onboarding"]
    FIRST -->|"Tidak"| WEL["A3 Selamat Datang"]
    OB -->|"Mulai / Lewati"| WEL

    WEL -->|"Masuk"| LG["A4 Login"]
    WEL -->|"Daftar sebagai Orang Tua"| RG["A5 Registrasi Orang Tua"]
    WEL -->|"Bantuan"| FAQ["D8 Bantuan & FAQ"]

    LG --> ROLE{"Peran pengguna"}
    ROLE -->|"Orang Tua"| B1
    ROLE -->|"Kader"| C1
    ROLE -->|"Admin"| D3["D3 Akses Ditolak<br/>Gunakan dashboard web"]

    SP -.->|"versi usang"| D5["D5 Pembaruan Wajib"]
    SP -.->|"tanpa internet"| D1["D1 Tidak Ada Koneksi"]

    B1 -.->|"idle 30 menit"| D2["D2 Sesi Berakhir"]
    C1 -.-> D2
    D2 -->|"Masuk kembali"| LG

    classDef public fill:#eaf0fe,stroke:#3a6ff0,color:#1e3a8a;
    classDef peserta fill:#e8f6ed,stroke:#15a05a,color:#14532d;
    classDef kader fill:#e7f6f1,stroke:#0f9d7a,color:#0b5f4a;
    classDef sistem fill:#fbf1e1,stroke:#c77a16,color:#7c4a0a;
    classDef usulan fill:#f4effd,stroke:#7c5ce7,color:#3b2f9e,stroke-dasharray:4 3;
    class OPEN,PUSH,SP,SES,FIRST,OB,WEL,LG,RG,FAQ,ROLE public;
    class B1 peserta;
    class C1 kader;
    class D1,D2,D3 sistem;
    class D5 usulan;
```

### 3.2 Autentikasi, Registrasi & Pemulihan Akun

```mermaid
flowchart TD
    WEL["A3 Selamat Datang"] -->|"Daftar"| R1["A5 Registrasi 1<br/>Nama + No. WhatsApp"]
    R1 --> R2["A6 Registrasi 2<br/>Kode ID Anak"]
    R2 -.->|"Pindai QR Kartu Anak"| QR["Kamera pemindai"]
    QR -.-> IDOK
    R2 --> IDOK{"Kode ID valid?"}
    IDOK -->|"Tidak"| R2ERR["Pesan error di field"]
    R2ERR --> R2
    IDOK -->|"Ya"| CONF{"Apakah ini<br/>anak Anda?"}
    CONF -->|"Bukan"| R2
    CONF -->|"Ya, benar"| R3["A7 Registrasi 3<br/>Kata sandi + setuju syarat"]
    R3 -->|"baca syarat"| TOS["A12 Syarat & Privasi"]
    TOS -->|"Saya Mengerti"| R3
    R3 --> OTP["A8 Verifikasi OTP WhatsApp"]
    OTP --> OTPOK{"OTP valid?"}
    OTPOK -->|"Salah / kedaluwarsa<br/>Kirim ulang"| OTP
    OTPOK -->|"Ya"| DONE["A11 Registrasi Berhasil"]
    DONE --> PERM["A10 Izin Notifikasi"]

    WEL -->|"Masuk"| LOGIN["A4 Login"]
    LOGIN --> CRED{"Kredensial valid?"}
    CRED -->|"Tidak, percobaan < 5"| ERR["Pesan error Bahasa Indonesia"]
    ERR --> LOGIN
    CRED -->|"Gagal 5 kali"| LOCK["Terkunci 15 menit<br/>hitung mundur · SEC-007"]
    LOCK --> LOGIN
    CRED -->|"Ya"| JWT["Sesi JWT + peran<br/>AUTH-003"]
    JWT --> FIRSTDEV{"Login pertama<br/>di perangkat ini?"}
    FIRSTDEV -->|"Ya"| PERM
    FIRSTDEV -->|"Tidak"| ROLE{"Redirect sesuai peran"}
    PERM -->|"Izinkan / Nanti saja"| ROLE
    PERM -.->|"Izinkan"| OSD["Dialog izin Android / iOS"]
    ROLE -->|"Orang Tua"| B1["B1 Beranda"]
    ROLE -->|"Kader"| C1["C1 Dashboard Kader"]

    LOGIN -->|"Lupa kata sandi"| FP["A9 Lupa Kata Sandi<br/>No. WhatsApp terdaftar"]
    FP --> OTP2["A8 Verifikasi OTP<br/>komponen yang sama"]
    OTP2 --> NEWPW["Kata sandi baru + konfirmasi"]
    NEWPW -->|"Kembali ke Login"| LOGIN

    classDef auth fill:#eaf0fe,stroke:#3a6ff0,color:#1e3a8a;
    classDef peserta fill:#e8f6ed,stroke:#15a05a,color:#14532d;
    classDef kader fill:#e7f6f1,stroke:#0f9d7a,color:#0b5f4a;
    classDef usulan fill:#f4effd,stroke:#7c5ce7,color:#3b2f9e,stroke-dasharray:4 3;
    class WEL,R1,R2,IDOK,R2ERR,CONF,R3,TOS,OTP,OTPOK,DONE,PERM,LOGIN,CRED,ERR,LOCK,JWT,FIRSTDEV,ROLE,FP,OTP2,NEWPW,OSD auth;
    class B1 peserta;
    class C1 kader;
    class QR usulan;
```

> **Catatan prototype:** login dibuat dengan dua tombol demo, **Masuk sebagai Orang Tua** dan **Masuk sebagai Kader**, agar setiap peran bisa dicoba tanpa backend. OTP, dialog izin sistem, dan kamera hanya berupa tampilan.

---

### 3.3 Struktur Navigasi Tab Bar

```mermaid
flowchart TB
    subgraph OT["Orang Tua — Tab Bar"]
        direction LR
        T1["🏠 Beranda<br/>B1"] ~~~ T2["📋 Riwayat<br/>B4"] ~~~ T3["📈 Grafik<br/>B7"] ~~~ T4["📅 Jadwal<br/>B9"] ~~~ T5["👤 Akun<br/>B13"]
    end
    subgraph KD["Kader — Tab Bar"]
        direction LR
        K1["🏠 Beranda<br/>C1"] ~~~ K2["👥 Peserta<br/>C2"] ~~~ K3["➕ Input<br/>C7"] ~~~ K4["📅 Jadwal<br/>C11"] ~~~ K5["👤 Akun<br/>C19"]
    end
    T1 -.->|"🔔 header"| N1["B11 Notifikasi"]
    K1 -.->|"🔔 header"| N2["C20 Notifikasi Kader"]

    classDef peserta fill:#e8f6ed,stroke:#15a05a,color:#14532d;
    classDef kader fill:#e7f6f1,stroke:#0f9d7a,color:#0b5f4a;
    classDef fab fill:#0f9d7a,stroke:#0b7a5f,color:#ffffff;
    class T1,T2,T3,T4,T5,N1 peserta;
    class K1,K2,K4,K5,N2 kader;
    class K3 fab;
```

**Aturan navigasi:**
- Tab bar tampil di layar utama setiap tab. Layar turunan (detail, form) menyembunyikan tab bar dan memakai tombol **Kembali** di header.
- Mengetuk tab yang sedang aktif mengembalikan pengguna ke layar paling atas tab tersebut.
- Tombol ➕ kader selalu membuka **C7 Pilih Peserta**, dari tab mana pun.

---

### 3.4 Alur Orang Tua (Peserta)

```mermaid
flowchart LR
    B1["B1 Beranda<br/>Ringkasan kondisi terkini"]

    B1 -->|"tap pemilih anak"| B2["B2 Pilih Anak<br/>bottom sheet"]
    B2 -->|"pilih anak"| B1
    B2 -->|"+ Hubungkan anak lain"| B3["B3 Hubungkan Anak Baru"]
    B3 -->|"berhasil"| B1

    B1 -->|"tab Riwayat"| B4["B4 Riwayat Kesehatan<br/>Pengukuran | Imunisasi"]
    B4 -->|"tap entri"| B5["B5 Detail Kunjungan<br/>Ukur + catatan kader"]
    B4 -->|"segmen Imunisasi"| B6["B6 Imunisasi<br/>Timeline per usia"]
    B5 -->|"Lihat di grafik"| B7

    B1 -->|"tab Grafik"| B7["B7 Grafik Pertumbuhan<br/>BB | TB, zona WHO"]
    B7 -->|"tap titik"| B8["B8 Detail Titik<br/>bottom sheet"]
    B8 -->|"Lihat detail kunjungan"| B5

    B1 -->|"tab Jadwal"| B9["B9 Jadwal & Kalender"]
    B1 -->|"kartu jadwal terdekat"| B10
    B9 -->|"tap jadwal"| B10["B10 Detail Jadwal"]
    B10 -.->|"Tambah ke kalender / Buka peta"| EXT["Aplikasi Kalender / Maps"]
    B6 -->|"vaksin terjadwal"| B10

    B1 -->|"🔔"| B11["B11 Notifikasi"]
    B11 -->|"pengingat"| B10
    B11 -->|"pengumuman"| B12["B12 Detail Pengumuman"]
    B12 -.->|"jadwal terkait"| B10

    B1 -->|"tab Akun"| B13["B13 Akun Saya"]

    classDef peserta fill:#e8f6ed,stroke:#15a05a,color:#14532d;
    classDef usulan fill:#f4effd,stroke:#7c5ce7,color:#3b2f9e,stroke-dasharray:4 3;
    class B1,B2,B3,B4,B5,B6,B7,B8,B9,B10,B11,B12,B13 peserta;
    class EXT usulan;
```

**Poin penting:**
- Semua layar orang tua hanya menampilkan data anak milik akun yang login (`SEC-004`, `SEC-005`).
- Anak aktif dipilih lewat **B2 bottom sheet** dari header Beranda. Pilihan ini berlaku di semua tab.
- Grafik B7 mendukung geser horizontal dan *pinch-to-zoom* (`GRAFIK-006`), serta mode layar penuh *landscape* 🟣.
- Daftar B4 dan B11 mendukung *pull-to-refresh*. Saat kosong, ditampilkan **D9 Empty State**.

---

### 3.5 Alur Kader (Input Data & Operasional)

```mermaid
flowchart TD
    H["C1 Dashboard Kader"]

    subgraph MP["Manajemen Peserta"]
        direction LR
        P["C2 Daftar Peserta"]
        DP["C3 Detail Peserta"]
        F["C4 Tambah / Edit Peserta<br/>3 langkah"]
        OK["C5 Berhasil Didaftarkan<br/>Kode ID + QR"]
        P -->|"tap peserta"| DP
        P -->|"+ Tambah Peserta"| F
        F -->|"Simpan"| OK
        OK -->|"Selesai"| P
    end

    subgraph MG["Input Pengukuran (tombol ➕)"]
        direction TB
        SEL["C7 Pilih Peserta"]
        QR["C6 Pindai QR"]
        FORM["C8 Form Pengukuran"]
        RES["C9 Hasil Pengukuran<br/>Status WHO"]
        EDIT["C10 Edit Pengukuran<br/>maks. 24 jam"]
        SEL -->|"tap peserta"| FORM
        SEL -.->|"Pindai QR"| QR
        QR -.->|"terpindai"| FORM
        FORM -->|"Simpan (valid)"| RES
        RES -->|"Input peserta berikutnya"| SEL
        EDIT -->|"Simpan"| RES
    end

    subgraph MJ["Jadwal & Komunikasi"]
        direction LR
        JD["C11 Kelola Jadwal"]
        JF["C12 Tambah / Ubah Jadwal"]
        IM["C13 Atur Imunisasi Peserta"]
        PG["C14 Kirim Pengumuman"]
        RP["C15 Riwayat Pengumuman"]
        JD -->|"+ Jadwal"| JF
        JF -->|"Simpan"| JD
        PG -->|"Kirim + konfirmasi D6"| RP
    end

    subgraph ML["Pemantauan & Laporan"]
        direction LR
        KOL["C16 Pemantauan Kolektif"]
        KH["C17 Kehadiran<br/>Iterasi 2"]
        LP["C18 Laporan Bulanan<br/>Iterasi 2"]
        REPORT["PDF / XLSX<br/>share sheet ponsel"]
        LP -.-> REPORT
    end

    NOTIF["Push ke orang tua<br/>B11 Notifikasi"]
    WA["WhatsApp orang tua"]

    H -->|"tab Peserta"| P
    H -->|"tombol ➕"| SEL
    H -->|"tab Jadwal"| JD
    H -->|"aksi cepat"| PG
    H -->|"kartu statistik"| KOL
    H -.->|"aksi cepat Pindai QR"| QR
    H -.-> KH
    H -.-> LP
    H -->|"🔔"| NK["C20 Notifikasi Kader"]

    DP -->|"Input pengukuran"| FORM
    DP -->|"Edit data"| F
    DP -->|"Atur imunisasi"| IM
    DP -->|"edit entri ≤ 24 jam"| EDIT
    RES -->|"Lihat detail"| DP
    OK -->|"Input pengukuran sekarang"| FORM
    OK -.->|"Kirim ke WhatsApp"| WA
    P -.->|"swipe: Input"| FORM
    KOL -->|"tap peserta"| DP
    KH -.->|"absen ≥ 2 bulan"| P
    NK -.->|"pengukuran bisa diedit"| EDIT

    JF -.->|"Beritahu orang tua"| NOTIF
    IM -.-> NOTIF
    PG -.-> NOTIF

    classDef kader fill:#e7f6f1,stroke:#0f9d7a,color:#0b5f4a;
    classDef iter fill:#eaf0fe,stroke:#3a6ff0,color:#1e3a8a,stroke-dasharray:4 3;
    classDef usulan fill:#f4effd,stroke:#7c5ce7,color:#3b2f9e,stroke-dasharray:4 3;
    class H,P,DP,F,OK,SEL,FORM,RES,EDIT,JD,JF,IM,PG,RP,KOL,NK,NOTIF kader;
    class KH,LP,REPORT iter;
    class QR,WA usulan;
```

**Alur input pengukuran (C7 → C8 → C9) secara rinci:**

1. Kader mengetuk tombol **➕** dari tab mana pun, atau **Input pengukuran** dari Detail Peserta (C3).
2. Di **C7**, kader memilih peserta dari daftar **Belum ditimbang bulan ini**, mencari nama/Kode ID, atau 🟣 memindai QR Kartu Anak.
3. Di **C8**, kader mengisi BB dan TB dengan stepper/wheel picker, lingkar kepala (opsional), imunisasi hari ini (chip), dan catatan (maks. 200 karakter).
4. Validasi berjalan real-time. Nilai di luar rentang langsung ditandai merah di field terkait.
5. 🟣 Jika nilai berbeda jauh dari bulan lalu, muncul peringatan lunak "Sudah benar?".
6. **Simpan** menampilkan loading state (maks. 2 detik, `PERF-002`), lalu sistem menghitung status WHO dan menyimpan audit trail (nama kader + waktu).
7. **C9** menampilkan status, perubahan dari bulan lalu, dan saran tindak lanjut. Kader bisa langsung **Input peserta berikutnya** (kembali ke C7).
8. Data bisa diedit di **C10** selama 24 jam (`KADER-013`), dan langsung muncul di B1, B4, dan B7 milik orang tua.

---

### 3.6 Alur Akun & Pengaturan (Kedua Peran)

```mermaid
flowchart LR
    B13["B13 Akun Saya<br/>Orang Tua"]
    C19["C19 Akun Kader"]

    B13 --> B14["B14 Edit Profil"]
    B13 --> B18["B18 Anak Saya"]
    B13 --> B16["B16 Kartu Anak Digital"]
    B13 --> B15["B15 Pengaturan Notifikasi"]
    B13 --> B17["B17 Ubah Sandi & Keamanan"]
    B13 --> D8["D8 Bantuan, FAQ & Tentang"]
    B13 -->|"Keluar + dialog D6"| LG["A4 Login"]

    C19 -->|"Edit Profil"| B14
    C19 -->|"Ubah Kata Sandi"| B17
    C19 --> B15
    C19 -->|"Panduan Kader"| D8
    C19 -->|"Keluar + dialog D6"| LG

    B14 -.->|"ganti nomor WhatsApp"| OTP["A8 Verifikasi OTP"]
    B18 -->|"+ Hubungkan anak"| B3["B3 Hubungkan Anak Baru"]
    B18 -.->|"Minta koreksi data"| WA["WhatsApp kader"]
    B16 -.->|"dipindai di meja pendaftaran"| C6["C6 Pindai QR"]
    B15 -.->|"izin sistem mati"| OS["Pengaturan ponsel"]
    D8 --> A12["A12 Syarat & Privasi"]
    D8 -->|"buka ulang tutorial"| A2["A2 Onboarding"]

    classDef peserta fill:#e8f6ed,stroke:#15a05a,color:#14532d;
    classDef kader fill:#e7f6f1,stroke:#0f9d7a,color:#0b5f4a;
    classDef public fill:#eaf0fe,stroke:#3a6ff0,color:#1e3a8a;
    classDef sistem fill:#fbf1e1,stroke:#c77a16,color:#7c4a0a;
    classDef usulan fill:#f4effd,stroke:#7c5ce7,color:#3b2f9e,stroke-dasharray:4 3;
    class B13,B14,B18,B15,B17,B3 peserta;
    class C19 kader;
    class LG,OTP,A12,A2 public;
    class D8 sistem;
    class B16,C6,WA,OS usulan;
```

> B14, B15, B17, dan D8 dipakai bersama oleh kedua peran. Isinya menyesuaikan peran yang login.

---

### 3.7 Alur Layar Sistem & Komponen

```mermaid
flowchart TD
    ANY["Layar mana pun"] --> STATE{"Kondisi"}

    STATE -->|"Tidak ada internet"| D1["D1 Tidak Ada Koneksi"]
    STATE -->|"Idle 30 menit"| D2["D2 Sesi Berakhir"]
    STATE -->|"Data di luar hak akses"| D3["D3 Akses Ditolak"]
    STATE -->|"Pemeliharaan 22.00–05.00 WIB"| D4["D4 Pemeliharaan"]
    STATE -->|"Versi aplikasi usang"| D5["D5 Pembaruan Wajib"]
    STATE -->|"Memuat / daftar kosong"| D9["D9 Skeleton / Empty State"]

    D1 -->|"Coba Lagi"| ANY
    D1 -.->|"lihat data terakhir"| CACHE["Mode baca saja"]
    D2 -->|"Masuk Kembali"| LOGIN["A4 Login"]
    D3 -->|"Kembali"| HOME["Beranda sesuai peran<br/>B1 / C1"]
    D4 -->|"Coba Lagi"| SPLASH["A1 Splash"]
    D5 -.->|"Perbarui"| STORE["App Store / Google Play"]
    D9 -->|"aksi empty state"| HOME

    ANY -.->|"aksi berisiko<br/>Keluar, Kirim, Hapus"| D6["D6 Dialog Konfirmasi"]
    ANY -.->|"setelah aksi berhasil"| D7["D7 Toast"]
    D6 -->|"Batal"| ANY

    classDef sistem fill:#fbf1e1,stroke:#c77a16,color:#7c4a0a;
    classDef public fill:#eaf0fe,stroke:#3a6ff0,color:#1e3a8a;
    classDef usulan fill:#f4effd,stroke:#7c5ce7,color:#3b2f9e,stroke-dasharray:4 3;
    class D1,D2,D3,D4,D6,D7,D9 sistem;
    class ANY,STATE,LOGIN,HOME,SPLASH public;
    class D5,CACHE,STORE usulan;
```

---

## 4. Sub-Alur Status Pertumbuhan (WHO)

```mermaid
flowchart LR
    IN["C8 Input BB / TB / LK<br/>stepper / wheel picker"] --> VAL{"Validasi rentang"}
    VAL -->|"Tidak valid"| ERR["Field merah:<br/>BB ≤ 50 kg, TB ≥ 30 cm"]
    ERR --> IN
    VAL -->|"Valid"| DIFF{"Selisih jauh dari<br/>bulan lalu?"}
    DIFF -->|"Ya"| SOFT["Peringatan lunak:<br/>Sudah benar?"]
    SOFT -->|"Periksa lagi"| IN
    SOFT -->|"Ya, simpan"| WHO
    DIFF -->|"Tidak"| WHO["Hitung Z-score<br/>standar WHO"]
    WHO --> N1["Normal"]
    WHO --> N2["Perlu Perhatian"]
    WHO --> N3["Kritis"]
    N1 --> ACT1["Edukasi gizi &<br/>jadwal rutin"]
    N2 --> ACT2["Konsultasi kader /<br/>pemantauan intensif"]
    N3 --> ACT3["Sarankan rujukan<br/>ke Puskesmas"]
    ACT1 --> SHOW["C9 Hasil Pengukuran<br/>+ tampil di B1, B4, B7"]
    ACT2 --> SHOW
    ACT3 --> SHOW

    classDef ok fill:#e8f6ed,stroke:#15a05a,color:#14532d;
    classDef warn fill:#fbf1e1,stroke:#c77a16,color:#7c4a0a;
    classDef crit fill:#fbeaea,stroke:#d64545,color:#7f1d1d;
    classDef usulan fill:#f4effd,stroke:#7c5ce7,color:#3b2f9e,stroke-dasharray:4 3;
    class N1,ACT1 ok;
    class N2,ACT2 warn;
    class N3,ACT3 crit;
    class DIFF,SOFT usulan;
```

Status ini bersifat **indikatif** dan bukan pengganti konsultasi medis (SRS 2.4). Acuan: WHO Child Growth Standards dan Permenkes No. 2 Tahun 2020. Pengecekan selisih dari bulan lalu (ungu) adalah usulan mobile 🟣.

---

## 5. Sequence Diagram Alur Kritis

### 5.1 Membuka Aplikasi, Login & Redirect Peran

```mermaid
sequenceDiagram
    autonumber
    actor U as Pengguna
    participant App as Aplikasi PosCare
    participant SS as Secure Storage
    participant A as Auth Service
    participant DB as Database

    U->>App: Buka aplikasi (A1 Splash)
    App->>SS: Ambil token tersimpan
    alt Token masih valid
        SS-->>App: JWT + peran
        App-->>U: B1 Beranda / C1 Dashboard Kader
    else Tidak ada / kedaluwarsa
        App-->>U: A3 Selamat Datang lalu A4 Login
        U->>App: Isi nomor WhatsApp + kata sandi
        App->>A: POST /auth/login
        A->>DB: Verifikasi kredensial & peran
        alt Kredensial valid
            DB-->>A: Data pengguna + role
            A-->>App: JWT + role
            App->>SS: Simpan token (Ingat saya)
            alt Orang Tua
                App-->>U: B1 Beranda
            else Kader
                App-->>U: C1 Dashboard Kader
            else Admin
                App-->>U: D3 Akses Ditolak (gunakan web)
            end
        else Gagal 5 kali
            A-->>App: Akun dikunci 15 menit
            App-->>U: Pesan + hitung mundur (SEC-007)
        end
    end

    Note over App,U: Prototype memakai tombol demo<br/>Masuk sebagai Orang Tua / Kader.
```

### 5.2 Input Pengukuran hingga Tampil ke Orang Tua

```mermaid
sequenceDiagram
    autonumber
    actor K as Kader
    participant F as Form C8
    participant V as Validasi
    participant W as Kalkulator WHO
    participant DB as Database
    participant N as Notification Engine
    actor O as Orang Tua

    K->>F: Pilih peserta (C7 / QR) & isi BB/TB/LK
    F->>V: Validasi rentang real-time
    alt Tidak valid
        V-->>F: Field ditandai merah
        F-->>K: Minta koreksi
    else Valid
        V->>W: Hitung status antropometri
        W-->>F: Normal / Perlu Perhatian / Kritis
        F->>DB: Simpan + audit trail (maks. 2 detik)
        F-->>K: C9 Hasil Pengukuran + opsi edit 24 jam
        DB-->>N: Data pengukuran baru
        N-->>O: Push "Data Aisyah diperbarui" (usulan)
        O->>O: Buka B1 / B5 / B7
    end

    Note over K,O: Data yang sama menjadi sumber B1, B4, B5, B7<br/>dan C1, C3, C16 milik kader.
```

### 5.3 Pengingat Jadwal Otomatis (Push Native + WhatsApp)

```mermaid
sequenceDiagram
    autonumber
    participant S as Scheduler
    participant N as Notification Engine
    participant P as FCM / APNs
    participant W as WhatsApp API
    actor O as Orang Tua
    participant App as Aplikasi PosCare

    S->>N: Trigger H-3 / H-1 / hari-H 07.00 WIB
    N->>P: Kirim push native
    P-->>O: Notifikasi di layar kunci
    alt Dibuka dalam 2 jam
        O->>App: Ketuk notifikasi
        App->>App: Cek sesi (A1 Splash)
        App-->>O: Deep link ke B10 Detail Jadwal
    else Tidak dibuka
        N->>W: Kirim pesan cadangan
        W-->>O: Pesan WhatsApp
    end

    Note over S,App: Mengikuti NOTIF-001 s.d. NOTIF-003.<br/>Izin notifikasi diminta di A10.
```

### 5.4 Pindai QR Kartu Anak di Meja Pendaftaran (Usulan 🟣)

```mermaid
sequenceDiagram
    autonumber
    actor O as Orang Tua
    participant KA as B16 Kartu Anak
    actor K as Kader
    participant QR as C6 Pindai QR
    participant DB as Database

    O->>KA: Buka Kartu Anak Digital
    O->>K: Tunjukkan QR di meja pendaftaran
    K->>QR: Arahkan kamera ke QR
    QR->>DB: Cari Kode ID (mis. PK-0086)
    alt Ditemukan
        DB-->>QR: Data anak
        QR-->>K: Buka C8 Form Pengukuran / C3 Detail
    else Tidak ditemukan
        QR-->>K: Pesan error + Ketik Kode ID manual
    end

    Note over O,DB: Usulan mobile. Memperluas SRS 5.2 (akses kamera)<br/>dan perlu persetujuan tim.
```

---

## 6. Matriks Hak Akses Aplikasi Mobile

| Fitur / Modul | Kader | Orang Tua | Admin |
|---|:---:|:---:|:---:|
| Registrasi & Login di aplikasi | ✅ (akun dibuat admin) | ✅ | ❌ (web) |
| Tambah/Edit Data Peserta | ✅ | ❌ | ❌ (web) |
| Input Hasil Pengukuran | ✅ | ❌ | ❌ (web) |
| Lihat Riwayat Anak | ✅ (semua) | ✅ (anak sendiri) | ❌ (web) |
| Lihat Grafik Pertumbuhan | ✅ (semua) | ✅ (anak sendiri) | ❌ (web) |
| Kelola Jadwal Kegiatan & Imunisasi | ✅ | ❌ | ❌ (web) |
| Terima Notifikasi Jadwal | ❌ (hanya notifikasi kader) | ✅ | ❌ |
| Kirim Pengumuman | ✅ | ❌ | ❌ (web) |
| Pemantauan Kehadiran 🔵 | ✅ | ❌ | ❌ (web) |
| Unduh Laporan Bulanan 🔵 | ✅ | ❌ | ❌ (web) |
| Kartu Anak Digital 🟣 | ✅ (memindai) | ✅ (menampilkan) | ❌ |
| Manajemen Akun Kader | ❌ | ❌ | ❌ (web) |

Sumber: SRS 8.2, disesuaikan untuk aplikasi mobile. Admin yang login di aplikasi diarahkan ke **D3 Akses Ditolak** dengan pesan untuk memakai dashboard web. Pelanggaran akses lain juga diarahkan ke **D3** (`SEC-004`, `SEC-005`).

---

## 7. Cakupan Modul & Layar

| Modul SRS | Layar Terkait | Status |
|---|---|---|
| AUTH | A1, A3–A9, A11, B14, B17, C19, D2 | 🟢 MVP |
| Dashboard Kader / Input Data (I-4) | C1–C5, C7–C13 | 🟢 MVP |
| Riwayat Kesehatan Anak (I-1) | B1–B6, B18, C3 | 🟢 MVP |
| Grafik Pertumbuhan & Status (I-3) | B1, B7, B8, C3, C9, C16 | 🟢 MVP |
| Pengingat Jadwal Otomatis (I-2) | A10, B9–B12, B15, C13–C15, C20 | 🟢 MVP + 🔵 (status kirim C15) |
| Pemantauan Kehadiran (I-6) | C17 | 🔵 Iterasi 2 |
| Rekap & Laporan Bulanan (I-5) | C18 | 🔵 Iterasi 2 |
| Keamanan & Privasi | A12, B17, D3 | 🟢 MVP |
| Utilitas sistem & komponen | D1–D9 | 🟢 MVP + 🟣 (D5) |
| Usulan mobile | B16, C6, D5, sebagian B10, B17, C5, C8, D1 | 🟣 Perlu persetujuan |

---

## 8. Catatan Implementasi Prototype Mobile

1. **Dibuat di Figma, tanpa backend.** Satu frame per layar (390 × 844 pt, iPhone 14/15) mengikuti `PosCare_Style_Guide.md`: warna utama `#0F9D7A`, aksen `#FF6B5A`, font Inter, kartu radius 16, teks isi min. 15 pt.
2. **Navigasi prototype.** Tab bar dibuat sebagai komponen dengan variant per tab aktif. Layar turunan memakai aksi **Back**. Tombol ➕ kader dihubungkan ke C7 dari semua tab utama.
3. **Overlay.** B2 Pilih Anak, B8 Detail Titik Grafik, D6 Dialog Konfirmasi, dan D7 Toast dibuka dengan *Open overlay* (posisi bawah untuk bottom sheet, tengah untuk dialog).
4. **Login demo.** A4 memiliki tombol **Masuk sebagai Orang Tua** dan **Masuk sebagai Kader** agar setiap alur peran bisa dicoba langsung.
5. **Interaksi tiruan.** OTP, dialog izin sistem, kamera/QR, push notification, deep link, *pull-to-refresh*, dan unduh PDF/XLSX hanya berupa tampilan. Bila perlu, push notification dibuat sebagai frame layar kunci yang mengarah ke B10.
6. **Data contoh konsisten.** Gunakan data yang sama di semua layar: Aisyah Farida (24 bulan, 11,2 kg, 85 cm, Normal), Raka Aditya (9 bulan, Perlu Perhatian), Bunda Dewi Lestari, Bu Sri Rahayu, Kode ID PK-0086, Posyandu Sabtu 14 Nov 2026 08.00 WIB.
7. **Label fase di frame.** Frame 🔵 Iterasi 2 dan 🟣 Usulan Mobile diberi label di pojok frame agar penguji tahu layar mana yang belum masuk MVP.
8. **Relasi dengan prototype web.** Kode layar mobile (A1–D9) **berbeda** dari kode halaman web (A1–E4). Pemetaannya:

| Fitur | Web | Mobile |
|---|---|---|
| Landing / pintu masuk | A1 Landing | A1 Splash, A3 Selamat Datang |
| Login / Registrasi / Lupa sandi | A2 / A3 / A4 | A4 / A5–A8, A11 / A9 |
| Onboarding / FAQ | A5 / A6 | A2 / D8 |
| Dashboard / Beranda peserta | B1 | B1 (+ B2, B3) |
| Riwayat / Detail kunjungan / Imunisasi | B2 / B3 / B4 | B4 / B5 / B6 |
| Grafik | B5 | B7 (+ B8) |
| Jadwal / Notifikasi / Pengaturan | B6 / B7 / B8 | B9–B10 / B11–B12 / B13–B18 |
| Dashboard kader / Daftar / Form / Detail | C1 / C2 / C3 / C4 | C1 / C2 / C4–C5 / C3 |
| Input pengukuran | C5 | C7–C10 |
| Jadwal / Imunisasi / Pengumuman | C6 / C7 / C8 | C11–C12 / C13 / C14–C15 |
| Kehadiran / Laporan | C9 / C10 | C17 / C18 |
| Admin | D1–D5 | — (tetap di web) |
| 404 / 403 / Sesi / Maintenance | E1 / E2 / E3 / E4 | — / D3 / D2 / D4 |

---

*Disusun berdasarkan SRS SiPosya v1.0, mobile-page.md (59 layar), dan PROTOTYPE-FLOW.md versi web — PosCare, 2026.*