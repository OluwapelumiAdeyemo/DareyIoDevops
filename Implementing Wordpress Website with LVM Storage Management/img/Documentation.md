## IMPLEMENTING WORDPRESS WEBSITE WITH LOGIC VOLUME MANAGEMENT (LVM) STORAGE MANAGEMENT

## Step 1 - PREPARE A WEB SERVER.
-Launch an EC2 instance the will serve as "Web Server"
- Create 3 Volumes in the same Az as your Web server EC", each of 10gigs
- Launching an EC2 Instance called Web-Server with a Redhat OS
  
![1_name!](../img/1_linuxwebserver.png)

## Create 3 volumes , 10Gb each.

![1_name!](../img/1_volumecreation.png)

## To attach each Volume one by one to the Webserver EC2 Instance
Click on the Volume and right click to select the attach option.
Select the Web-server EC2 instance and click attach

![1_name!](../img/5_attachvolumetoinstance.png)

## To connect to redhat ec2 instance

![1_name!](../img/2_redhatconnect.png)

To inspect what block device is attched to the server
lsblk

![1_name!](../img/3_lsblkviewpaartitions.png)
![1_name!](../img/7_lsdevcommand.png)

## To see all mount and free space on the web-server
df -h

![1_name!](../img/8_dfhcommand.png)

## To create a single partition on each of the disk using the gdisk Utility, run the below command:
sudo gdisk /dev/nvme1n1
sudo gdisk /dev/nvme2n1
sudo gdisk /dev/nvme3n1
Run a new entry by entering n and click the number of partition in this case 1
Click yes to complete the process

![1_name!](../img/12_gdiskpartition.png)
![1_name!](../img/12_gdpartition.png)
![1_name!](../img/13_gdpartition2and3.png)

## To view the newly configured partition on each of the 3 disks
lsblk 

![1_name!](../img/14_newlyconfiguredpartitionview2.png)

## Run the below command to check for available partitions
sudo lvmdiskscan

![1_name!](../img/15_diskscan2.png)

## To mark each of the three disks as physical Volumes(Pvs) to be used by LVM, run the below commands
sudo pvcreate /dev/nvme1n1p1 
sudo pvcreate /dev/nvme2n1p1 
sudo pvcreate /dev/nvme3n1p1

![1_name!](../img/16_pvcreate.png)

## To verify that the physical volume has been created successfully

![1_name!](../img/17_sudovolume.png)

## To verify the logic Volumes has been created successfully.
sudo lvs

![1_name!](../img/18_lvcreate.png)

![1_name!](../img/19_formatlogicalvolume.png)

## To mount var/log on logs-lv logical volume
sudo mount /dev/webdata-vg/logs-lv /var/log

![1_name!](../img/20_mount.png)

## Install lvm2 package using the below command;
sudo yum install lvm2

![1_name!](../img/10_lvm2install.png)

## To view the available partitions

![1_name!](../img/11_availablepartitions.png)

![1_name!](../img/20_sudoupdate.png)

##To update /etc/fstab so that the mount configuration will persist after restart. Copy the UUID of the device to upate the /etc/fstab
sudo blkid

![1_name!](../img/21_updatefstab.png)

## To test the configuration and reload the Daemon
sudo mount -a 
AND
sudo systemctl daemon-reload

![1_name!](../img/21_testconfiguration.png)

## To verify the set up is running well
df -h

![1_name!](../img/1_df-h.png)

## HEADING - INSTALLING WORDPRESS AND CONFIGURING IT TO USE MYSQL DATABASE
STEP-2 PREPARING THE DATABASE SERVER
Repeating the same step above, BUt instead of apps-lv create db-lv and mount it into directory /db instead of /var/www/html
Launch an EC2 instance DB-serveron redhart OS

![1_name!](../img/1_linuxwebserver.png)

## Create and attach 3-volumes to the DB-Server

![1_name!](../img/1_volumecreation.png)
![1_name!](../img/5_attachvolumetoinstance.png)
![1_name!](../img/3_lsblkviewpartition.png)
![1_name!](../img/4_installlvm2.png)
![1_name!](../img/6_webdatacreate.png)

## STEP-3 INSTALLING WORDPRESS ON YOUR WEB SERVER EC2 INSTANCE
Before we install Wordpress, we would first update the reprository by running the below command
sudo yum -y update

![1_name!](../img/6a_sudoupdate.png)

## To install Apache, wget and its dependencies
sudo yum -y install wget httpd php php-mysqlnd php-fpm php-json

![1_name!](../img/6_mysql-serverinstall.png)

## To install PHP and its dependencies, run the below command;
sudo yum install https://dl.fedoraproject.org/pub/epel/epel-release-latest-8.noarch.rpm
sudo yum install yum-utils http://rpms.remirepo.net/enterprise/remi-release-8.rpm
sudo yum module list php
sudo yum module reset php
sudo yum module enable php:remi-7.4
sudo yum install php php-opcache php-gd php-curl php-mysqlnd

![1_name!](../img/13_installingphpdependencies.png)

## To downlaod Wordpress and copy wordpress to var/www/html, run the below command;
mkdir wordpress
cd   wordpress
sudo wget http://wordpress.org/latest.tar.gz
sudo tar xzvf latest.tar.gz
sudo rm -rf latest.tar.gz
sudo cp wordpress/wp-config-sample.php wordpress/wp-config.php
sudo cp -R wordpress /var/www/html/

![1_name!](../img/4_wordpressinstallation.png)

## STEP 4 - INSTALLING MYSQL ON YOUR DB SERVER EC2
To update and Install mysql-server
sudo yum update

![1_name!](../img/6a_sudoupdate.png)

## sudo yum install mysql-server

![1_name!](../img/6_mysql-serverinstall.png)

## To verify if the set-up is running
sudo systemctl restart mysqld
sudo systemctl status mysqld,

![1_name!](../img/7_verifymysqlserver.png)

## CONFIGURE DB TO WORK WITH WORDPRESS
sudo mysql
CREATE DATABASE wordpress;
CREATE USER `myuser`@`<Web-Server-Private-IP-Address>` IDENTIFIED BY 'mypass';
GRANT ALL ON wordpress.* TO 'myuser'@'<Web-Server-Private-IP-Address>';
FLUSH PRIVILEGES;
SHOW DATABASES;
exit

![1_name!](../img/8_sudomysql.png)

![1_name!](../img/9_connectdbtowordpress.png)

 ## CONFIGURE WORDPRESS TO CONNECT TO REMOTE DATABASE
Open MYSQL port 3306 on DB-server and access it only from web-servers IP address
In the inbound rule configure source as /32

![1_name!](../img/10_port3306.png)

## To Install MySQL client on the web server and test that you can connect from Web-server to DB-server using mysql-client

sudo yum install mysql
On the Database Server, Create an admin user in mysql using the below parameter. This will be used to create a remote connection through the web server.

CREATE USER 'username'@'host' IDENTIFIED BY 'password';
Note: Username should be your desired name; host - replace host with the Subnet cidr of the webserver

![1_name!](../img/10_testconfiguration.png)

## in the web server, vi into the wp-config file by runing the below command

sudo vi /var/www/html/wordpress/wp-config.php
Note - Replace the following with the real values. database_name_here with the wordpress, username_here with admin, password_here with the password of the admin, localhost with the private ip of the database server.

![1_name!](../img/13_Wordpressconfig2.png)

## Now, try to access from your browser link to the wordpress using your web server ip.

http://<web-server-public-ip-address>/wordpress/

![1_name!](../img/14_wordpresspage.png)














