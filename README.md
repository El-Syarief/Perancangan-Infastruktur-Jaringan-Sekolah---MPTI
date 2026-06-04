# Instalasi dan Konfigurasi Server Lokal untuk Manajemen Jaringan di SMP Al-Hidayah Wattaqwa

[cite_start]Proyek ini merupakan simulasi perancangan infrastruktur jaringan lokal (LAN) dan konfigurasi server untuk SMP Al-Hidayah Wattaqwa menggunakan Cisco Packet Tracer[cite: 2, 18, 409]. [cite_start]Sistem ini dirancang menggunakan topologi *Star* dan metode pengembangan *Network Development Life Cycle* (NDLC)[cite: 69, 611].

[cite_start]Proyek ini disusun untuk memenuhi tugas mata kuliah Manajemen Proyek Teknologi Informasi di Universitas Bina Sarana Informatika (2025)[cite: 13, 15, 22].

## 👥 Tim Pengembang (Kelompok 6)
* [cite_start]**Idris Haidir Ali** (17230172) - *Project Manager* [cite: 6, 155]
* [cite_start]**Muhammad Amir Syarifuddin** (17230462) - *Network Engineer* [cite: 9, 155]
* [cite_start]**Nabillah April Riyanti** (17230631) - *System Administrator* [cite: 10, 155]
* [cite_start]**Dita Rhevinda Putri** (17230440) - *Documentation & Training Officer* [cite: 8, 155]
* [cite_start]**Aditiya Saputra** (17230476) - *Quality Control* [cite: 7, 155]

## 🎯 Fitur Utama
* [cite_start]**Segmentasi Logis (VLAN):** Pemisahan jaringan berdasarkan peran pengguna (Guru, Murid, Staf, Tamu) untuk keamanan dan efisiensi[cite: 643, 647].
* [cite_start]**Keamanan Berlapis (ACL & WPA2-Enterprise):** Menggunakan *Access Control List* (ACL) untuk memblokir komunikasi antar-VLAN yang tidak berwenang, serta otentikasi Wi-Fi internal menggunakan Server RADIUS 802.1X[cite: 727, 738, 740].
* [cite_start]**Manajemen Jaringan Terpusat:** Distribusi IP dinamis dengan DHCP Server terpusat, pengontrolan nirkabel menggunakan *Wireless LAN Controller* (WLC), dan Inter-VLAN Routing pada *Core Switch*[cite: 683, 707, 712].
* [cite_start]**Server Private Cloud:** Simulasi penyediaan server penyimpanan mandiri berbasis Ubuntu dan Nextcloud untuk kolaborasi dokumen digital sekolah[cite: 286, 705].

## 🏗️ Skema VLAN dan IP Addressing
[cite_start]Jaringan ini dibagi menjadi beberapa subnet IPv4 (Kelas C /24) berdasarkan fungsionalitasnya[cite: 649]:

| VLAN ID | Nama VLAN | Network Address | Default Gateway | Fungsi |
| :--- | :--- | :--- | :--- | :--- |
| **VLAN 10** | Guru | `192.168.10.0/24` | `192.168.10.1` | [cite_start]Perangkat guru (Kabel & Nirkabel) [cite: 647, 651] |
| **VLAN 20** | Kepala Sekolah | `192.168.20.0/24` | `192.168.20.1` | [cite_start]Prioritas pimpinan sekolah [cite: 647, 652] |
| **VLAN 30** | Staf Kantor | `192.168.30.0/24` | `192.168.30.1` | [cite_start]Administrasi ruang gabungan [cite: 647, 653] |
| **VLAN 40** | Tata Usaha | `192.168.40.0/24` | `192.168.40.1` | [cite_start]Administrasi gedung terpisah [cite: 647, 654] |
| **VLAN 50** | Lab Komputer | `192.168.50.0/24` | `192.168.50.1` | [cite_start]Khusus 20 PC Lab Komputer [cite: 647, 655] |
| **VLAN 60** | Murid | `192.168.60.0/24` | `192.168.60.1` | [cite_start]Wi-Fi perangkat siswa [cite: 647, 656] |
| **VLAN 70** | Tamu | `192.168.70.0/24` | `192.168.70.1` | [cite_start]Wi-Fi publik (Terisolasi dari jaringan internal) [cite: 647, 657, 732] |
| **VLAN 99** | Control Panel | `192.168.99.0/24` | `192.168.99.1` | [cite_start]Manajemen server, WLC, dan Router [cite: 647, 658] |

## 🛠️ Infrastruktur Perangkat Inti
* [cite_start]**Router Gateway:** Menyediakan fitur NAT dan perlindungan keamanan awal ke eksternal[cite: 673].
* [cite_start]**Core Switch (Layer 3):** Dikonfigurasi dalam mode *VTP Server* untuk mengelola komunikasi Inter-VLAN dan menyediakan fungsi *DHCP Relay* ke server utama[cite: 686, 689].
* [cite_start]**Access Switch & Access Point:** Menyediakan konektivitas Layer 2 ke pengguna akhir dan memancarkan SSID Wi-Fi yang dikelola oleh WLC[cite: 694, 712, 718].
* [cite_start]**Server Lokal:** Berjalan di VLAN 99, menampung layanan DHCP Server (dengan banyak *pool* IP), *Authentication Server* (RADIUS), dan *File Server*[cite: 704, 707, 708, 709].

## 🚀 Cara Menjalankan Simulasi
1. Pastikan Anda telah menginstal aplikasi **Cisco Packet Tracer**.
2. Unduh *file* `topologi-3-2.pkt` dari dalam folder `/pkt`.
3. Buka *file* tersebut dengan Cisco Packet Tracer.
4. Tunggu beberapa saat hingga *Spanning Tree Protocol* (STP) menyelesaikan konvergensi pada titik jaringan *Switch*.
5. [cite_start]Lakukan uji coba dengan melakukan *ping* antar perangkat di dalam VLAN yang sama, dan uji penerapan keamanan dengan melakukan *ping* antar VLAN (misalnya PC Murid ke Server) untuk mengonfirmasi fungsi blokir dari *Access Control List* (ACL)[cite: 420, 743].