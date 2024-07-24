# Web Stack Implementation (LEMP STACK)!

## Shows that the Instance has been succesfully connected

![1_load!](./img/1_load.png)

## Installing the Nginx Web Server
sudo apt update

![1_load!](./img/2_nginxinstall.png)

## To verify that nginx was installed properly
sudo systemctl status nginx

![1_load!](./img/2_nginxrunning.png)

## To access Nginx server via local machine
Run curl http://localhost:80
or curl http://127.0.0.1:80

![1_load!](./img/3_accessingubuntu.png)

## To Access Nginx via the web browser using the public IP Address.
http://<Public-IP-Address>:80

![1_load!](./img/4_welcometonginx.png)

## To Install mysql on Nginx Server
sudo apt install mysql-server

![1_load!](./img/5_mysqlserverinstall.png)

## To Login into mysql console
sudo mysql

![1_load!](./img/6_mysql-p.png)

## To Install the 2 packages.
sudo apt install php-fpm php-mysql

![1_load!](./img/7_phpinstallation.png)

## Create a folder called projectLEMP
sudo mkdir /var/www/projectLEMP

![1_load!](./img/9_nginxtestok.png)
![1_load!](./img/10_nanoindex.html.png)

## To try to open my website through my web browser, using the my public IP, run the below command.
http://<Public-IP-Address>:80

![1_load!](./img/11_Lempoutput.png)

## Testing PHP with Nginx
Inside the ProjectLEMP folder, create a LEMP file with the name info.php.
touch info.php

![1_load!](./img/12_nanotestwithphp.png)

## Now, we can access this page in the web browser by visiting the domain name or public IP address we had setup in the Nginx configuration file.
http://`server_domain_or_IP`/info.php

![1_load!](./img/13_phpinfo.png)

Connect to MySQL using the below command, provide your MySQL password to gain entrance to the database
sudo mysql -p

Create a new Database by running the below command
CREATE DATABASE example_database;

![1_load!](./img/14_connectingtomysql2.png)

## Create a new user and grant him full priviledges on the database you have just created. create a new user with the name example_user, using mysql_native_password as default authentication method. We're defining the user's password as PassWord.1 but will be replacing the password with a more secured password.
CREATE USER 'example_user'@'%' IDENTIFIED WITH mysql_native_password BY 'PassWord.1';

![1_load!](./img/15_createuser.png)

## Show the list of MySQL Databases
SHOW DATABASES;

![1_load!](./img/18_showrealdatabase.png)

## We will create a table called todo_list using the command below
CREATE TABLE example_database.todo_list (item_id INT AUTO_INCREMENT,content VARCHAR(255),PRIMARY KEY(item_id));

![1_load!](./img/19_todolist.png)

## Now, I will create a PHP script that will connect to MySQL and query for the content. Create a new PHP file called todo_list.php from the custom root directory using the below command

nano /var/www/projectLEMP/todo_list.php
<Images/Create a new PHP file called todo_list.php>
Copy the below content into the nano file editor. Kindly note that the below PHP script connects to the MySQL database and queries for the content of the todo_list table; displays the result in a list.

![1_load!](./img/20_nanotodolist.png)

## I can now access the page in my web broswer by visiting the public IP address for my website follwoed by /todo_list.php:.

http://<Public_domain_or_IP>/todo_list.php

![1_load!](./img/21_todolistoutput.png)






