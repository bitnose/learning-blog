+++
author = "Anniina Korkiakangas"
title = "Linux 10: DJ Ango"
date = "2023-02-16"
description = "PostgreSQL on Linux"
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

## **Linux h10: DJ Ango**
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

## **Build database application with Django**

**a) Kannattavaa.** Tee oma tietokantasovellus. jossa on weppiliittymä. Kirjautuneet käyttäjät saavat lisätä, muokata ja poistaa tietueita. 

##### **Started at 17:00**

I read this tutorial: [Django instant crm tutorial](https://terokarvinen.com/2022/django-instant-crm-tutorial/) and opened the documention of [Django](https://docs.djangoproject.com/en/4.1/) to read about the framework. I know the basics of Python language (did Python Programming course recently), but I've never used Django before. 

I **logged in** to my local linux box and did the basic updates. 

    anniinak$ sudo apt-get update
    anniinak$ sudo apt-get -y dist-upgrade

First I **installed tool for development environment.** The manual tells it's Python environment creator. I checked the version. 

    anniinak$ sudo apt-get -y install virtualenv
    anniinak$ man virtualenv
    anniinak$ virtualenv --version

**Installed a new virtual environment**, and installed Python packages into env/ folder. Launched new virtual env.

    anniinak$ virtualenv --system-site-packages -p python3 env/
    anniinak$ source env/bin/activate

Inside the virtual env, I passed commands to **install Django**. I had already micro editor installed.  

    env anniinak$ which pip
    env anniinak$ micro requirements.txt 
    env anniinak$ cat requirements.txt
        django
    env anniinak$ pip install - requirements.txt
    env anniinak$ django-admin --version
        4.1.7
    env anniinak$ pip show Django

{{< figure src="/img/h10/django.png" title="" width="600">}}

## **Creating a website project with Django**
##### 17:30

**Created a new website project** and ran it: 

    env anniinak$ django-admin startproject anniinak
    env anniinak$ cd anniinak
    env anniinak$ ./manage.py runserver

Tested on the browser:

{{< figure src="/img/h10/testpage.png" title="" width="600">}}

I pressed CTRL-C to exit back to the command line. 
I **created a new admin user** for the project. Before I installed a password generater (which claims to generate humanfriendly passwords...). 

    env anniinak$ sudo apt-get install pwgen
     ******password****
    env anniinak$ pwgen -s 20 1
    env anniinak$ ./manage.py createsuperuser

I headed to 127.0.0.1:8000/admin but the server didn't respond. I run again the command to start the server but it hit an error, saying the address is already in use. The solution is simple, I checked which process is using the port 8000 and then kill that process.

    env anniinak$ cd anniinak
    env anniinak$ ./manage.py runserver

    env anniinak$ lsof -i:8080
    env anniinak$ kill -9 <pid>

{{< figure src="/img/h10/bug.png" title="" width="600">}}

    env anniinak$ ./manage.py runserver

**It worked.** I loged in to the admin panel, and played aroud: created user, deleted, etc. 

{{< figure src="/img/h10/admin.png" title="" width="600">}}

## **Create new database (for book records!)**

I wanted to make a database for book records. 

    env anniinak$ ./manage.py startapp library
    env anniinak$ micro anniinak/settings.py
    
Added a new line to install the app:

{{< figure src="/img/h10/library.png" title="" width="600">}}

Created a new **model** with a name column for the books: 

    env anniinak$ micro library/models.py

        from django.db import models

        class Book(models.Model):
            name = models.CharField(max_length=300)


**Migrated** the changes and **registered** the database to admin: 

    env anniinak$ ./manage.py makemigrations
    env anniinak$ ./manage.py migrate
    env anniinak$ micro library/admin.py

        from django.contrib import admin
        from . import models

        admin.site.register(models.Book)

    env anniinak$ ./manage.py runserver

I **tested** on the borwser, logged into admin panel and found the access to the books. Played around - removed, added and updated book records. Updated file to fix the naming of records to include the book name to title when the records are listed:

    env anniinak$ micro library/models.py

Book database is done! Ready for more... 

{{< figure src="/img/h10/books.png" title="" width="600">}}

## **b) Many-to-one relationship**


