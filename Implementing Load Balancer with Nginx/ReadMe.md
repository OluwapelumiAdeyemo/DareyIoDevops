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

![1_name!](./img/6_scriptrun.png)

##

