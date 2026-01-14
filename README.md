# 🔄 Supabase Ping Tool - Panduan Mudah

Tool otomatis untuk ping Supabase agar database tidak shutdown karena inaktivitas.

---

## 🎯 Apa yang Dilakukan Tool Ini?

Tool ini akan **ping database Supabase Anda secara otomatis setiap 3 hari** menggunakan GitHub Actions (gratis!).

---

## � Setup - Ikuti Langkah Ini

### **STEP 1: Dapatkan Supabase Credentials**

1. Buka [Supabase Dashboard](https://app.supabase.com)
2. Pilih project Anda
3. Klik **Settings** (⚙️) di sidebar kiri
4. Klik **API**
5. Copy 2 hal ini:
   - **Project URL** (contoh: `https://xxxxx.supabase.co`)
   - **anon public** key (yang panjang, dimulai dengan `eyJh...`)

**Simpan di notepad sementara!**

---

### **STEP 2: Push Repository ke GitHub**

```bash
# Di folder ini
git add .
git commit -m "Setup Supabase ping tool"
git push origin main
```

---

### **STEP 3: Tambahkan Secrets di GitHub**

1. Buka repository Anda di GitHub
2. Klik **Settings** (tab paling kanan)
3. Di sidebar kiri, klik **Secrets and variables** → **Actions**
4. Klik **New repository secret**

**Tambahkan 2 secrets:**

**Secret 1:**

- Name: `SUPABASE_URL_1`
- Value: Paste **Project URL** dari Step 1

**Secret 2:**

- Name: `SUPABASE_ANON_KEY_1`
- Value: Paste **anon public key** dari Step 1

---

### **STEP 4: Aktifkan GitHub Actions**

1. Klik tab **Actions** di repository
2. Jika ada tombol **"I understand my workflows, go ahead and enable them"**, klik tombol itu
3. Selesai! ✅

---

## ✅ Verifikasi

### Test Manual (Opsional)

1. Pergi ke tab **Actions**
2. Klik **Ping Multiple Supabase Projects** di sidebar kiri
3. Klik **Run workflow** → **Run workflow**
4. Tunggu beberapa detik
5. Klik workflow run yang muncul
6. Klik **Ping Project 1**
7. Lihat log - seharusnya ada ✅ **Ping berhasil!**

---

## 🎯 Selesai!

Tool akan otomatis ping Supabase Anda **setiap 3 hari** pada jam 00:00 UTC.

Anda tidak perlu melakukan apa-apa lagi! 🎉

---

## 🔧 Untuk Ping Lebih dari 1 Project

Jika Anda punya beberapa project Supabase:

### 1. Edit File Workflow

Buka file `.github/workflows/ping-supabase.yml`

Uncomment (hapus `#`) bagian Project 2 atau 3:

```yaml
# Uncomment jika ada project ke-2
- name: "Project 2"
  url_secret: "SUPABASE_URL_2"
  key_secret: "SUPABASE_ANON_KEY_2"
```

Menjadi:

```yaml
- name: "Project 2"
  url_secret: "SUPABASE_URL_2"
  key_secret: "SUPABASE_ANON_KEY_2"
```

### 2. Tambahkan Secrets untuk Project 2

Di GitHub Secrets, tambahkan:

- `SUPABASE_URL_2` → URL project ke-2
- `SUPABASE_ANON_KEY_2` → Key project ke-2

### 3. Push Changes

```bash
git add .
git commit -m "Add project 2"
git push
```

Selesai! Sekarang 2 project akan di-ping.

---

## ❓ Troubleshooting

### "Workflow tidak berjalan"

- Pastikan repository **public** (atau punya GitHub Actions minutes untuk private repo)
- Pastikan GitHub Actions sudah diaktifkan

### "Ping gagal"

- Cek apakah URL dan key sudah benar
- Pastikan nama secret **persis sama**: `SUPABASE_URL_1` dan `SUPABASE_ANON_KEY_1`
- Lihat log di tab Actions untuk detail error

### "Secret tidak ditemukan"

- Nama secret harus **persis sama** (huruf besar/kecil harus sama)
- Cek lagi di Settings → Secrets and variables → Actions

---

## 📝 Info Tambahan

- **Jadwal**: Setiap 3 hari sekali
- **Gratis**: GitHub Actions gratis untuk public repository
- **Parallel**: Jika ada banyak project, semua di-ping bersamaan
- **Fail-safe**: Jika 1 project gagal, yang lain tetap jalan

---

**Itu saja! Simple kan?** �
