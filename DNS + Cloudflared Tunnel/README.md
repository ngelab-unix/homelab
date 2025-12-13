# Local DNS & Reverse Proxy Lab + SSL/TLS

## 📌 Deskripsi Proyek
Proyek ini mensimulasikan implementasi **DNS Server internal** dengan **Bind9** di dalam LXD Container, yang digunakan untuk mengelola subdomain lokal aplikasi-aplikasi lab:

- `guac.labunix.biz.id` → Apache Guacamole  
- `cac01.labunix.biz.id` → Cacti Monitoring  
- `unifi.labunix.biz.id` → UniFi Controller  

Selain itu, digunakan juga **Nginx Reverse Proxy + SSL/TLS** sebagai pintu masuk untuk tiap subdomain agar layanan lebih terstruktur dan mudah diakses menggunakan protokol HTTPS.

---

## 🏗️ Topologi Jaringan

| Komponen                  | IP Address      | Deskripsi                                  |
|----------------------------|----------------|-------------------------------------------|
| DNS Server (Bind9) + Nginx | 10.105.28.250  | Authoritative & Recursive DNS             |
| Guacamole Server           | 10.105.28.160  | Web Remote Access (`guac.labunix.biz.id`) |
| Cacti Server               | 10.105.28.161  | Monitoring Tool (`cac01.labunix.biz.id`)  |
| UniFi Controller           | 10.105.28.162  | Network Management (`unifi.labunix.biz.id`) |

### 📊 Diagram Topologi
[ Diagram placeholder – bisa diganti dengan gambar topologi nyata ]

yaml
Copy code

---

## 🎯 Tujuan
- Mengimplementasikan **DNS lokal dengan Bind9**  
- Mengatur **subdomain internal** untuk tiap aplikasi lab  
- Menggunakan **Nginx Reverse Proxy** sebagai front-end akses aplikasi  
- Menggunakan **SSL/TLS** untuk keamanan HTTPS  
- Memberikan akses berbasis **domain** alih-alih menggunakan IP:Port  

---

## ⚙️ Teknologi yang Digunakan
- **OS**: Debian 12 (LXD Container)  
- **DNS Server**: Bind9  
- **Reverse Proxy**: Nginx  
- **Virtualization**: Canonical LXD  
- **SSL/TLS**: Let’s Encrypt atau Self-Signed CA  

---

## 📷 Tampilan Lab (Contoh)

### Tanpa Reverse Proxy
| Fitur        | Screenshot Placeholder |
|-------------|----------------------|
| DNS Lookup  | ![DNS](path/to/image.png) |
| Guacamole   | ![Guac](path/to/image.png) |
| Cacti       | ![Cacti](path/to/image.png) |
| UniFi       | ![UniFi](path/to/image.png) |
| Tracert     | ![Tracert](path/to/image.png) |

### Dengan Reverse Proxy + SSL
| Fitur        | Screenshot Placeholder |
|-------------|----------------------|
| DNS Lookup  | ![DNS](path/to/image.png) |
| Guacamole   | ![Guac](path/to/image.png) |
| Cacti       | ![Cacti](path/to/image.png) |
| UniFi       | ![UniFi](path/to/image.png) |
| Tracert     | ![Tracert](path/to/image.png) |

### DNS Eksternal & Cloudflared + SSL/TLS
| Fitur        | Screenshot Placeholder |
|-------------|----------------------|
| DNS Lookup  | ![DNS](path/to/image.png) |
| Guacamole   | ![Guac](path/to/image.png) |
| Cacti       | ![Cacti](path/to/image.png) |
| UniFi       | ![UniFi](path/to/image.png) |
| Tracert     | ![Tracert](path/to/image.png) |

🔗 contoh: `cac01.ngelab-unix.biz.id` | `zabb01.ngelab-unix.biz.id`

---

## 📌 Catatan
- Semua subdomain diselesaikan oleh **Bind9 (internal DNS server)**  
- **MikroTik DHCP** memastikan semua klien memakai DNS internal secara otomatis  
- Bisa mengatur **2 domain dalam 1 DNS** dan masing-masing domain ada subdomain  
- Nginx memudahkan akses **domain → IP container** tanpa perlu port khusus  
- Menggunakan SSL/TLS Let’s Encrypt (jika server publik) atau **Self-Signed CA**  

---

## 👤 Author
**Aditya Ramadhani**  
🔗 [LinkedIn](https://www.linkedin.com/in/aditya-ramadhani) | 📧 aditya@example.com  

---

## 📝 License (Optional)
```text
Copyright (c) 2025 Aditya Ramadhani
Portofolio ini hanya untuk tujuan demonstrasi dan evaluasi.
