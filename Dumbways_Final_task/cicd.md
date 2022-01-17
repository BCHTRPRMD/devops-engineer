# CI/CD Jenkins

### Install Jenkins Docker

- Buat file docker-compose untuk instalasi jenkins didalam direktory `docker-files`
  
```
version: '3.9'
services:
  jenkins:
    image: jenkins/jenkins:lts
    ports:
      - 8080:8080
      - 50000:50000
    privileged: true
    user: root
    container_name: jenkins
    volumes:
      - ~jenkins:/var/jenkins_home
      - /var/run/docker.sock:/var/run/docker.sock
      - /usr/local/bin/docker:/usr/local/bin/docker   
```
- Kemudian buat file ansible-playbook yang berisi perintah untuk instalasi jenkins pada server cicd
```
- name: Setup CI/CD Jenkins Docker
  hosts: app
  become: true
  tasks:
    - name: Copy docker compose
      copy:
        src: docker-files/docker-compose-jenkins.yml 
        dest: /home/adi/jenkins/

    - name: Run docker compose
      shell:
        cmd: "docker-compose -f docker-compose-jenkins.yml up -d"
        chdir: /home/adi/jenkins/

```

   ![08](assets/cicd-0.png) 

### Setup Jenkins
1. Install plugin publish over ssh dan slack notification (optional)
 
   ![08](assets/cicd-1.png)

2. Setup Publish over ssh

   ![08](assets/cicd-2.png)

3. Membuat Credentials
   
   ![08](assets/cicd-1.2.png)

### Setup jenkins job frontend
1. Buat freestyle project
2. Configure, setup source code management

   ![08](assets/cicd-4.png)

2. Setup build triggers

   ![08](assets/cicd-3.png)

3. Setup build command 

   ![08](assets/cicd-5.png)

4. Save

6. Test build
    
   ![08](assets/cicd-6.png)


