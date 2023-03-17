+++
author = "Anniina Korkiakangas"
title = "Linux 14"
date = "2023-03-17"
description = ""
tags = [
    "linux",
    "virtualmachine",
    "debian",
]
categories = [
    "themes",
    "syntax",
]
series = ["Themes Guide"]
aliases = ["migrate-from-jekyl"]
+++

## **Linux h14**
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

## **Bash** 

Create a program in Bash for multiple users.

    # A new bash script I created
    anniinak$ cd /home/anniinak/Projects/Bash
    anniinak$ micro dateis

Here is the content: 

    #!/usr/bin/bash

    echo "TODAY"
    date
    whoami
    pwd

I tested the program:

    anniinak$ cat dateis
    anniinak$ bash dateis

I copied the file to /usr/local/bin/.

    anniinak$ sudo cp dateis /usr/local/bin/
    anniinak$ cd /usr/local/bin/

I Updated the rights so user, group and others can read and execute the file.

    anniinak$ ls -la
    anniinak$ chmod ugo+rx dateis
    anniinak$ ls -la
    anniinak$ cd
    anniinak$ dateis

I created a program to list all files and rights.

    # New bash script
    anniinak$ cd /home/anniinak/Projects/Bash
    anniinak$ micro ll

    #!/usr/bin/bash
    ls -al

    # Test the program
    anniinak$ cat ll
    anniinak$ bash ll

    # Copy the file to /usr/local/bin/
    anniinak$ sudo cp ll /usr/local/bin/
    anniinak$ cd /usr/local/bin/

    # Update the rights so user, group and others can read and execute the file.
    anniinak$ ls -la
    anniinak$ chmod ugo+rx ll
    anniinak$ ll
    anniinak$ cd
    anniinak$ ll




