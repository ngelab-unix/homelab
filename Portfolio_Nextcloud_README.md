# 📁 Nextcloud Deployment & Management  
### **Portfolio Project — by mrtg**

---

## 🚀 Overview  
Project ini mendeskripsikan proses lengkap instalasi, konfigurasi, dan manajemen Nextcloud sebagai solusi private cloud storage untuk kebutuhan personal maupun organisasi.  
Dokumen ini dapat digunakan sebagai portofolio profesional untuk menunjukkan kemampuan Anda dalam:

- Sistem Linux Administration  
- Deployment Nextcloud  
- Manajemen user & keamanan  
- Reset password via email  
- Automasi & monitoring  
- Struktur server modern (LXD/VM/Baremetal)

---

## 🏗️ Infrastruktur Proyek  
### **1. Platform Server**
- Ubuntu Server (LTS)
- LXD Container untuk pemisahan aplikasi
- Reverse proxy (opsional)
- Database: MariaDB / PostgreSQL
- Web: Apache atau Nginx

### **2. Komponen Utama**
- Nextcloud 29+
- PHP-FPM 8.x
- Redis untuk file locking
- SMTP Email untuk notifikasi & reset password

---

## 🔧 Instalasi Nextcloud  
### **Step 1 — Update Server**
```bash
sudo apt update && sudo apt upgrade -y
```

### **Step 2 — Install Dependencies**
```bash
sudo apt install apache2 mariadb-server php php-fpm php-mysql php-zip php-xml php-mbstring php-gd php-curl php-intl php-bz2 php-imagick php-gmp redis-server -y
```

### **Step 3 — Install Nextcloud**
```bash
wget https://download.nextcloud.com/server/releases/latest.zip
unzip latest.zip
sudo mv nextcloud /var/www/
sudo chown -R www-data:www-data /var/www/nextcloud
```

---

## 🛠️ Konfigurasi User Nextcloud  
### ➤ Buat user admin pertama  
Dilakukan via web installer pada pertama kali login.

### ➤ Tambah user baru  
1. Login sebagai admin  
2. Masuk menu **Users**  
3. Klik **New User**  
4. Tentukan password, grup, dan quota

---

## ✉️ Reset Password via Email  
### Step 1 — Konfigurasi SMTP Nextcloud  
Masuk menu:  
**Settings → Basic Settings → Email Server**

Contoh SMTP Gmail:
```
Encryption: TLS
From Address: cloud@domainkamu.com
SMTP Server: smtp.gmail.com
Port: 587
Authentikasi: Ya
Username: cloud@domainkamu.com
Password: app password (bukan password Gmail akun)
```

### Step 2 — User reset password  
1. Masuk halaman login  
2. Klik **Forgot Password**  
3. Nextcloud mengirim token ke email user  
4. User klik link dan membuat password baru

---

## 🔐 Keamanan  
- Enforce HTTPS  
- HSTS Enabled  
- Password Policy  
- Rate Limit login  
- 2FA support (TOTP / WebAuthn)  
- Redis untuk file locking & performance  

---

## 🔍 Monitoring  
Integrasi dengan:
- Grafana  
- Prometheus exporter  
- Fail2ban (brute-force protection)  

---

## 📦 Backup
### Full backup:
- `/var/www/nextcloud`
- Database `nextcloud`
- Folder data (default: `/var/www/nextcloud/data`)

### Restore:
- Restore file  
- Import database  
- Perbaiki permission:
```bash
sudo chown -R www-data:www-data /var/www/nextcloud
```

---

## 📄 Status Proyek  
| Komponen | Status |
|---------|--------|
| Instalasi Nextcloud | ✔️ Selesai |
| Konfigurasi User | ✔️ Selesai |
| Reset Password via Email | ✔️ Selesai |
| SMTP Deployment | ✔️ Selesai |
| Dokumentasi | ✔️ Selesai |

---

## 🧑‍💻 Skill yang Ditunjukkan  
- Linux Server Management  
- Web Security  
- SMTP Integration  
- PHP + Apache/Nginx Configuration  
- Backup Strategy  
- LXD Containerization  
- System Hardening  
- Full Documentation Writing  

---

## 📬 Contact  
Jika ingin melihat demo, repo project, atau environment server:  
**Email:** mrtg@example.com *(ganti sesuai kebutuhan)*  
**Website:** https://srvlab.my.id *(opsional)*  

---

> **README ini bisa langsung digunakan sebagai portofolio DevOps/System Administrator.  
Jika ingin versi PDF, markdown premium, atau versi English — tinggal bilang!**

