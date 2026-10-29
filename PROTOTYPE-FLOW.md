# Prototype Flow — SiPosya

**Sistem Informasi Posyandu Digital — Posyandu Kartini IV A**
Kelompok 12 TI-C1 · D4 Teknik Informatika · Universitas Airlangga

> Dokumen ini memetakan alur prototype berdasarkan **SRS SiPosya v1.0 (Oktober 2026)**, **list-all-page.txt (33 halaman)**, dan **seluruh file HTML yang sudah dibuat**. Struktur file telah dipisahkan per peran agar alur navigasi tidak tercampur.

---

## 1. Ringkasan Peran & Struktur Folder

| Kelompok | Folder | Peran | Jumlah Halaman | Fase |
|---|---|---|---|---:|---|
| Umum / Publik & Autentikasi | `umum/` | Semua | 6 | 🟢 MVP |
| Area Peserta | `peserta/` | Peserta (orang tua/wali) | 8 | 🟢 MVP |
| Area Kader | `kader/` | Kader Posyandu | 10 + 1 duplikat | 🟢 MVP + 🔵 Iterasi 2 |
| Area Administrator | `admin/` | Administrator | 5 | 🟢 MVP + 🔵 Iterasi 2 |
| Halaman Sistem | `sistem/` | Semua | 4 | 🟢 MVP |
| **Total** | — | — | **33 halaman** | — |

**Struktur file aktual:**

```text
allpage/
├─ index.html                         # Portal seluruh halaman
├─ PROTOTYPE-FLOW.md                  # Dokumen ini
├─ SRS.md
├─ list-all-page.txt
├─ umum/
│  ├─ landing.html                    # A1
│  ├─ login.html                      # A2
│  ├─ register.html                   # A3
│  ├─ lupa-sandi.html                 # A4
│  ├─ onboarding.html                 # A5
│  └─ bantuan-faq.html                # A6
├─ peserta/
│  ├─ peserta-dashboard.html          # B1
│  ├─ peserta-riwayat.html            # B2
│  ├─ peserta-kunjungan-detail.html   # B3
│  ├─ peserta-imunisasi.html          # B4
│  ├─ peserta-grafik.html             # B5
│  ├─ peserta-jadwal.html             # B6
│  ├─ peserta-notifikasi.html         # B7
│  └─ peserta-pengaturan.html         # B8
├─ kader/
│  ├─ home.html                       # C1 (dashboard utama)
│  ├─ kader-dashboard.html            # C1 (duplikat desain)
│  ├─ kader-peserta.html              # C2
│  ├─ kader-peserta-form.html         # C3
│  ├─ kader-peserta-detail.html       # C4
│  ├─ kader-input-pengukuran.html     # C5
│  ├─ kader-jadwal.html               # C6
│  ├─ kader-imunisasi.html            # C7
│  ├─ kader-pengumuman.html           # C8
│  ├─ kader-kehadiran.html            # C9
│  └─ kader-laporan.html              # C10
├─ admin/
│  ├─ admin-dashboard.html            # D1
│  ├─ admin-kader.html                # D2
│  ├─ admin-peserta.html              # D3
│  ├─ admin-konfigurasi.html          # D4
│  └─ admin-log.html                  # D5
└─ sistem/
   ├─ 404.html                        # E1
   ├─ 403.html                        # E2
   ├─ sesi-berakhir.html              # E3
   └─ maintenance.html                # E4
```

> **Catatan:** `kader/home.html` adalah dashboard kader yang menjadi acuan desain. `kader/kader-dashboard.html` adalah duplikat desain dengan navigasi sidebar yang lebih lengkap. Keduanya dipertahankan.

---

## 2. Peta Halaman & Traceability SRS

