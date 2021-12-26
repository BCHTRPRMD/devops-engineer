# SSL Configuration for Backend App

## Konfigurasi SSL

- Mengakses server gateway menggunakan perintah `ssh devops@nginx`
- Menjalankan perintah `sudo certbot`, lalu pilih 2 `api.bpramadi.onlinecamp.id untuk diaktifkan dengan https

  ![1](assets/ssl-9.png)

- Apabila proses sudah selesai, lakukan pengecekan sertifikasi dengan masuk ke `cd /etc/nginx/dumbflix`
- Menjalankan perintah `cat bpramadi.onlinecamp.id` untuk menampilkan perubahan

  ![1](assets/ssl-10.png)

- Menjalankan perintah sudo nginx -t untuk melakukan pengecekan konfigurasi
- Menjalankan perintah sudo systemctl restart nginx

- Mengakses web browser dan memasukan domain `http://api.bpramadi.onlinecamp.id/`

  ![1](assets/ssl-11.png)

## Konfigurasi Frontend

- Mengakses server frontend menggunakan perintah `ssh devops@frontend`
- Melakukan konfigurasi pada file api.js untuk mengarahkan baseurl ke domain backend app dengan menjalankan perintah `sudo nano /src/config/api.js/`

  ![1](assets/front-1.png)

  ![1](assets/front-2.png)

- Melakukan restart app menggunakan `pm2 restart Frontend`

  ![1](assets/front-3.png)

## Akses Website

- Mengakses web browser dan memasukan domain `https://bpramadi.onlinecamp.id/` dan login

  ![1](assets/ssl-7.png)

  ![1](assets/ssl-8.png)
