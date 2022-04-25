+++
author = "Anniina Korkiakangas"
title = "Report 4: The Tor Browser "
date = "2022-04-18"
description = "A writing based on given homework"
tags = [
    "encryption",
    "tor",
    "dark-web",
    "homework",
]
categories = [
    "themes",
    "syntax",
]
series = ["Themes Guide"]
aliases = ["migrate-from-jekyl"]
+++

# **Report 4: The Tor Browser**
#### **Instructions**
This is a post based on the given homework at the course:
[ICT Security Basics from Trust to Blockchain ICT4HM103-3003, 2022 Spring](https://terokarvinen.com/2021/trust-to-blockchain-2022/)

**a)** Read and summarize 
Shavers & Bair 2016: [Hiding Behind the Keyboard: The Tor Browser](https://learning.oreilly.com/library/view/hiding-behind-the/9780128033524/XHTML/B9780128033401000021/B9780128033401000021.xhtml) 

## **The Tor Browser: Summary**
[Tor](https://www.torproject.org), **The Onion Router** browser, has empowered any person even without technical background to **communicate anonymously over the Internet**. It hides the user’s original IP address when using the browser. This makes tracing nearly impossible.

#### **Overview**
- Tor allows uncencored and anonymous communication over the Internet.
- Simply a modified Firefox browser
- The most commonly used anonymoys Internet tool in the world
- Used for both **legitimate and illicit** communication 
- Initially developed by the US government in 2002, not controlled by them anyone.
- Open for improvements by anyone with technical ability to test and improve it. It brings lots of experts together and ensures its relevancy.
- It’s free, easy to use, portable, fast to set up, and provides amount of anonymity
- In the most of countries it's legal to use Tor. **What is illegal is all so illegal in Tor!**

#### **How does it work?**
Tor directs the route of a user’s Internet traffic **through random relays** on the Internet. 

- Uses **Elliptic curve cryptography** (unbreakable with brute-force atm) to encrypt the connection between Tor nodes and creates **several layers of encryption**, “onion”, where each layer is encrypted.
- Hops are encrypted except **the last hop of data is unencrypted**
- Node can know only the previous and the next node
- It's **run by volunteers** using servers: “remove the outer envelope(layer of encryption) and forward the inner envelope” 
- **More users increases the anonymity**: Hard to know who is just an innocent volunteer or a criminal

#### **Tracking users of Tor**

Trials of finding vulnerabilities, identifying users and decrypting data in Tor network has been ongoing for years. Government agencies are working on **deanonymizing Tor**. The breaks in the Tor have been made by **exploiting errors made by suspects** instead of breaking the Tor itself. Some ways to spoof information of users:

- Using **forensic analysis** to Tor browser can provide an historical usage of Tor that can be useful when compared with other activity.
- Getting control of as many entry and exit nodes as possible to understand traffic and identify users. Though, trial's unlikely to be fruitful because entry nodes are rotated regularly and the contents of messages are still encrypted. 

- The **man-in-the-middle attack** is a method to bypass the security of Tor users by injecting a capture service between the Tor user and destination
- The most common goal of any Internet-related analysis is obtaining the true IP address 
- One way to reach this goal is to place a tracking code in a document that is e-mailed to the suspect. The document needs to be opened outside of the browser.

#### **Weaknesses of Tor browser**
One of the weaknesses of the Tor browser is the **user**. 
The browser is preconficured with security in mind and customization is not recommended because private information might leak through.

- Geolocation should never be shared
- Plugins for video and animation might reveal IP addresses
- For example a suspect may be using the Tor browser properly, but might mistakenly use another browser falsely believing the non-Tor browser provides anonymity.

#### **Enhance the privacy in Tor using some Tools and Methods**

- **End-to-end** encryption & VPNs
- Using a non-owned computer on a non-owned network
- [**Tails**](https://tails.boum.org) operating system which is an **OS that can be used anonymously**
Based on Debian/Linux and runs from a DVD, USB flash drive, or SD card and does not need to be installed
    - **Portability**, security, and anonymity
    - Tor browser is preinstalled and preconfigured
    - Does not leave any trace on the host computer system: It leaves the host computer hard drive alone (except for the ISO access)
    - Linux can be configured to bypass the OS and boot from an ISO that is stored on the host system hard drive
    - Provides tools for encryption, encrypted chat, an office suite, MAC address spoofing for example. 
- [**Anonabox**](http://www.anonabox.com) hardware router that **routes all Internet traffic through Tor**: eliminates the risk of using a non-Tor browser connection as the entire Internet connection runs through Tor
- Tor can run on Android: **Orbot** app forces Internet traffic on mobile devices to the Tor network, encrypting and sending traffic through worldwide Tor nodes. Combined with prepaid phone plans.
- **Hidden services** a server on the Tor network that provides a service, such as e-mail or file hosting and they are not indexes by search engines. They **do not use exit nodes** hence they are using end-to-end encryption: user connects directly to a hidden service with unbreakable encryption

## **The Tor Browser: Hands on**

#### **a) Install TOR browser and access TOR network** (.onion addresses). (Explain in detail how you installed it, and how you got access to TOR).


Installed the Tor browser on Ubuntu 18.04 virtual machine. 
1. Downloaded the [Tor browser](https://www.torproject.org/download/) for Linux and update the package list.

        $ sudo apt-get update

2. Install atool for unzipping the tar file. 

        $ sudo apt-get install atool

3. Find the location (Downloads usually and move the file to a desidred location). Unzip the file. Go to project directory. Run the script.
 
        $ aunpack tor-browser-linux64-11.0.10_en-US.tar.xz
        $ cd tor-project_en-US
        $ ./start-tor-browser.desktop

4. Tor browser is running!

#### **b) Browsing TOR network** (.onion addresses)

I surfed around, tried [ahmia](https://ahmia.fi) which is a search engine for onion-router (which is the forbidden not a fruit but.. )

