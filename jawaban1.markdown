Langkah pertama mengakses vm terlebih dahulu
![image](https://user-images.githubusercontent.com/122170858/217474103-3eec20f7-12f2-4d1e-83f6-df5d37f65f7b.png)

1. Install Docker

   edit file /etc/selinux/config dengan vi /etc/selinux/config dan ganti menjadi  SELINUX=permissive
   ![image](https://user-images.githubusercontent.com/122170858/217474962-db8608d7-3816-42aa-b6d4-7d5d2a5ef5b7.png)
   
   selanjutnya install terlebih dahulu dependencynya dengan perintah berikut: dnf install dnf-utils device-mapper-persistent-data lvm2 fuse-overlayfs wget
   
   kemudian menambahkan repository docker-ce untuk centos dengan perintah berikut
   
   "
   sudo yum install -y yum-utils
 
   sudo yum-config-manager \
      --add-repo \
      https://download.docker.com/linux/centos/docker-ce.repo
   "
      
   selanjutnya check dengan perintah "cat /etc/yum.repos.d/docker-ce.repo", hasilnya seperti berikut
   ![image](https://user-images.githubusercontent.com/122170858/217478755-93241b96-42ed-4c32-9435-5d5da39d5626.png)
   
   setelah kita menambahkan repositorynya, selanjutnya kita install docker-ce package
   ![image](https://user-images.githubusercontent.com/122170858/217479649-09be802e-5d11-40b5-b620-999c05da0dc7.png)
   
   kemudian jalankan service dockernya, dengan perintah: systemctl enable --now docker
   setelah itu cek dengan perintah: docker info , hasilnya seperti berikut
   ![image](https://user-images.githubusercontent.com/122170858/217481565-cce9ce04-589f-44f4-8217-a5bf3b8be47f.png)
   
   selanjutnya setting firewall seperti berikut
   ![image](https://user-images.githubusercontent.com/122170858/217482682-7d7a8eaf-da74-47e8-89fc-6a4d1fa1de5c.png)

   menambahkan properti "-H tcp://0.0.0.0:2375" dengan mengedit file /lib/systemd/system/docker.service , seperti berikut
   ![image](https://user-images.githubusercontent.com/122170858/217484254-ddf589d8-b877-459b-8a61-652796ea812c.png)

   kemudian restar docker service : systemctl restart docker.service
  
2. Configure insecure registry ke nexus oss
   
   pertama buat folder telebih dahulu: mkdir /etc/docker/ , setelah itu kita buat file daemon.json : vi /etc/docker/daemon.json
   ![image](https://user-images.githubusercontent.com/122170858/217486273-c8a725b0-4010-4cfb-989d-91c2b6558ad8.png)
   
   kemudian kita restart lagi dockernya : systemctl restart docker.service
   
   selanjutnya kita login seperti berikut
   ![image](https://user-images.githubusercontent.com/122170858/217487795-82fb17c0-e780-4ef1-9d01-c701612459a6.png)
   
3. Menjalankan container dengan menggunakan image 192.168.100.250:8086/httpd:latest dengan port export 8081

   setelah login, kita pull image terlebih dahulu dengan perintah berikut: docker pull 192.168.100.250:8086/httpd:latest
   
   selanjutnya kita cek, hasilnya seperti berikut:
   ![image](https://user-images.githubusercontent.com/122170858/217489506-c09855f1-f057-4313-a941-49939c8ef447.png)

   kemudian kita jalankan container dengan port 8081
   ![image](https://user-images.githubusercontent.com/122170858/217492049-6fd8e080-b18b-418b-be86-fda9a3b4f005.png)
   
4. Akses dari local komputer
   ![Screenshot (8)](https://user-images.githubusercontent.com/122170858/217492260-4cbb9b42-83b6-4f1c-9126-c47559cca06d.png)

   
   
   

   
   
   
  
   

   


   
