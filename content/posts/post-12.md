+++
author = "Anniina Korkiakangas"
title = "Linux 12: Debug"
date = "2023-03-06"
description = ""
tags = [
    "linux",
    "virtualmachine",
    "debian",
    "python",
    "django",
    "debugging"
]
categories = [
    "themes",
    "syntax",
]
series = ["Themes Guide"]
aliases = ["migrate-from-jekyl"]
+++

## **Linux h12: debug**
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

# 

## **Debugging Django & Apache: Start**

The purpose of the homework is to cause problmes to debug in Django production installation. 

I **logged in** to my local linux box and did the basic updates. I've already installed Django for production (previous post). I activated environment, checked the pip and started apache2. I tested everything is working properly on the browser.

    anniinak$ sudo apt-get update
    anniinak$ sudo apt-get -y dist-upgrade
    anniinak$ cd publicd/
    anniinak$ source env/bin/activate

    env anniinak$ which pip
    env anniinak$ sudo systemctl restart apache2

{{< figure src="/img/h12/debug_01.png" title="" width="600">}}

It worked. I took a snapshot of VM and I started to cause some problems.

#

### **Problem a) Typo in a Python file.** 


**1. Cause the problem**

    env anniinak$ cd publicd/annik/
    env anniinak$ cat annik/settings.py
    env anniinak$ micro annik/settings.py 

{{< figure src="/img/h12/debug_02.png" title="" width="600">}}

I made a typo on this line in setting.py file, removed p at the end of the line. Then I touched wsgi.py file to load changes to Apache: 

    env anniinak$ touch annik/wsgi.py

**2. Show the symptoms**

The problem in action: 

    env anniinak$ curl -sI localhost|grep Server 

{{< figure src="/img/h12/debug_03.png" title="" width="600">}}

The same results on browser. It gave `500: Internal Server Error` response.

{{< figure src="/img/h12/debug_04.png" title="" width="600">}}

**3. Locate the logs**

First, I checked the error logs files of Apache:

    env anniinak$ sudo tail /var/log/apache2/error.log.1
    env anniinak$ sudo tail /var/log/apache2/error.log.1|grep -w --color setting.py
    env anniinak$ sudo tail /var/log/apache2/error.log.1|grep -w --color parent

{{< figure src="/img/h12/debug_05.png" title="" width="600">}}

**4. Analyze the logs**

- `[Mon Mar 06 11:48:27.789238]` Timestamp of the log, date and time. Answers question when.  
- `wsgi` The module that produced the error. In this case it was the wsgi module to my understanding. `error` means the type of event. 
- `pid` The process id or identfier: Which process was interrupted.
- `tid` The thread id or identifier: Which thread.
- `client` The address and the port number. In this case the client was localhost and the port 45090. 
- The rest of the log file is the `message`. It tells the path to the file where the error was, which line. The second log contains the content of line which has the typo. The third log told that the error was `AttributeError` and precisely what's wrong, in this case `paren`. 

##### Sources: https://httpd.apache.org/docs/2.4/mod/core.html#errorlogformat

**5. Fix the problem**

I fix the problem by editing the settings.py file and reloading the changes to apache2. 

    env anniinak$ micro annik/settings.py 
    env anniinak$ touch annik/wsgi.py

The edited line: 

{{< figure src="/img/h12/debug_07.png" title="" width="600">}}

**6. Proof of solution**
    
The site worked correctly.

{{< figure src="/img/h12/debug_06.png" title="" width="600">}}

The server was ran by Apache: 

{{< figure src="/img/h12/debug_08.png" title="" width="600">}}

#

### **Problem b) Django project in wrong location.** 
The project folder is the one containing manage.py file.

**1. Cause the problem**

I created a new folder named wrong_public in user's home dir, located the manage.py file and the project. Then I moved the project (still the one containing manage.py) to `wrong_public` folder

{{< figure src="/img/h12/debug_09.png" title="" width="600">}}

**2. Show the symptoms**

Apache2 was still running:

{{< figure src="/img/h12/debug_10.png" title="" width="600">}}

**3. Locate the logs**

Vm crashed so I needed to start it again. I checked the access logs at first. To my understanding, the error log should be forbidden like it was on the browser. 

    env anniinak$ sudo tail /var/log/apache2/access.log.1

{{< figure src="/img/h12/debug_11.png" title="" width="600">}}

**4. Analyze the logs**

- `127.0.0.1.` IP-address of the request (client)
- `[Mon Mar xx xx:xx.xxxxxx]` Timestamp of the log, date and time, timezone. Answers question when.
- `GET / ` The client made the get request to ask index.html file in given directory.
- `HTTP/1.1` The protocol which was used.
- `404` HTTP response from Apache. Means the request was Forbidden. 
- `409` The size of the response. 
- The rest tells the User Agent, which browser was used to make the request. In case, it was Mozilla Firefox on Linux.

The log means that the GET request made and the response was forbidden because the Apache doesn't have the access to requested the files anymore because the project lives in different directory. 

**5. Fix the problem**

I moved the project back to the original location, which is publicd folder, the same folder where the env files and packages are, static files and requirements.txt file.

{{< figure src="/img/h12/debug_12.png" title="" width="600">}}

It showed Internal Server Error. Hence I tried to restart  Apache. 

