# Full-Stack Blogging Platform

Sebuah platform blog *full-stack* modern yang memisahkan antara antarmuka pengguna (Frontend) dan pemrosesan data (Backend). Proyek ini dibangun menggunakan **Vue 3 (Vite)** sebagai *Single Page Application* (SPA) dan **Flask (Python)** sebagai REST API (Headless CMS).

## 🚀 Fitur Utama
* **Autentikasi Pengguna**: Registrasi, Login, dan Logout menggunakan sistem sesi (Flask-Login).
* **CRUD Artikel**: Pengguna yang masuk dapat membuat dan menghapus artikel miliknya sendiri.
* **Paginasi & Pencarian**: API mendukung pengambilan data dengan parameter halaman, batas data, dan kata kunci.
* **Keamanan API**: Dilengkapi *Rate Limiting* (Flask-Limiter) untuk mencegah *brute-force* dan *spam*.
* **Dokumentasi Interaktif**: Seluruh *endpoint* API terdokumentasi secara otomatis dengan Swagger UI (Flasgger).
* **CORS Enabled**: Mendukung *cross-origin requests* dari antarmuka Vue.

## 🛠️ Tech Stack
**Frontend:**
* Vue 3 (Composition API)
* Vite
* Vue Router 4
* Axios

**Backend:**
* Python 3 & Flask
* Flask-SQLAlchemy & PyMySQL (MySQL Database)
* Flask-Login
* Flask-CORS & Flask-Limiter
* Flasgger (Swagger UI)

## 📁 Struktur Proyek
```text
vue-blog-platform/
├── blog-backend/      # Lingkungan backend Flask (REST API)
└── blog-frontend/     # Lingkungan frontend Vue 3 (SPA)

```

## ⚙️ Prasyarat

Sebelum menjalankan proyek ini, pastikan sistem Anda telah terinstal:

* **Python 3.x**
* **Node.js** (versi 18+ direkomendasikan)
* **MySQL Server** (misalnya via XAMPP)

## 💻 Cara Instalasi & Menjalankan Aplikasi

### 1. Konfigurasi Backend (Flask API)

Pastikan server MySQL Anda sudah berjalan dan memiliki *database* bernama `flask_blog`.

```bash
# Masuk ke direktori backend
cd blog-backend

# Aktifkan virtual environment (Windows)
.\venv\Scripts\activate

# Jalankan server Flask (berjalan di [http://127.0.0.1:5000](http://127.0.0.1:5000))
python run.py

```

*Dokumentasi API (Swagger) dapat diakses di:* `http://127.0.0.1:5000/apidocs`

### 2. Konfigurasi Frontend (Vue 3)

Buka terminal baru, biarkan terminal backend tetap menyala.

```bash
# Masuk ke direktori frontend
cd blog-frontend

# Instalasi dependensi
npm install

# Jalankan server pengembangan Vite
npm run dev

```

*Aplikasi frontend dapat diakses di:* `http://localhost:5173`
