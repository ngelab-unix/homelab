# Panduan Instalasi Nextcloud & Konfigurasi User

Dokumen ini memberikan langkah-langkah instalasi Nextcloud, cara membuat pengguna, serta konfigurasi reset password melalui email.

---

## 1. **Instalasi Nextcloud (Ubuntu Server)**

### 1.1 Update sistem
```bash
sudo apt update && sudo apt upgrade -y
```

### 1.2 Instal dependency
```bash
sudo apt install apache2 mariadb-server libapache2-mod-php php php-mysql php-xml php-gd php-curl php-zip php-mbstring php-intl php-bz2 php-imagick php-gmp -y
```

### 1.3 Download Nextcloud
```bash
cd /var/www/
sudo wget https://download.nextcloud.com/server/releases/latest.zip
sudo unzip latest.zip
sudo chown -R www-data:www-data nextcloud
```

### 1.4 Konfigurasi Database
```bash
sudo mysql -u root -p
```

Di dalam MariaDB:
```sql
CREATE DATABASE nextcloud;
CREATE USER 'ncuser'@'localhost' IDENTIFIED BY 'passwordku123';
GRANT ALL PRIVILEGES ON nextcloud.* TO 'ncuser'@'localhost';
FLUSH PRIVILEGES;
EXIT;
```

### 1.5 Konfigurasi Apache
```bash
sudo nano /etc/apache2/sites-available/nextcloud.conf
```

Isi:
```
<VirtualHost *:80>
    DocumentRoot /var/www/nextcloud/
    ServerName nextcloud.example.com

    <Directory /var/www/nextcloud/>
        Require all granted
        AllowOverride All
    </Directory>
</VirtualHost>
```

Aktifkan:
```bash
sudo a2ensite nextcloud
sudo a2enmod rewrite headers env dir mime
sudo systemctl restart apache2
```

### 1.6 Akses
Buka browser:
```
http://IP-SERVER/nextcloud
```

---

## 2. **Konfigurasi User Nextcloud**

### 2.1 Menambah user
Admin → **Users** → **New user**

### 2.2 Menghapus user
Admin → **Users** → Delete

### 2.3 Reset password manual oleh admin
Admin → **Users** → Set new password

---

## 3. **Reset Password Via Email**

### 3.1 Konfigurasi SMTP
Settings → Basic settings → Email server

Contoh SMTP Gmail:
```
Send mode: SMTP
Encryption: SSL/TLS
SMTP server: smtp.gmail.com:465
Username: email@gmail.com
Password: password aplikasi
```

---

## 4. **User Reset Password**
1. Klik *Forgot Password*  
2. Masukkan email  
3. Terima link reset  
4. Buat password baru

---

## 5. **Troubleshooting**
### Email tidak terkirim:
- Cek port 465/587  
- Periksa firewall  
- Gunakan password aplikasi

### Reset password admin:
```bash
sudo -u www-data php /var/www/nextcloud/occ user:resetpassword admin
```

