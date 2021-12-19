# VMware Install Ubuntu server and Setup Network

## Persiapan VMware.

- Melakukan download VMware pada link berikut. `https://www.vmware.com/products/workstation-player.html`
- Apabila sudah diunduh masuk ke terminal. dan masuk ke directory yang berisi file VMware yang telah diunduh.
- Menjalankan perintah `sudo sh VMware-Player-Full-16.2.1-18811642.x86_64.bundle` untuk melakukan instalasi.
- Tunggu hingga proses pemasangan selesai dan VMware siap digunakan.

## Pemasangan ubuntu server pada VMware.

Adapun Langkah-Langkahnya sebagai berikut :

- Membuka VMware yang telah di install sebelumnya

  ![1](assets/vmware-1.png)

- Download ISO ubuntu server di website `https://ubuntu.com download/server` dan memilih opsi pemasangan manual.
- Masuk ke VMware lalu tekan `Create a new virtual machine`
- Apabila telah masuk ke tampilan seperti gambar dibawah silahkan pilih `use ISO image` lalu masukan ISO image yang telah diunduh.

  ![2](assets/vmware-2.png)

- Memasukan personalize linux sesuai kebutuhan.

  ![2](assets/vmware-3.png)

- Memasukan nama sesuai virtual machine yang akan dijalankan dan pilih lokasi virtual machine sesuai penempatan yang diinginkan

  ![2](assets/vmware-4.png)

- Memasukan ukuran disk yang dibutuhkan.

  ![2](assets/vmware-5.png)

- Apabila telah selesai tekan customize hardware dan dapat disesuaikan sesuai kebutuhan atau seperti gambar dibawah.

  ![2](assets/vmware-6.png)

  ![2](assets/vmware-7png)

  ![2](assets/vmware-8.png)

  ![2](assets/vmware-9.png)

- Apabila semua tahapan diatas telah dilakukan, kemudian tekan `close` lalu tekan `finish`
- Selanjutnya masuk ke Virtual Machine yang sudah dibuat dan tekan `power on`
- Tunggu hingga muncul pilihan bahasa.

  ![2](assets/vmware-11.png)

- Pilih bahasa dan Keyboard layout yang akan digunakan pada sistem operasi.

  ![2](assets/vmware-12.png)

  ![2](assets/vmware-12-1.png)

  ![2](assets/vmware-13.png)

- Melakukan konfigurasi `IPv4 Method manual (DHCP)` untuk penggunaan IP Static pada Network Conections

  ![2](assets/vmware-14.png)

  ![2](assets/vmware-14-1.png)

- Konfigurasi proxy dan ubuntu archive mirror

  ![2](assets/vmware-15.png)

  ![2](assets/vmware-16.png))

- Membuat partisi server dengan memilih `custom storage layout`

  ![2](assets/vmware-17.png)

  ![2](assets/vmware-18.png)

  ![2](assets/vmware-19.png)

- Melakukan konfigurasi profile untuk login ke dalam sistem

  ![2](assets/vmware-20.png)

- Melakukan install OpenSSH dengan memilih Install OpenSSH server

  ![2](assets/vmware-21.png)

- Berikut merupakan proses instalasi ketika berlangsung

  ![2](assets/vmware-22.png)

- Apabila pemasangan telah selesai, tekan `Reboot now`
- Melakukan login menggunakan username dan password yang telah dibuat

  ![23](assets/vmware-23.png)

- Melakukan perintah `ping google.com` untuk mencoba apakah telah terhubung dengan internet atau belum.

  ![23](assets/vmware-24.png)

- Apabila akan melakukan setup network lanjutan, dapat menjalankan perintah `cd /etc/netplan` dan masuk ke file `sudo nano 00-installer-config.yaml`

- Pada file tersebut dapat dilakukan perubahan sesuai dengan kebutuhan terkait ip, gateway, ataupun nameservers addresses, setelah selesai melakukan setup, selanjutnya menjalankan perintah `netplan apply` untuk mengkonfirmasi setiap perubahannya.

  ![23](assets/vmware-25.png)

  ![23](assets/vmware-26.png)

  ![23](assets/vmware-27.png)
