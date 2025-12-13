# Secure Remote Office Access Lab with Apache Guacamole

## 📌 Deskripsi Proyek
Proyek ini mensimulasikan **akses remote kantor yang aman** menggunakan Apache Guacamole dengan Two-Factor Authentication (TOTP) di atas lingkungan **LXD Canonical**.  
Tujuan utama adalah memberikan solusi remote desktop/web access yang mudah, aman, dan dapat diadaptasi ke lingkungan produksi.

---

## 🏗️ Topologi Jaringan

| Komponen         | IP Address        | Deskripsi                               |
|-----------------|-----------------|----------------------------------------|
| LXD Host         | 192.168.1.xx     | Canonical LXD Hypervisor               |
| Apache Guacamole | 10.105.28.160    | Web-based Remote Access                 |
| PC Remote Access | 10.105.28.170    | Client RDP/SSH/VNC                      |
| DNS guaca.ngelab-unix.biz.id | 10.105.28.160 | DNS local Guacamole + Nginx         |

### 📊 Diagram Topologi
[ Diagram placeholder – bisa diganti gambar topologi sebenarnya ]

yaml
Copy code

---

## 🎯 Tujuan
- Remote desktop/server via browser (RDP, SSH, VNC)  
- Apache Guacamole + TOTP (2FA) untuk keamanan tambahan  
- Google Authenticator sebagai lapisan verifikasi kedua  
- SSL dengan Tomcat (opsional)  
- Isolasi environment dengan Canonical/LXD  

---

## 📷 Tampilan Lab 
| Fitur             | Screenshot Placeholder |
|------------------|---------------------|
| Nslookup          | ![Nslookup](path/to/image.png) |
| Login Page        | ![Login](path/to/image.png) |
| HTTPS Access      | ![HTTPS](path/to/image.png) |
| TOTP Auth         | ![TOTP](path/to/image.png) |
| Remote Desktop    | ![RDP](path/to/image.png) |

> Screenshots hanya bersifat ilustrasi, menggunakan lingkungan lab lokal.

---

## ⚙️ Teknologi yang Digunakan
- **OS**: Debian 12 (LXD Container)  
- **Remote Access**: Apache Guacamole  
- **Authentication**: TOTP + Google Authenticator  
- **Web Server**: Tomcat (optional SSL termination)  
- **Virtualization**: Canonical LXD  

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

