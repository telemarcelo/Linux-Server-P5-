# Linux-Server-P5-
Project 5 for Udacity Nanodegree program

### Description
This project involves taking a baseline Linux installation from "zero to hero."  I created an instance on AWS Lightsail and configured it properly for security and performance (see steps).  I then cloned my previous project Item Catalog and made it available online through and IP address.

### Steps
1. Log in via SSH and upgrade packages (Secure the Server)
  ```
  I used the SSH button found on AWS log in to my instance. I then used the following commands to upgrade my packages:
  
    sudo apt-get update
    sudo apt-get upgrade
  ```
2. Change the SSH port from 22 to 2200 (Secure the Server)
  ```
  I used the nano editor to configure the /etc/ssh/sshd_conig file
  
    sudo nano /etc/ssh/sshd_config
    
  I then changed "Port 22" to "Port 2200" and saved the file.
  ```
  ```
  Important:
    Even though I later proceeded to change ufw (firewall) settings (detailed below), I still had to open port 2200 through the Networking tab of the Lightsail instance manager.
  ```
  
3.

### Support
telemarcelo@gmail.com

### Authors and acknowledgment
Marcelo Antunes
