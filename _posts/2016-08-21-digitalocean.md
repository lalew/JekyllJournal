---
layout: post
title: DigitalOcean
date:   2016-08-21
tags: [Digital Ocean, Server]
---
Todo: LAMP and Seperate Server Deployment
<!-- More -->

#Topic 1: LAMP on Ubuntu 16.04

# 1. Installing Apache
```shell
sudo apt-get update  
sudo apt-get install apache2

sudo ufw app list  
sudo ufw app info "Apache Full"

**Allows incoming traffic**  
sudo ufw allow in "Apache Full"

http://your_server_IP_address

Public IP Address  
ip addr show eth0 | grep inet | awk '{ print $2; }' | sed 's/\/.*$//'

sudo apt-get install curl  
curl http://icanhazip.com
```

# 2. Installing MySQL
```shell
sudo apt-get install mysql-server  
sudo mysql_secure_installation

VALIDATE PASSWORD PLUGIN can be used to test passwords
and improve security. It checks the strength of password
and allows the users to set only those passwords which are
secure enough. Would you like to setup VALIDATE PASSWORD plugin?

Press y|Y for Yes, any other key for No:

No -> Allows Weak Passwords <- **Choose This**

For the rest of the questions, you should press Y and hit the Enter key at each prompt. This will remove some anonymous users and the test database, disable remote root logins.  
```

# 3. Installing PHP
```shell
sudo apt-get install php libapache2-mod-php php-mcrypt php-mysql

//Setting priority of index.php over index.html
sudo nano /etc/apache2/mods-enabled/dir.conf

/etc/apache2/mods-enabled/dir.conf
<IfModule mod_dir.c>
    DirectoryIndex index.html index.cgi index.pl index.php index.xhtml index.htm
</IfModule>
<IfModule mod_dir.c>
    DirectoryIndex index.php index.html index.cgi index.pl index.xhtml index.htm
</IfModule>

sudo systemctl restart apache2
sudo systemctl status apache2
```

## 3.1 PHP Modules
```shell
apt-cache search php- | less
apt-cache show package_name

sudo apt-get install package1 package2 ...
```

# 4 Testing PHP on Web Server
```shell
/var/www/html/
sudo nano /var/www/html/info.php

<?php
phpinfo();

http://your_server_IP_address/info.php

sudo rm /var/www/html/info.php
```

# Topic 2: Setting Up Virtual Hosts (Multiple Websites on one Server) - Reference
https://www.digitalocean.com/community/tutorials/how-to-set-up-apache-virtual-hosts-on-ubuntu-14-04-lts


# Server Setup on Ubuntu
https://www.digitalocean.com/community/tutorials/initial-server-setup-with-ubuntu-14-04

# 1. Root Login
ssh root@SERVER_IP_ADDRESS

# 2. Create New User
adduser demo

# 3. Root Privileges
gpasswd -a demo sudo

# 4. Public Key Auth
ssh-keygen

This generates a private key, id_rsa, and a public key, id_rsa.pub, in the .ssh directory of the localuser's home directory. Remember that the private key should not be shared with anyone who should not have access to your servers!

# 4.1 Copy your public Key via ssh-copy-id
ssh-copy-id demo@SERVER_IP_ADDRESS

your public key will be added to the remote user's .ssh/authorized_keys file


# 4.2 Copy your public Key Manually

cat ~/.ssh/id_rsa.pub
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDBGTO0tsVejssuaYR5R3Y/i73SppJAhme1dH7W2c47d4gOqB4izP0+fRLfvbz/tnXFz4iOP/H6eCV05hqUhF+KYRxt9Y8tVMrpDZR2l75o6+xSbUOMu6xN+uVF0T9XzKcxmzTmnV7Na5up3QM3DoSRYX/EP3utr2+zAqpJIfKPLdA74w7g56oYWI9blpnpzxkEd3edVJOivUkpZ4JoenWManvIaSdMTJXMy3MtlQhva+j9CgguyVbUkdzK9KKEuah+pFZvaugtebsU+bllPTB0nlXGIJk98Ie9ZtxuY3nCKneB+KjKiXrAvXUPCI9mWkYS/1rggpFmu3HbXBnWSUdf localuser@machine.local

On Server
su - demo
mkdir .ssh
chmod 700 .ssh
nano .ssh/authorized_keys
--> Insert Public Key <--
chmod 600 .ssh/authorized_keys

# 5. Configure SSH Daemon

nano /etc/ssh/sshd_config

/etc/ssh/sshd_config (before)
PermitRootLogin no

# 6. Reload SSH
service ssh restart
ssh demo@SERVER_IP_ADDRESS


# Automatic Deployment with Git
https://www.digitalocean.com/community/tutorials/how-to-set-up-automatic-deployment-with-git-with-a-vps

Your server live directory: /var/www/domain.com

Your server repository: /var/repo/site.git

# Server
Repo:
cd /var
mkdir repo && cd repo
mkdir site.git && cd site.git
git init --bare

Hooks:
From Repo:
cd hooks
cat > post-receive
Inside post-receive:
#!/bin/sh
git --work-tree=/var/www/domain.com --git-dir=/var/repo/site.git checkout -f
Ctrl+D to Save
chmod +x post-receive

# Local Machine
cd /my/workspace
mkdir project && cd project
git init

git remote add live ssh://user@mydomain.com/var/repo/site.git

git add .
git commit -m "My project is ready"
git push live master

# Beta Directory
cd /var/www/
mkdir beta

cd /var/repo
mkdir beta.git && cd beta.git
git init --bare

cd hooks
cat > post-receive
Inside File:
#!/bin/sh
git --work-tree=/var/www/beta --git-dir=/var/repo/beta.git checkout -f

chmod +x post-receive

exit
cd /my/workspace/project

git remote add beta ssh://user@mydomain.com/var/repo/beta.git

git add .
git commit -m "New version"
git push beta master

git push live master

# Going Live from Server

cd /var/repo/beta.git
git remote add live ../site.git

// From Beta to Live
cd /var/repo/beta.git
git push live master

