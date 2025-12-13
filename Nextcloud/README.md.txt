# Nextcloud Private Cloud Lab

## 📌 Deskripsi Proyek
Proyek ini mensimulasikan **private cloud storage** menggunakan Nextcloud di atas lingkungan **LXD Canonical**.  
Tujuannya adalah memberikan solusi **file sharing, collaboration, dan backup** yang aman, mudah diakses, dan dapat diadaptasi ke lingkungan produksi.

---

## 🏗️ Topologi Jaringan

| Komponen        | IP Address        | Deskripsi                              |
|-----------------|-----------------|---------------------------------------|
| LXD Host        | 192.168.1.xx     | Canonical LXD Hypervisor              |
| Nextcloud       | 10.105.28.98     | Nextcloud Instance                     |
| Database Server | 10.105.28.100    | MariaDB/PostgreSQL (Nextcloud DB)      |
| DNS             | 10.105.28.160    | Local DNS + Nginx reverse proxy        |
| Client PC       | 192.168.1.50     | Untuk akses web / sync Nextcloud       |

### 📊 Diagram Topologi
[ Diagram placeholder – bisa diganti dengan gambar topologi Nextcloud ]

yaml
Copy code

---

## 🎯 Tujuan
- File sharing dan kolaborasi tim via browser / desktop client  
- User management dengan grup dan hak akses terkontrol  
- SSL/TLS untuk koneksi aman  
- Integrasi email untuk notifikasi dan reset password  
- Backup dan restore data Nextcloud  
- Isolasi environment menggunakan Canonical LXD  

---

## 📷 Tampilan Lab 
| Fitur             | Screenshot Placeholder |
|------------------|---------------------|
| Login Page        | ![Login](path/to/image.png) |
| Dashboard         | ![Dashboard](path/to/image.png) |
| File Upload       | ![Upload](path/to/image.png) |
| Sharing           | ![Sharing](path/to/image.png) |
| Sync Client       | ![Sync](path/to/image.png) |

> Screenshots bersifat ilustrasi, menggunakan lingkungan lab lokal.

---

## ⚙️ Teknologi yang Digunakan
- **OS**: Debian 12 (LXD Container)  
- **Cloud Storage**: Nextcloud  
- **Database**: MariaDB/PostgreSQL  
- **Web Server**: apache + PHP-FPM  
- **Virtualization**: Canonical LXD  
- **SSL/TLS**: Optional via Let's Encrypt / self-signed  

---

## 📌 Catatan
- Tested on Debian 12 LXD Canonical container  
- Dapat diadaptasi untuk production server (VM / baremetal)  
- Semua IP bersifat placeholder / lab environment  

---

## 👤 Author
**Aditya Ramadhani**  
🔗 [LinkedIn](https://www.linkedin.com/in/aditya-ramadhani) | 📧 aditya@example.com  

---

## 📝 License (Optional)
```text
Copyright (c) 2025 Aditya Ramadhani
Portofolio ini hanya untuk tujuan demonstrasi dan evaluasi.