| Kode | Halaman | File | Peran | Fase | Referensi SRS |
|---|---|---|---|---|---|
| A1 | Landing Page | `umum/landing.html` | Semua | 🟢 | Batasan 2.4 |
| A2 | Login | `umum/login.html` | Semua | 🟢 | AUTH-002, AUTH-003, SEC-002, SEC-007 |
| A3 | Registrasi Peserta | `umum/register.html` | Peserta | 🟢 | AUTH-001, KADER-002 |
| A4 | Lupa Kata Sandi | `umum/lupa-sandi.html` | Semua | 🟢 | AUTH-004 |
| A5 | Onboarding | `umum/onboarding.html` | Semua | 🟢 | SRS 5.1 |
| A6 | Bantuan / FAQ | `umum/bantuan-faq.html` | Semua | 🟢 | — |
| B1 | Dashboard Peserta | `peserta/peserta-dashboard.html` | Peserta | 🟢 | RIWAYAT-005, RIWAYAT-007, GRAFIK-005 |
| B2 | Riwayat Kesehatan Anak | `peserta/peserta-riwayat.html` | Peserta | 🟢 | RIWAYAT-001, RIWAYAT-003, RIWAYAT-006, RIWAYAT-007 |
| B3 | Detail Kunjungan | `peserta/peserta-kunjungan-detail.html` | Peserta | 🟢 | RIWAYAT-001, RIWAYAT-002, RIWAYAT-004, RIWAYAT-007 |
| B4 | Riwayat & Jadwal Imunisasi | `peserta/peserta-imunisasi.html` | Peserta | 🟢 | RIWAYAT-002, NOTIF-003 |
| B5 | Grafik Pertumbuhan | `peserta/peserta-grafik.html` | Peserta | 🟢 | GRAFIK-001 s.d. GRAFIK-006 |
| B6 | Jadwal & Kalender Kegiatan | `peserta/peserta-jadwal.html` | Peserta | 🟢 | KADER-016, NOTIF-001, NOTIF-003 |
| B7 | Notifikasi & Pengumuman | `peserta/peserta-notifikasi.html` | Peserta | 🟢 | NOTIF-001 s.d. NOTIF-005, NOTIF-007 |
| B8 | Pengaturan Akun Peserta | `peserta/peserta-pengaturan.html` | Peserta | 🟢 | NOTIF-004, RIWAYAT-008, AUTH-005 |
| C1 | Dashboard Kader | `kader/home.html` | Kader | 🟢 | KADER-005, KADER-016, GRAFIK-007 |
| C2 | Daftar Peserta | `kader/kader-peserta.html` | Kader | 🟢 | KADER-003, KADER-005, KADER-006 |
| C3 | Tambah / Edit Peserta | `kader/kader-peserta-form.html` | Kader | 🟢 | KADER-001, KADER-002, KADER-004 |
| C4 | Detail Peserta (Kader) | `kader/kader-peserta-detail.html` | Kader | 🟢 | KADER-004, RIWAYAT-001, GRAFIK-007 |
| C5 | Input Hasil Pengukuran | `kader/kader-input-pengukuran.html` | Kader | 🟢 | KADER-007 s.d. KADER-013 |
| C6 | Kelola Jadwal Kegiatan | `kader/kader-jadwal.html` | Kader | 🟢 | KADER-014, KADER-016 |
| C7 | Kelola Jadwal Imunisasi | `kader/kader-imunisasi.html` | Kader | 🟢 | KADER-015 |
| C8 | Kirim Pengumuman | `kader/kader-pengumuman.html` | Kader | 🟢 | NOTIF-005, NOTIF-007 |
| C9 | Pemantauan Kehadiran | `kader/kader-kehadiran.html` | Kader | 🔵 | HADIR-001 s.d. HADIR-004 |
| C10 | Rekap & Laporan Bulanan | `kader/kader-laporan.html` | Kader | 🔵 | LAPORAN-001 s.d. LAPORAN-004 |
| D1 | Dashboard Administrator | `admin/admin-dashboard.html` | Admin | 🟢 | SRS 8.2 |
| D2 | Manajemen Akun Kader | `admin/admin-kader.html` | Admin | 🟢 | AUTH-006 |
| D3 | Manajemen Peserta (Admin) | `admin/admin-peserta.html` | Admin | 🟢 | SRS 8.2 |
| D4 | Konfigurasi Sistem | `admin/admin-konfigurasi.html` | Admin | 🟢 | Batasan 2.4 |
| D5 | Log Aktivitas Sistem | `admin/admin-log.html` | Admin | 🔵 | AUTH-007, NOTIF-006 |
| E1 | Error 404 | `sistem/404.html` | Semua | 🟢 | — |
| E2 | Akses Ditolak (403) | `sistem/403.html` | Semua | 🟢 | SEC-004, SEC-005 |
| E3 | Sesi Berakhir | `sistem/sesi-berakhir.html` | Semua | 🟢 | AUTH-005 |
| E4 | Pemeliharaan Sistem | `sistem/maintenance.html` | Semua | 🟢 | AVAIL-002 |

