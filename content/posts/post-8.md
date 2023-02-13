+++
author = "Anniina Korkiakangas"
title = "Linux h8 Say my name"
date = "2023-02-13"
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

## **Linux h8 Say my name**
- Based on Tero Karvinen 2023: [Linux Palvelimet 2023 alkukevät, ICI003AS2A-3002](https://terokarvinen.com/2023/linux-palvelimet-2023-alkukevat/).

## **Linux: Hands on**

**a) Rent a domain name and point it to your virtual server** 

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

**Virual Cloud Server** 
- Debian 11 Image
-  (should be more than enough)
- Region: Frankfurt, DE
- Linode Plan > Shared CPU > 1 GB RAM (Nanode)
- 5$/month (Free credits)
- IP-Address

**Renting a domain name**

I decided to go with [namecheap.com]() for the domain name because: 
1) I've used it happily before
2) It's affordable
3) My family name was free 

I typed korkiakangas.com on the search field, selected it, created an account, added a promocode, filled the form up with the minimal required personal information, and voilà, the domain name was registered succesfully under my name and use. 

{{< figure src="/img/h8/start.png" title="" width="600">}}

On the fresh namecheap web console, they ask me to verify the account. I opened my email account to verify the account by clicking an email link. Success! I logged in to my namecheap account to point the domain to the server. 

I opened the linode console of my server to get the IP address and copied to clipboard. 
Back in namecheap.com:

##### **Domain List > korkiakangas.com > Manage > Advanced DNS > Host Records**

I added two new A records to point the IP address of the server: 

{{< figure src="/img/h8/record.png" title="" width="600">}}

I typed the domain name korkiakangas.com on the browser and it automatically redirected to www.korkiakangas.com so I assume the both records work properly!

{{< figure src="/img/h8/works.png" title="" width="600">}}

**b) Analyze your domain's information with 'host' and 'dig' commands. Analyze the results.**

### **host**

On my local terminal (Linux box), I did the basic update, checked the manual of 'host':

    anniina$ sudo apt-get update 
    anniina$ sudo apt-get -y dist-upgrade
    anniina$ man host
    anniina$ host -v

According to the manual page, 'host' is a tool for DNS lookups. It converts the domain to ip address and vice versa. In the manual, there were different parameters, and using the command 'host -v', I could see a compact summary about the host command and its different parameters. 

{{< figure src="/img/h8/verbose.png" title="" width="600">}}

    anniina$ host korkiakangas.com
    anniina$ host www.korkiakangas.com

{{< figure src="/img/h8/host.png" title="" width="600">}}

**korkiakangas.com** 
- IP address 162.255.119.67 is different from the one I declared on namecheap.com
- The second line ('mail is handled by') specifies [a MX record](https://en.wikipedia.org/wiki/MX_record) of DNS. The MX stands for a **mail exchanger record** and its job is specify the server which handles mails on the behalf of a DNS
- **10** priority number
- **host for the mail services**

**www.korkiakangas.com** 
- IP address is the same as the one I declared on namecheap.com.

When doing vice versa (host IP address), it didn't print the korkiakangas.com but actually we can see what is the hosting provider (linode).

### **dig**

First, I checked the manual. Then verbose. No results. Means I, need to install the tool. I tried to find the utility with this command:

    anniina$ apt-cache search dig|grep --color -i dig 

I couldn't find the program. According the [post](https://superuser.com/questions/141623/installing-dig-on-debian), I need to install dnsutils to use the command.

    anniina$ apt-cache search dnsutils|grep --color -i -w dnsutils
    anniina$ sudo apt-get install -y dnsutils
    anniina$ man dnsutils           
    # NO Results
    anniina$ man dig

Got the manual. According it, dig is a tool for troubleshooting and analyzing DNS name servers by sending queries to the servers.

    anniina$ man -v
    anniina$ man -h
    anniina$ dig www.korkiakangas.com

 {{< figure src="/img/h8/digwww.png" title="" width="600">}}

After a quick look I could find information about: 

- **DiG 9.16.37-Debian** version
- **www.korkiakangas.com** domain name (the target name server to query)
- **Global options +cmd** According manual +cmd is a parameter which tells to print the version etc on the console (default setting) 
- **flags** Query options
- **Response HEADER** Here, the most obvious is the status, NOERROR. 
- **OPT PSEUDOSECTION** This section seems to tell where the query was sent
- **ANSWER SECTION**: Tells the domain name and the IP address it's connected. Letter **A** indicates the type of query. Here it means a A record. 
- **QUERY TIME**: Tells how long the request took, where and when it came from, the size of the request

Conclusion: The domain www.korkiakangas.com is pointing to the IP address 143.42.59.10. The query was successfully made. 


Sources: 
- https://superuser.com/questions/141623/installing-dig-on-debian