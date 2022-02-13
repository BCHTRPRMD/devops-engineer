# [Setup User] di Instance/Server

1. Buat file hosts untuk menyimpan ip remote host
   ```
    [app]
    10.243.16.104 ansible_user=ubuntu
    [monitor]
    10.243.16.198 ansible_user=ubuntu
    [nginx]
    10.243.16.104 ansible_user=ubuntu

   ```

2. Buat [file ansbile](https://github.com/BCHTRPRMD/setup-ansible) ``create-user.yml``
3. Buat task untuk create user di ansible
   ```
    - name: Create User
      hosts: all
      become: true
      vars_files:
        - vars/create_user_vars.yml
      tasks:

        - name: Create new user
          user:
            name: "{{username}}"
            password: "{{password}}"
            groups:
              - sudo
              - admin
            state: present
            shell: /bin/bash
            system: no
            createhome: yes
            home: /home/{{username}}

        - name: Create directory .ssh
          file:   
            path: /home/{{username}}/.ssh
            state: directory
            owner: adi
            group: adi
            mode: 700

        - name: Copy authorized_key
          copy: 
            src: docker-files/authorized_key
            dest: /home/{{username}}/.ssh/

        - name: Change owner authorized_key
          file: 
            path: /home/{{username}}/.ssh/authorized_key
            owner: {{username}}
            group: {{username}}
            mode: 600

        - name: Enable Password Authentication
          lineinfile:
            path: /etc/ssh/sshd_config
            search_string: 'PasswordAuthentication no'
            line: PasswordAuthentication yes

        - name: Enable Password Authentication
          lineinfile:
            path: /etc/ssh/sshd_config
            search_string: '#PubkeyAuthentication yes'
            line: PubkeyAuthentication yes

        - name: Restart SSH Service
          service:
            name: ssh
            state: restarted

   ```
3. Buat file untuk variabel ``create_user_vars.yml``
   ```
   username: adi
   password: '$6$qzExQyQThEZsn0$AKa/lQBcFwtMRJOok4VeEQDy3Gyd/KGWm4t3COefAyDJbR3E6NPY9jDq1pUV/PBAuNjby/QZC7IWJHB6/Ab4s1'
   
   ```
4. Install mkpasswd
5. Gunakan mkpasswd untuk enkripsi passwordnya
6. Buat authorized file, fungsinya untuk memberi akses login ssh kepada user baru
7. Buat authorized key dari sshkey.pem
8. ``ssh-keygen -y -f sshkey.pem`` perintah ini akan mengenerate authorized key

   ![03](assets/ssh-key.png) <br />

9. Jalankan ansible-playbook ``ansible-playbook create_users.yml``

   ![03](assets/create-user-4.png) <br />

### Setup server - Install docker & docker compose di semua server

1. Buat file YAML ``setup-docker.yml``
   ```
    ---
    - name: Setup Docker & Docker Compose
      hosts: all
      become: true
      vars_files:
        - vars/create_user_vars.yml
      tasks:
        - name: Update system
          apt:
            update_cache: yes

        - name: Upgrade system
          apt:
            upgrade: yes

        - name: Setup repository
          shell: "sudo apt-get install ca-certificates curl gnupg lsb-release"
          args:
            executable: /bin/bash

        - name: Add docker GPG key
          apt_key:
            url: https://download.docker.com/linux/ubuntu/gpg
            state: present

        - name: Add docker repository
          apt_repository:
            repo: deb https://download.docker.com/linux/ubuntu focal stable
            state: present

        - name: Update system
          apt:
            update_cache: yes

        - name: Install docker engine
          apt:
            name: "{{item}}"
            state: latest
            update_cache: yes
          loop:
            - docker-ce
            - docker-ce-cli
            - containerd.io

        - name: Install stable release docker compose
          shell: sudo curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
          args:
            executable: /bin/bash


        - name: Apply executable permission to the binary
          shell: "sudo chmod +x /usr/local/bin/docker-compose"
          args:
            executable: /bin/bash

        - name: Remove sudo on docker command
          shell: sudo usermod -aG docker {{username}}
          args:
            executable: /bin/bash
   ```

2. Save.
3. Edit ``hosts`` file, tambahkan:
   ```
    [app]
    10.243.16.104 ansible_user=adi ansible_sudo_password=$6$qzExQyQThEZsn0$AKa/lQBcFwtMRJOok4VeEQDy3Gyd/KGWm4t3COefAyDJbR3E6NPY9jDq1pUV/PBAuNjby/QZC7IWJHB6/Ab4s1
    [nginx]
    10.243.16.39 ansible_user=adi ansible_sudo_password=$6$qzExQyQThEZsn0$AKa/lQBcFwtMRJOok4VeEQDy3Gyd/KGWm4t3COefAyDJbR3E6NPY9jDq1pUV/PBAuNjby/QZC7IWJHB6/Ab4s1
    [monitor]
    10.243.16.198 ansible_user=adi ansible_sudo_password=$6$qzExQyQThEZsn0$AKa/lQBcFwtMRJOok4VeEQDy3Gyd/KGWm4t3COefAyDJbR3E6NPY9jDq1pUV/PBAuNjby/QZC7IWJHB6/Ab4s1

   ```
4. Isi ansible_sudo_password dengan password login server yang telah di enkrip menggunakan mkpasswd 
5. Save
6. Run ``ansible-playbook setup-docker.yml``
7. Masukkan password
8. Tunggu proses otomatis ansible selesai

   ![03](assets/ansible-docker.png) <br />
  
