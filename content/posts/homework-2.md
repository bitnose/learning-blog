+++
author = "Anniina Korkiakangas"
title = "Report 2: Hashes"
date = "2022-04-11"
description = "A writing based on given homework"
tags = [
    "hash",
    "protocol",
    "homework",
]
categories = [
    "themes",
    "syntax",
]
series = ["Themes Guide"]
aliases = ["migrate-from-jekyl"]
+++

# **Report 2: Hashes**
#### **Instructions**
This is a post based on the given homework at the course:
[ICT Security Basics from Trust to Blockchain ICT4HM103-3003, 2022 Spring](https://terokarvinen.com/2021/trust-to-blockchain-2022/)

z) Read and summarize (some bullet points, feel free to concentrate on things you find interesting)

- € Schneier 2015: Applied Cryptography: [Chapter 2 - Protocol Building Blocks](https://learning.oreilly.com/library/view/applied-cryptography-protocols/9781119096726/10_chap02.html): From beginning of chapter to the end of "2.4 One-Way Hash Functions".
- Karvinen 2020: [Command Line Basics Revisited](https://terokarvinen.com/2020/command-line-basics-revisited/)
- € Santos et al 2017: Security Penetration Testing - The Art of Hacking Series LiveLessons: [Lesson 6: Hacking User Credentials](https://learning.oreilly.com/videos/security-penetration-testing/9780134833989/9780134833989-sptt_00_06_00_00) 
- Karvinen 2022: [Cracking Passwords with Hashcat](https://terokarvinen.com/2022/cracking-passwords-with-hashcat/)

## **z) What are protocols?** 

***“Protocol is a series of steps, involving two or more parties, designed to accomplish a task.”***

The steps must be clear and well defined: No space for ambiguity. All the parties involved in the protocol must know the protocol and the steps in advance. They must agree and follow it. The protocol must be complete and reach its objectives. 
- There are informal protocols for almost everything: ordering food, playing games, voting
- To ensure fairness and security, protocols rely on the presence of people
- Nowadays, more human interactions are taken place online and virtually, over the computer networks
- ***“A cryptographic protocol is a protocol that uses cryptography.”***
- The goal of using cryptography in a protocol is to prevent or detect malicious behavior like eavesdropping and cheating
- Cryptography solves problems that involve secrecy, authentication, integrity, and dishonest people
- Parties can be adversary and defender, or two trusting parties for example

## **Arbitrated Protocols**
An arbitrator is a **trusted third party**, a middle-man, with **no interest** in a protocol or other parties involved - and it’s trusted to complete the protocol it’s involved. They can help complete protocols between two parties that do not trust each other. In the real world, arbitrators are trusted bankers, notaries, lawyers, real estate agents, galleries, grocery stores, brands, etc.

My comment: An arbitrator must be incorruptible!

#### **Some Problems with Computer Arbitrators**
- Faceless: More likely difficulties to trust him
- The network must handle the cost 
- The arbitrator must deal with every transaction so it can be a bottleneck in large projects
- Arbitrator represents a vulnerable point of protocol because everyone on the network must trust him

**Arbitrated protocols can be divided into two subprotocols:**

- **A nonarbitrated subprotocol** is executed every time parties want to complete the protocol
- **An arbitrated subprotocol** is executed only when there is **a dispute**. This type of arbitrator is an **adjudicator**
- An adjudicator is an unbiased and trusted third party, called in only to determine if a protocol was carried out with justice. 
For example a judge 
- Adjudicated computer protocols could determine if someone cheated and determine the id of the cheater: **They detect cheating**

## **Self-Enforcing protocols**
Self-Enforcing **protocols themselves guarantee fairness** —> no middle-men, arbitrators, or adjudicators needed for completion. If one of the parties tries to cheat, the other party immediately detects the cheating, and the protocol stops. Protocols architecture ensures there cannot be disputes. 

Comment: Maybe smart contracts and blockchain could help with it?

## **Attacks against Protocols (themselves)**
**Passive Attack** 
- Eavesdropping the protocol
- It does not affect the protocol,  it only observes and seeks to acquire information
- Difficult to detect —> Prevention instead of detection
- Motive: gain information

**Active Attack**
- The attacker is trying to manipulate the protocol to his advantage 
- Requires active intervention —> Depends on the network
- Pretend to be someone else, use messages in the protocol, alter information, interrupt a communication channel, for example
- Motive: Obtain information, get access, data corruption, degrading system performance
- More serious attacks
- Can be a legitimate system user, an outsider, an admin, a group, a party from the protocol (from supply chain), etc

## **What are one-way functions?** 
#### **One-way Function** 
- Central building blocks for many protocols
- Easy to compute but much harder to reverse, 
- Like “breaking a plate” —> Easy to break, hard to fix
- No mathematically proof that one-way functions exist nor real evidence they can be built!
- It’s not useful for encrypting messages: no one could decrypt it
- **Trapdoor one-way function**: Same to a one-way function plus an extra secret key so the function becomes easier to reverse and compute

#### **One-way Hash Function**
- Central building blocks for many protocols
- a function that takes a variable-length input string called a pre-image and converts it to a fixed-length, generally smaller output string, called a hash value
- A good one-way hash function is collision-free: hard to generate two pre-images with the same hash value
- Hash function is public, the security is its one-wayness
- Computationally unfeasible to find a pre-image that hashes to that value
“Fingerprinting”

###### **Schneier 2015: Applied Cryptography: [Chapter 2 - Protocol Building Blocks](https://learning.oreilly.com/library/view/applied-cryptography-protocols/9781119096726/10_chap02.html)**. read: 10.4.2022


## **Hacking User Credentials**

#### **About Authentication and Authorization Mechanism**
- Password are stored in databases or a text file
- Passwords must be protected on the storage side and while they are transmitted over the network 
- Encryption, access management, endpoint protection, longer passwords and two-factor-authentication protect against intruders 
- Default passwords, password reuse are simple passwords create vulnerabilities that attackers might leverage

#### **Capturing credential over the network**
- MITM 
- Attacks against clear text protocols (telnet, FTP, SIP, POP3, IMAP, HTTP, etc)
- Against ciphered protocols
- Spoof an SSL certificate, SSH downgrade attacks
- Relay attacks: steal the creds directly from the device

#### **Why is it so easy to crack passwords these days**
- Used to rely on CPU speed
- Distribute across CPUS 
- Weak algorithms 
- Dictionaries like rainbow tables
- Multiple GPU’s makes it much faster by decreasing computation times: key space of 69 characters takes only 1 day

###### Summary of Santos et al 2017: Security Penetration Testing - The Art of Hacking Series LiveLessons: [Lesson 6: Hacking User Credentials](https://learning.oreilly.com/videos/security-penetration-testing/9780134833989/9780134833989-sptt_00_06_00_00)

## **Cracking passwords with hashcat**
#### **a) Install hashcat and test that it works.**

I installed hashcat according [this article](https://terokarvinen.com/2022/cracking-passwords-with-hashcat/). The excersice was done on Ubuntu 18 virtual machine. 

#### **b) Crack this hash: 21232f297a57a5a743894a0e4a801fc3**

At first, I try to get more information of the hash type with this command:
       
    $ hashid -m 21232f297a57a5a743894a0e4a801fc3

It gives a result like this: 

    [+] MD2 
    [+] MD5 [Hashcat Mode: 0]
    
Now I can try with:

    $ hashcat -m 0 '21232f297a57a5a743894a0e4a801fc3' rockyou.txt -o solved --force

Cracking was successfull! Print the solved password with this command:

    $ cat solved
    21232f297a57a5a743894a0e4a801fc3:admin

#### **c) Crack this Windows NTLM hash: f2477a144dff4f216ab81f2ac3e3207d**

At first, I try to get more information of the hash by typing this command:
        
    $ hashid -m f2477a144dff4f216ab81f2ac3e3207d

We know already it's a NTLM hash so I can select the right hashcat mode (which is 1000 in this case).

    $ hashcat -m 1000 'f2477a144dff4f216ab81f2ac3e3207d' rockyou.txt -o solved --force

Hurray! The cracking was successful. The password is:

    $ cat solved
    ...
    f2477a144dff4f216ab81f2ac3e3207d:monkey


#### **d) Try cracking this hash and comment on your hash rate $2y$18$axMtQ4N8j/NQVItQJed9uORfsUK667RAWfycwFMtDBD6zAo1Se2eu** 

I start by trying get more information of the hash type and the mode to use:

     $ hashid -m '$2y$18$axMtQ4N8j/NQVItQJed9uORfsUK667RAWfycwFMtDBD6zAo1Se2eu'

     [+] Blowfish(OpenBSD) [Hashcat Mode: 3200]
     [+] Woltlab Burning Board 4.x
     [+] bcrypt [Hashcat Mode: 3200]

Next, I try: 

     $ hashcat -m 3200 '$2y$18$axMtQ4N8j/NQVItQJed9uORfsUK667RAWfycwFMtDBD6zAo1Se2eu' rockyou.txt -o solved --force

The process timed out. I tried again and actually it worked! 

    $ cat solved
    ...
    $2y$18$axMtQ4N8j/NQVItQJed9uORfsUK667RAWfycwFMtDBD6zAo1Se2eu:12345

The cracking took 22 minutes and 23 seconds. A hashrate 








