# Dokumentasi Load Balancing

Merupakan proses pembagian beban traffic sebuah aplikasi atau server. Dengan load balancer, salah satu server tidak akan menanggung terlalu banyak beban permintaan.

<p align="center">
  <img src="https://github.com/BCHTRPRMD/dumbways-dev/blob/master/week-4/assets/load-balancer.png" />
</p>

# Metode Load Balancing

- Least Connection : Membagikan beban server berdasarkan server yang mempunyai koneksi paling sedikit di daftar server yang ada.

- Ratio : Membagikan beban server berdasarkan oleh ratio yang diberikan kepada server yang ada. Semakin besar rasio yang dimiliki server, semakin besar beban yang akan diberikan kepada server .

- IP Hash: Alamat IP dari klien menentukan server mana yang akan menerima permintaan.

- Round Robin: Membagikan beban server ke setiap server secara bergantian

# Contoh penerapan metode Round Robin menggunakan Nginx

- Menjalankan perintah `cd /etc/nginx` untuk mengakses direktori nginx

- Menjalankan perintah `sudo mkdir load-balancing` untuk membuat sebuah direktori `load-balancing`

- Menjalankan perintah `sudo nano nginx.conf` untuk melakukan penambahan folder yang telah dibuat kedalam `nginx.conf` dengan memasukan `include /etc/nginx/load-balancing/*;` ke dalam file tersebut

  ![1](assets/monitoring-1.png)

  ![1](assets/monitoring-2.png)

- Menjalankan perintah `cd load-balancing` untuk berpindah direktori

- Membuat file `sudo nano load.conf` dan melakukan setup didalamnya sesuai kebutuhan

  ![1](assets/monitoring-5.png)

  ![1](assets/monitoring-4.png)

- Menjalankan perintah `sudo nginx -t` untuk melakukan pengecekan konfigurasi
- Menjalankan perintah `sudo systemctl reload nginx` untuk memuat ulang konfigurasi nginx

  ![1](assets/monitoring-3.png)

- Menjalankan server dengan `port 3000 dan port 5000` yang merupakan aplikasi yang telah dibuat sebelumnya

  ![1](assets/monitoring-6.png)

  ![1](assets/monitoring-7.png)

- Mengakses domain aplikasi `load-balancer.net` pada Web Browser dan memuat ulang pada halaman aplikasi, maka trafik akan diberikan secara bergantian sehingga membentuk sebuah rotation atau putaran dengan menampilkan halaman dari server A dan server B

  ![1](assets/monitoring-8.png)

  ![1](assets/monitoring-9.png)
