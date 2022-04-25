+++
author = "Anniina Korkiakangas"
title = "Report 4: The Tor Browser "
date = "2022-04-25"
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
- Tor allows unregulated and anonymous communication over the Internet
- Simply a modified Firefox browser
- The most commonly used anonymoys Internet tool in the world
- Used for both **legitimate and illicit** communication 
- Initially developed by the US government in 2002, not controlled by them anymore
- Open for improvements by anyone with technical ability to test and improve it. It brings lots of experts together and ensures its relevancy
- It’s free, easy to use, portable, fast to set up, and provides amount of anonymity
- In the most of countries it's legal to use Tor. **What is illegal is all so illegal in Tor!**

#### **How does it work?**
Tor directs the route of a user’s Internet traffic **through random relays** on the Internet. 

- Uses **Elliptic curve cryptography** to encrypt the connection between Tor nodes and creates **several layers of encryption**, “onion”. It uses multi-hop routing where each layer is encrypted. 
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

I surfed around, tried [ahmia](https://ahmia.fi) which is a search engine for Tor. I used random(ish) keywords like ukraine, unicorns, democracy, nft and got several results. Think before clicking. All so explored ProPublica, which is a onion site for investigative journalism. 

Some other pretty interesting onion sites are forums where people are speaking very freely and leveraging anonymity. There are all so several onion marketplaces to check out if interested. 

#### **c) Find an example where anonymity of TOR user was compromized**. How was it done? Who did it? Could the deanonymization be replicated?

The [anonymity of TOR user was compromized](https://www.coindesk.com/markets/2013/10/03/silk-road-fell-due-to-a-catalogue-of-errors-by-owner-ross-ulbricht/) by FBI, federal agents who were able to link unidentified Tor identity with user's personal information on the open Internet. The user, Ross Ulbricht, was a founder of an underground black market called Silk Road. The operation to get the site deanonymized lasted more than two years, according the post.

The investigators obtained the identity due to Ross Ulbricht actions on the public Internet and were able to connect the dots with his Tor identity. This kind of deanonymization is harder to replicate because it involves random behaviour from human but the pattern or the tactic can be reused to reveal the identity: Explotation of irregularities, carelessness and randomness of human behaviour. 

#### **d) What other pseudonymous/anonymous networks are there?** What's their killer feature? How are they different from TOR?

### **I2P**
Some other anonymous networks are [I2P](https://geti2p.net/en/), The Invisible Internet Project. It's an encrypted private network layer. It is a peer-to-peer network, it relies on peers to route traffic. All the traffic in the network is internal and I2P does not interact with the Internet direclty. You can think it as a layer on top of the Internet. Connections are encrypted from route to route and end-to-end. 

The main differences between Tor and I2P are

- Differences in the threat model 
- I2P is more distributed 
- 
- The out-proxy design: I2P are optimized for **hidden services** and it's **end-to-end encrypted** unlike TOR where the last hop's data is plaintext 

###### Source: 12P. I2P Compared to Tor. https://geti2p.net/en/comparison/tor.


#### **e)** In your own words, **how does anonymity work in TOR?** (e.g. how does it use: public keys, encryption, what algorithms?)

Anonymity works in TOR by using several layers of encryption between each hop. The data is encrypted except on the exit hop. Entry node knows the IP address of middle node but don't know the IP'address of the exit node or the content of the message. The middle node knows the IP address of the previous node and exit node but doesn't know the encrypted content. The exit node knows the IP'address of the middle node but not the entry node. The message is plaintext. All so, it blocks the fingerprinting and tracking.

 Tor makes an use of Elliptic curve cryptography. Elliptic curve cryptograhy leverages public-key encryption and it's a one-way-function which means the private key cannot be calculated from the public key.

#### **f)** What kind of the **treath models could TOR fit**?

Exit nodes can be used for **spoofing** information which might become useful when combined with contextual information. 

Some other threats are:
- Denial of Service: To deny access to valid user by making it illegal to use Tor Browser
- Brute-force attacks 
- The anonymity protects all so adversaries which makes the platform great for distributing malicious content on user's machine if it's insufficiently protected or if the user's is careless
- Using Tor in malicious ways might cause a threat to people and societies 
- Man-in-the-middle attacks
















