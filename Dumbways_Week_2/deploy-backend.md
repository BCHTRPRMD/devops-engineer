# Deployment Backend App

## Clone Repository Backend App

- Menjalankan perintah `ssh devops@35.175.159.53` dan memasukan password yang telah dibuat pada terminal, untuk masuk ke server
- Menggunakan perintah `git clone https://github.com/sgnd/dumbflix-backend.git` untuk melakukan clone aplikasi yang akan digunakan.

  ![1](assets/deploy-1.png)

- Menjalankan perintah `sudo apt update && sudo apt upgrade`

  ![1](assets/deploy-2.png)

- Menjalankan perintah curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.0/install.sh | bash
- Menjalankan perintah `exec bash` digunakan apabila nvm tidak terdeteksi
- Menjalankan perintah `nvm install 14` untuk pemasangan nodejs versi 14

  ![1](assets/deploy-4.png)

- Menjalankan perintah `cd dumbflix-backend` untuk masuk ke direktori yang telah di clone
- Menjalankan perintah `npm install`

  ![1](assets/deploy-5.png)

- Menjalankan perintah `cp .env.example .env`

  ![1](assets/deploy-3.png)

- Melakukan konfigurasi file `config.json` dengan menyesuaikan username, password, nama database sesuai database pada mysql dan host address sesuai ip server database.

  ![1](assets/deploy-7.png)

  ![1](assets/deploy-8.png)

## Import database with sequelize

- Melakukan pemasangan sequelize-cli dengan perintah `npm install --save-dev -g sequelize-cli`

  ![1](assets/deploy-6.png)

- Menjalankan perintah `sequelize db:migrate` untuk melakukan migrate ke database yang telah dibuat

  ![1](assets/deploy-9.png)

- Masuk ke server database, lalu mengakses mysql dengan menjalankan perintah `mysql -u adi -p`
- Menjalankan perintah `show databases;` untuk menampilkan database yang telah dibuat
- Menampilkan data yang telah di migrate dari backend menggunakan perintah `use dumbflix;` lalu `show tables;`

  ![1](assets/deploy-10.png)

## Deploy Backend App

- Melakukan perintah `pm2 start ecosystem.config.js` untuk menjalankan aplikasi backend

  ![1](assets/deploy-11.png)