**Legenda fase:** 🟢 MVP · 🔵 Iterasi 2
**Legenda diagram:** garis **solid** = alur yang dapat ditelusuri di prototype (tautan halaman atau aksi form/tombol); garis **putus-putus** = alur otomatis/backend atau tautan lintas peran yang belum berupa tombol langsung.

---

## 3. Alur Utama Berdasarkan Peran

### 3.1 Routing Awal & Pemilihan Peran

```mermaid
flowchart TD
    L["A1 Landing<br/>umum/landing.html"] --> ASK{"Punya akun?"}
    ASK -->|"Ya"| LG["A2 Login<br/>umum/login.html"]
    ASK -->|"Belum"| RG["A3 Registrasi Peserta<br/>umum/register.html"]
    ASK -->|"Butuh bantuan"| FAQ["A6 Bantuan / FAQ<br/>umum/bantuan-faq.html"]

    RG -->|"Kode ID anak valid"| OB["A5 Onboarding<br/>umum/onboarding.html"]
    OB --> PD["B1 Dashboard Peserta<br/>peserta/peserta-dashboard.html"]

    LG --> ROLE{"Peran pengguna"}
    ROLE -->|"Peserta"| PD
    ROLE -->|"Kader"| KD["C1 Dashboard Kader<br/>kader/home.html"]
    ROLE -->|"Admin"| AD["D1 Dashboard Admin<br/>admin/admin-dashboard.html"]

    LG -->|"Lupa kata sandi"| FP["A4 Lupa Kata Sandi<br/>umum/lupa-sandi.html"]
    FP -->|"OTP valid + sandi baru"| LG

    PD -.->|"idle 30 menit"| SE["E3 Sesi Berakhir<br/>sistem/sesi-berakhir.html"]
    KD -.-> SE
    AD -.-> SE
    SE -->|"Masuk kembali"| LG

    IDX["index.html<br/>Portal 33 halaman"] -->|"akses langsung"| PD
    IDX --> KD
    IDX --> AD

    classDef public fill:#eaf0fe,stroke:#3a6ff0,color:#1e3a8a;
    classDef peserta fill:#e8f6ed,stroke:#15a05a,color:#14532d;
    classDef kader fill:#e7f6f1,stroke:#0f9d7a,color:#0b5f4a;
    classDef admin fill:#f1effd,stroke:#6c5ce7,color:#3b2f9e;
    classDef sistem fill:#fbf1e1,stroke:#c77a16,color:#7c4a0a;
    class L,LG,RG,FAQ,FP,OB public;
    class PD peserta;
    class KD kader;
    class AD admin;
    class SE sistem;
```

### 3.2 Autentikasi, Registrasi & Pemulihan Akun

