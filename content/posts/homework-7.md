+++
author = "Anniina Korkiakangas"
title = "Report 7: Final Countdown"
date = "2022-05-15"
description = "A report based on given homework"
tags = [
    "bitcoin",
    "cryptocurrencies",
    "blockchain",
    "homework",
]
categories = [
    "themes",
    "syntax",
]
series = ["Themes Guide"]
aliases = ["migrate-from-jekyl"]
+++

# **Report 7: Final Countdown**
#### **Instructions**

A report based on the homework 7 (h7 Final Countdown) on the course
[ICT Security Basics - from Trust to Blockchain - ICT4HM103-3003, 2022 Spring, Haaga-Helia University of Applied Sciences](https://terokarvinen.com/2021/trust-to-blockchain-2022/) given by teacher Tero Karvinen.

#### **Homework a)** Find a block and a transaction in BitCoin public ledger and explain its key parts.

I used [blockchain.com](https://www.blockchain.com/explorer?view=btc) Explorer funtion to find a block in bitcoin public ledger. 

I selected a block in **Latest Blocks** section
{{< figure src="/img/block.png" title="Screenshot 1: Block in Bitcoin public ledger" width="600">}}
A link to the [block](https://www.blockchain.com/btc/block/00000000000000000008bce7ad903f0c644bcc9896c80dd776f13ab36581f8e4)

#### **Keyparts of block**
- **Hash** A unique identifier for the block which identifies it
- **Confirmations** Tells how many confirmations the block has on the blockchain 
- **Timestamp** The moment when the block was mined by the miner
- **Miner** The computer that confirmed the transaction by computing a cryptocraphic hash puzzle
- **Number of Transactions** Tells how many transactions are bundled into the block 
- **Difficulty** The difficulty level of hash puzzle miners need to solve
- **Size** Tells the size of the block
- **Transaction Volume** Total amount of bitcoin transactions in the block
- **Block Reward** A reward for the miner of solving the hash of the block
- **Fee Reward** Rewards in a form of transaction fees for the miner of solving the hash of the block

In **Block transactions** section is a list of all the transactions which are included in the block. 

I selected a transaction in Block transactions section: 

{{< figure src="/img/transaction.png" title="Screenshot 2: Transaction in Bitcoin public ledger" width="600">}}
A link to the [transaction](https://www.blockchain.com/btc/tx/fe5f0d4bcdc25127060398584e521f15c4be32a85eeb20e9fcb297f8c304c5c8)

#### **Keyparts of transaction**
- **Hash** A unique identifier for the transaction 
- **Status** Tells whether the transaction has been validated
- **Received time** The moment when the transaction was distributed to the network
- **Included in Block** Tells the block which contains the transaction
- **Value when transacted** The value of the transaction

I can also see the wallet address which initiated the transaction and the wallet address(es) where the transaction was transacted.
