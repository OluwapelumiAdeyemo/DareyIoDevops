## Install and configure ansible on ec2 instance
Install and Configure Ansible on EC2 Instance

![1_name!](../img/1_Instance.png)

## Create a new repository called ansible-config-mgt in your GitHub account.
![1_name!](../img/2_ansibleconfig.png)

## Update the Name tag on your Jenkins EC2 Instance to Jenkins-Ansible. This server will be used to run playbooks.
Install Ansible on the Jenkins-Ansible server.

![1_name!](../img/2_ansibleinstallation.png)

## To check for ansible version
![1_name!](../img/3_ansibleversion.png)

## In order to access ansible through the web browser, go to your EC2 instance inbound rule and open TCP port 8080, IPV4 anywhere

![1_name!](../img/4_port8080.png)

## It is important to note that Jenkins wont work until Java is installed, hence, we need to install Java language before you can use Jenkins

![1_name!](../img/5_javainstall.png)

## To confirm that java is running

![1_name!](../img/6_javaisrunning.png)

![1_name!](../img/7_javarun2.png)

## Install Jenkins

![1_name!](../img/8_jenkinsinstall.png)

## To check Jenkins Status

![1_name!](../img/9_jenkinsstatus.png)

## Check with the url

![1_name!](../img/10_jenkinsurl.png)

## Set the default password

![1_name!](../img/11_jenkinspassword.png)

## Check the output

![1_name!](../img/12_jenkinsoutput.png)

![1_name!](../img/13_jenkinslogin.png)

![1_name!](../img/14_jenkins3.png)

![1_name!](../img/15_jenkins4.png)

## Login to Jenkins

![1_name!](../img/16_jenkinslogin.png)

![1_name!](../img/17_jenkinsproject.png)

![1_name!](../img/18_jenkinsgeneral.png)

![1_name!](../img/19_jenkinsmain.png)

![1_name!](../img/21_jenkinstrigger.png)

## Configure Jenkins build job to archive your repository content every time you change it.

![1_name!](../img/22_ansiblebuild.png)

![1_name!](../img/23_firstansible.png)

## Configure a Post-build job to save all (**) files.
Configure a webhook in GitHub and set the webhook to trigger ansible build.

![1_name!](../img/25_webhook.png)

## Create a playbooks (i.e. used to store all the playbook files) and inventory (i.e. used to keep your hosts organized) directory.

![1_name!](../img/27_ansibleplaybook.png)

![1_name!](../img/28_wireshark.png)

![1_name!](../img/29_updatewitlatest.png)

![1_name!](../img/30_mergepull.png)

![1_name!](../img/31_firstansible.png)

## se the Ansible Adhoc command to check if wireshark has been installed on the servers.
ansible webservers -i inventory/dev -m command -a "wireshark --version"

![1_name!](../img/32_wireshark.png)

![1_name!](../img/33_wiresharkversion.png)

![1_name!](../img/34_ansiblearchitecture.png)























