# 🚀 Quick Setup Guide

Panduan cepat untuk setup Supabase Ping Tool dengan jumlah project yang berbeda.

## 📋 Langkah Setup

### 1️⃣ Untuk 1 Project Saja

Edit `.github/workflows/ping-supabase.yml`:

```yaml
strategy:
  matrix:
    project:
      - name: "My Project"
        url_secret: "SUPABASE_URL"
        key_secret: "SUPABASE_ANON_KEY"
```

**GitHub Secrets yang dibutuhkan:**

- `SUPABASE_URL`
- `SUPABASE_ANON_KEY`

---

### 2️⃣ Untuk 2 Projects

Edit `.github/workflows/ping-supabase.yml`:

```yaml
strategy:
  matrix:
    project:
      - name: "Production"
        url_secret: "SUPABASE_URL_PROD"
        key_secret: "SUPABASE_ANON_KEY_PROD"

      - name: "Staging"
        url_secret: "SUPABASE_URL_STAGING"
        key_secret: "SUPABASE_ANON_KEY_STAGING"
```

**GitHub Secrets yang dibutuhkan:**

- `SUPABASE_URL_PROD` + `SUPABASE_ANON_KEY_PROD`
- `SUPABASE_URL_STAGING` + `SUPABASE_ANON_KEY_STAGING`

---

### 3️⃣ Untuk 3+ Projects

Edit `.github/workflows/ping-supabase.yml`:

```yaml
strategy:
  matrix:
    project:
      - name: "Production"
        url_secret: "SUPABASE_URL_PROD"
        key_secret: "SUPABASE_ANON_KEY_PROD"

      - name: "Staging"
        url_secret: "SUPABASE_URL_STAGING"
        key_secret: "SUPABASE_ANON_KEY_STAGING"

      - name: "Development"
        url_secret: "SUPABASE_URL_DEV"
        key_secret: "SUPABASE_ANON_KEY_DEV"

      # Tambahkan project lain dengan format yang sama
```

**GitHub Secrets yang dibutuhkan:**

- Untuk setiap project, tambahkan 2 secrets (URL + ANON_KEY)

---

## 🔑 Cara Menambahkan GitHub Secrets

1. Buka repository di GitHub
2. Pergi ke **Settings** → **Secrets and variables** → **Actions**
3. Klik **New repository secret**
4. Tambahkan secret dengan nama yang **persis sama** dengan yang ada di workflow

### Contoh:

- **Name**: `SUPABASE_URL_PROD`
- **Value**: `https://xxxxx.supabase.co`

Ulangi untuk setiap secret yang dibutuhkan.

---

## 📍 Mendapatkan Supabase Credentials

1. Buka [Supabase Dashboard](https://app.supabase.com)
2. Pilih project Anda
3. Pergi ke **Settings** → **API**
4. Copy:
   - **Project URL** → untuk `SUPABASE_URL_X`
   - **anon/public key** → untuk `SUPABASE_ANON_KEY_X`

---

## ✅ Test Workflow

Setelah setup:

1. Push changes ke GitHub
2. Pergi ke tab **Actions**
3. Pilih workflow "Ping Multiple Supabase Projects"
4. Klik **Run workflow** untuk test manual
5. Lihat hasilnya - seharusnya ada job untuk setiap project

---

## 💡 Tips

- **Nama project** bisa apa saja (contoh: "Production", "My App", "Client DB")
- **Nama secret** harus unik dan konsisten
- Gunakan naming convention yang jelas (contoh: `_PROD`, `_STAGING`, `_DEV`)
- Test manual setelah menambah project baru
- Workflow akan otomatis skip project yang tidak memiliki secrets

---

## ❓ Troubleshooting

### "Secret tidak ditemukan"

- Pastikan nama secret di GitHub **persis sama** dengan di workflow
- Nama secret case-sensitive (huruf besar/kecil harus sama)

### "Workflow tidak berjalan"

- Pastikan GitHub Actions sudah diaktifkan
- Untuk private repo, pastikan ada GitHub Actions minutes tersisa

### "Ping gagal untuk project tertentu"

- Cek apakah URL dan key sudah benar
- Pastikan Supabase project masih aktif
- Lihat log detail di tab Actions
