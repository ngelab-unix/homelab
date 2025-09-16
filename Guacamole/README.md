# 🔐 Secure Remote Office Access Lab with Apache Guacamole

## 📌 Deskripsi Proyek
Proyek ini mensimulasikan **akses remote kantor** yang aman menggunakan **Apache Guacamole** dengan **Two-Factor Authentication (TOTP)** di atas lingkungan **LXD Canonical**.  
Tujuan utama adalah memberikan solusi *remote desktop/web access* yang mudah, aman, dan dapat diadaptasi ke lingkungan produksi.  

---

## 🏗️ Topologi Jaringan

| Komponen              | IP Address      | Deskripsi                  |
|-----------------------|-----------------|-----------------------------|
| **LXD Host**          | 192.168.1.xx    | Canonical LXD Hypervisor    |
| **Apache Guacamole**  | 10.105.28.160   | Web-based Remote Access     |
| **PC Remote Access**  | 10.105.28.170   | Client RDP/SSH/VNC          |

📊 **Diagram Topologi**  
![Topologi Jaringan](/Image/ChatGPT%20Image%20Sep%2016%2C%202025%2C%2009_49_24%20AM.png)  

---

## 🎯 Tujuan
- ✅ **Remote desktop/server via browser (RDP, SSH, VNC)**  
- ✅ **Apache Guacamole + TOTP (2FA)** untuk keamanan tambahan  
- ✅ **Google Authenticator** sebagai lapisan verifikasi kedua  
- ✅ **SSL dengan Tomcat** (opsional)  
- ✅ **Isolasi environment dengan Canonical/LXD**  

---

## 📷 Tampilan Guacamole  
| Login Page | HTTPS Access | TOTP Auth  | Remote Desktop |DNS local + Nginx Proxy | DNS + Cloudflared |  
|------------|--------------|------------|----------------|------------------------|--------------------|
| ![Login Page](image/guacalabzerotrust.png) | ![HTTPS](guacamole_images/guacahttps.png) | ![TOTP](guacamole_images/guacalabtotp.png) | ![RDP](guacamole_images/guacalabrdp.png) |![RDP](guacamole_images/guacalabrdp.png) |![RDP](guacamole_images/guacalabrdp.png) |

---

## ⚙️ Teknologi yang Digunakan
- **OS**: Debian 12 (LXD Container)  
- **Remote Access**: Apache Guacamole  
- **Authentication**: TOTP + Google Authenticator  
- **Web Server**: Tomcat (optional SSL termination)  
- **Virtualization**: Canonical LXD  

---

## 🛠️ Instalasi Singkat
1. **Setup LXD Container**
   lxc launch images:debian/12 guacamole
   lxc exec guacamole bash
   

2. **Install Apache Guacamole**
   apt update && apt install guacamole -y

3. **Enable TOTP Authentication**
   - Tambahkan ekstensi `guacamole-auth-totp`  
   - Hubungkan dengan **Google Authenticator**  

4. **(Opsional) SSL dengan Tomcat**
   keytool -genkey -alias tomcat -keyalg RSA -keystore keystore.jks -keysize 2048


## 📌 Catatan
- Tested on Debian 12 LXD Canonical container  
- Dapat diadaptasi untuk production server (VM / baremetal)  
- Bisa dikombinasikan dengan **VPN (WireGuard)** atau **Cloudflare Tunnel** untuk keamanan lebih lanjut  


## 👤 Author
Aditya Ramadhani  
🔗 [LinkedIn](https://linkedin.com/in/username) | 📧 [Email](mailto:ramadhaniaditya19@gmail.com)  

























**TOPOLOGI JARINGAN**

- **LXD CANONICAL**   : 192.168.1.xx 
- **guacamole**       : 10.105.28.160
- **PC Remote Acces** : 10.105.28.170

## 📊 Diagram Topologi
![Topologi Jaringan](/Image/ChatGPT%20Image%20Sep%2016%2C%202025%2C%2009_49_24%20AM.png) 

# Remote Office Access Lab with Apache Guacamole 

## TUJUAN
Membangun simulasi remote access kantor:
- **Akses remote desktop via web (RDP, SSH, VNC)**
- **Apache Guacamole + TOTP** untuk akses desktop/server via web
- **TOTP + Google Authentifikator** sebagai lapisan keamanan kedua dalam proses autentikasi dua langkah (2FA)
- **Tomcat** sebagai terminator SSL (opsional)
- **Canonical/LXD** untuk isolasi environment


## 📷 Tampilan Guacamole  
![Login Page](image/guacalabzerotrust.png) ![Login Page](guacamole_images/guacahttps.png)
![Login Page](guacamole_images/guacalabtotp.png)![Login Page](guacamole_images/guacalabrdp.png)

## Catatan
- Tested on Debian 12 LXD Canonical container
- Bisa diadaptasi untuk production dengan server fisik/vm

-------------------------------------------------------------------------------------------------------------
## 👤 Author
Aditya Ramadhani – [LinkedIn](https://linkedin.com/in/username) | [Email](mailto:ramadhaniaditya19@gmail.com)
-------------------------------------------------------------------------------------------------------------










