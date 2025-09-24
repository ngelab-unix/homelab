# 🌐 Local DNS & Reverse Proxy Lab + SSL/TLS

## 📌 Deskripsi Proyek
Proyek ini mensimulasikan implementasi **DNS Server internal** dengan **Bind9** di dalam **LXD Container**, yang digunakan untuk mengelola **subdomain lokal** aplikasi-aplikasi lab:  

- `guac.labunix.biz.id` → Apache Guacamole  
- `cac01.labunix.biz.id` → Cacti Monitoring  
- `unifi.labunix.biz.id` → UniFi Controller  

Selain itu, digunakan juga **Nginx Reverse Proxy + SSL/TLS** sebagai pintu masuk untuk tiap subdomain agar layanan lebih terstruktur dan mudah diakses menggunakan protokol HTTPS.  

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
- ✅ Menggunakan **SSL/TLS** sebagai keamanan https  
- ✅ Memberikan **akses berbasis domain** alih-alih menggunakan IP:Port  
- ✅ Siap digunakan untuk lab enterprise kecil  

---

## ⚙️ Teknologi yang Digunakan
- **OS**: Debian 12 (LXD Container)  
- **DNS Server**: Bind9  
- **Reverse Proxy**: Nginx  
- **Virtualization**: Canonical LXD   

---

## 📷 Tampilan DNS Tanpa Reverse Proxy 

| DNS Lookup | Guacamole | Cacti | UniFi |
|------------|-----------|-------|-------|
| ![DNS Lookup](/Image/dnslookup.png) | ![Guacamole](/Image/guacamole.png) | ![Cacti](/Image/cacti.png) | ![UniFi](/Image/unifi.png) |

---
## 📷 Tampilan DNS Dengan Reverse Proxy + SSL  

| DNS Lookup | Guacamole | Cacti | UniFi |
|------------|-----------|-------|-------|
| ![DNS Lookup](/Image/dnslookup.png) | ![Guacamole](/Image/guacamole.png) | ![Cacti](/Image/cacti.png) | ![UniFi](/Image/unifi.png) |

---

## 📌 Catatan
- Semua subdomain diselesaikan oleh **Bind9** (internal DNS server)  
- **MikroTik DHCP** memastikan semua klien memakai DNS internal secara otomatis  
- **Nginx** memudahkan akses domain → IP container tanpa perlu port khusus  
- Menggunakan SSL/TLS **Let’s Encrypt** (jika server publik) atau **Self-Signed CA**  

---

## 👤 Author
Aditya Ramadhani  
🔗 [LinkedIn](https://linkedin.com/in/username) | 📧 [Email](mailto:ramadhaniaditya19@gmail.com)  
