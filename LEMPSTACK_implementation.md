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

    ` sudo apt update`
    
Upgrade the installed packages to the latest versions.

    ` sudo apt upgrade -y`

### Step 3. Installing and configuring  the nginx web server

    ` sudo apt install nginx`
    
Check statust os Nginx

    ` sudo systemctl status nginx`
    
Check to see if we can access nginx locally on our Ubuntu shell, run:

     ` curl http://localhost:80`
     
On any brower enter the following url:

     ` http://<Public-IP-Address>:80`
     
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
    
    ` sudo mysql -p`
    
you may exit mysql once everything is running fine
    
    ` mysql> exit`
![Screenshot (218)](https://github.com/ettebaDwop/dareyProject2/assets/7973831/eaf0cba7-25e5-4561-8e4c-33c6a0a39f78)
    
    
    
### Step 5. Installing and configuring php
    
* You have Nginx installed to serve your content and MySQL installed to store and manage your data. Now you can install PHP to process code and generate dynamic content for the web server. While Apache embeds the PHP interpreter in each request, Nginx requires an external program to handle PHP processing and act as a bridge between the PHP interpreter itself and the web server. This allows for a better overall performance in most PHP-based websites, but it requires additional configuration. You’ll need to install php-fpm, which stands for “PHP fastCGI process manager”, and tell Nginx to pass PHP requests to this software for processing. Additionally, you’ll need php-mysql, a PHP module that allows PHP to communicate with MySQL-based databases. Core PHP packages will automatically be installed as dependencies. *
    
To install php and all its dependencies, run:
    
    ` sudo apt install php-fpm php-mysql`
    
### Step 6. Configuring nginx to use php processor
   * When using the Nginx web server, we can create server blocks (similar to virtual hosts in Apache) to encapsulate configuration details and host more than one domain on a single server. In this guide, we will use projectLEMP as an example domain name.

On Ubuntu 20.04, Nginx has one server block enabled by default and is configured to serve documents out of a directory at /var/www/html. While this works well for a single site, it can become difficult to manage if you are hosting multiple sites. Instead of modifying /var/www/html, we’ll create a directory structure within /var/www for the your_domain website, leaving /var/www/html in place as the default directory to be served if a client request does not match any other sites.*
    
Create a root web directory for your-domain website
    
   ` sudo mkdir /var/www/projectLEMP`
    
 Assign ownership of this your_domain website to current user using the $USER environment variable 
    
   ` sudo chown -R $USER:$USER /var/www/projectLEMP`
    
 Open a new configuration file in NGINX sites-available directory
    
   ` sudo nano /etc/nginx/sites-available/projectLEMP`
    
 Paste the following bare-bone configuration into the new configuration file:
    
 ``` 
    #/etc/nginx/sites-available/projectLEMP

server {
    listen 80;
    server_name projectLEMP www.projectLEMP;
    root /var/www/projectLEMP;

    index index.html index.htm index.php;

    location / {
        try_files $uri $uri/ =404;
    }

    location ~ \.php$ {
        include snippets/fastcgi-php.conf;
        fastcgi_pass unix:/var/run/php/php8.1-fpm.sock;
     }

    location ~ /\.ht {
        deny all;
    }

} 
  ```
    
 Activate your configuration by linking to the config file from Nginx’s sites-enabled directory:
    
    ` sudo ln -s /etc/nginx/sites-available/projectLEMP /etc/nginx/sites-enabled/`
 
 Test NGINX, run the command:
    
   ` sudo nginx -t`
    
 ![Screenshot (222)](https://github.com/ettebaDwop/dareyProject2/assets/7973831/0e7ca27e-ecf6-438a-8a50-76dbe95595a3)
    
Reload NGINX:
    
    ` sudo systemctl reload nginx`
 
![Screenshot (221)](https://github.com/ettebaDwop/dareyProject2/assets/7973831/a29b19f0-4a21-4b8a-be6a-abba219120e2)
   
Create an index file to show this content on your site using the following commands:
    
    ` sudo echo 'Hello LEMP from hostname' 
      $(curl -s http://169.254.169.254/latest/meta-data/public-hostname) 'with public IP'
      $(curl -s http://169.254.169.254/latest/meta-data/public-ipv4) > /var/www/projectLEMP/index.html
    `
The screen below shows that we have a connection and everything has been configured successfully.
    
 ![Screenshot (223)](https://github.com/ettebaDwop/dareyProject2/assets/7973831/d1600b6b-65b9-4f4d-b0fe-4d18be20386d)
    
### Step 7. Testing php with nginx
From the results obtained in the preceeding step, our LEMP stack setup is now complete and fully operational. However, we need to test to see if it works as expected. 
Thus, using Nano a new file info.php would be created to test the setup. To create the file run the command:
       
 ` sudo nano /var/www/projectLEMP/info.php`
    
and paste the following code into the info.php file.
    
  ```
    <?php
       phpinfo();
  ```
![Screenshot (227)](https://github.com/ettebaDwop/dareyProject2/assets/7973831/d87ba9cf-b688-4770-9e29-529181b953e5)

 In any brower type the following url:

` http://<IP-Address>/info.php`

This page should be displayed:

![Screenshot (229)](https://github.com/ettebaDwop/dareyProject2/assets/7973831/b95a0370-ce46-4b97-9950-efd0d160e780)
This showws that nginx is capable of handling php files 

### Step 8. Retrieving data from mysql database with php
