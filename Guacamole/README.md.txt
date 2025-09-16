
**TOPOLOGI JARINGAN**

- **LXD CANONICAL**   : 192.168.1.xx 
- **guacamole**       : 10.105.28.160
- **PC Remote Acces** : 10.105.28.170

## 📊 Diagram Topologi
![Topologi Jaringan](https://github.com/ngelab-unix/homelab/blob/main/Image/ChatGPT%20Image%20Sep%2016%2C%202025%2C%2009_49_24%20AM.png) 

# Remote Office Access Lab with Apache Guacamole 

## TUJUAN
Membangun simulasi remote access kantor menggunakan:
- Akses remote desktop via web (RDP, SSH, VNC)
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






