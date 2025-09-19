# 🌐 Local DNS & Reverse Proxy Lab

## 📌 Deskripsi Proyek
Proyek ini mensimulasikan implementasi **DNS Server internal** dengan **Bind9** di dalam **LXD Container**, yang digunakan untuk mengelola **subdomain lokal** aplikasi-aplikasi lab:  

- `guac.labunix.biz.id` → Apache Guacamole  
- `cac01.labunix.biz.id` → Cacti Monitoring  
- `unifi.labunix.biz.id` → UniFi Controller  

Selain itu, digunakan juga **Nginx Reverse Proxy** sebagai pintu masuk untuk tiap subdomain agar layanan lebih terstruktur dan mudah diakses menggunakan protokol HTTPS.  

---

## 🏗️ Topologi Jaringan

| Komponen                          | IP Address      | Deskripsi                       |
|-----------------------------------|-----------------|---------------------------------|
| **DNS Server (Bind9) + Nginx**    | 10.105.28.250   | Authoritative & Recursive DNS    |
| **Guacamole Server**              | 10.105.28.160   | Web Remote Access (guac.labunix.biz.id) |
| **Cacti Server**                  | 10.105.28.161   | Monitoring Tool (cac01.labunix.biz.id)  |
| **Unifi Controller**              | 10.105.28.162   | Network Management (unifi.labunix.biz.id) |

📊 **Diagram Topologi**  
![Topologi Jaringan](/Image/topologi-dns-nginx.png)  

---

## 🎯 Tujuan
- ✅ Mengimplementasikan **DNS lokal** dengan Bind9  
- ✅ Mengatur **subdomain internal** untuk tiap aplikasi lab  
- ✅ Menggunakan **Nginx Reverse Proxy** sebagai front-end akses aplikasi  
- ✅ Memberikan **akses berbasis domain** alih-alih menggunakan IP:Port  
- ✅ Siap digunakan untuk lab enterprise kecil  

---

## ⚙️ Teknologi yang Digunakan
- **OS**: Debian 12 (LXD Container)  
- **DNS Server**: Bind9  
- **Reverse Proxy**: Nginx  
- **Virtualization**: Canonical LXD   

---

## 📷 Tampilan DNS & Aplikasi

| DNS Lookup | Guacamole | Cacti | UniFi |
|------------|-----------|-------|-------|
| ![DNS Lookup](/Image/dnslookup.png) | ![Guacamole](/Image/guacamole.png) | ![Cacti](/Image/cacti.png) | ![UniFi](/Image/unifi.png) |

---

## 🔧 Konfigurasi Utama

### 1️⃣ DNS Zone File (`/etc/bind/zones/db.labunix.biz.id`)
```dns
$TTL 3600
@   IN  SOA dns.labunix.biz.id. admin.labunix.biz.id. (
        2025091901 ; Serial
        3600       ; Refresh
        1800       ; Retry
        604800     ; Expire
        86400 )    ; Minimum TTL

    IN  NS  dns.labunix.biz.id.

dns     IN  A   10.105.28.250
guac    IN  A   10.105.28.160
cac01   IN  A   10.105.28.161
unifi   IN  A   10.105.28.162
```

### 2️⃣ Konfigurasi MikroTik DHCP (menyebarkan DNS internal)
```routeros
/ip dhcp-server network set [find address=192.168.1.0/24] dns-server=10.105.28.250
```

### 3️⃣ Konfigurasi Nginx Reverse Proxy
File: `/etc/nginx/sites-available/labunix.conf`
```nginx
server {
    listen 80;
    server_name guac.labunix.biz.id;

    location / {
        proxy_pass http://10.105.28.160:8080/;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
    }
}

server {
    listen 80;
    server_name cac01.labunix.biz.id;

    location / {
        proxy_pass http://10.105.28.161/;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
    }
}

server {
    listen 80;
    server_name unifi.labunix.biz.id;

    location / {
        proxy_pass https://10.105.28.162:8443/;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
    }
}
```

Aktifkan konfigurasi:
```bash
ln -s /etc/nginx/sites-available/labunix.conf /etc/nginx/sites-enabled/
nginx -t
systemctl reload nginx
```

---

## 📌 Catatan
- Semua subdomain diselesaikan oleh **Bind9** (internal DNS server)  
- **MikroTik DHCP** memastikan semua klien memakai DNS internal secara otomatis  
- **Nginx** memudahkan akses domain → IP container tanpa perlu port khusus  
- Bisa ditingkatkan dengan SSL/TLS menggunakan **Let’s Encrypt** (jika server publik) atau **Self-Signed CA** (jika lab internal)  

---

## 👤 Author
Aditya Ramadhani  
🔗 [LinkedIn](https://linkedin.com/in/username) | 📧 [Email](mailto:ramadhaniaditya19@gmail.com)  