```mermaid
flowchart TD
    START["Buka aplikasi"] --> LAND["A1 Landing"]
    LAND -->|"Masuk"| LOGIN["A2 Login"]
    LAND -->|"Daftar Peserta"| REG["A3 Registrasi Peserta"]
    LAND -->|"Bantuan"| FAQ["A6 FAQ"]

    LOGIN -->|"Lupa Kata Sandi"| FORGOT["A4 Lupa Kata Sandi"]
    FORGOT --> WA["Masukkan nomor WhatsApp terdaftar"]
    WA --> OTP["Kirim OTP via WhatsApp"]
    OTP --> OTPOK{"OTP valid?"}
    OTPOK -->|"Tidak / kedaluwarsa"| OTP
    OTPOK -->|"Ya"| NEW["Isi kata sandi baru + konfirmasi"]
    NEW --> LOGIN

    LOGIN --> CRED{"Kredensial valid?"}
    CRED -->|"Tidak, percobaan < 5"| ERR["Pesan error Bahasa Indonesia"]
    ERR --> LOGIN
    CRED -->|"Gagal 5 kali"| LOCK["Akun dikunci 15 menit<br/>SEC-007"]
    LOCK --> LOGIN

    CRED -->|"Ya"| AUTH["Buat sesi JWT<br/>AUTH-003"]
    AUTH --> ROLE{"Redirect sesuai peran"}
    ROLE -->|"Peserta"| NEWUSER{"Pengguna baru?"}
    NEWUSER -->|"Ya"| ONB["A5 Onboarding"]
    NEWUSER -->|"Tidak"| PD["B1 Dashboard Peserta"]
    ONB --> PD
    ROLE -->|"Kader"| KD["C1 Dashboard Kader"]
    ROLE -->|"Admin"| AD["D1 Dashboard Admin"]

    REG --> FIELDS["Nama, No. WhatsApp,<br/>Kata Sandi, Kode ID Anak"]
    FIELDS --> IDOK{"Kode ID cocok<br/>dengan data anak?"}
    IDOK -->|"Tidak"| REGERR["Tampilkan error validasi"]
    REGERR --> FIELDS
    IDOK -->|"Ya"| LINK["Akun terhubung ke data anak"]
    LINK --> ONB

    classDef auth fill:#eaf0fe,stroke:#3a6ff0,color:#1e3a8a;
    classDef peserta fill:#e8f6ed,stroke:#15a05a,color:#14532d;
    classDef kader fill:#e7f6f1,stroke:#0f9d7a,color:#0b5f4a;
    classDef admin fill:#f1effd,stroke:#6c5ce7,color:#3b2f9e;
    class START,LAND,LOGIN,REG,FAQ,FORGOT,WA,OTP,NEW,ERR,LOCK,AUTH,ROLE,NEWUSER,ONB,FIELDS,IDOK,REGERR,LINK auth;
    class PD peserta;
    class KD kader;
    class AD admin;
```

> **Catatan prototype:** tab peran dan tombol demo pada `umum/login.html` mengarah ke dashboard masing-masing (`peserta-dashboard`, `kader/home`, `admin-dashboard`) agar alur dapat dicoba tanpa backend.

---

### 3.3 Alur Peserta (Orang Tua / Wali)

```mermaid
flowchart LR
    D["B1 Dashboard Peserta<br/>Ringkasan kondisi terkini"] --> R["B2 Riwayat Kesehatan<br/>Filter bulan/tahun"]
    R -->|"tap entri"| K["B3 Detail Kunjungan<br/>Ukur + catatan kader + imunisasi"]
    K -->|"kembali"| R

    D --> G["B5 Grafik Pertumbuhan<br/>WHO Median, -2 SD, +2 SD"]
    D --> I["B4 Riwayat & Jadwal Imunisasi<br/>Sudah / Belum / Terjadwal"]
    D --> J["B6 Jadwal & Kalender<br/>Posyandu + imunisasi"]
    D --> N["B7 Notifikasi<br/>H-3, H-1, hari-H, pengumuman"]
    D --> S["B8 Pengaturan Akun<br/>Profil, anak, notifikasi, sandi"]

    S -->|"kelola / ganti anak aktif"| D
    S -->|"buka ulang tutorial"| OB["A5 Onboarding"]
    OB --> D
    S -->|"logout"| LG["A2 Login"]
    J -->|"lihat detail imunisasi"| I
    I -->|"vaksin terjadwal"| J
    N -->|"buka jadwal"| J

    classDef peserta fill:#e8f6ed,stroke:#15a05a,color:#14532d;
    classDef public fill:#eaf0fe,stroke:#3a6ff0,color:#1e3a8a;
    class D,R,K,G,I,J,N,S peserta;
    class OB,LG public;
```

