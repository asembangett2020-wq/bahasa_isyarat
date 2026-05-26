# 🤟 BISINDO Detector

Aplikasi web deteksi **Bahasa Isyarat Indonesia (BISINDO)** secara real-time menggunakan kamera dan model ONNX langsung di browser — tanpa server, tanpa backend!

---

## 📂 Struktur File

```
bisindo-detector/
├── index.html      ← Aplikasi utama (HTML + CSS + JS)
└── best.onnx       ← Model deteksi BISINDO (letakkan di sini!)
```

> ⚠️ **Penting:** File `best.onnx` harus berada di **folder yang sama** dengan `index.html`.

---

## 🚀 Cara Deploy / Menjalankan

### Opsi 1 — Local Server (Paling Mudah)

Browser modern memblokir pemuatan file `.onnx` via `file://` karena CORS.  
Gunakan salah satu server lokal berikut:

#### Python (sudah terinstall di hampir semua OS)

```bash
# Python 3
cd bisindo-detector
python -m http.server 8080

# Buka di browser
http://localhost:8080
```

#### Node.js / npx

```bash
cd bisindo-detector
npx serve .

# Buka di browser
http://localhost:3000
```

#### VS Code — Live Server Extension

1. Install ekstensi **Live Server** di VS Code
2. Klik kanan `index.html` → **"Open with Live Server"**
3. Browser otomatis terbuka ✅

---

### Opsi 2 — GitHub Pages (Gratis, Online)

1. Buat repository baru di GitHub (Public)
2. Upload `index.html` dan `best.onnx` ke repository
3. Buka **Settings → Pages → Deploy from branch: `main` / `root`**
4. Tunggu beberapa menit → web tersedia di:
   ```
   https://<username>.github.io/<repo-name>/
   ```

> ⚠️ Pastikan `best.onnx` terupload ke GitHub. File besar (>100MB) perlu [Git LFS](https://git-lfs.com/).

---

### Opsi 3 — Netlify (Drag & Drop)

1. Buka [netlify.com](https://netlify.com) → Login
2. Drag & drop **folder** `bisindo-detector/` ke dashboard Netlify
3. Selesai! URL langsung aktif 🎉

---

### Opsi 4 — Vercel

```bash
npm install -g vercel
cd bisindo-detector
vercel

# Ikuti instruksi, web akan live di
# https://bisindo-detector-xxxx.vercel.app
```

---

## 🎮 Cara Menggunakan

1. **Buka** aplikasi di browser
2. **Tunggu** status berubah menjadi ✅ "Model siap!"
3. **Klik** "▶ Mulai Kamera" dan izinkan akses kamera
4. **Tunjukkan** isyarat tangan ke kamera — deteksi berjalan real-time!
5. **Klik** "📸 Tangkap" atau "➕ Tambah Huruf" untuk menyusun kalimat
6. **Salin** hasilnya dengan tombol "📋 Salin"

---

## 🔧 Konfigurasi Model (Opsional)

Jika model kamu memiliki nama input/output yang berbeda, edit di `index.html`:

```js
// Baris ~170 — nama input otomatis diambil dari model
const inputName = session.inputNames[0];

// Ukuran input gambar (default: 224x224)
const INPUT_SIZE = 224;

// Daftar kelas — sesuaikan urutan dengan training kamu
const CLASSES = [
  'A','B','C','D','E','F','G','H','I','J',
  'K','L','M','N','O','P','Q','R','S','T',
  'U','V','W','X','Y','Z'
];
```

---

## 🧠 Preprocessing

Model menerima input:
- **Shape:** `[1, 3, 224, 224]` (batch, channel, height, width)
- **Format:** Float32, normalized ImageNet
  - Mean: `[0.485, 0.456, 0.406]`
  - Std:  `[0.229, 0.224, 0.225]`

Jika model kamu menggunakan preprocessing berbeda, sesuaikan fungsi `preprocessImage()` di `index.html`.

---

## 🌐 Browser yang Didukung

| Browser | Status |
|---------|--------|
| Chrome 90+ | ✅ Direkomendasikan |
| Firefox 90+ | ✅ |
| Edge 90+ | ✅ |
| Safari 15+ | ✅ |
| Mobile Chrome | ✅ |
| Mobile Safari | ⚠️ Terbatas |

---

## 📦 Dependencies

Semua dimuat via CDN — tidak perlu install apapun:

- **[ONNX Runtime Web](https://onnxruntime.ai/)** `v1.x` — inference model di browser
- **[Google Fonts](https://fonts.google.com/)** — Fredoka One + Nunito

---

## ❓ Troubleshooting

| Masalah | Solusi |
|---------|--------|
| "Gagal memuat model" | Pastikan `best.onnx` ada di folder yang sama & jalankan via server lokal |
| Kamera tidak muncul | Izinkan akses kamera di browser; gunakan HTTPS atau localhost |
| Deteksi lambat | Tutup tab lain; model berjalan di CPU (WebAssembly) |
| Model error shape | Sesuaikan `INPUT_SIZE` dan `CLASSES` dengan konfigurasi training |
| GitHub Pages lambat | File onnx besar diakses per-request; pertimbangkan CDN |

---

## 📄 Lisensi

MIT License — bebas digunakan, dimodifikasi, dan didistribusikan.

---

*Dibuat dengan 💜 untuk mendukung komunikasi inklusif di Indonesia*
