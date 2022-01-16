# Server

Membuat instance di Multipass

1. Melakukan pemasangan multipass `sudo snap install multipass`
2. Setup server seperti langkah berikut :

#### Server Apps
1. OS ubuntu 20 
2. Memory 2 Gb
3. Storage 15 Gb

![02](assets/server-1.png) <br />


#### Server Webserver(Nginx)
1. OS ubuntu 20 
2. Memory 1 Gb
3. Storage 10 Gb
   
![02](assets/server-2.png) <br />

#### Server Monitoring
1. OS ubuntu 20 
2. Memory 1 Gb
3. Storage 10 Gb
   
![02](assets/server-3.png) <br />


### Setup Load balance untuk apps frontend dan backend
1. Login Webserver instance
2. Masuk ke /etc/nginx
3. Edit file config app frontend

![02](assets/server-4.png) <br />

5. Save
6. Edit file config app backend
   
![02](assets/server-5.png) <br />

7. Save
8. Test config ``sudo nginx -t``


