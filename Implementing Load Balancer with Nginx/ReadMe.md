# IMPLEMENTING LOAD BALANCING WITH NGINX

## Provision EC2 Instance
Open the AWS Console and create the instances

![1_name!](./img/1_Instancecreation.png)

## Open Port 8000, we will be running our webservers on port 8000 while the load balancers run port 80. we will need to open port 8000 to allow traffic from anywhere. To do this we need to add a rule to the security group of each of our webserver.
Click On the instance ID to get of your EC2 instances.
Load-balancer - Apache

![1_name!](./img/2_allowport8000.png)

Connect via ssh for both Servers
Apache 1

![1_name!](./img/3_sshconnect.png)

## Install Apache on both Webservers using the below commands;
sudo apt update -y

![1_name!](./img/4_script.png)
![1_name!](./img/5_installapacheonpub.png)

## sudo systemctl status apache2

![1_name!](./img/13_nginxrunning2.png)
![1_ec2connect.png!](./img/5_apacheisrunning.png)

## To configure Apache to serve content on port 8000.

Using the nano text editor, open the file/etc/apache2/ports.conf
sudo nano /etc/apache2/ports.conf 

![1_ec2connect.png!](./img/6_vimport80.png)

## On both servers, open the file /etc/apache2/sites-available/000-default.conf , and change port 80 on the virtualhost to 8000.
sudo nano /etc/apache2/sites-available/000-default.conf

![1_ec2connect.png!](./img/7_edittoport8000.png)

![1_ec2connect.png!](./img/9_publicipchange.png)

## A Welcome Web Browser Apache 1 & 2 Servers

![1_ec2connect.png!](./img/11_welcometoec2.png)

## Install Nginx
sudo apt update -y && sudo apt install nginx -y

![1_ec2connect.png!](./img/12_nginxinstall2.png)

## Verify Nginx is installed and working
sudo systemctl status nginx

![1_ec2connect.png!](./img/13_nginxrunning2.png)

## Open Nginx Configuration File
sudo nano /etc/nginx/conf.d/loadbalancer.conf

![1_ec2connect.png!](./img/14_nginxconfig.png)

## To test Configuration, Run
sudo nginx -t

![1_ec2connect.png!](./img/15_nginxtest.png)

## In the web browser paste the Ip-address of the Nginx load paste and hit enter.

THE RESULT
Load-balancer apache

![1_ec2connect.png!](./img/16_nginxdisplay.png)







