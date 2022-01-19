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

 
 ## STEP 5 – TESTING PHP WITH NGINX
 Lets test it validate that Nginx can correctly hand .php files off to your PHP processor. we would create a test PHP file in your document root. Open a new file called info.php within your document root in your text editor:

 *sudo nano /var/www/projectLEMP/info.php*
 Type or paste the following lines into the new file. This is valid PHP code that will return information about your server:
 
 <img width="191" alt="PHP code" src="https://user-images.githubusercontent.com/51254648/150069327-d856d51f-633a-4c94-b0dd-e645b9b58cab.png">

 we can now access this page in the web browser by visiting the domain name or public IP address we’ve set up in your Nginx configuration file, followed by /info.php: http://44.201.223.110/info.php
 
 <img width="1280" alt="PHP default page" src="https://user-images.githubusercontent.com/51254648/150069336-7a42713c-1074-4326-b76e-b1ce403c4f2b.png">

 
 it’s best to remove the file we created as it contains sensitive information about your PHP environment and our Ubuntu server. we can use rm to remove that file:
 *sudo rm /var/www/your_domain/info.php*
 
 
 ## STEP 6 – RETRIEVING DATA FROM MYSQL DATABASE WITH PHP (CONTINUED)
 We will create a database named example_database and a user named example_user, but you can replace these names with different values. First, connect to the MySQL console using the root account: *sudo mysql*

 <img width="564" alt="connect mysql" src="https://user-images.githubusercontent.com/51254648/150069347-05376687-555e-41c9-815a-6152f37a720a.png">
 
 To create a new database, run the following command from your MySQL console:

*mysql> CREATE DATABASE `example_database`;*
 
 Now you can create a new user and grant him full privileges on the database you have just created
 *mysql>  CREATE USER 'first_user'@'%' IDENTIFIED WITH mysql_native_password BY 'password';*
 
 <img width="655" alt="create user" src="https://user-images.githubusercontent.com/51254648/150069348-007616ad-c55d-4c28-a5a8-2d51d19097be.png">

 
 Now we need to give this user permission over the example_database database:

*mysql> GRANT ALL ON example_database.* TO 'first_user'@'%';*

 <img width="499" alt="grant user permission" src="https://user-images.githubusercontent.com/51254648/150069349-a85ed520-53ba-49ce-89e3-2e16b61ab6f7.png">
 
 confirm that we have access to the example_database database:
 *mysql> SHOW DATABASES;*

 <img width="578" alt="show database" src="https://user-images.githubusercontent.com/51254648/150069351-855e807e-ce24-41cd-bd52-575367c2aec5.png">

 
 create a test table named todo_list. From the MySQL console, run the following statement:
 *CREATE TABLE example_database.todo_list (item_id INT AUTO_INCREMENT, content VARCHAR(255), PRIMARY KEY(item_id));*
 <img width="876" alt="create todo table" src="https://user-images.githubusercontent.com/51254648/150069352-0b7dd298-c791-42ba-a3fd-c5fb088595f3.png">

 
 Insert a few rows of content in the test table.
 *mysql> INSERT INTO example_database.todo_list (content) VALUES ("My first important item");*
 
 <img width="740" alt="insert table content" src="https://user-images.githubusercontent.com/51254648/150069353-c8550f32-09c0-48dc-9d15-6e63dd5d8f0d.png">
 
 To confirm that the data was successfully saved to your table, run:
  *mysql>  SELECT * FROM example_database.todo_list;*

 <img width="366" alt="table output" src="https://user-images.githubusercontent.com/51254648/150069354-e7c87fc3-b432-4180-8f60-382d216e7124.png">

 
 create a PHP script that will connect to MySQL and query for your content. 
 *nano /var/www/projectLEMP/todo_list.php*
 Copy this content into your todo_list.php script:

 <img width="557" alt="php script" src="https://user-images.githubusercontent.com/51254648/150069356-62eb238a-1c2f-4e6a-9993-eebb169e33fa.png">

 Save and close the file when you are done editing.
 
 we can now access this page in your web browser by visiting the domain name or public IP address configured for your website, followed by /todo_list.php:
 http://'Public_domain_or_IP'/todo_list.php
 
 <img width="457" alt="browser todo" src="https://user-images.githubusercontent.com/51254648/150069358-30371ff1-4d59-4ea4-ae0f-23fe8ba048a8.png">



