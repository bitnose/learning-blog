+++
author = "Anniina Korkiakangas"
title = "Linux h7: Real Internet(tm)"
date = "2023-02-09"
description = "Apachen asentaminen Linuxiin."
tags = [
    "linux",
    "virtualmachine",
    "debian",
    "cloud",
    "domain",
    "web"
]
categories = [
    "themes",
    "syntax",
]
series = ["Themes Guide"]
aliases = ["migrate-from-jekyl"]
+++

## **Linux h8 Real Internet(tm)**
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


