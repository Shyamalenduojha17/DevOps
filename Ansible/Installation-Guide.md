## Install Ansible on Ubuntu Operating System
```
$ sudo apt update -y
$ sudo apt install software-properties-common
$ sudo add-apt-repository --yes --update ppa:ansible/ansible
$ sudo apt install ansible -y
```

## Setup Ansible Master and Slave Architecture

### On Master Server
1. Generate a SSH Key:
   ```
   $ ssh key-gen
   ```
2. Copy Public key:
   ```
   $ cd .ssh/
   $ ls
   $ sudo cat id_rsa.pub
   ```
3. Add/Paste Slave Servers Private IP Address on Host file of Ansible Master
   ```
   $ sudo cd etc/ansible
   $ ls
   $ sudo nano hosts
   ```
    
### On Slave Server

   Paste public key of Master server in .ssh/authorized_keys on Slave servers
   ```
   $ cd .ssh/
   $ sudo nano authorized_keys
   ```
