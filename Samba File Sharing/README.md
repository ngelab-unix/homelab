# 📂 Samba File Server – Multi Divisi & User Private Lab

## 📌 Deskripsi Proyek
Proyek ini mensimulasikan **file server berbasis Samba** pada lingkungan **LXD Canonical**.  
Struktur dibangun untuk mendukung **folder bersama per divisi** sekaligus **folder privat per user**.  

Dengan desain ini:
- Divisi (HR, IT, Marketing, Finance) memiliki folder bersama.
- Setiap user dalam divisi memiliki folder pribadi yang tidak bisa diakses user lain.
- Tersedia folder **Public** yang bisa diakses semua divisi.

---

## 🏗️ Topologi Jaringan

| Komponen             | IP Address     | Deskripsi                          |
|----------------------|---------------|------------------------------------|
| **Mikrotik Router**  | 192.168.1.1   | Gateway & DHCP Server              |
| **Laptop/PC Client** | 192.168.1.251 | Akses user ke file server          |
| **LXD Host**         | 192.168.1.250 | Canonical LXD Hypervisor           |
| **lxbr0**            | 10.105.28.1   | Bridge network isolation           |
| **Samba Server**     | 10.105.28.105 | File server untuk multi divisi     |

📊 **Diagram Topologi**  
Samba berjalan di dalam **LXC container** dengan network bridge `lxbr0` yang terhubung ke LAN melalui Mikrotik.  

---

## 🎯 Tujuan
- ✅ Membuat **file server per divisi** (HR, IT, Marketing, Finance).  
- ✅ Memberikan **akses private per user** di dalam divisi.  
- ✅ Menyediakan **folder public** untuk semua divisi.  
- ✅ Mengisolasi server menggunakan **LXD container**.  

---

## ⚙️ Teknologi yang Digunakan
- **OS**: Debian 12 (LXD Container)  
- **File Sharing**: Samba (SMB/CIFS)  
- **Virtualization**: Canonical LXD  
- **Network**: Mikrotik + lxbr0 bridge  

---

## 📂 Struktur Folder

---

## 📌 Catatan
- Folder **divisi** hanya bisa diakses anggota divisi.  
- Folder **user** hanya bisa diakses user tersebut + admin.  
- Folder **public** terbuka untuk semua user.  
- Pengaturan hak akses menggunakan kombinasi **group** dan **chmod**.  

---

## 👤 Author
Aditya Ramadhani  
🔗 [LinkedIn](https://linkedin.com/in/username) | 📧 [Email](mailto:ramadhaniaditya19@gmail.com)  
