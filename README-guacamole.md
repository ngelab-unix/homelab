# 🚀 Instalasi Apache Guacamole di Debian 11 (LXC/LXD)

## 1. Topologi GUACAMOLE
- **Web UI**: Tomcat9 (port 8080) + guacamole.war  
- **Proxy daemon**: guacd (port 4822)  
- **Database**: MariaDB (schema Guacamole + JDBC extension)  
- **Konfigurasi**: `/etc/guacamole/`  
- **Akses web**: `http://IP:8080/guacamole`  

---

## 2. Instalasi Paket Dasar
Tambahkan repo Debian 11 (bullseye) untuk Tomcat9:  
```bash
echo "deb http://deb.debian.org/debian/ bullseye main" | sudo tee /etc/apt/sources.list.d/bullseye.list
sudo apt update
sudo apt install -y wget curl unzip \
tomcat9 tomcat9-admin mariadb-server mariadb-client \
build-essential autoconf automake libtool-bin pkg-config \
libcairo2-dev libjpeg-dev libpng-dev libossp-uuid-dev \
libavcodec-dev libavformat-dev libavutil-dev libswscale-dev \
freerdp2-dev libpango1.0-dev libssh2-1-dev libtelnet-dev \
libvncserver-dev libwebsockets-dev libpulse-dev libssl-dev \
libvorbis-dev libwebp-dev libmariadb-java
```

---

## 3. Install & Jalankan guacd

### 3.1 Unduh & kompilasi guacamole-server 1.6.0
```bash
cd /usr/src
sudo wget https://archive.apache.org/dist/guacamole/1.6.0/source/guacamole-server-1.6.0.tar.gz
sudo tar -xzf guacamole-server-1.6.0.tar.gz
cd guacamole-server-1.6.0
sudo ./configure --with-systemd-dir=/etc/systemd/system
sudo make -j$(nproc)
sudo make install
sudo ldconfig
```

### 3.2 Buat user service & unit systemd
```bash
sudo groupadd --system guacd || true
sudo useradd --system --no-create-home --shell /usr/sbin/nologin --gid guacd guacd || true
```

Jika file service belum ada, buat:
```bash
cat | sudo tee /etc/systemd/system/guacd.service >/dev/null <<'EOF'
[Unit]
Description=Guacamole proxy daemon
After=network.target

[Service]
Type=simple
User=guacd
Group=guacd
ExecStart=/usr/local/sbin/guacd -f
Restart=on-failure

[Install]
WantedBy=multi-user.target
EOF
```

### 3.3 Start guacd
```bash
sudo systemctl daemon-reload
sudo systemctl enable --now guacd
sudo systemctl status guacd --no-pager
```

---

## 4. Siapkan folder Guacamole (untuk Tomcat9)
```bash
sudo mkdir -p /etc/systemd/system/tomcat9.service.d
cat | sudo tee /etc/systemd/system/tomcat9.service.d/guacamole.conf >/dev/null <<'EOF'
[Service]
Environment=GUACAMOLE_HOME=/etc/guacamole
EOF

sudo systemctl daemon-reload
```

---

## 5. Deploy Guacamole Webapp + Extensions

### 5.1 Unduh WAR & extension
```bash
cd /tmp
wget -O guacamole-1.6.0.war https://archive.apache.org/dist/guacamole/1.6.0/binary/guacamole-1.6.0.war
wget -O guacamole-auth-jdbc-1.6.0.tar.gz https://archive.apache.org/dist/guacamole/1.6.0/binary/guacamole-auth-jdbc-1.6.0.tar.gz
wget -O guacamole-auth-totp-1.6.0.tar.gz https://archive.apache.org/dist/guacamole/1.6.0/binary/guacamole-auth-totp-1.6.0.tar.gz

tar -xzf guacamole-auth-jdbc-1.6.0.tar.gz
tar -xzf guacamole-auth-totp-1.6.0.tar.gz
```

### 5.2 Pasang WAR ke Tomcat
```bash
sudo mkdir -p /etc/guacamole/extensions
sudo cp /tmp/guacamole-1.6.0.war /var/lib/tomcat9/webapps/guacamole.war
```

### 5.3 Pasang extension JAR
```bash
# JDBC (MySQL/MariaDB)
sudo cp /tmp/guacamole-auth-jdbc-1.6.0/mysql/guacamole-auth-jdbc-mysql-1.6.0.jar /etc/guacamole/extensions/

# TOTP (2FA)
sudo cp /tmp/guacamole-auth-totp-1.6.0/guacamole-auth-totp-1.6.0.jar /etc/guacamole/extensions/
```

### 5.4 Tambahkan JDBC driver
```bash
sudo mkdir -p /etc/guacamole/lib
sudo ln -sf /usr/share/java/mariadb-java-client.jar /etc/guacamole/lib/mariadb-java-client.jar
```

---

## 6. Buat Database & Schema di MariaDB

### 6.1 Buat DB & user
```sql
mysql -u root -p
CREATE DATABASE guacamole_db;
CREATE USER 'guacamole_user'@'localhost' IDENTIFIED BY 'GuacDBpass!';
GRANT SELECT,INSERT,UPDATE,DELETE ON guacamole_db.* TO 'guacamole_user'@'localhost';
FLUSH PRIVILEGES;
EXIT;
```

### 6.2 Import schema
```bash
cd /tmp/guacamole-auth-jdbc-1.6.0/mysql/schema
for f in *.sql; do
  echo "Import $f"
  mysql -u guacamole_user -pGuacDBpass! guacamole_db < "$f"
done
```

---

## 7. Konfigurasi `guacamole.properties`
```bash
sudo tee /etc/guacamole/guacamole.properties >/dev/null <<'EOF'
# MariaDB connection
mysql-hostname: localhost
mysql-port: 3306
mysql-database: guacamole_db
mysql-username: guacamole_user
mysql-password: GuacDBpass!
mysql-ssl-mode: disabled
EOF
```

---

## 8. (Opsional) Aktifkan TOTP (2FA)
Jika JAR TOTP sudah ada di `/etc/guacamole/extensions/`, restart Tomcat:
```bash
sudo systemctl restart tomcat9
```

---

## 9. Tes & Akses Web UI
Cek service:
```bash
systemctl status guacd --no-pager
systemctl status tomcat9 --no-pager
```

Buka browser:  
`http://IP-Container:8080/guacamole`  

Login default:  
- **Username**: `guacadmin`  
- **Password**: `guacadmin`  
