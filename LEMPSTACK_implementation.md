## Web stack implementation (LEMP stack)
### Introduction
A LEMP stack refers to a software stack that includes Linux, Nginx (pronounced "Engine-X"), MySQL, and PHP. It is a popular combination for hosting websites and web applications.This project will highlight the process of implementing a LEMP stack on Amazon AWS using an Ubuntu Server.
### Summary of steps involved in this Web stack Implementation
- Launch an Amazon EC2 Instance
- Set up the Ubuntu server
- installing and configuring  the nginx web server
- installing and configuring mysql
- installing and configuring php
- configuring nginx to use php processor
- testing php with nginx
- retrieving data from mysql database with php
#### Launch an Amazon EC2 Instance

#### Set up the Ubuntu server
Connect to your EC2 instance via SSH using the key pair you selected during instance launch.
**insert key pair image ***

Update the package repository cache.

    `sudo apt update`
    
Upgrade the installed packages to the latest versions.

    `sudo apt upgrade -y`

#### Installing and configuring  the nginx web server
