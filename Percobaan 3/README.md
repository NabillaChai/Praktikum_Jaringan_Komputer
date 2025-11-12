# Configure VLANs and Trunking

Link Youtube : https://youtu.be/BMt7LfJn_VA 
<br><br>

## Topologi Jaringan

<img width="799" height="326" alt="image" src="https://github.com/user-attachments/assets/774958c6-0c53-4028-8438-e0255b961aa5" />
<br><br>

### Tabel Konfigurasi IP Device

| **Device** | **Interface** | **IP Address** | **Subnet Mask**     | **Default Gateway** |
|-------------|----------------|----------------|----------------------|----------------------|
| S1          | VLAN 1         | 192.168.1.11   | 255.255.255.0        | N/A                  |
| S2          | VLAN 1         | 192.168.1.12   | 255.255.255.0        | N/A                  |
| PC-A        | NIC            | 192.168.10.3   | 255.255.255.0        | 192.168.10.1         |
| PC-B        | NIC            | 192.168.10.4   | 255.255.255.0        | 192.168.10.1         |
| PC-C        | VLAN 30        | 192.168.30.3   | 255.255.255.0        | —                    |

<br><br>
## Penjelasan Ping

**1. Ping PC-A ke PC-B**

<img width="405" height="186" alt="image" src="https://github.com/user-attachments/assets/e79ca0e6-1091-4939-8e10-e60a3e73a62d" />

Ping dari PC-A ke PC-B berhasil karena keduanya berada di VLAN 10 (Operations) dan menggunakan jaringan dengan subnet yang sama (192.168.10.0/24). Paket data dapat dikirim dan diterima dengan baik tanpa ada yang hilang. Hal ini menunjukkan bahwa konfigurasi VLAN dan port untuk kedua PC sudah benar, serta koneksi fisik dari masing-masing PC ke switch berfungsi dengan baik. Dengan kata lain, komunikasi antar perangkat dalam VLAN yang sama sudah berjalan normal.
<br><br>

**2. Ping PC-A ke PC-C**

<img width="424" height="164" alt="image" src="https://github.com/user-attachments/assets/1d8956a6-01e6-4695-bf0c-e7c3195b518e" />

Ping dari PC-A ke PC-C gagal, karena kedua PC berada di VLAN yang berbeda. PC-A berada di VLAN 10, sedangkan PC-C berada di VLAN 30 (Guest). Karena belum ada konfigurasi inter-VLAN routing atau perangkat Layer 3 yang menghubungkan antar VLAN, maka paket dari PC-A tidak dapat diteruskan ke PC-C. Akibatnya, komunikasi antar keduanya tidak bisa dilakukan.
<br><br>

**3. Ping PC-A ke S1**

<img width="419" height="161" alt="image" src="https://github.com/user-attachments/assets/b993b682-f826-48c0-a456-16794de425be" />

Ping dari PC-A ke switch S1 gagal karena perbedaan VLAN. PC-A berada di VLAN 10, sedangkan alamat IP manajemen switch S1 ada di VLAN 99 (Management). Karena belum ada mekanisme routing antar VLAN, maka paket dari PC-A tidak dapat mencapai alamat IP S1. Selain itu, konfigurasi VLAN 99 digunakan khusus untuk manajemen switch, sehingga tidak bisa langsung diakses oleh perangkat di VLAN lain tanpa pengaturan tambahan seperti router atau Layer 3 switch.
<br><br>

**4. Ping PC-B ke S2**

<img width="418" height="161" alt="image" src="https://github.com/user-attachments/assets/6b1d86dc-c609-4b2e-a6b9-e2d42afe3deb" />

Ping dari PC-B ke switch S2 juga gagal karena alasan yang sama seperti sebelumnya. PC-B berada di VLAN 10, sementara S2 memiliki IP address pada VLAN 99. Karena VLAN 10 dan VLAN 99 tidak memiliki koneksi langsung dan belum ada konfigurasi inter-VLAN routing, paket yang dikirim dari PC-B tidak dapat mencapai S2. Hal ini menegaskan bahwa komunikasi antar VLAN tidak bisa terjadi tanpa adanya perangkat atau konfigurasi khusus yang menghubungkannya.
<br><br>

**5. Ping S1 ke S2**

<img width="491" height="92" alt="image" src="https://github.com/user-attachments/assets/5a86d039-9194-46d1-abf2-41745e1ee7a3" />

Ping dari S1 (192.168.1.11) ke S2 (192.168.1.12) berhasil dengan 100% sukses, artinya semua paket terkirim dan diterima tanpa ada yang hilang. Hal ini menunjukkan bahwa koneksi antar switch sudah berjalan dengan baik melalui VLAN 99 (Management). Port yang menghubungkan kedua switch yaitu F0/1 telah dikonfigurasi sebagai trunk port, sehingga lalu lintas dari VLAN 99 dapat melewati link antar switch. Hasil ping ini membuktikan bahwa VLAN manajemen sudah aktif dan berfungsi, serta komunikasi antar switch sudah stabil dan dapat digunakan untuk kebutuhan pengelolaan jaringan.
<br><br>



