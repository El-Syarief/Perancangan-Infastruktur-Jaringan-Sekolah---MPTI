# Instalasi dan Konfigurasi Server Lokal untuk Manajemen Jaringan di Sekolah

Proyek ini merupakan simulasi perancangan infrastruktur jaringan lokal (LAN) dan konfigurasi server untuk sekolah menggunakan Cisco Packet Tracer. Sistem ini dirancang menggunakan topologi *Star* dan metode pengembangan *Network Development Life Cycle* (NDLC).

Proyek ini disusun untuk memenuhi tugas mata kuliah Manajemen Proyek Teknologi Informasi di Universitas Bina Sarana Informatika (2025).

## 👥 Tim Pengembang (Kelompok 6)
* **Idris Haidir Ali** (17230172) - *Project Manager*
* **Muhammad Amir Syarifuddin** (17230462) - *Network Engineer*
* **Nabillah April Riyanti** (17230631) - *System Administrator*
* **Dita Rhevinda Putri** (17230440) - *Documentation & Training Officer*
* **Aditiya Saputra** (17230476) - *Quality Control*

## 🎯 Fitur Utama
* **Segmentasi Logis (VLAN):** Pemisahan jaringan berdasarkan peran pengguna (Guru, Murid, Staf, Tamu) untuk keamanan dan efisiensi.
* **Keamanan Berlapis (ACL & WPA2-Enterprise):** Menggunakan *Access Control List* (ACL) untuk memblokir komunikasi antar-VLAN yang tidak berwenang, serta otentikasi Wi-Fi internal menggunakan Server RADIUS 802.1X.
* **Manajemen Jaringan Terpusat:** Distribusi IP dinamis dengan DHCP Server terpusat, pengontrolan nirkabel menggunakan *Wireless LAN Controller* (WLC), dan Inter-VLAN Routing pada *Core Switch*.
* **Server Private Cloud:** Simulasi penyediaan server penyimpanan mandiri berbasis Ubuntu dan Nextcloud untuk kolaborasi dokumen digital sekolah.

## 🏗️ Skema VLAN dan IP Addressing
Jaringan ini dibagi menjadi beberapa subnet IPv4 (Kelas C /24) berdasarkan fungsionalitasnya:

| VLAN ID | Nama VLAN | Network Address | Default Gateway | Fungsi |
| :--- | :--- | :--- | :--- | :--- |
| **VLAN 10** | Guru | `192.168.10.0/24` | `192.168.10.1` | Perangkat guru (Kabel & Nirkabel) |
| **VLAN 20** | Kepala Sekolah | `192.168.20.0/24` | `192.168.20.1` | Prioritas pimpinan sekolah |
| **VLAN 30** | Staf Kantor | `192.168.30.0/24` | `192.168.30.1` | Administrasi ruang gabungan |
| **VLAN 40** | Tata Usaha | `192.168.40.0/24` | `192.168.40.1` | Administrasi gedung terpisah |
| **VLAN 50** | Lab Komputer | `192.168.50.0/24` | `192.168.50.1` | Khusus 20 PC Lab Komputer |
| **VLAN 60** | Murid | `192.168.60.0/24` | `192.168.60.1` | Wi-Fi perangkat siswa |
| **VLAN 70** | Tamu | `192.168.70.0/24` | `192.168.70.1` | Wi-Fi publik (Terisolasi dari jaringan internal) |
| **VLAN 99** | Control Panel | `192.168.99.0/24` | `192.168.99.1` | Manajemen server, WLC, dan Router |

## 🛠️ Infrastruktur Perangkat Inti
* **Router Gateway:** Menyediakan fitur NAT dan perlindungan keamanan awal ke eksternal.
* **Core Switch (Layer 3):** Dikonfigurasi dalam mode *VTP Server* untuk mengelola komunikasi Inter-VLAN dan menyediakan fungsi *DHCP Relay* ke server utama.
* **Access Switch & Access Point:** Menyediakan konektivitas Layer 2 ke pengguna akhir dan memancarkan SSID Wi-Fi yang dikelola oleh WLC.
* **Server Lokal:** Berjalan di VLAN 99, menampung layanan DHCP Server (dengan banyak *pool* IP), *Authentication Server* (RADIUS), dan *File Server*.

## 🚀 Cara Menjalankan Simulasi
1. Pastikan Anda telah menginstal aplikasi **Cisco Packet Tracer**.
2. Unduh *file* `topologi-3-2.pkt` dari dalam folder `/pkt`.
3. Buka *file* tersebut dengan Cisco Packet Tracer.
4. Tunggu beberapa saat hingga *Spanning Tree Protocol* (STP) menyelesaikan konvergensi pada titik jaringan *Switch*.
5. Lakukan uji coba dengan melakukan *ping* antar perangkat di dalam VLAN yang sama, dan uji penerapan keamanan dengan melakukan *ping* antar VLAN (misalnya PC Murid ke Server) untuk mengonfirmasi fungsi blokir dari *Access Control List* (ACL).