**Poin penting:**
- Semua halaman peserta hanya menampilkan data anak milik akun yang login (`SEC-004`, `SEC-005`).
- Pemilih anak aktif berada di B1/B8; tidak ada halaman terpisah.
- Grafik B5 memakai referensi WHO dan dapat digeser horizontal pada layar kecil.
- Notifikasi B7 menandai pesan sudah/belum dibaca.

---

### 3.4 Alur Kader (Input Data & Operasional)

```mermaid
flowchart TD
    H["C1 Dashboard Kader<br/>kader/home.html"]

    subgraph MP["Manajemen Peserta"]
        direction LR
        P["C2 Daftar Peserta"]
        F["C3 Tambah / Edit Peserta"]
        DP["C4 Detail Peserta"]
        P -->|"Tambah"| F
        P -->|"Detail"| DP
        F -->|"Simpan (Kode ID unik)"| P
    end

    subgraph MG["Pengukuran"]
        direction TB
        IN["C5 Input Pengukuran"]
        STATUS["Status WHO<br/>Normal / Perlu Perhatian / Kritis"]
        IN -->|"Validasi + hitung WHO"| STATUS
        STATUS -->|"Simpan + audit trail"| P
        STATUS -.->|"Tampil di riwayat / grafik"| DP
    end

    subgraph MJ["Jadwal & Komunikasi"]
        direction LR
        JD["C6 Jadwal Kegiatan"]
        IM["C7 Jadwal Imunisasi"]
        PG["C8 Pengumuman"]
        NOTIF["Notifikasi peserta<br/>H-3 / H-1 / hari-H"]
        JD -->|"Kalender gabungan"| IM
        IM -.-> NOTIF
        PG -.->|"Pratinjau & kirim"| NOTIF
        NOTIF -.-> B7["B7 Notifikasi Peserta"]
    end

    subgraph ML["Pemantauan & Laporan"]
        direction LR
        KH["C9 Kehadiran<br/>Iterasi 2"]
        LP["C10 Laporan<br/>Iterasi 2"]
        REPORT["Laporan Puskesmas<br/>PDF / XLSX"]
        KH -.->|"Absen >= 2 bulan"| P
        LP -.-> REPORT
    end

    H --> P
    H --> IN
    H --> JD
    H --> PG
    H --> KH
    H --> LP
    P -->|"Input"| IN
    DP -->|"Input baru"| IN
    DP -->|"Edit data"| F
    DP -->|"Atur imunisasi"| IM

    classDef kader fill:#e7f6f1,stroke:#0f9d7a,color:#0b5f4a;
    classDef iter fill:#eaf0fe,stroke:#3a6ff0,color:#1e3a8a,stroke-dasharray:4 3;
    class H,P,F,DP,IN,JD,IM,PG,STATUS,NOTIF kader;
    class KH,LP,REPORT,B7 iter;
```

**Alur input pengukuran (C5) secara rinci:**

1. Pilih/konfirmasi peserta dari daftar atau pencarian.
2. Isi tanggal kunjungan, BB, TB, lingkar kepala (opsional), dan status imunisasi.
3. Validasi otomatis berjalan; error ditampilkan di field terkait.
4. Sistem menghitung status pertumbuhan berdasarkan tabel WHO.
5. Data disimpan dengan audit trail (nama kader + waktu).
6. Kader melihat status akhir dan dapat mengedit dalam 24 jam.
7. Data langsung muncul di riwayat, grafik, dan dashboard peserta.

