# Ansible--AWS---Webserver

# 🧰 Ansible Setup on AWS EC2 (Control Node + 2 Clients)

This project demonstrates how to manually install and configure
**Ansible** on an AWS EC2 instance and use it to manage two additional
EC2 client servers.\
It includes directory setup, Ansible configuration, inventory files, and
connectivity testing.

------------------------------------------------------------------------

## 📌 Project Overview

-   Launch **3 EC2 instances**\
    ✔ 1 Ansible Control Node\
    ✔ 2 Client Nodes\
-   Instance Type: **t3.medium**\
-   Create & use **ansible.pem** key pair\
-   Install and configure Ansible manually\
-   Create inventory, playbook, and ansible.cfg\
-   Perform successful connectivity test using `ansible -m ping`

------------------------------------------------------------------------

## 🚀 Step 1: Launch EC2 Instances

You will need:

-   VPC\
-   Subnet\
-   Security Group allowing SSH (port 22)\
-   Key Pair: **ansible.pem**\
-   3 Instances (Amazon Linux 2)

------------------------------------------------------------------------

## 🖥️ Step 2: Login to Ansible Control Node

``` bash
ssh -i ansible.pem ec2-user@<ANSIBLE_SERVER_PUBLIC_IP>
```

------------------------------------------------------------------------

## ⚙️ Step 3: Install Ansible & Dependencies

``` bash
sudo yum update -y
sudo yum install python -y
sudo yum install pip -y
sudo pip install ansible
sudo yum install ansible.noarch -y
```

### ✔ Verify Versions

``` bash
python --version
pip --version
ansible --version
```

------------------------------------------------------------------------

## 📁 Step 4: Configure Ansible Directory Structure

``` bash
cd /etc/ansible
```

Create required folders/files:

``` bash
sudo touch ansible.cfg
sudo mkdir inventory
sudo touch inventory/hosts
sudo mkdir playbooks
sudo touch playbooks/ping.yml
sudo mkdir aws
sudo touch aws/ansible.pem
```

### Final Structure

    /etc/ansible
    ├── ansible.cfg
    ├── aws
    │   └── ansible.pem
    ├── inventory
    │   └── hosts
    ├── playbooks
    │   └── ping.yml
    └── roles

------------------------------------------------------------------------

## ⚙️ Step 5: Configure Ansible

``` ini
[defaults]
inventory = ./inventory
remote_user = ec2-user
private_key_file = aws/ansible.pem
host_key_checking = False
retry_files_enabled = False

[privilege_escalation]
become = true
become_method = sudo
become_user = root
become_ask_pass = false
```

------------------------------------------------------------------------

## 🧩 Step 6: Add Client IPs to Inventory

``` ini
[all]
100.25.43.133
44.192.38.38
```

------------------------------------------------------------------------

## 🧪 Step 7: Test Connectivity

``` bash
sudo ansible -m ping all
```

Expected response:

    100.25.43.133 | SUCCESS => {...}
    44.192.38.38 | SUCCESS => {...}

------------------------------------------------------------------------

## 🎉 Completed!

You have successfully:

✔ Installed Ansible\
✔ Configured ansible.cfg\
✔ Added hosts inventory\
✔ Verified connectivity between control node and clients

------------------------------------------------------------------------

## 📌 Optional Enhancements

I can also generate:

-   Terraform code for EC2 + VPC\
-   Architecture diagram (PNG)\
-   Production-ready playbooks\
-   GitHub badges & improved styling


