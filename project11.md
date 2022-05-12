# ANSIBLE CONFIGURATION MANAGEMENT
## INSTALL AND CONFIGURE ANSIBLE ON EC2 INSTANCE
> Update Name tag on your Jenkins EC2 Instance to Jenkins-Ansible. We will use this server to run playbooks.
> Instal Ansible
```
sudo apt update
sudo apt install ansible
ansible --version
```
> Configure Jenkins build job to save your repository content every time you change it
## BEGIN ANSIBLE DEVELOPMENT
> create a new branch in your github repository that will be used for development of a new feature

1. Setting the environment

Create a directory and name it playbooks – it will be used to store all your playbook files.
Create a directory and name it inventory – it will be used to keep your hosts organised.
Within the playbooks folder, create your first playbook, and name it common.yml
Within the inventory folder, create an inventory file (.yml) for each environment (Development, Staging Testing and Production) dev, staging, uat, and prod respectively.

2. Set up an Ansible Inventory
> Update your inventory/dev.yml file with this snippet of code