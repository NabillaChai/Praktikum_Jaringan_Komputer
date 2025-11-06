# Build a Switch and Router Network

Link Youtube : https://youtu.be/GFW9VdGuSeg?si=xNuiTki9XC1RlMTD

#

## Ping PC-A ke PC-B sebelum dilakukan konfigurasi pada Router
<img width="698" height="301" alt="Cuplikan layar 2025-11-05 084542" src="https://github.com/user-attachments/assets/708b688e-8213-4594-b4fb-ab002414fb31" />

Berdasarkan gambar di atas, hasil pengujian ping dari PC-A (192.168.1.3) ke PC-B (192.168.0.3) menunjukkan pesan “Request timed out” yang berarti pengiriman paket data gagal. Tidak ada balasan (reply) dari PC-B dan seluruh paket mengalami 100% packet loss.
Kondisi ini terjadi karena router belum dikonfigurasi sehingga belum ada perangkat yang berfungsi sebagai penghubung antar subnet. PC-A berada pada jaringan 192.168.1.0/24, sedangkan PC-B berada pada jaringan 192.168.0.0/24. Tanpa adanya konfigurasi router, komunikasi hanya dapat berlangsung dalam satu jaringan (Layer 2). Karena tidak ada perangkat Layer 3 yang meneruskan paket antar subnet, maka paket ICMP yang dikirim dari PC-A tidak dapat mencapai alamat tujuan.
Oleh karena itu, hasil pada gambar di atas menunjukkan bahwa komunikasi antar jaringan tidak dapat dilakukan sebelum router diaktifkan dan dikonfigurasi dengan benar.



## Ping PC-A ke PC-B setelah dilakukan konfigurasi pada Router
<img width="696" height="297" alt="Cuplikan layar 2025-11-05 084604" src="https://github.com/user-attachments/assets/ef4d245f-00e2-4429-8aec-4c4c22ae12d6" />

Berdasarkan gambar di atas, hasil pengujian ping dari PC-A (192.168.1.3) ke PC-B (192.168.0.3) menunjukkan balasan “Reply from 192.168.0.3” yang menandakan bahwa pengiriman paket data berhasil. Semua paket berhasil diterima tanpa kehilangan data (0% packet loss), dengan waktu respon (time) kurang dari 1 ms, yang menunjukkan bahwa koneksi berlangsung sangat cepat dalam jaringan lokal.
Keberhasilan ini terjadi setelah router R1 dikonfigurasi dengan benar, di mana interface G0/0/0 diberikan alamat IP 192.168.0.1/24 yang terhubung ke PC-B, dan interface G0/0/1 diberikan alamat IP 192.168.1.1/24 yang terhubung ke PC-A melalui switch S1. Setiap interface juga telah diaktifkan menggunakan perintah no shutdown, dan routing IPv6 diaktifkan melalui perintah ipv6 unicast-routing. Nilai TTL = 127 menunjukkan bahwa paket hanya melewati satu perangkat router sebelum mencapai tujuan.
Berdasarkan hasil pada gambar di atas, dapat disimpulkan bahwa router telah berfungsi dengan baik sebagai penghubung antar subnet, sehingga komunikasi antar jaringan dapat dilakukan dengan lancar.