---

### 3.5 Alur Administrator

```mermaid
flowchart LR
    AD["D1 Dashboard Admin<br/>admin/admin-dashboard.html"] --> AK["D2 Manajemen Akun Kader"]
    AD --> AP["D3 Manajemen Peserta"]
    AD --> CFG["D4 Konfigurasi Sistem"]
    AD --> LOG["D5 Log Aktivitas"]

    AK -.->|"Buat akun kader baru"| NEWK["Nama, No. WhatsApp,<br/>sandi awal, peran"]
    AK -.->|"Edit / nonaktifkan / reset"| AK

    AP -.->|"CRUD & koreksi data"| AP
    AP -->|"Lihat detail sebagai kader"| KD["C4 Detail Peserta<br/>kader/kader-peserta-detail.html"]

    CFG -.->|"Unit Posyandu"| UNIT["Posyandu Kartini IV A"]
    CFG -.->|"Integrasi notifikasi"| NOTIFCFG["WhatsApp API / Web Push"]
    CFG -.->|"Parameter WHO"| WHO["Ambang status pertumbuhan"]

    LOG -.->|"Filter tanggal/pengguna/jenis"| LOG

    classDef admin fill:#f1effd,stroke:#6c5ce7,color:#3b2f9e;
    classDef kader fill:#e7f6f1,stroke:#0f9d7a,color:#0b5f4a;
    classDef iter fill:#eaf0fe,stroke:#3a6ff0,color:#1e3a8a,stroke-dasharray:4 3;
    class AD,AK,AP,CFG,UNIT,NOTIFCFG,WHO,NEWK admin;
    class KD kader;
    class LOG iter;
```

**Batasan admin (sesuai SRS 8.2):**
- Hanya admin yang dapat membuat/mengelola akun kader (`AUTH-006`).
- Admin dapat melakukan CRUD seluruh peserta sebagai cadangan/koreksi lintas kader.
- Konfigurasi sistem hanya tersedia untuk admin.

---

### 3.6 Alur Halaman Sistem / Utilitas

```mermaid
flowchart TD
    REQ["Pengguna membuka halaman"] --> STATE{"Kondisi sistem"}

    STATE -->|"URL tidak ditemukan"| E404["E1 404<br/>sistem/404.html"]
    STATE -->|"Tidak berwenang / RBAC"| E403["E2 403<br/>sistem/403.html"]
    STATE -->|"Idle 30 menit"| E3["E3 Sesi Berakhir<br/>sistem/sesi-berakhir.html"]
    STATE -->|"Pemeliharaan 22.00-05.00 WIB"| E4["E4 Pemeliharaan<br/>sistem/maintenance.html"]

    E404 -->|"kembali"| DASH["Dashboard sesuai peran"]
    E403 -->|"kembali"| DASH
    E403 -->|"bantuan"| FAQ["A6 FAQ"]
    E3 -->|"Masuk kembali"| LOGIN["A2 Login"]
    E3 -->|"bantuan"| FAQ
    E4 -->|"Coba lagi"| LAND["A1 Landing"]
    E4 -->|"Hubungi kader"| FAQ
    DASH --> IDX["index.html"]

    classDef sistem fill:#fbf1e1,stroke:#c77a16,color:#7c4a0a;
    classDef public fill:#eaf0fe,stroke:#3a6ff0,color:#1e3a8a;
    class E404,E403,E3,E4 sistem;
    class DASH,FAQ,LOGIN,LAND,IDX public;
```

---

## 4. Sub-Alur Status Pertumbuhan (WHO)

