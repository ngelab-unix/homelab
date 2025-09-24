# 📊 Zabbix Monitoring Migration Lab

## 📌 Deskripsi Proyek
Proyek ini mensimulasikan **migrasi server monitoring Zabbix** dari **old server** ke **new server** di atas lingkungan **LXD Canonical**.  
Tujuan utama adalah memastikan data grafik, konfigurasi, serta database **Zabbix** dapat dipindahkan tanpa kehilangan informasi historis, sekaligus mempelajari skenario **backup & restore** monitoring system.  

---

## 🏗️ Topologi Jaringan

| Komponen                 | IP Address      | Deskripsi                          |
|--------------------------|-----------------|------------------------------------|
| **LXD Host**             | 192.168.1.xx    | Canonical LXD Hypervisor           |
| **Zabbix Old Server**    | 10.105.28.91    | Server lama (sumber data + graph)  |
| **Zabbix New Server**    | 10.105.28.181   | Server baru (target migrasi)       |
| **Database (MariaDB)**   | internal        | Backup & Restore schema + data     |

📊 **Diagram Topologi Migrasi**  
![Topologi Migrasi Zabbix](/Image/Zabbixmigration.png)
![Topologi Migrasi Zabbix](/Image/Zabbixmigration.png)

---

## 🎯 Tujuan
- ✅ **Backup database Zabbix (MySQL/MariaDB)** dari server lama  
- ✅ **Export configuration & RRD data**  
- ✅ **Restore ke server baru dengan versi terbaru**  
- ✅ **Verifikasi grafik & data historis**  
- ✅ **Siapkan server baru dengan opsi skalabilitas lebih baik**  

---

## 📷 Proses Migrasi  

| Backup DB | Transfer Data | Restore DB | Verify Graph |
|-----------|---------------|------------|--------------|
| ![Backup](/Image/cacti_backup.png) | ![Transfer](/Image/cacti_transfer.png) | ![Restore](/Image/cacti_restore.png) | ![Verify](/Image/cacti_verify.png) |

## 📷 Cacti + DNS External + Cloudflare  

| Nslookup  | Zabbix |
|-----------|--------|
| ![Backup](/Image/cacti_backup.png) | ![Transfer](/Image/cacti_transfer.png) |

---

## ⚙️ Teknologi yang Digunakan
- **OS**: Debian 12 (LXD Container)  
- **Monitoring**: Cacti (PHP + RRDTool)  
- **Database**: MariaDB/MySQL  
- **Web Server**: Apache/Nginx  
- **Virtualization**: Canonical LXD  

---

## 📌 Catatan
- Tested on Debian 12 LXD Canonical container  
- Migrasi diuji antara versi **Zabbix 1.2.x → 1.3.x (latest)**  
- Bisa diintegrasikan dengan **Nginx Load Balancer + Failover** jika jumlah client lebih banyak  

---

## 👤 Author
Aditya Ramadhani  
🔗 [LinkedIn](https://linkedin.com/in/username) | 📧 [Email](mailto:ramadhaniaditya19@gmail.com)  
