+++
author = "Anniina Korkiakangas"
title = "Report 5: BitCoin"
date = "2022-05-01"
description = "A report based on given homework"
tags = [
    "bitcoin",
    "white-paper",
    "cryptocurrencies",
    "blockchain",
]
categories = [
    "themes",
    "syntax",
]
series = ["Themes Guide"]
aliases = ["migrate-from-jekyl"]
+++

# **Report 5: Bitcoin**
#### **Instructions**
This is a report based on the given homework at the course:
[ICT Security Basics from Trust to Blockchain ICT4HM103-3003, 2022 Spring](https://terokarvinen.com/2021/trust-to-blockchain-2022/)

**v)** Read/watch and summarize 

- Nakamoto, Satoshi 2008: [Bitcoin: A Peer-to-Peer Electronic Cash System.](https://bitcoin.org/bitcoin.pdf) ([A colored HTML version](https://git.dhimmel.com/bitcoin-whitepaper/). This is the paper that defined and introduced BitCoin. You can skip "11. Calculations" if you don't like sigma symbols. URL and email address on top of the paper seem unbeliveable and added by third party.

- Felten et al 2015: [Bitcoin and Cryptocurrency Technologies](https://www.coursera.org/learn/cryptocurrency/home/week/1), videos Week 1 (about 1 hour). Requires free registration. If you find it easy to follow, you can also optionally look at week 2 (1,5 h).

## **Bitcoin: A Peer-to-Peer Electronic Cash System by Satoshi Nakamoto October 31, 2008, summary**

The paper introduces a peer-to-peer network of nodes that relais on proof-of-work to record a public history of transactions and this way it ensures digital coins are not spent twice.

- This kind of network would allow online payments to be sent directly with parties without traditional financial institutions
- An electronic payment system based on cryptographic proof instead of trust 
- If honest nodes control a majority of CPU power, it's computionally impractical for an adversary to try to douple spent money: Nodes vote with their CPU power their acceptance of valid blocks by working on them and rejecting invalid blocks by refusing to work on them. 
- Each block contains information of previous block 

## **Felten et al 2015: Bitcoin and Cryptocurrency Technologies, week 1, Summary**

#### Building blocks of Cryptocurrency Technologies

**Cryptographic hash functions**
- They are mathematical functions which take any string as input and return a fixed size output 
- They are efficiently computable
 
**Hash pointer**
- Pointer tells where some information is stored and what is a cryptographic hash of the information
- With hash pointer you can verify information hasn't changed 
- They can be used in pointer-based asyclic data structure, for example in **Merkle tree**

**Merkle tree**
- A data structure which is build with hash pointers
- It can hold many items and can verify membership of an item belonging in the tree
- Sorted Merkle tree can verigy non-membership of item in tree

**Digital signatures and Public keys**
- Digital signatures are used for verifying transactions
- Public key is used for verifying signatures and private keys are used for signing 
- Public key can be seen as an identity and it's controlled with the private key
- Generating a new public key generates also a new identity 
- Public keys are not directly connected to real-world identity 


#### **a)** Value of bit money. **How much is one BitCoin (BTC) worth now?** Using historical BTC course, show that you could have lost a lot of money investing in BTC. Also show that you could have won a lot of money with BTC.

One Bitcoin (BTC) is worth of **38,902.51 USD** (02/05/2022 at 10:56 UTC1+1)

**Case 1**

I would have lost a lot of money investing in BTC if I would have:

Bought 1 BTC
- 15.2.2021 
- price: 47 945$

Sold 1 BTC, because not believing it will go up again:
- 2.5.2022
- price: 38 912.05$

I would have lost 9032.95€ (excluding all the additional fees, inflation etc).

**Case 2**

I would have won a lot of money investing in BTC very at the beginning, in 2009, for example by doing some mining or just by buying some coins and converting them into fiat at the moment when BTC value was high. 

Bought 1 BTC:    
- 17.10.2015 
- price 270.64$

Sold 1 BTC:
- 4.13.2021
- price: 63 503.46$

I would have made 63 232.82$ (excluding all the additional fees, inflation etc).

##### Source:  CoinMarketCap. Bitcoin. 2022. https://coinmarketcap.com/currencies/bitcoin/.

#### **b) Is it legal to own BitCoin in Finland?** Why do you think so?

Yes, it is legal to own Bitcoin in Finland. Some thoughts of mine:

- Bitcoin can be taxed when it's legally accepted
- Easier to control when something is legally accepted: the structure around it can be created
- Might increase or direct the adaptation and development of new technology when it is accepted in society 
- Bitcoin can be seen as a competing system for traditional banks and fiat. By legalizing owning BitCoins, it can be moved under the supervicing centralized power/institution to ensure and control the laws are followed. 
By legalizing something, you have to ensure the laws are applied also either using self-enforcing protocols, being willingly naive and trust or just create a trusted third party. 

#### **c) What's a block chain?** Give a simple but detailed explanation. (Feel free to use the most narrow and simple definition of blockchain - no need to consider a whole cryptocurrency).

A block chain is a database where records are linked together using cryptography. Each block contains a hash of previous block so together they form chain of nodes that can be tracked. If information in one block changes, it modifies the whole chain. Block chain leverages Merkle tree structure, hash pointers and cryptography.

Usually block chain network is ran by peers relaying on decentralization. 

#### **d) Not BitCoin**. Give examples of some AltCoins, crypto currencies compiting with BitCoin. For each AltCoin: how does it differ, what's it's claim for fame?

Altcoins are cryptocurrencies other than BitCoin. They share some traits but also differs. 

**Ethereum**
[Ethereum](https://ethereum.org/en/what-is-ethereum/) ETH is the second valuable cryptocurrency measured in USD price at the moment 2,835$. The technology is very developer friendly and it can be tweeked to create decentralized applications - Dapps or digital assets like NFTs Non-fungible tokens. 

It shares the common characteristics with BitCoin: For example it uses a peer-to-peer network, is decentralized. Both networks serving a role of an trusted arbitary who let you use digital money without traditional banks. 

Ethereum blockchain can be used also other than payments. Transaction can also represent:
- **Smart contracts** Pieces of code that get executed in the blockchain t. For example a royalty system. 
- **Digital assets** like NFT's Non-Fungible-Tokens. 










