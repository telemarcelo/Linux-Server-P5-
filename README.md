# Linux-Server-P5
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
  Important:
  ```
    Even though I later proceeded to change ufw (firewall) settings (detailed in step 3 below), 
    I still had to open port 2200 through the Networking tab of the Lightsail instance manager.
  ```
  
3. Configure the ufw (uncomplicated firewall) (Secure the server)
  ```
  $ sudo ufw default deny incoming
  $ sudo ufw default allow outgoing
  $ sudo ufw allow 2200/tcp
  $ sudo ufw allow 80/tcp
  $ sudo ufw allow 123
  $ sudo ufw enable
  ```
  
4. Created a "grader" user (give grader access)
  ```
  Create a new user using the adduser command:
  $ adduser grader
  ```
5. Give grader sudo access (give grader access)
  ```
  Created and edited a file in /etc/sudoers.d
  $ nano /etc/sudoers.d/grader
  
  Set the contents of the file to:
  grader ALL=(ALL) NOPASSWD:ALL 
  ```
6. Create a SSH key pair using ssh-keygen (give grader access)
  ```
  Created an SSH key pair LOCALLY by typing:
  $ ssh-keygen
  
  I then logged in AS GRADER and installed the public key by executing the following commands:
  $ mkdir .ssh
  $ touch .ssh/authorized_keys
  
  I opened and pasted the PUBLIC key inside the file using:
  $ nano .ssh/authorized_keys
  
  At this point I proceeded to revoke password login by editing /etc/ssh/sshd_config and changing:
  
  PasswordAuthentication no
  ```
  
7. Configure time zone (deploy project):
  ```
  $ sudo dpkg-reconfigure tzdata
  Select none of the above and then UTC (both highlighted defaults)
  ```
  
8. Install and configure Apache (deploy project):
  ```
  Installed Apache and wsgi for Python 3:
  $ sudo apt-get install apache2
  $ sudo apt-get install libapache2-mod-wsgi
  $ sudo apt-get install libapache2-mod-wsgi-py3
  
  Configure Apache:
  $ sudo nano /etc/apache2/sites-enabled/000-default.conf
  and add
  WSGIScriptAlias / /var/www/html/myapp.wsgi
  right before </virtual host>
  ```
 
9. Install and configure Postgres (deploy project):
  ```
  Install Postgres:
  $ sudo apt-get install postgresql
  
  By default, postrgresql does not allow remote connections.
  
  Create a new user:
  $ sudo adduser catalog
  
  Creat permissions:
  $ sudo su - postgres
  $ createuser --interactive --pwprompt #answer the questions in the interactive prompt
  
  Create DB (still as postgres su)
  $ createdb -O catalog ItemCatalog
  ```
 
10. Clone git repository (deploy Item Catalog)
```
Project available at:
  https://github.com/telemarcelo/Item-Catalog.git
```
 Instead of using a virtualenv I opted to use sudo install:
```
 sudo -H pip3 install psycopg2
  flask
  sqlalchemy
  psycopg2
  oauth2
  oauth2client
  finger
  apache
  git
```

IP address: http://34.205.90.128.xip.io/ port 80
URL :http://34.205.90.128.xip.io/

### Support
telemarcelo@gmail.com

### Sources
https://www.a2hosting.com/kb/developer-corner/postgresql/managing-postgresql-databases-and-users-from-the-command-line
https://help.ubuntu.com/community/PostgreSQL

### Authors and acknowledgment
Marcelo Antunes


