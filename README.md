# Supabase Multi-Project Ping Tool

Tools otomatis untuk melakukan ping ke **beberapa project Supabase** sekaligus agar tidak shutdown karena inaktivitas.

## ✨ Fitur

- 🔄 Ping otomatis ke multiple Supabase projects
- ⏰ Jadwal yang dapat dikustomisasi
- 🚀 Berjalan parallel untuk efisiensi
- 📊 Log terpisah untuk setiap project
- ⚡ Gratis menggunakan GitHub Actions

## 🚀 Cara Setup

### 1. Konfigurasi Projects

Edit file `.github/workflows/ping-supabase.yml` untuk menambah/mengurangi project:

```yaml
strategy:
  matrix:
    project:
      - name: "Project 1"
        url_secret: "SUPABASE_URL_1"
        key_secret: "SUPABASE_ANON_KEY_1"
      - name: "Project 2"
        url_secret: "SUPABASE_URL_2"
        key_secret: "SUPABASE_ANON_KEY_2"
      # Tambahkan project lain di sini
```

**Contoh untuk 5 projects:**

```yaml
- name: "Production DB"
  url_secret: "SUPABASE_URL_PROD"
  key_secret: "SUPABASE_ANON_KEY_PROD"
- name: "Staging DB"
  url_secret: "SUPABASE_URL_STAGING"
  key_secret: "SUPABASE_ANON_KEY_STAGING"
- name: "Development DB"
  url_secret: "SUPABASE_URL_DEV"
  key_secret: "SUPABASE_ANON_KEY_DEV"
- name: "Testing DB"
  url_secret: "SUPABASE_URL_TEST"
  key_secret: "SUPABASE_ANON_KEY_TEST"
- name: "Demo DB"
  url_secret: "SUPABASE_URL_DEMO"
  key_secret: "SUPABASE_ANON_KEY_DEMO"
```

### 2. Setup GitHub Secrets

Tambahkan secrets untuk **setiap project** di repository GitHub Anda:

1. Buka repository di GitHub
2. Pergi ke **Settings** → **Secrets and variables** → **Actions**
3. Klik **New repository secret**
4. Tambahkan secrets sesuai dengan nama yang didefinisikan di workflow

**Contoh untuk 3 projects:**

| Secret Name           | Value                       |
| --------------------- | --------------------------- |
| `SUPABASE_URL_1`      | `https://xxxxx.supabase.co` |
| `SUPABASE_ANON_KEY_1` | `eyJhbGc...`                |
| `SUPABASE_URL_2`      | `https://yyyyy.supabase.co` |
| `SUPABASE_ANON_KEY_2` | `eyJhbGc...`                |
| `SUPABASE_URL_3`      | `https://zzzzz.supabase.co` |
| `SUPABASE_ANON_KEY_3` | `eyJhbGc...`                |

> 💡 **Cara mendapatkan credentials:**
>
> 1. Buka [Supabase Dashboard](https://app.supabase.com)
> 2. Pilih project Anda
> 3. Pergi ke **Settings** → **API**
> 4. Copy **Project URL** dan **anon/public key**

### 2. Aktifkan GitHub Actions

1. Push repository ini ke GitHub
2. Pergi ke tab **Actions** di repository
3. Jika diminta, klik **Enable GitHub Actions**
4. Workflow akan berjalan otomatis sesuai jadwal

## ⏰ Jadwal Ping

GitHub Action akan melakukan ping:

- **Otomatis**: Setiap 3 hari sekali pada jam 00:00 UTC
- **Manual**: Bisa trigger manual melalui tab Actions → Ping Supabase → Run workflow

## 📊 Monitoring

Untuk melihat hasil ping:

1. Buka tab **Actions** di repository
2. Klik workflow run yang ingin dilihat
3. Anda akan melihat job terpisah untuk setiap project (misalnya: "Ping Project 1", "Ping Project 2")
4. Klik job untuk melihat log detail ping project tersebut

> ✅ Setiap project akan di-ping secara **parallel** untuk efisiensi waktu

## 🔧 Kustomisasi

### Mengubah Frekuensi Ping

Edit file `.github/workflows/ping-supabase.yml`:

```yaml
schedule:
  # Setiap 3 jam
  - cron: "0 */3 * * *"

  # Setiap 12 jam
  - cron: "0 */12 * * *"

  # Setiap hari jam 00:00 UTC
  - cron: "0 0 * * *"
```

> 📖 Referensi cron syntax: [Crontab Guru](https://crontab.guru)

## ❓ Troubleshooting

### Workflow tidak berjalan

- Pastikan repository adalah **public** atau Anda memiliki GitHub Actions minutes untuk private repo
- Pastikan GitHub Actions sudah diaktifkan di repository settings

### Ping gagal untuk semua projects

- Periksa apakah secrets sudah ditambahkan dengan nama yang benar
- Pastikan format nama secret sesuai dengan yang didefinisikan di workflow
- Cek log di tab Actions untuk detail error

### Ping gagal untuk project tertentu

- Periksa apakah `SUPABASE_URL_X` dan `SUPABASE_ANON_KEY_X` sudah benar untuk project tersebut
- Pastikan Supabase project masih aktif
- Project lain akan tetap di-ping meskipun ada yang gagal (fail-fast: false)

### Secret tidak ditemukan

- Pastikan nama secret di GitHub Secrets **persis sama** dengan yang didefinisikan di workflow
- Nama secret bersifat case-sensitive (huruf besar/kecil harus sama)
- Jika project tidak memiliki secret, workflow akan skip dengan warning

## 📝 Catatan

- GitHub Actions gratis untuk public repositories
- Untuk private repositories, ada limit monthly minutes (2000 menit/bulan untuk free tier)
- Setiap ping hanya memakan waktu beberapa detik
- **Parallel execution**: Semua projects di-ping secara bersamaan untuk efisiensi
- **Fail-safe**: Jika satu project gagal, project lain tetap akan di-ping
- Anda bisa menambah/mengurangi project kapan saja dengan edit workflow file

## 📄 License

MIT
