# Web stack implementation (LEMP stack)
## Introduction
A LEMP stack refers to a software stack that includes Linux, Nginx (pronounced "Engine-X"), MySQL, and PHP. It is a popular combination for hosting websites and web applications.This project will highlight the process of implementing a LEMP stack on Amazon AWS using an Ubuntu Server.
## Summary of steps involved in this Web stack Implementation
- Launch an Amazon EC2 Instance
- Set up the Ubuntu server
- installing and configuring  the nginx web server
- installing and configuring mysql
- installing and configuring php
- configuring nginx to use php processor
- testing php with nginx
- retrieving data from mysql database with php
- 
### Step 1.  Launch an Amazon EC2 Instance

![Screenshot (216)](https://github.com/ettebaDwop/dareyProject2/assets/7973831/b27d3d14-2654-4612-b0f1-c30df1a71a6f)

### Step 2.  Set up the Ubuntu server

Connect to your EC2 instance via SSH using the key pair you selected during instance launch.

![Screenshot (214)](https://github.com/ettebaDwop/dareyProject2/assets/7973831/f015894c-7938-483a-97d3-2fdebfd2fd98)

Update the package repository cache.

    `sudo apt update`
    
Upgrade the installed packages to the latest versions.

    `sudo apt upgrade -y`

### Step 3. Installing and configuring  the nginx web server

    `sudo apt install nginx`
    
Check statust os Nginx

    `sudo systemctl status nginx`
    
Check to see if we can access nginx locally on our Ubuntu shell, run:

     `curl http://localhost:80`
     
On any brower enter the following url:

     `http://<Public-IP-Address>:80`
     
replacing the <Public-IP-Address> with our ip address generated from AWS.
    
![Screenshot (215)](https://github.com/ettebaDwop/dareyProject2/assets/7973831/99150c85-106c-410e-a2a8-d46ef1217153)

### Step 4. Installing and configuring mysql

To install and configure mysql, run the following commands:
    
```sudo apt install mysql-server
   sudo mysql
   ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'PassWord.1';
   mysql> exit 
   sudo mysql_secure_installation
 ```
log in to mysql
    
    `sudo mysql -p`
    
you may exit mysql once everything is running fine
    
    `mysql> exit`
![Screenshot (218)](https://github.com/ettebaDwop/dareyProject2/assets/7973831/eaf0cba7-25e5-4561-8e4c-33c6a0a39f78)
    
    
    
### Step 5. Installing and configuring php
### Step 6. Configuring nginx to use php processor
### Step 7. Testing php with nginx
### Step 8. Retrieving data from mysql database with php
