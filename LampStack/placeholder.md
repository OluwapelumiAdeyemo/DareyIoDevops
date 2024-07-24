# My Lamp Stack Project!
## Web Stack Implementation (Web Stack in AWS)!

## This shows the succesful connection to the ec2 instance!

![1_ec2connect.png!](./img/1.ec2connect.png)

## This shows the succesful connection to the second ec2 instance

![2_ec2connect.png!](./img/2_ec2connect.png)

## Installing Apache using ubuntu's package manager 'apt'

![3_sudoupdate.png!](./img/3_sudoupdate.png)

## To verify that Apache2 is running as a service in our OS - sudo systemctl status nginx

![4_apacheserver!](./img/4_runningapacheserver.png)

## To access Nginx server via local machine
Run curl http://localhost:80
or curl http://127.0.0.1:80

![4_apacheserver!](./img/5_checkingort80.png)

## View the url in web browser to show that the web server is correctly installed

![4_apacheserver!](./img/6_apachedefaultpage.png)

## To Install mysql on Nginx Server
sudo apt install mysql-server

![4_apacheserver!](./img/7_mysqlserver2.png)

## To set password for the Root user ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'PassWord.1';

![4_apacheserver!](./img/8_mysqlpassword.png)

## To Install the 2 packages.
sudo apt install php-fpm php-mysql

![4_apacheserver!](./img/10_phpinstallation.png)

## Configuring Nginx to Use PHP Processor
Create a root web directory for your_domain as follows
sudo mkdir /var/www/projectLEMP
To cd into the root directory
sudo -i
cd /var/www/

![4_apacheserver!](./img/11_varfile.png)

![4_apacheserver!](./img/12_enablesiteprojectlamp.png)

![4_apacheserver!](./img/13_sudonano.png)

![4_apacheserver!](./img/14_enablesites.png)

![4_apacheserver!](./img/15_hostname.png)

## To try to open my website through my web browser, using the my public IP, run the below command.
http://<Public-IP-Address>:80

![4_apacheserver!](./img/16_lampprojectcurlpage.png)

## Testing PHP with Nginx
Inside the ProjectLEMP folder, create a LEMP file with the name info.php.
touch info.php

![4_apacheserver!](./img/17_phpinfo.png)

![4_apacheserver!](./img/18_phpnewfile.png)

## Open the php page with Ip address
![4_apacheserver!](./img/20_phppage.png)