```mermaid
flowchart LR
    IN["Input BB / TB / LK"] --> VAL{"Validasi rentang"}
    VAL -->|"Tidak valid"| ERR["Error: BB <= 50 kg<br/>TB >= 30 cm"]
    ERR --> IN
    VAL -->|"Valid"| WHO["Hitung Z-score<br/>standar WHO"]
    WHO --> N1["Normal"]
    WHO --> N2["Perlu Perhatian"]
    WHO --> N3["Kritis"]
    N1 --> ACT1["Edukasi gizi &<br/>jadwal rutin"]
    N2 --> ACT2["Konsultasi kader /<br/>pemantauan intensif"]
    N3 --> ACT3["Rujukan ke<br/>Puskesmas"]
    ACT1 --> SHOW["Tampilkan di riwayat,<br/>grafik, dan dashboard"]
    ACT2 --> SHOW
    ACT3 --> SHOW

    classDef ok fill:#e8f6ed,stroke:#15a05a,color:#14532d;
    classDef warn fill:#fbf1e1,stroke:#c77a16,color:#7c4a0a;
    classDef crit fill:#fbeaea,stroke:#d64545,color:#7f1d1d;
    class N1,ACT1 ok;
    class N2,ACT2 warn;
    class N3,ACT3 crit;
```

Status ini bersifat **indikatif** dan bukan pengganti konsultasi medis (SRS 2.4). Acuan: WHO Child Growth Standards dan Permenkes No. 2 Tahun 2020.

---

## 5. Sequence Diagram Alur Kritis

### 5.1 Login & Redirect Berdasarkan Peran

```mermaid
sequenceDiagram
    autonumber
    actor U as Pengguna
    participant P as Prototype
    participant A as Auth Service
    participant DB as Database

    U->>P: Buka login.html
    U->>P: Isi nomor WhatsApp + kata sandi
    P->>A: POST /auth/login
    A->>DB: Verifikasi kredensial & peran

    alt Kredensial valid
        DB-->>A: Data pengguna + role
        A-->>P: JWT + role
        alt Peserta
            P-->>U: B1 Dashboard Peserta
        else Kader
            P-->>U: C1 Dashboard Kader
        else Admin
            P-->>U: D1 Dashboard Admin
        end
    else Gagal 5 kali
        A-->>P: Akun dikunci 15 menit
        P-->>U: Pesan kunci sementara (SEC-007)
    end

    Note over P,U: Prototype statis memakai tautan demo<br/>langsung ke dashboard masing-masing peran.
```

### 5.2 Input Pengukuran hingga Tampil ke Peserta

```mermaid
sequenceDiagram
    autonumber
    actor K as Kader
    participant F as Form C5
    participant V as Validasi
    participant W as Kalkulator WHO
    participant DB as Database
    participant PP as Portal Peserta

    K->>F: Pilih peserta & isi BB/TB/LK
    F->>V: Validasi rentang nilai
    alt Tidak valid
        V-->>F: Pesan error real-time
        F-->>K: Minta koreksi field
    else Valid
        V->>W: Hitung status antropometri
        W-->>F: Normal / Perlu Perhatian / Kritis
        F->>DB: Simpan pengukuran + audit trail
        DB-->>PP: Riwayat, grafik, ringkasan terbaru
        F-->>K: Status pertumbuhan + opsi edit 24 jam
    end

    Note over K,PP: Data yang sama menjadi sumber B1-B5<br/>dan dashboard pemantauan kader.
```

### 5.3 Pengingat Jadwal Otomatis

```mermaid
sequenceDiagram
    autonumber
    participant S as Scheduler
    participant N as Notification Engine
    participant B as Web Push
    participant W as WhatsApp API
    actor P as Peserta

    S->>N: Trigger H-3 / H-1 / hari-H 07.00 WIB
    N->>B: Kirim web push
    alt Dibaca <= 2 jam
        P->>B: Buka notifikasi
        B-->>P: Detail jadwal / imunisasi
    else Tidak dibaca
        N->>W: Kirim pesan cadangan
        W-->>P: WhatsApp
    end
    P->>P: Buka B6 Jadwal atau B7 Notifikasi

    Note over S,P: Alur ini mengikuti NOTIF-001 s.d. NOTIF-003.<br/>Prototype menampilkan UI-nya, bukan engine sungguhan.
```

