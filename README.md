# 🌿 ECO-SHARE — Platform Penyewaan Alat Elektronik Bekas

> **Dibuat oleh: Riando Muhamad Subakti**
> Mahasiswa Universitas Dian Nusantara | UTS Pemrograman Fullstack 2025/2026

---

## 📋 Deskripsi Proyek

Eco-Share adalah platform web fullstack untuk menyewa dan menyewakan alat elektronik bekas. Dibangun dengan **Node.js + Express** (backend API) dan **Vanilla JS + Vite** (frontend), menggunakan **MySQL** sebagai database.

---

## 🏗️ Arsitektur Sistem

```
UTS_PEMROGRAMAN_FULLSTACK/
├── config/db.js              # Koneksi MySQL Pool
├── controllers/
│   ├── authController.js     # Register, Login, Profile
│   ├── itemController.js     # CRUD Barang
│   └── rentController.js     # Transaksi Peminjaman
├── middleware/
│   ├── auth.js               # JWT Guard + Role Check
│   └── errorHandler.js       # Global Error Handler
├── models/schema.sql         # Skema Database
├── routes/
│   ├── authRoutes.js
│   ├── itemRoutes.js
│   └── rentRoutes.js
├── services/
│   └── rentService.js        # Logika Bisnis (DB Transaction)
├── index.html                # Frontend SPA
├── vite.config.js
├── server.js                 # Entry Point
└── .env
```

---

## ⚙️ Cara Menjalankan

### 1. Persiapan Database MySQL
Buka MySQL Workbench atau phpMyAdmin, lalu jalankan file `models/schema.sql`

### 2. Konfigurasi .env
Edit file `.env` sesuai database Anda:
```
DB_HOST=localhost
DB_USER=root
DB_PASSWORD=password_mysql_kamu
DB_NAME=ecoshare_db
JWT_SECRET=ecoshare_secret_key_random_panjang
```

### 3. Install Dependencies
```bash
npm install
```

### 4. Jalankan Backend
```bash
npm run dev
```
Backend berjalan di: http://localhost:3000

### 5. Jalankan Frontend (terminal baru)
```bash
npm run frontend
```
Frontend berjalan di: http://localhost:5173

---

## 🔌 Endpoint API

### Auth
| Method | Endpoint | Deskripsi | Auth |
|--------|----------|-----------|------|
| POST | /api/auth/register | Daftar akun | - |
| POST | /api/auth/login | Login | - |
| GET  | /api/auth/profile | Profil saya | JWT |

### Items (Barang)
| Method | Endpoint | Deskripsi | Auth |
|--------|----------|-----------|------|
| GET | /api/items | Semua barang | - |
| GET | /api/items/:id | Detail barang | - |
| GET | /api/items/milik-saya | Barang saya | Pemilik |
| POST | /api/items | Tambah barang | Pemilik |
| PUT | /api/items/:id | Update barang | Pemilik |
| DELETE | /api/items/:id | Hapus barang | Pemilik |

### Rentals (Sewa)
| Method | Endpoint | Deskripsi | Auth |
|--------|----------|-----------|------|
| POST | /api/rentals | Buat sewa | Penyewa |
| GET | /api/rentals/riwayat | Riwayat sewa | Penyewa |
| GET | /api/rentals/semua | Semua sewa barangku | Pemilik |
| PUT | /api/rentals/:id/selesai | Kembalikan barang | Penyewa |
| PUT | /api/rentals/:id/batalkan | Batalkan sewa | Penyewa |

---

## 🔒 Fitur Keamanan

- **JWT Stateless Authentication** — Token dikirim via Authorization header
- **Role-Based Access Control** — Penyewa vs Pemilik punya akses berbeda
- **MySQL Transaction** — Sewa barang pakai `BEGIN TRANSACTION` + `ROLLBACK` untuk hindari data korup
- **SELECT FOR UPDATE** — Lock baris saat sewa untuk cegah race condition
- **bcrypt** — Password di-hash sebelum disimpan
- **Global Error Handler** — Semua error ditangkap dan dikembalikan sebagai JSON

---

## 📊 Skema Database

```sql
users       → id, nama, email, password, role (penyewa/pemilik)
items       → id, pemilik_id, nama_barang, harga_per_hari, stok, status
rentals     → id, penyewa_id, item_id, tanggal_mulai, tanggal_selesai, total_biaya, status
```

---

## 🐙 Git Workflow

```bash
git init
git add .
git commit -m "feat: inisialisasi project Eco-Share dengan struktur MVC"

git add models/schema.sql config/db.js
git commit -m "feat: tambah skema database dan koneksi MySQL pool"

git add controllers/ routes/ middleware/ services/
git commit -m "feat: implementasi REST API dengan JWT auth dan service layer"

git add index.html vite.config.js
git commit -m "feat: tambah frontend SPA dengan tema ungu dan integrasi API"

git remote add origin https://github.com/username/ecoshare-uts.git
git push -u origin main
```

---

*© 2026 Riando Muhamad Subakti — Universitas Dian Nusantara*