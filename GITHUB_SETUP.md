# 🚀 Panduan Push ke GitHub dengan Akun Berbeda

## 📋 Langkah-Langkah

### 1️⃣ Setup Git Config untuk Repository Ini

Pertama, set username dan email untuk akun GitHub yang ingin digunakan **khusus untuk repository ini**:

```bash
cd /media/yusuf/WORK/ping_supabase/ping

# Ganti dengan username GitHub yang ingin digunakan
git config user.name "username-github-baru"

# Ganti dengan email GitHub yang ingin digunakan
git config user.email "email-github-baru@example.com"
```

> 💡 **Catatan**: Ini hanya akan mengubah config untuk repository ini saja, tidak mempengaruhi repository lain.

### 2️⃣ Buat Repository Baru di GitHub

1. Login ke akun GitHub yang ingin digunakan
2. Klik tombol **+** di pojok kanan atas → **New repository**
3. Isi:
   - **Repository name**: `ping-supabase` (atau nama lain)
   - **Description**: "Automated Supabase ping tool to prevent database shutdown"
   - **Public** atau **Private** (pilih sesuai kebutuhan)
   - **JANGAN** centang "Initialize this repository with a README"
4. Klik **Create repository**

### 3️⃣ Hubungkan Repository Lokal ke GitHub

Setelah repository dibuat, GitHub akan menampilkan instruksi. Gunakan perintah ini:

```bash
cd /media/yusuf/WORK/ping_supabase/ping

# Tambahkan semua file
git add .

# Commit dengan pesan
git commit -m "Initial commit: Multi-project Supabase ping tool"

# Ganti URL dengan repository yang baru dibuat
# Format: https://github.com/USERNAME/REPO-NAME.git
git remote add origin https://github.com/USERNAME-BARU/ping-supabase.git

# Push ke GitHub
git branch -M main
git push -u origin main
```

### 4️⃣ Autentikasi

Saat push, GitHub akan meminta autentikasi. Ada 2 cara:

#### **Cara 1: Personal Access Token (Recommended)**

1. Pergi ke GitHub → **Settings** → **Developer settings** → **Personal access tokens** → **Tokens (classic)**
2. Klik **Generate new token** → **Generate new token (classic)**
3. Isi:
   - **Note**: "Ping Supabase Tool"
   - **Expiration**: 90 days (atau sesuai kebutuhan)
   - **Scopes**: Centang **repo** (full control of private repositories)
4. Klik **Generate token**
5. **COPY TOKEN** (hanya muncul sekali!)

Saat push, masukkan:

- **Username**: username GitHub Anda
- **Password**: TOKEN yang baru di-copy (bukan password GitHub)

#### **Cara 2: SSH Key**

Jika ingin menggunakan SSH (lebih aman, tidak perlu password setiap kali):

```bash
# Generate SSH key
ssh-keygen -t ed25519 -C "email-github-baru@example.com"

# Tekan Enter untuk default location
# Bisa set passphrase atau kosongkan

# Copy public key
cat ~/.ssh/id_ed25519.pub
```

Lalu:

1. Copy output dari command di atas
2. Pergi ke GitHub → **Settings** → **SSH and GPG keys** → **New SSH key**
3. Paste key yang di-copy
4. Klik **Add SSH key**

Ubah remote URL ke SSH:

```bash
git remote set-url origin git@github.com:USERNAME-BARU/ping-supabase.git
git push -u origin main
```

---

## 🔄 Jika Ingin Ganti Akun untuk Repository Ini

### Cek Config Saat Ini

```bash
git config user.name
git config user.email
git remote -v
```

### Ganti Username & Email

```bash
git config user.name "username-baru"
git config user.email "email-baru@example.com"
```

### Ganti Remote URL

```bash
# Hapus remote lama
git remote remove origin

# Tambah remote baru
git remote add origin https://github.com/USERNAME-BARU/REPO-BARU.git
```

---

## 📝 Contoh Lengkap

Misalkan Anda ingin push ke akun GitHub `bahagiakita`:

```bash
# 1. Masuk ke directory
cd /media/yusuf/WORK/ping_supabase/ping

# 2. Set config untuk repository ini
git config user.name "bahagiakita"
git config user.email "bahagiakita@example.com"

# 3. Add dan commit
git add .
git commit -m "Initial commit: Multi-project Supabase ping tool"

# 4. Tambahkan remote (ganti dengan URL repository Anda)
git remote add origin https://github.com/bahagiakita/ping-supabase.git

# 5. Push
git branch -M main
git push -u origin main
```

Saat diminta password, masukkan **Personal Access Token**, bukan password GitHub.

---

## ❓ Troubleshooting

### "remote origin already exists"

```bash
git remote remove origin
git remote add origin https://github.com/USERNAME/REPO.git
```

### "Authentication failed"

- Pastikan menggunakan **Personal Access Token**, bukan password
- Pastikan token memiliki scope **repo**

### "Permission denied (publickey)"

- Pastikan SSH key sudah ditambahkan ke GitHub
- Test koneksi: `ssh -T git@github.com`

### Ingin menggunakan akun berbeda untuk repository berbeda

Gunakan `git config` (tanpa `--global`) di setiap repository untuk set username/email yang berbeda.

---

## 💡 Tips

1. **Personal Access Token** lebih mudah untuk pemula
2. **SSH Key** lebih praktis untuk jangka panjang (tidak perlu input password)
3. Simpan Personal Access Token di tempat aman (password manager)
4. Bisa menggunakan akun berbeda untuk repository berbeda dengan `git config` lokal
5. Untuk private repository, pastikan menggunakan akun yang memiliki akses

---

## ✅ Verifikasi

Setelah push berhasil:

1. Buka repository di GitHub
2. Refresh halaman
3. Semua file seharusnya sudah ada
4. Pergi ke tab **Actions** untuk setup secrets
