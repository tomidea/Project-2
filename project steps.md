# WEB STACK IMPLEMENTATION (LEMP STACK)
Project 2 covers similar concepts as Project 1 and helps to cement your skills of deploying Web solutions using LA(E)MP stacks. In this project you will implement a similar stack, but with an alternative Web Server – NGINX, which is also very popular and widely used by many websites in the Internet.

## STEP 1 – INSTALLING THE NGINX WEB SERVER
We’ll use the apt package manager to install this package.
*sudo apt update*

*sudo apt install nginx*

To verify that nginx was successfully installed and is running as a service in Ubuntu, run:

*sudo systemctl status nginx*

Add a rule to EC2 configuration to open inbound connection through port 80:


First, let us try to check how we can access it locally in our Ubuntu shell, run:

curl http://localhost:80
or
curl http://127.0.0.1:80

 Test how our Nginx server can respond to requests from the Internet. Open a web browser of your choice and try to access following url
http://<Public-IP-Address>:80
  
  
  
  ## Step 2 — Installing MySQL
  We need to install a Database Management System (DBMS) to be able to store and manage data for your site in a relational database. MySQL is a popular relational database management system used within PHP environments, so we will use it in our project.
  
  *sudo apt install mysql-server*
  
  
 This script will remove some insecure default settings and lock down access to your database system. Start the interactive script by running:

*sudo mysql_secure_installation*
  
 To connect to the MySQL server as the administrative database user root
*sudo mysql*
  
  
 ## STEP 3 – INSTALLING PHP
 A PHP module that allows PHP to communicate with MySQL-based databases. Core PHP packages will automatically be installed as dependencies.
  
 To install these 2 packages at once, run:

*sudo apt install php-fpm php-mysql*
  
  
  ## STEP 4 — CONFIGURING NGINX TO USE PHP PROCESSOR
  
  Create the root web directory for your_domain as follows:


