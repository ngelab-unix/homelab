# Remote Office Access Lab with Apache Guacamole 

## TUJUAN
Membangun simulasi remote access kantor menggunakan:
- Akses remote desktop via web (RDP, SSH, VNC)
- **Apache Guacamole + TOTP** untuk akses desktop/server via web
- **TOTP + Google Authentifikator** sebagai lapisan keamanan kedua dalam proses autentikasi dua langkah (2FA)
- **Tomcat** sebagai terminator SSL (opsional)
- **Canonical/LXD** untuk isolasi environment

## 📊 Diagram Topologi
![Topologi Jaringan](guacamole_images/guaca_cloudflaredtopologi.png) 

## 📷 Tampilan Guacamole  
![Login Page](guacamole_images/guacalabzerotrust.png) ![Login Page](guacamole_images/guacahttps.png)
![Login Page](guacamole_images/guacalabtotp.png)![Login Page](guacamole_images/guacalabrdp.png)

## Catatan
- Tested on Debian 12 LXD Canonical container
- Bisa diadaptasi untuk production dengan server fisik/vm

-------------------------------------------------------------------------------------------------------------
## 👤 Author
Aditya Ramadhani – [LinkedIn](https://linkedin.com/in/username) | [Email](mailto:ramadhaniaditya19@gmail.com)
-------------------------------------------------------------------------------------------------------------


