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

![1_name!](../img/6_lsblkinspect.png)
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

![1_name!](../img/14_newlyconfiguredpartitionview.png)

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



![1_name!](../img/21_updatefstab.png)


