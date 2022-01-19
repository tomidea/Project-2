# WEB STACK IMPLEMENTATION (LEMP STACK)
Project 2 covers similar concepts as Project 1 and helps to cement your skills of deploying Web solutions using LA(E)MP stacks. In this project you will implement a similar stack, but with an alternative Web Server – NGINX, which is also very popular and widely used by many websites in the Internet.

## STEP 1 – INSTALLING THE NGINX WEB SERVER
We’ll use the apt package manager to install this package.
*sudo apt update*

<img width="843" alt="Apt update" src="https://user-images.githubusercontent.com/51254648/150017682-d3fe53a4-3ad3-447d-95c4-53a8e1ae6375.png">

*sudo apt install nginx*

<img width="1228" alt="apt install" src="https://user-images.githubusercontent.com/51254648/150017698-acbb755e-0a7b-4767-9292-1d505fc99bc3.png">

To verify that nginx was successfully installed and is running as a service in Ubuntu, run:

*sudo systemctl status nginx*

<img width="811" alt="nginx status active" src="https://user-images.githubusercontent.com/51254648/150017703-0913251d-95dc-45af-9ad7-725d8c673b6f.png">

Add a rule to EC2 configuration to open inbound connection through port 80:
<img width="1172" alt="Edit inbound rule" src="https://user-images.githubusercontent.com/51254648/150017706-3b6f8e51-adca-4f88-86e2-cb313cb87cfb.png">


First, let us try to check how we can access it locally in our Ubuntu shell, run:

curl http://localhost:80
or
curl http://127.0.0.1:80

<img width="574" alt="curl localhost" src="https://user-images.githubusercontent.com/51254648/150017710-630aa7dc-3784-4f42-a657-64c9b74197e1.png">


 Test how our Nginx server can respond to requests from the Internet. Open a web browser of your choice and try to access following url
http://<Public-IP-Address>:80
  
 <img width="1278" alt="welcome to nginx" src="https://user-images.githubusercontent.com/51254648/150017708-e4345460-1063-40ad-ba56-b9eee448c4c4.png">
 
  
  ## Step 2 — Installing MySQL
  We need to install a Database Management System (DBMS) to be able to store and manage data for your site in a relational database. MySQL is a popular relational database management system used within PHP environments, so we will use it in our project.
  
  *sudo apt install mysql-server*
  
 <img width="1267" alt="install mysql" src="https://user-images.githubusercontent.com/51254648/150017712-c7b215b7-5e5d-4ad5-b309-2142734ca251.png">

  
 This script will remove some insecure default settings and lock down access to your database system. Start the interactive script by running:

*sudo mysql_secure_installation*
 <img width="871" alt="secure installation" src="https://user-images.githubusercontent.com/51254648/150017718-152e3edf-d76a-42c4-9323-8756fae1f5e4.png">

  
 To connect to the MySQL server as the administrative database user root
*sudo mysql*
 <img width="606" alt="sudo mysql" src="https://user-images.githubusercontent.com/51254648/150017726-501b8607-3cbb-43e7-992f-fd9bd0896a69.png">
 
  
 ## STEP 3 – INSTALLING PHP
 A PHP module that allows PHP to communicate with MySQL-based databases. Core PHP packages will automatically be installed as dependencies.
  
 To install these 2 packages at once, run:

*sudo apt install php-fpm php-mysql*
  <img width="1048" alt="install core PHP pacakages" src="https://user-images.githubusercontent.com/51254648/150017730-3d13a566-5bcb-4810-a3da-57fc133de237.png">

  
  ## STEP 4 — CONFIGURING NGINX TO USE PHP PROCESSOR
  
  Create the root web directory for your_domain as follows:
  *sudo mkdir /var/www/projectLEMP*

 <img width="571" alt="root web directory" src="https://user-images.githubusercontent.com/51254648/150063062-be02e2c1-1ab1-40c7-972f-b007560d49ce.png">

 Assign ownership of the directory with the $USER environment variable
 
 *sudo chown -R $USER:$USER /var/www/projectLEMP*
 
 
 Open a new configuration file in Nginx’s sites-available directory using your preferred command-line editor.
 *sudo nano /etc/nginx/sites-available/projectLEMP*
 

 This will create a new blank file. Paste in the following bare-bones configuration:
 <img width="495" alt="bare-bones configuration" src="https://user-images.githubusercontent.com/51254648/150063072-3ec5307e-c57f-4d42-bb9c-e9edcf4bad69.png">


Activate your configuration by linking to the config file from Nginx’s sites-enabled directory:

sudo ln -s /etc/nginx/sites-available/projectLEMP /etc/nginx/sites-enabled/
 
 This will tell Nginx to use the configuration next time it is reloaded. You can test your configuration for syntax errors by typing:
 *sudo nginx -t*
 
 <img width="521" alt="check syntax" src="https://user-images.githubusercontent.com/51254648/150063077-0c1452c9-ce14-4b47-905a-59c37465a0ac.png">

 We also need to disable default Nginx host that is currently configured to listen on port 80, for this run:
sudo unlink /etc/nginx/sites-enabled/default

Reload Nginx to apply the changes:

*sudo systemctl reload nginx*
 <img width="559" alt="reload nginx" src="https://user-images.githubusercontent.com/51254648/150063081-4f1d9b34-d9e6-4dac-89ec-7c90f892f370.png">
  
 Create an index.html file in that location so that we can test that your new server block works as expected:

 sudo echo 'Hello LEMP from hostname' $(curl -s http://169.254.169.254/latest/meta-data/public-hostname) 'with public IP' $(curl -s http://169.254.169.254/latest/meta-data/public-ipv4) > /var/www/projectLEMP/index.html
 
 Now go to your browser and try to open your website URL using IP address:

http://'Public-IP-Address':80
<img width="1280" alt="website" src="https://user-images.githubusercontent.com/51254648/150063079-3718e9b2-09c8-43cf-87a0-a97903a78105.png">

