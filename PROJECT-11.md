# ANSIBLE CONFIGURATION MANAGEMENT

## Install and configure Ansible client to act as a Jump Server/Bastion Host 

Create an EC2 instance that will serve as ansible and jenkins server

Update the instance 

`sudo apt update`

![](images/2.png)

Install Ansible

`sudo apt install ansible`

![](images/3.png)

Check Ansible version 

`ansible --version`

![](images/4.png)

Install jenkins and verify its running 

![](images/5.png)

Create a github repository 

![](images/1.png)

Create a freestyle project "ansible" in jenkins and point it to a github repository 

![](images/6.png)

Configure a Post-build job to save all (**) files

Configure webhooks on github repo for the ansible-config-mgt repository 

![](images/7.png)

Test your setup by making some change in README.MD file

![](images/8.png)

Make sure the build starts automatically 

![](images/9.png)

Check if jenkins saved the build artifact on server 

`ls /var/lib/jenkins/jobs/ansible/builds/5/archive/`

![](images/10.png) 

Using VS code clone ansible-config-mgt repo to jenkins-ansible instance 

`git clone https://github.com/ladifa1/ansible-config-mgt.git`

In your ansible-config-mgt GitHub repository, create a new branch

Create a directory and name it playbooks 

Create a directory and name it inventory 

Within the playbooks folder, create common.yml

Within the inventory folder, create the following .yml files  dev, staging, uat, and prod respectively.

![](images/11.png)

![](images/12.png)

![](images/13.png)

![](images/14.png)

##  Set up an Ansible Inventory

Setup SSH agent and connect VS Code to your Jenkins-Ansible instance on your local machine

![](images/16.png)

Confirm the key has been added

`ssh-add -l`

SSH into your Jenkins-Ansible server using ssh-agent

`ssh -A ubuntu@public-ip`

![](images/17.png) 

Update your inventory/dev.yml file with code

![](images/18.png)

Update your playbooks/common.yml file

![](images/19.png)

Push changes and merge with Github main repo

![](images/20.png)

![](images/21.png)

![](images/22.png)

![](images/23.png)

![](images/24.png)

Confirm Jenkins build started automatically

![](images/25.png)

![](images/26.png)

check build artifacts on server

`ls /var/lib/jenkins/jobs/ansible/builds/7/archive/playbooks/common.yml`

![](images/27.png)

![](images/28.png)

## Run first Ansible test

Change directory to ansible-config-mgt

`cd ansible-config-mgt`

Execute ansible playbook

`ansible-playbook -i /var/lib/jenkins/jobs/ansible/builds/16/archive/invenotry/dev.yml /var/lib/jenkins/jobs/ansible/builds/16/archive/playbooks/common.yml`

![](images/30.png)

![](images/31.png)

![](images/32.png)

Check each of the servers to see if wireshark has been installed

![](images/33.png)

![](images/34.png)

![](images/35.png)
