## DevOps-Tooling-Website-Solution
## Prepare NFS Server
Spin up a new EC2 instance with RHEL Linux 8 Operating System.

![cd](./img/1_nfsserver.png)

## To install the lvm2 package run the below command;
sudo yum install lvm2

![cd](./img/2_sudoyuminstall.png)

## To see all mount and free space on the web-server
df -h

![cd](./img/2_dfh.png)


## Create single partitions
To create a single partition on each of the disk using the gdisk Utility, run the below command:
sudo gdisk /dev/nvme1n1
sudo gdisk /dev/nvme2n1
sudo gdisk /dev/nvme3n1

![cd](./img/3_gdisk.png)

## Run the below command to check for available partitions
sudo lvmdiskscan

![cd](./img/4_partition.png)

## To verify that the physical volume has been created successfully
sudo pvs

![cd](./img/5_webdata.png)

## To add all the three Physical volumes(Pvs) to a Volume Group (VG). Name the VG webdata-vg
sudo vgcreate webdata-vg /dev/nvme1n1p1 /dev/nvme2n1p1 /dev/nvme3n1p1

![cd](./img/6_formatlogicalvolumes.png)

## To create 3-logic Volumes lv-opt, lv-apps and lv-logs, run the below commands;
sudo lvcreate -n lv-apps -L 9G webdata-vg 
sudo lvcreate -n lv-logs -L 9G webdata-vg 
sudo lvcreate -n lv-opt -L 9G webdata-vg

![cd](./img/7_sudorsync.png)

## To format the logical Volumes with xfs file system using mkfs.xfs
sudo mkfs -t xfs /dev/webdata-vg/lv-opt
sudo mkfs -t xfs /dev/webdata-vg/lv-apps
sudo mkfs -t xfs /dev/webdata-vg/lv-logs

![cd](./img/8_sudoblkid.png)

## Create mount points on /mnt directory for the logical volumes as follow:
sudo mkdir /mnt/apps
sudo mkdir /mnt/logs
sudo mkdir /mnt/opt

![cd](./img/9_sudofstab.png)

## To mount /mnt/apps on lv-apps logical volume
sudo mount /dev/webdata-vg/lv-apps /mnt/apps
- To mount /mnt/logs on lv-apps
sudo mount /dev/webdata-vg/lv-logs /mnt/logs

![cd](./img/10_sudoverify.png)

## Use rsync utility to backup all the files in the log directory /var/log into /mnt/logs (This is required before mounting the file system).
sudo rsync -av /var/log/. /mnt/logs

![cd](./img/7_sudorsync2.png)

## To Mount /var/log on logs-lv logical volume. (Note that all the existing data on /var/log will be deleted).
sudo mount /dev/webdata-vg/lv-logs /var/log

![cd](./img/15_mnt.png)

## To install NFS server, run the below command;
sudo yum -y update

![cd](./img/11_sudonfsinstall.png)

## To verfify the installation
![cd](./img/13_sudosystemctlstatus.png)

## Export the mount for webserver subnet cidr to connect as clients. For simplicity, you will install the three webservers inside the subnet, but in production set up you would probably want to seperate each tier inside its own subnet for higher level of security.

## To configure access to NFS for clients within the same subnets, run the below command;
sudo vi /etc/exports
![cd](./img/16_exports.png)

![cd](./img/17_securitygroup.png)

## Set up a MySQL Database Instance

![cd](./img/18_mysqldbinstance.png)

## MySQL server Installation

![cd](./img/19_installmysqlserver.png)

## sudo mysql
Run the below command in the database environment. % means - any IP range under that
sudo mysql
CREATE DATABASE tooling;
CREATE USER `myuser`@`<NFS-Server-Subnet CIDR-IP-Address>` IDENTIFIED BY 'mypass';
GRANT ALL ON tooling.* TO 'myuser'@'<NFS-Server-Subnet CIDR-IP-Address>';
FLUSH PRIVILEGES;
SHOW DATABASES;
exit

![cd](./img/20_toolingdatabase.png)

![cd](./img/21_toolingdatabase2.png)

![cd](./img/22_toolingdatabase4.png)

![cd](./img/23_checkdatabase.png)

## Change the bind-address and mysqlx-bind-addresses to 0.0.0.0
sudo vi /etc/mysql/mysql.conf.d/mysqld.cnf

![cd](./img/24_changebindaddress.png)

## sudo systemctl restart mysql
sudo systemctl status mysql

![cd](./img/25_mysqlstatusrunning.png)

## Create a new web Instance

![cd](./img/26_webinstance.png)

## Verify that NFS was mounted successfully by running of df -h . Make sure that the changes will persist on Web Server after reboot:
sudo vi /etc/fstab

![cd](./img/27_sudofstab.png)

## Install Apache

![cd](./img/28_installapache.png)

## Install php remi's repo

![cd](./img/29_installphpremi'srepo.png)

![cd](./img/30_step4.png)

## Sudo Install git

![cd](./img/31_sudoinstallgit.png)

## git clone

![cd](./img/32_gitclone.png)

## git list

![cd](./img/33_gitlist.png)

![cd](./img/34_gitvi.png)

## Check the status to see if it's running

![cd](./img/35_systemctl.png)

## Create in MySQL a new admin user with username: myuser and password: password:

![cd](./img/36_mysql.png)

## Open the website in your browser
http://<Web-Server-Public-IP-Address-or-Public-DNS-Name>/index.php

![cd](./img/37_mysqloutput.png)

## The expected outcome

![cd](./img/38_mysqloutput2.png)













