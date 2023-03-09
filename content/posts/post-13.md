+++
author = "Anniina Korkiakangas"
title = "Linux 13: Hello world!"
date = "2023-03-09"
description = ""
tags = [
    "linux",
    "virtualmachine",
    "debian",
    "python",
    "java",
    "c++"
]
categories = [
    "themes",
    "syntax",
]
series = ["Themes Guide"]
aliases = ["migrate-from-jekyl"]
+++

## **Linux h13: Hello World**
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


## Write "Hello World" in tree language
**a) Käännä "Hei maailma" kolmella kielellä.**

The purpose is to set Linux up for three different programming language, and test them with simple Hello world program.

At first, I took a snapshot of vm and started it. **logged in** to vm and did the basic updates. I decided to use already existing box instead of creating a new one. 

    anniinak$ date
    anniinak$ whoami
    anniinak$ sudo apt-get update
    anniinak$ sudo apt-get -y dist-upgrade
    
I created a folder `Projects` in home directory.

    anniinak$ mkdir Projects/
    anniinak$ cd Projects/

## **Python** 

I decided to go with Python. I created a folder named `Python` inside `Projects` folder. Then I created new python file and added some code.

    anniinak$ mkdir Python
    anniinak$ micro helloworld.py

### **Hello world**

To checked if I had Python installed (which should be so). `-V` told the version. I found more information in the manual. Next I printed the content of file with cat and ran it. It didn't work at the first shot but so needed to modify the Python file because I made a typo. After fixing the typo, the program it ran like expected.

    anniinak$ python3 -V
    anniinak$ cat helloworld.py
    anniinak$ python3 helloworld.py 

{{< figure src="/img/h13/python.png" title="" width="600">}}

## **Java** 

### **Installation**
I read [this](https://www.digitalocean.com/community/tutorials/how-to-install-java-with-apt-on-debian-11) article to install java.

I installed default version of Java. It has two different components: The **JDK** - Java Developer Kit - and **JRE** Java Runtime Environment. JDK is a compiler for Java code.

I created a folder named `Java` inside `Projects`. 
I checked if the Java is installed. It wasn't so I installed it.

    # Install default JRE
    anniinak$ java -version
    anniinak$ sudo apt-get install default-jre
    anniinak$ java -version
    # Install default JDK
    anniinak$ sudo apt-get install default-jdk
    anniinak$ javac -version

The installation was successfull:

{{< figure src="/img/h13/java-version.png" title="" width="600">}}

### **Hello world**
Next, I created a Java program to test Java on Linux.

    anniinak$ mkdir /home/anniinak/Projects/Java
    anniinak$ cd /home/anniinak/Projects/Java
    anniinak$ micro HelloWorld.java
    anniinak$ cat HelloWorld.java

    # Compiles the code and creates a class for file
    anniinak$ javac HelloWorld.java 

    # Execute program
    anniinak$ java HelloWorld

{{< figure src="/img/h13/java.png" title="" width="600">}}

It worked!

## **Bash** 

Create a HelloWorld program in Bash. 

    # Version of Bash
    anniinak$ bash -version

    # New bash script
    anniinak$ mkdir /home/anniinak/Projects/Bash
    anniinak$ cd /home/anniinak/Projects/Bash
    anniinak$ micro helloworld.sh
    anniinak$ cat helloworld.sh
    anniinak$ bash helloworld.sh

{{< figure src="/img/h13/bash.png" title="" width="600">}}

## **Greetme program in Python**
b) Create a program that greets the user.

I created a program that greets the user. I created a new file in my Python folder in Projects.

    anniinak$ micro greetme.py
    anniinak$ ls
    anniinak$ cat greetme.py
    anniinak$ python3 greetme.py

{{< figure src="/img/h13/greetme.png" title="" width="600">}}

## **Greetme program in Bash**

    anniinak$ micro greetme.sh
    anniinak$ cat greetme.sh
    anniinak$ bash greetme.sh

{{< figure src="/img/h13/bash.png" title="" width="600">}}

