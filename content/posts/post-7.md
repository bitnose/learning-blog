+++
author = "Anniina Korkiakangas"
title = "Linux 7: Real Internet(tm)"
date = "2023-02-09"
description = ""
tags = [
    "linux",
    "virtualmachine",
    "debian",
    "cloud",
]
categories = [
    "themes",
    "syntax",
]
series = ["Themes Guide"]
aliases = ["migrate-from-jekyl"]
+++

## **Linux h7: Real Internet(tm)**
- Perustuu Tero Karvinen 2023: [Linux Palvelimet 2023 alkukevät, ICI003AS2A-3002](https://terokarvinen.com/2023/linux-palvelimet-2023-alkukevat/).

#### **x) Summary** 

[Karvinen 2012: First Steps on a New Virtual Private Server – an Example on DigitalOcean and Ubuntu 16.04 LTS](https://terokarvinen.com/2017/first-steps-on-a-new-virtual-private-server-an-example-on-digitalocean/)

- How to install virtual private (cloud) server and take the firts steps to configure it remotely
- Use only good passwords, always
- Keep your programs up to date (apt-get upgrade)

**Login** to server and setting up the password:

    local$ ssh root@<SERVER_IP-ADRRESS_HERE!> 

**Setting up the firewall** (ufw) to allow the traffic through the port 22 for now

    server$ sudo ufw allow 22/tcp 
    server$ sudo ufw enable

**Creating a new user** with the sudo rigths and login

    server$ sudo adduser anniina
    server$ sudo adduser anniina sudo
    server$ sudo adduser anniina adm
    server$ sudo adduser anniina admin
    local$ ssh anniina@<SERVER_IP-ADRRESS_HERE!>

**Locking** the root account

    server$ sudo usermod --lock root
    server$ sudoedit /etc/ssh/sshd_config
        PermitRootLogin no
    server$ sudo service ssh restart

**Update the packages**: sudo apt-get update, sudo apt-get -y dist-upgrade.

**Start using it!**
- If want tp install Apache, open the port 80 for the web traffic 
- Add a domain name 

## **Linux: Hands on**

**a) Renting a virtual private cloud** 

During the previous lesson, I rented some virtual private cloud from Linode with free credits. I created an account and followed the given intstructions and finally selected the server with this gear:

**Host Machine:**
- MacBook Pro Retina, 2015
- OS: macOS Big Sur 11.7
- Intel Core i7

**Server** 
- Debian 11 Image
-  (should be more than enough)
- Region: Frankfurt, DE
- Linode Plan > Shared CPU > 1 GB RAM (Nanode)
- 5$/month

I could find more information and analytics about the server on the Linode's cloud console. 

**Opening a remote connection**

I opened a local terminal to connect to the server. 

    local$ ssh root@<SERVER_IP-ADRRESS_HERE!>

The connection was established successfully. Though, it gave a warning that complains about local settings because of the unknown environment variables ($LC and $LANG). I deciced to take care of this after doing the first steps. 

{{< figure src="/img/h7/warning.png" title="" width="600">}}

**b) First steps:** Firewall, close root access, updates

**Setting up firewall**

Next, I updated the packages and set up the firewall. I didn't have the ufw packages so I installed it:

    root$ sudo apt-get update
    root$ sudo apt-get -y dist-upgrade
    root$ sudo apt-get install ufw
    root$ man ufw
    root$ sudo ufw allow 22/tcp 
    root$ sudo ufw enable
    root$ sudo ufw status


**New user and disabling sudo**

The firewall was set up . I created a new user with the following commands:

    root$ sudo adduser anniina
    root$ sudo adduser anniina sudo
    root$ sudo adduser anniina adm
    root$ sudo adduser anniina admin

After the last command, it prompted "The group 'admin' does not exist." I checked the manual about adduser: didn't find a command to list all the groups. I tried to find if the group named "admin" exists and got no hits. 

    root$ less /etc/group
    root$ less /etc/group|grep admin

I wasn't sure what's the goal of the **sudo adduser anniina admin** command. 

I tried to **login with the new user** from the local machine. It worked.

    local$ ssh anniina@<IP>

Next, back to the root connection, I disabled the root access and edited sshd_config file. 

    root$ sudo usermod --lock root
    root$ sudoedit /etc/ssh/sshd_config

Found the line with PermitRootLogin, and updated it with **no** like this:

{{< figure src="/img/h7/permit.png" title="" width="600">}}

Restarted the ssh service and quited the session with root:

    root$ sudo service ssh restart
    root$ exit

**c) Install a webservice on your machine.** Replace the test page. Check if it works online. Open a port in the firewall. 

I installed apache2, and checked it works:

    anniina$ sudo apt-get -y install apache2
    anniina$ sudo systemctl start apache2
    anniina$ curl http://localhost/

It worked. Changed the example site and created a site for the user: 

    anniina$ echo "Hello"|sudo tee /var/www/html/index.html 
    anniina$ sudo a2enmod userdir
    anniina$ sudo systemctl restart apache2
    anniina$ curl http://localhost/
    Hello
    
    anniina$ sudoedit /etc/apache2/sites-available/frontpage.conf
    anniina$ cat /etc/apache2/sites-available/frontpage.conf 
    anniina$ sudo a2ensite frontpage.conf
    anniina$ sudo a2dissite 000-default.conf
    anniina$ sudo systemctl restart apache2

    anniina$ cd; pwd;
    anniina$ mkdir sites_available
    anniina$ touch index.html
    anniina$ nano index.html
    anniina$ cat index.html

Opened the port 80 to make the site accessible for outsiders (over Internet): 

    anniina$ sudo ufw allow 80/tcp

For some reason, the site still showed 403 forbidden when I tried to access the front page curl http://localhost/ and through IP address. I tried to restart but it didn't help. 

**UPDATE:**

The mistake was that I had a mismatch with the path name in the frontpage.conf file and folder name. I corrected it by creating a corresponding folder (public_sites) and adding the correct, matching path in frontpage.conf file.

{{< figure src="/img/h7/final.png" title="" width="600">}}

{{< figure src="/img/h7/final_terminal.png" title="" width="600">}}
    
d) Etsi merkkejä murtautumisyrityksistä.

In the /var/log/auth.log file I found lines like this but with different IP addresses. A little disclaimer, it could be me making typos. 

    Feb  9 11:41:53 localhost sshd[7430]: pam_unix(sshd:auth): authentication failure; logname= uid=0 euid=0 tty=ssh ruser= rhost=103.138.71.242 

    anniina$ cat /var/log/auth.log|grep --color invalid
 

### **UPDATE: Fixing locale error**

{{< figure src="/img/h7/locale_error.png" title="" width="600">}}

According this [post](https://askubuntu.com/questions/599808/cannot-set-lc-ctype-to-default-locale-no-such-file-or-directory) and the top voted answer, the problem arises because MacOS sends automatically some locale [environment variables](https://help.ubuntu.com/community/EnvironmentVariables) to configure the environment for the selected character encoding when connecting to Linux over ssh. This causes the conflict between variables. I fixed it easily on my macOS by: 

- Terminal>Preferences>Profiles>Advanced tab
- **Unchek** the box with "Set locale..."

{{< figure src="/img/h7/locale.png" title="" width="600">}}

I closed the session and opened the new one to see if the change was effective: 

It worked. Locale conflict solved. 

{{< figure src="/img/h7/locale_end.png" title="" width="600">}}

Sources: 
- https://help.ubuntu.com/community/EnvironmentVariables,
- https://askubuntu.com/questions/599808/cannot-set-lc-ctype-to-default-locale-no-such-file-or-directory
- Earlier homework posts