---

## 6. Matriks Hak Akses Prototype

| Fitur / Modul | Admin | Kader | Peserta |
|---|:---:|:---:|:---:|
| Registrasi & Login | ✅ | ✅ (dibuat admin) | ✅ |
| Tambah/Edit Data Peserta | ✅ | ✅ | ❌ |
| Input Hasil Pengukuran | ✅ | ✅ | ❌ |
| Lihat Riwayat Anak | ✅ (semua) | ✅ (semua) | ✅ (anak sendiri) |
| Lihat Grafik Pertumbuhan | ✅ (semua) | ✅ (semua) | ✅ (anak sendiri) |
| Kelola Jadwal Kegiatan | ✅ | ✅ | ❌ |
| Terima Notifikasi Jadwal | ✅ | ❌ | ✅ |
| Kirim Pengumuman | ✅ | ✅ | ❌ |
| Pemantauan Kehadiran | ✅ | ✅ | ❌ |
| Unduh Laporan Bulanan | ✅ | ✅ | ❌ |
| Manajemen Akun Kader | ✅ | ❌ | ❌ |

Sumber: SRS 8.2. Pelanggaran akses diarahkan ke **E2 403** (`SEC-004`, `SEC-005`).

---

## 7. Cakupan Modul & Halaman

| Modul SRS | Halaman Terkait | Status |
|---|---|---|
| AUTH | A2, A3, A4, E3, D2 | 🟢 MVP |
| Dashboard Kader / Input Data (I-4) | C1–C8 | 🟢 MVP |
| Riwayat Kesehatan Anak (I-1) | B1–B4, C4 | 🟢 MVP |
| Grafik Pertumbuhan & Status (I-3) | B1, B5, C1, C4 | 🟢 MVP |
| Pengingat Jadwal Otomatis (I-2) | B6, B7, C6, C7, C8 | 🟢 MVP |
| Pemantauan Kehadiran (I-6) | C9 | 🔵 Iterasi 2 |
| Rekap & Laporan Bulanan (I-5) | C10 | 🔵 Iterasi 2 |
| Tata kelola & audit | D1–D5 | 🟢 MVP + 🔵 Iterasi 2 |
| Utilitas sistem | E1–E4 | 🟢 MVP |

---

## 8. Catatan Implementasi Prototype

1. **Statis, tanpa JavaScript.** Seluruh halaman dibuat dengan HTML + CSS inline. Interaksi visual (tab, toggle, stepper, checklist) adalah mockup; navigasi memakai tautan antarfolder yang sudah diperbaiki.
2. **Satu file per halaman.** Setiap halaman memuat CSS-nya sendiri dan mengikuti design system `kader/home.html`: warna aksen `#0f9d7a`, font Inter, kartu `radius 16px`, sidebar desktop, dan hamburger CSS-only di seluler.
3. **Struktur per peran.** Folder `umum`, `peserta`, `kader`, `admin`, dan `sistem` memisahkan konteks agar prototype mudah ditinjau.
4. **Portal indeks.** `index.html` di root menjadi pintu masuk ke seluruh 33 halaman dan tetap menampilkan kelompok A–E.
5. **Duplikat dashboard.** `kader/home.html` adalah acuan desain; `kader/kader-dashboard.html` adalah variasi dengan sidebar lengkap.
6. **Belum ada backend.** Login, OTP, penyimpanan, notifikasi, ekspor PDF/XLSX, dan pembatasan RBAC masih berupa tampilan/alur, bukan fungsi nyata.
7. **Aksesibilitas & responsif.** Layout diuji pada lebar 320–1440 px; tabel lebar dapat digeser horizontal, tab panjang dapat di-scroll, dan sidebar berubah menjadi menu hamburger pada layar kecil.

---

*Disusun berdasarkan SRS SiPosya v1.0 dan 33 halaman prototype — Kelompok 12 TI-C1, Universitas Airlangga, 2026.*
