# AWS Create And Setup Server

# Create server gateway

- Membuka AWS Educate dan Sign In.
- Pilih `My Classrooms` dan tekan `go to classroom`

  ![1](assets/setup-1.png)

- Tekan `continue`
- Apabila sudah nanti akan di arahkan ke `labs.vocareum.com` dan tekan `AWS console`

  ![1](assets/setup-2.png)

- Pilih `Launch a Virtual Machine With EC2`

  ![1](assets/setup-3.png)

- Search dan Pilih `Ubuntu server 20.04 LTS`, lalu tekan `Select` .

  ![1](assets/setup-4.png)

- Pada tahapan `Choose an Instance Type` pilih `t2.micro` dengan cpu 1 dan memory 1, lalu tekan `Next: configure instance details`

  ![1](assets/setup-5.png)

- selanjutnya pilih `number of instance` sesuai dengan kebutuhan server yang ingin dibuat dan `auto-assign Public ip` di disable agar ketika server mati dan dijalankan kembali ip tidak berubah / static, seperti pada gambar di bawah.
- Tekan `next:add storage:`

  ![1](assets/setup-6.png)

- Pada tahap `add storage` dapat dilakukan pengaturan storage sesuai keperluan, adapun penggunaan yang akan dipilih yakni ukuran default yaitu 8gb, lalu tekan add tags.

  ![1](assets/setup-7.png)

- Pada tahap `Add tags` dapat di skip dan klik `next configure security group`

  ![1](assets/setup-8.png)

- Pada tahap `configure security group` dapat diisi dengan memasukan nama security group dan deskripsi. Kemudian kita `add rule` SSH, HTTP dan HTTPS sesuai gambar dibawah, lalu tekan `review and launch`

  ![1](assets/setup-9.png)

- selanjutnya pada tahap `review instance launch` dapat dilihat detail daripada konfigurasi yang telah ditambahkan, apabila sudah tekan `launch`

  ![1](assets/setup-10.png)

- Selanjutnya akan muncul tampilan untuk membuat key pair yang digunakan masuk keserver yang dibuat, lalu pilih `create a new key pair`
- Pilih `rsa` dan masukkan `nama key pair` dan download key pair
- Pilih `launch instance` dan tunggu prosesnya

  ![1](assets/setup-11.png)

- Melakukan edit nama server menjadi `gateway`.
- Apabila proses telah selesai maka tampilannya sebagai berikut.

  ![1](assets/setup-12.png)

- Melakukan set ip static menggunakan elastic ip.
- Masuk ke pilihan `elastic IPs` lalu kalian tekan `Allocate elastic ip address`

  ![1](assets/setup-13.png)

  ![1](assets/setup-14.png)

- Tekan ke pilihan `Actions` lalu pilih `associate elastic ip address`.

  ![1](assets/setup-15.png)

- Pada bagian instance pilih server yang telah dibuat tadi. jika sudah tekan `associate`

  ![1](assets/setup-16.png)

- Selanjutnya kembali ke instances untuk melihat elastic ip telah terpasang pada server.

  ![1](assets/setup-17.png)

- Membuka terminal untuk masuk ke server yang telah dibuat
- Masuk ke direktori tempat keypair tersimpan
- Menjalankan perintah `sudo chmod 400 dumbways.pem` untuk memberikan akses terhadap file
- Menjalankan perintah `ssh -i dumbways.pem ubuntu@54.163.110.219`

  ![1](assets/setup-18.png)

# Create server app

- Masuk AWS dan pilih `Launch a Virtual Machine With EC2`
- Search dan Pilih `Ubuntu server 20.04 LTS`, lalu tekan `Select`
- Pada tahapan `Choose an Instance Type` pilih `t2.micro` dengan cpu 1 dan memory 1, lalu tekan `Next: configure instance details`

  ![1](assets/setup-app-1.png)

- selanjutnya pilih `number of instance` sesuai dengan kebutuhan server yang ingin dibuat dan `auto-assign Public ip` di disable agar ketika server mati dan dijalankan kembali ip tidak berubah / static, seperti pada gambar di bawah.
- Tekan `next:add storage:`

  ![1](assets/setup-app-2.png)

- Pada tahap `add storage` dapat dilakukan pengaturan storage sesuai keperluan, adapun penggunaan yang akan dipilih yakni ukuran default yaitu 8gb, lalu tekan add tags.

  ![1](assets/setup-app-3.png)

- Pada tahap `Add Tags` juga bisa di skip saja, klik `next configure security group`

  ![1](assets/setup-app-4.png)

- Pada `Configure Security Group` mengisi security group name dan deskripsinya dengan memasukan Frontend, lalu `add rule dan typenya` dijadikan all traffic agar dapat diakses dari semua port dan pilih 0.0.0.0/0. lalu klik review and launch

  ![1](assets/setup-app-5.png)

- selanjutnya pada tahap `review instance launch` dapat dilihat detail daripada konfigurasi yang telah ditambahkan, apabila sudah tekan `launch`

  ![1](assets/setup-app-6.png)

- Selanjutnya akan muncul tampilan untuk membuat key pair yang digunakan masuk keserver yang dibuat, lalu pilih `choose an existing key pair`
- Pilih keypair sama seperti yang sebelumnya dan centang opsi yang tersedia
- Melakukan edit nama server menjadi `appserver`.

  ![1](assets/setup-app-7.png)
  ![1](assets/setup-app-8.png)

- Selanjutnya `allocate elastic ip` untuk server app
- Pada pilihan instance masukkan `appserver` kemudian `associate`

  ![1](assets/setup-app-9.png)

- Membuka terminal dan masuk kedalam server app dengan menggunakan ip yang telah dibuat, `ssh -i dumbways.pem ubuntu@54.158.109.67`

  ![1](assets/setup-app-10.png)
