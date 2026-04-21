# SIPALUM — Sistem Pelacakan Alumni Publik UMM

> Daily Project 3 | Rekayasa Kebutuhan D  
> **Nama:** Naira Septina Kiswandani | **NIM:** 202310370311375

---

## 📌 Deskripsi Sistem

SIPALUM adalah sistem web berbasis HTML/CSS/JavaScript untuk melacak dan mengelola data alumni Universitas Muhammadiyah Malang (UMM). Sistem ini merupakan implementasi dari pseudocode, use case diagram, dan activity diagram yang telah dirancang pada **Daily Project 2**.

Sistem memuat **142.292 data alumni** dari tahun 1986–2025 berdasarkan file Excel UMM, dengan fitur confidence scoring, query generator, dan manajemen kontak alumni.

---

## 🔐 Akun Login

| Role | Username | Password |
|------|----------|----------|
| Admin Utama | `admin.umm` | `sipalum2025` |
| Operator | `operator` | `umm123` |

---

## 🚀 Fitur Utama

| Fitur | Deskripsi |
|-------|-----------|
| 🔐 **Login System** | Autentikasi berbasis username/password, session management |
| 📊 **Dashboard** | Statistik alumni, distribusi fakultas, aktivitas terbaru |
| 👤 **Data Alumni** | Tabel 142K+ alumni dengan search, filter fakultas & status |
| 🔍 **Jalankan Pelacakan** | Generate query dari pseudocode algoritma DP2 |
| ⚙️ **Generator Query** | Template query berdasarkan sumber & bidang alumni |
| 💾 **Input Data Kontak** | Admin input manual: LinkedIn, IG, email, HP, tempat kerja, posisi, status kerja |
| 📊 **Confidence Scoring** | Disambiguasi dengan skor: nama (30%) + afiliasi (25%) + timeline (25%) + bidang (20%) |
| 📋 **Jejak Audit** | Log semua aktivitas sistem (pelacakan, update, import) |
| 📈 **Statistik** | Distribusi alumni per fakultas lengkap |

---

## 🏗️ Arsitektur Sistem

```
SIPALUM Web App
├── Login Layer       → Autentikasi admin/operator
├── Dashboard         → Overview & monitoring
├── Data Alumni       → CRUD + filter + search 142K data
├── Pelacakan Engine  → Query generator + scoring
│   ├── Bentuk_Profil_Pencarian()
│   ├── Generate_Query()
│   ├── Disambiguasi()
│   └── Cross_Validation()
├── Audit Trail       → Simpan_Jejak_Bukti()
└── Statistik         → Analisis distribusi
```

---

## 🧪 Hasil Pengujian

### Tabel Pengujian Kualitas Sistem (ISO 25010)

| No | Aspek Kualitas | Kriteria Pengujian | Hasil | Status |
|----|---------------|-------------------|-------|--------|
| 1 | **Functional Suitability** | Login berhasil dengan kredensial benar | Username `admin.umm` + password `sipalum2025` → masuk ke dashboard | ✅ Pass |
| 2 | **Functional Suitability** | Login gagal dengan kredensial salah | Menampilkan pesan error "Username atau password salah" | ✅ Pass |
| 3 | **Functional Suitability** | Filter alumni berdasarkan Fakultas | Filter "Teknik" → hanya menampilkan alumni Teknik & Teknik (spasi) | ✅ Pass |
| 4 | **Functional Suitability** | Filter alumni berdasarkan Status | Filter "Teridentifikasi" → hanya tampil alumni dengan status found | ✅ Pass |
| 5 | **Functional Suitability** | Search alumni by nama | Ketik "Berliana" → muncul Berliana Oktaviani | ✅ Pass |
| 6 | **Functional Suitability** | Search alumni by NIM | Ketik "201710460311088" → muncul record yang tepat | ✅ Pass |
| 7 | **Functional Suitability** | Generate query pelacakan | Input nama → menghasilkan 6 query template sesuai pseudocode DP2 | ✅ Pass |
| 8 | **Functional Suitability** | Confidence scoring | Disambiguasi menghasilkan skor + klasifikasi (Kuat/Verifikasi/Tidak Cocok) | ✅ Pass |
| 9 | **Functional Suitability** | Input & simpan data kontak | Admin isi form kontak → tersimpan dan status berubah jadi Teridentifikasi | ✅ Pass |
| 10 | **Functional Suitability** | Audit log tercatat | Setiap aksi (pelacakan, update, login) masuk ke jejak audit | ✅ Pass |
| 11 | **Usability** | Navigasi antar halaman | Semua 6 menu sidebar dapat berpindah halaman tanpa error | ✅ Pass |
| 12 | **Usability** | Modal detail alumni | Klik baris tabel → modal terbuka dengan data lengkap | ✅ Pass |
| 13 | **Usability** | Responsif pagination | Data 43 alumni → pagination otomatis (3 halaman × 15 record) | ✅ Pass |
| 14 | **Usability** | Toast notification | Simpan data → muncul notifikasi "✅ Data berhasil disimpan" | ✅ Pass |
| 15 | **Performance** | Load 43 sample alumni | Render tabel langsung tanpa delay | ✅ Pass |
| 16 | **Performance** | Filter real-time | Filter/search menampilkan hasil instan saat mengetik | ✅ Pass |
| 17 | **Security** | Session management | Refresh halaman setelah login → tetap login (sessionStorage) | ✅ Pass |
| 18 | **Security** | Logout bersih | Klik logout → kembali ke halaman login, session dihapus | ✅ Pass |
| 19 | **Security** | Perlindungan data pribadi | Tidak ada scraping otomatis; data kontak hanya diisi manual oleh admin | ✅ Pass |
| 20 | **Maintainability** | Struktur kode | Fungsi terpisah per fitur (login, filter, modal, scoring, audit) | ✅ Pass |

### Keterangan Status
- ✅ **Pass** — Fitur berjalan sesuai ekspektasi
- ⚠️ **Warning** — Berjalan namun perlu perbaikan minor  
- ❌ **Fail** — Fitur tidak berjalan sesuai ekspektasi

---

## 📁 Struktur File

```
alumni-tracker/
├── index.html          # Single-file web app (HTML + CSS + JS)
└── README.md           # Dokumentasi & hasil pengujian
```

---

## 🔗 Link

- **Source Code:** [GitHub Repository]
- **Live Demo:** [Link Publish Web]

---

## 📝 Catatan Etika & Privasi

Sistem ini dirancang untuk keperluan **tracer study akademik** dengan prinsip:
1. Data kontak alumni **hanya diisi manual** oleh admin setelah alumni memberikan consent
2. **Tidak ada scraping otomatis** dari media sosial atau platform pihak ketiga
3. Data terlindungi dengan sistem login; tidak dapat diakses publik
4. Seluruh data alumni bersumber dari database resmi institusi
5. Sistem mematuhi **UU Perlindungan Data Pribadi (UU No. 27 Tahun 2022)**

---

## 👩‍💻 Pengembang

**Naira Septina Kiswandani**  
NIM: 202310370311375  
Kelas: Rekayasa Kebutuhan D  
Program Studi: Teknik Informatika — Universitas Muhammadiyah Malang
