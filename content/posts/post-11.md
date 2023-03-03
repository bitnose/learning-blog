+++
author = "Anniina Korkiakangas"
title = "Linux 11: prod"
date = "2023-03-02"
description = ""
tags = [
    "linux",
    "virtualmachine",
    "debian",
    "cloud",
    "postgresql",
    "sql"
]
categories = [
    "themes",
    "syntax",
]
series = ["Themes Guide"]
aliases = ["migrate-from-jekyl"]
+++

## **Linux h11: prod**
- Based on Tero Karvinen 2023: [Linux Palvelimet 2023 alkukevät, ICI003AS2A-3002](https://terokarvinen.com/2023/linux-palvelimet-2023-alkukevat/).


## **Hands on**


**Host Machine**
- MacBook Pro Retina, 2015
- OS: macOS Big Sur 11.7
- Intel Core i7

**Virtual Box (local)**
- VM: debian-live-11.6.0-amd64-xfce-nonfree.iso
- Operating System: Debian (64-bit)
- Type: Linux
- Memory size: 4000 MB
- File size: 60 GB
- Hard disk file type: VDI

## **Install Django for production**

**a) Tee Djangon tuotantoasennus.** The goal is to install Django for production.

##### **17:20**

I read this tutorial: [Deploy Django 4 - Production Install](https://terokarvinen.com/2022/deploy-django/).

I **logged in** to my local linux box and did the basic updates. 

    anniinak$ sudo apt-get update
    anniinak$ sudo apt-get -y dist-upgrade

I created new directory and page for testing purposes.

    anniinak$ mkdir -p publicd/anni/static/   #at home dir
    anniinak$ echo "Hello world"|tee publicd/anni/static/index.html
        Hello world
    anniinak$ sudoedit /etc/apache2/sites-available/anni.conf
    anniinak$ sudo a2ensite anni.conf
    anniinak$ sudo a2dissite frontpage.conf
    anniinak$ sudo systemctl restart apache2
    anniinak$ cat /etc/apache2/sites-available/anni.conf
    anniinak$ curl http://localhost/static/

{{< figure src="/img/h11/start_1.png" title="" width="600">}}

I had already installed a virtual environment for Python, [the post is here](https://anniina-korkiakangas.netlify.app/posts/linux-10-dj-ango/). Next, I created a new virtual environment for the project. ``-p python3`` to install the modern and ``--system-site-packages env`` for python packages. 


    anniinak$ cd puclicd/
    anniinak$ virtualenv -p python3 --system-site-packages env
    anniinak$ source env/bin/activate
    env anniinak$ which pip

{{< figure src="/img/h11/virtualenv_2.png" title="" width="600">}}

    #Install Django
    env anniinak$ micro requirements.txt
    env anniinak$ pip install -r requirements.txt
    env anniinak$ django-admin --version

{{< figure src="/img/h11/django_3.png" title="" width="600">}}

Next, I created new project, to make everything correctly before I start to mess around with existing projects. 

    env anniinak$ django-admin startproject annik

I connected the project with Apache by modifying anni.config:

    env anniinak$ sudoedit /etc/apache2/sites-available/anni.conf

        Define TDIR /home/anniinak/publicd/annik
        Define TWSGI /home/anniinak/publicd/annik/annik/wsgi.py
        Define TUSER anniinak
        Define TVENV /home/anniinak/publicd/env/lib/python3.9/site-packages

        <VirtualHost *:80>
                Alias /static/ ${TDIR}/static/
                <Directory ${TDIR}/static/>
                        Require all granted
                </Directory>

                WSGIDaemonProcess ${TUSER} user=${TUSER} group=${TUSER} threads=5 python-path="${TDIR}:${TVENV}"
                WSGIScriptAlias / ${TWSGI}
                <Directory ${TDIR}>
                    WSGIProcessGroup ${TUSER}
                    WSGIApplicationGroup %{GLOBAL}
                    WSGIScriptReloading On
                    <Files wsgi.py>
                        Require all granted
                    </Files>
                </Directory>

        </VirtualHost>

        Undefine TDIR
        Undefine TWSGI
        Undefine TUSER
        Undefine TVENV


In config file, I needed to find the correct paths to directories so Apache can serve the files. 

- **TDIR** Directory for manage.py of Python project.
- **TWSGI** Path to wsgi.py file.
- **TUSER** The user.
- **TVENV** site-packages (for environment).

Next, I installed ``libapache2-mod-wsgi-py3`` which is a Apache WSGI module for Apache to read wsgi.py file. Didn't know how, but it worked! 

    env anniinak$ sudo apt-get -y install libapache2-mod-wsgi-py3
    env anniinak$ sudo systemctl restart apache2
    env anniinak$ curl -s localhost|grep title
    env anniinak$ curl -sI localhost|grep Server

{{< figure src="/img/h11/debug_5.png" title="" width="600">}}

Next, I disabled the debug so it would be more secure, and added localhost. 

    env anniinak$ cd publicd/annik/
    env anniinak$ micro annik/settings.py 

To load changes (to Apache), touch wsgi.py file and restart apache2:

    env anniinak$ touch annik/wsgi.py
    env anniinak$ sudo systemctl restart apache2

{{< figure src="/img/h11/debug_7.png" title="" width="500">}}

To make sure the debug is false, I opened the browser: 


{{< figure src="/img/h11/notfound_7.png" title="" width="600">}}


After all, it worked. Python is installed for production. 