**6. Proof of solution**

After restarting Apache, I made the test again on the browser: 

{{< figure src="/img/h12/debug_13.png" title="" width="600">}}

It worked!

#

### **Problem c) No access to the project folder.** 

**1. Cause the problem**

The django project lives inside publicd/annik/ folder in home directory. First, I removed the read, write and execute rights from the user, group and others. The command is not recursive, meaning it doesn't change the permits of each file and folder inside. To my understanding, they stayed intack.

    env anniinak$ cd publicd/
    env anniinak$ chmod ugo-rwx annik/

**2. Show the symptoms***

Next, I tried to see if any changes has happened by going localhost/admin:

{{< figure src="/img/h12/debug_14.png" title="" width="600">}}

This means the apache is still running but it doesn't have the access to requested file. It showed the same symptom as in problem b) so I knew where to look for logs. 

**3. Locate the logs**

I checked the access logs but there was nothing interesting. Next, I checked the error log. 

**4. Analyze the logs**

{{< figure src="/img/h12/debug_15.png" title="" width="600">}}

- `[Weekday MM DD hh:mm:ss.msms yyyy]` Timestamp of the log, date and time. Answers question when.  
- `core` The module that produced the error. In this case it was the core module. `error` means the type of event. 
- `pid` The process id or identfier: Which process was interrupted.
- `tid` The thread id or identifier: Which thread.
-  `(13)Permission denied` What was the problem
- `client` The address and the port number. 

The log told that there is a problem with accessing the project files. 

**5. Fix the problem**

I tried to fix the problem by modifying access to the Django project. Add read and write access to the user for annik folder.

    env anniinak$ chmod u+rx annik/

I didn't work, still showed the same error. Next, I checked the permissions of the files and folders to understand what was going on. I still needed to modify the permissions. At this point, I asked helped from my better (at least in Linux) half who knows the Linux like his own pockets.

To elaborate what I learnt: 

    env anniinak$ cd publicd/
    env anniinak$ mkdir toto 
    env anniinak$ ls -al  # To list files and accesses
    env anniinak$ chmod ugo-rwx toto/ # Remove all
    env anniinak$ ls -al

{{< figure src="/img/h12/toto_1.png" title="" width="600">}}

I added read and execute access for user:

    env anniinak$ chmod u+rx toto 

{{< figure src="/img/h12/toto_02.png" title="" width="600">}}

To update all the rights like they were originally:

    env anniinak$ chmod u+rwx toto
    env anniinak$ chmod go+rx toto

{{< figure src="/img/h12/toto_3.png" title="" width="600">}}

So I had to apply the same logic for the project folder as the example folder.

    env anniinak$ chmod u+rwx annik/
    env anniinak$ chmod go+rx annik/

{{< figure src="/img/h12/toto_04.png" title="" width="600">}}

**6. Proof of solution**

    env anniinak$ curl localhost/admin/

After updating the access rights, I made a test on browser: 

{{< figure src="/img/h12/toto_5.png" title="" width="600">}}

#

### **d) Typo in** /etc/apache2/sites-available/anni.conf (Apache config file)

**1. Cause the problem**

First I edited the file:

    env anniinak$ sudoedit /etc/apache2/sites-available/anni.conf
    env anniinak$ sudo systemctl start apache2

**2. Show the symptoms***

Apache2 didn't start. I checked the browser but got "unable to connect" page. The problem was caused.

    env anniinak$ sudo systemctl status apache2

{{< figure src="/img/h12/conf_02.png" title="" width="600">}}

Checking the status message showed the problem (syntax error, the file, the line number).
I checked syntax:

    env anniinak$ /sbin/apache2ctl configtest

{{< figure src="/img/h12/conf_03.png" title="" width="600">}}

**3. Locate the logs**

I couldn't find much in `/var/log/apache2/` log files. Instead, there was lots of logs in `/var/log/syslog/`: 

    env anniinak$ sudo tail /var/log/syslog

I guess this was the log. 

{{< figure src="/img/h12/conf_04.png" title="" width="600">}}

**4. Analyze the logs**

According the logs, Apache wasn't able to start because of the syntax error, a missinf >, on line 255 in anni.conf file. Pretty straight forward. 

**5. Fix the problem**

The solution was already proposed when running status or just config check.

    env anniinak$ sudoedit /etc/apache2/sites-available/anni.conf
    env anniinak$ /sbin/apache2ctl configtest
    env anniinak$ sudo systemctl restart apache2

**6. Proof of solution**

Tested on browser, and it worked:

{{< figure src="/img/h12/conf_05.png" title="" width="600">}}

e) Apachen WSGI-moduli puuttuu ('sudo apt-get purge libapache2-mod-wsgi-py3' tms)

**1. Cause the problem**
**2. Show the symptoms***
**3. Locate the logs**
**4. Analyze the logs**
**5. Fix the problem**
**6. Proof of solution**


f) Väärät domain-nimet ALLOWED_HOSTS-kohdassa (settings.py, ja DEBUG=False)

**1. Cause the problem**
**2. Show the symptoms***
**3. Locate the logs**
**4. Analyze the logs**
**5. Fix the problem**
**6. Proof of solution**








e) Vapaaehtoinen bonus: oma, itse keksitty ongelma.