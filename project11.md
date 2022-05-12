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
```
[nfs]
<NFS-Server-Private-IP-Address> ansible_ssh_user='ec2-user'

[webservers]
<Web-Server1-Private-IP-Address> ansible_ssh_user='ec2-user'
<Web-Server2-Private-IP-Address> ansible_ssh_user='ec2-user'

[db]
<Database-Private-IP-Address> ansible_ssh_user='ec2-user' 

[lb]
<Load-Balancer-Private-IP-Address> ansible_ssh_user='ubuntu'
```
3. Create a Common Playbook
> Update your playbooks/common.yml file with following code
```
---
- name: update web, nfs and db servers
  hosts: webservers, nfs, db
  remote_user: ec2-user
  become: yes
  become_user: root
  tasks:
    - name: ensure wireshark is at the latest version
      yum:
        name: wireshark
        state: latest

- name: update LB server
  hosts: lb
  remote_user: ubuntu
  become: yes
  become_user: root
  tasks:
    - name: Update apt repo
      apt: 
        update_cache: yes

    - name: ensure wireshark is at the latest version
      apt:
        name: wireshark
        state: latest
```
> Commit your new branch to Github and create a pull request into master branch. 

4. Run first Ansible test
```
ansible-playbook -i inventory/dev.yml playbooks/common.yml
```
> You can go to each of the servers and check if wireshark has been installed by running which wireshark or git
> You should have the following result:




