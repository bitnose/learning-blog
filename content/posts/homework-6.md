+++
author = "Anniina Korkiakangas"
title = "Report 6: Can of worms"
date = "2022-05-09"
description = "A report based on given homework"
tags = [
    "bitcoin",
    "cryptocurrencies",
    "blockchain",
    "cybersecurity",
]
categories = [
    "themes",
    "syntax",
]
series = ["Themes Guide"]
aliases = ["migrate-from-jekyl"]
+++

# **Report 6: Can of worms**
#### **Instructions**

A report based on the homework 6 (h6 can of worms) on the course
[ICT Security Basics - from Trust to Blockchain - ICT4HM103-3003, 2022 Spring, Haaga-Helia University of Applied Sciences](https://terokarvinen.com/2021/trust-to-blockchain-2022/) given by teacher Tero Karvinen.

#### **Homework v)** Read/watch and summarize 

- Felten et al 2015: [Bitcoin and Cryptocurrency Technologies](https://www.coursera.org/learn/cryptocurrency/home/week/1), videos Week 2 (about 1,5 hours). Requires free registration. If you find it easy to follow, you can also optionally look at weeks 3 and four.

## **v) Bitcoin and Cryptocurrency Technologies**

#### **About decentralization and Bitcoin**
- Bitcoin reaches decentralization combining technical and smart incentive engineering 
- Decentralization is often combination of decentralized and centralized services 
- Bitcoin’s key challenge is decentralized e-cash (in other words distributed consensus)

#### **Identities: Pseudonymity is a goal of Bitcoin**
- No real world identities required to participate in the Bitcoin protocol
- Anyone can generate a key pair whenever and as many as they want
- Bitcoin nodes don’t have identities

#### **Transactions** 
- When bitcoin payment (transaction) happens, the transactions will be broadcasted to all nodes
- Transaction contains:
    - Senders signature (nodes can verify the sender)
    - Hash (hash pointer, links to transaction to previous transaction of coin)
    - Receiver’s public key (to address where bitcoin will be send)

#### **Peer-to-peer network**
Nodes form a peer-to-peer network which is open to anyone and has a low entry barrier. Network transfers a coin (chain of transactions) from one address to another.

- So when bitcoin payment (transaction) happens, the transactions will be broadcasted to all nodes
- Transaction will be collected into a block by each node
- In each round a random node gets to broadcast its block
-  Other nodes accept the block if all transactions in it are valid (means no double spending, or wrong signatures)
- Then nodes signal the acceptance of the valid block by adding its hash to the next block nodes create 

#### **Blockchain & Consensus**

How consensus could work in Bitcoin?
- All the nodes have a sequence of blocks of transactions they’ve agreed
- Each node has a punch of transaction that are not yet being resolved (the set is different within each node)
- Consensus happens over a long period of time

Factors that make distributed consensus hard
- Nodes may crash or be malicious
- Network has faults: no notion of global time and all the peer groups are not connected together

Bitcoin consensus works better in practise compared to theory. It uses its currency to reward peers to encourages them to work together, honestly. 

#### **Hash puzzles & mining**

 Bitcoin introduces the idea of incentives for miners to reward them of validating transactions by solving hash puzzles, creating new blocks. It's possible because Bitcoin is a currency so they can reward honest peers with it. Mining is open to anyone, but inevitable concentration of power often seen as unwanted. Different kind of incentives are:

- **Block reward**
    -  Creater of block gets to include coin-creation transaction in the block and choose recipient address of this transaction
    - The value of block reward was 50BTC at the beginning, and it halves every 4 years 
    - Block creater gets to collect the reward only if the block ends up on long-term consensus branch

- **Transaction fees**
    - Purely voluntary given by sender of transaction
    - Like “a tip”
    - Creator of transaction can choose to make output value less than input value

**Hash puzzles** 
- Are there to create blocks: To create a block, you need to find a nonce which will be also included to the block 
- **Miners** are nodes that joining competitions to solve these hash puzzles using their computing power    
- Solving a hash puzzle takes an averege 10 minutes
- The network automatically adjust the difficulty of hash rate
- For miners mining is reward - cost (electrical and hardware)  

Ownership of Bitcoins: Nodes thinking that public address has a certain number of Bitcoins. 
	
#### **Bitcoin is bootstrapped**
Coins' good exchange rate creates more incentive for miners which affects to the health of mining ecosystem and then again to the security of blockchain and it affects to the value of currency. 


##### Summary of Felten et al 2015, Week 2: Bitcoin and Cryptocurrency Technologies, https://www.coursera.org/learn/cryptocurrency/home/week/1

#### **Homework a) Can of worms.** Run some malware in https://any.run web interface. What malware was that? How did it work? Take some screenshots, and explain what we see. Do you recognize any techniques or tactics? What did you learn? Do not download any malware samples to your own computer.

## **a) Malware Analysis sandbox: ANY.RAN**

#### **About ANY.RUN**

ANY.RUN is a malwaro tool to detect and analyse cybersecurity threats. It's a tool for students to experts to learn and run investigations in real time. 

#### **Hands on**

First, I went to https://any.run and accessed the dashboard by clicking *Let's Hunt* button. A screenshot of dashboard looks like this:

{{< figure src="/img/dashboard.png" title="Dashboard" width="600">}}

I clicked Finland on the map to see more details. 

{{< figure src="/img/submission-finland.png" title="Public submissions in Finland" width="600">}}

I can see different tasks, their statuses and machines they are running on. The status tells whether threats were detected.

To run a new task, I needed to register to the service. Next I created a new task (default task).

{{< figure src="/img/new-task-1.png" title="Task" width="600">}}

Here the analysis was running:

{{< figure src="/img/running-task.png" title="Analyses running" width="600">}}

The dashboard seems pretty overwhelming for a newbie. I found some information though: There was no malicious indicators detected with the file.

{{< figure src="/img/activities.png" title="Result" width="600">}}

 I looked Mitre ATT&CK Matrix which is available on the dashboard. 

{{< figure src="/img/mitre-matrix.png" title="ATT&CK Matrix" width="600">}}

There are more technical details of the threat. For example, the file got 4 warnings. 2 about gathering information of system.

**Case x: Stealer**

I ran another test too. 
How the malware appears on the screen:

{{< figure src="/img/task-2.png" title="Second task" width="600">}}

This one seems to be more worrysome. 

It seems that malware is trying to **steal user information and credentials**. It's labeled **stealer**.
The result of scanning the task ran total 221 events (163 dangers, 51 warnings and 7 other). According Mitre ATT&CK matrix, it uses 4 different tactics and 8 techniques. 

###### Source: Any run. Cybersecurity blog. How to use ANY.RUN. https://any.run/cybersecurity-blog/how-to-use-anyrun/. 

 #### **Homework b) Reference implementation**. Ever cop^H^H^Hlearned from StackOverflow? Pick a StackExchange site related to the course, sort questions by score, and briefly explain one question and answer. https://stackexchange.com/sites

## **a) Reference implementation: StackExchange**

 StackOverflow (and StackExchange) can offer bits of help along the way of learning. 

#### **Q: Question**

[Where are the user's bitcoins actually stored?](https://bitcoin.stackexchange.com/questions/1600/where-are-the-users-bitcoins-actually-stored)

Some details of question:
- Asked 17.10.2011 by nickname Alex
- Votes: 47
- Viewed: 106K times 

Person wants to know where the bitcoins are stored. He would like to know where the information which tells how much person has coins. Very practical question, to my mind.

#### **A: Answer**

Some details of question:
- Answered 17.10.2011 by David Perry
- Votes: 58

Person starts by explaining two concepts of Bitcoin:

**Wallet**
- Cryptographic keypairs 
- Public Key, Bitcoin address, public information
- Private keys, signing transaction, lives in wallet.dat file)

**Blockchain**
- constantly growing database of transaction information
- Transactions will be distributed to all nodes
- When transaction is valid its hash will be included in the next block
- Balance is calculated when new transaction is initiated by scanning all the previous transactions to or from the wallet address (balance cannot go negative -> transaction rejected)

 He explains that the blockchain doesn't store coins but **transaction information** (in blocks) and bitcoin is here thanks to transaction histories and balances. Hence, "coins" themselves don't need storage. 