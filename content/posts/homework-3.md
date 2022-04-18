+++
author = "Anniina Korkiakangas"
title = "Report 3: Public key encryption and pgp"
date = "2022-04-18"
description = "A writing based on given homework"
tags = [
    "encryption",
    "public-key",
    "cryptography",
    "homework",
]
categories = [
    "themes",
    "syntax",
]
series = ["Themes Guide"]
aliases = ["migrate-from-jekyl"]
+++

# **Report 3: Public key encryption and pgp**
#### **Instructions**
This is a post based on the given homework at the course:
[ICT Security Basics from Trust to Blockchain ICT4HM103-3003, 2022 Spring](https://terokarvinen.com/2021/trust-to-blockchain-2022/)

**a)** Read and summarize (with 1-5 bullet points for each heading)
Schneier 2015: [Applied Cryptography Chapter 1: Foundations](https://learning.oreilly.com/library/view/applied-cryptography-protocols/9781119096726/10_chap02.html)

**b)** Give two examples of public key cryptography (other than PGP). Explain how public keys are used here.

**c)** Encrypt and sign a message. Then decrypt and verify it. Use PGP to encrypt and sign messages.

## **a) Applied Cryptography Chapter 1: Foundations** 
**Some terminology**

**Message** Plaintext which can be a text file, a stream of btis, a digital image etc binary data. 

**Encryption** The process of changing a message in a way it hides the message.	

**Ciphertext** An encrypted message.

**Decryption** The process of changing ciphertext back to plaintext. 

**Cryptography** The science and art of keeping messages secure. Cryptographers are people who practice cryptography. Provides confidentiality.

**Cryptoanalysis** The art and science of breaking ciphertext back to a plaintext without access to the key. People who practice it are cryptoanalysis.

**Cryptology** The branch of mathematics covering cryptography and cryptoanalysis. 

**Cryptosystem**
	An algorithm, plaintexts, ciphertexts, and keys. 

**Encryption and Decryption**

    Plaintext —> Encryption —> Ciphertext —> Decryption —> Original Plaintext

## **Algorithms and Keys**
- A cryptographic algorithm ie a cipher is the mathematical function used for encryption and decryption
- **Restricted** algorithm is an algorithm which security is based on its hidden use, the algorithm works a secret.
- Inadequate by today’s standard: if the secret is revealed, the algorithm must be changed
- Nonetheless very popular for low-security applications
- **Solution** is a key. The security is based on the key(s)

## **Key-based algorithms**
**Symmetric algorithms** (Conventional algorithms) 
- The encryption key can be calculated from the decryption key and vice versa.
- Often the keys are same for both  
- The sender and the receiver must agree on a key being able to communicate securely.
- Security relais in the key.

**Public-Key Algorithms** (Asymmetric algorithms) 
- The keys used for encryption and decryption are **different**
- The decryption key **cannot** be calculated from the encryption key (not in any reasonable amount of time)
- The encryption key can be made public and its often called the **public key**
- The decryption key is the **private key** and it’s secret

## **Cryptanalysis**

- **Cryptanalytic attack** is an attempted cryptanalysis. Some attacks are Ciphertext-only attack, Chosen-plaintext attack and Chosen-key attack 
- **Cost vs Benefit** The security of algorithm depends on how hard they are to crack
- Computationally secure algorithms cannot be broken with available resources, either current or future
- Good cryptosystems are designed to be infeasible to break with the computing power that is expected to evolve many years in the future
- The complexity of an attack depends on
    - **Data complexity** The amount of data needed as input to the attack
    - **Processing complexity** The time needed to perform the attack. This is often called the work factor.
    - **Storage requirements** The amount of memory needed to do the attack.
- Many cryptanalytic attacks are great fit for parallel machines: The task can be broken down and none of the processors need to interact with each other. 

## **Real life examples of  cryptosystems**
- **Steganography** Hides secret messages in other messages in a way that the secret's very existence is hidden. For example, invisible inks!
- **Substitution cipher** Each character in the plaintext is substituted for another character in the ciphertext  For example, cryptograms or ROT13!
- **Transposition ciphers** The plaintext remains the same, but the order of characters is shuffled. For example, Rotor Machines!
- **One-time pads** A large nonrepeating set of truly **random** key letters, written on sheets of paper, and glued together in a pad. A random key sequence added to a nonrandom plaintext message produces a completely random ciphertext message and no amount of computing power can change that.
- **Computer algorithms** For example RSA, DES and DSA, Simple XOR, 

###### Schneier 2015: Applied Cryptography: [Chapter 1 - Foundation](https://learning.oreilly.com/library/view/applied-cryptography-protocols/9781119096726/10_chap02.html). read: 16.4.2022


## **b) Examples of public key cryptosystems**

**RSA**

[RSA](https://en.wikipedia.org/wiki/RSA_(cryptosystem)) (Rivest, Shamir, and Adleman, named after invenrors) is the most popular and one of the oldest public-key algorithm. It is used for encryption of digital transactions and digital signatures. 

- Encryption key is public
- The security relies on the ["factoring problem"](https://en.wikipedia.org/wiki/Integer_factorization)
- 4 steps: Key generation, Key distribution, Encryption and Decryption

**ECDSA**

ECDSA (Elliptic Curce Digital Signature Algorithm) is a variant of the Digital Signature Algorithm and it uses [elliptic curve cryptography](https://en.wikipedia.org/wiki/Elliptic-curve_cryptography) to generate keys. 

Compared to RSA, ECDSA keys are shorter but they have the higher degree of [security level](https://www.hypr.com/elliptic-curve-digital-signature-algorithm/). ECDSA is used for creating digital signatures. [Ethereum](https://ethereum.org/en/developers/docs/accounts/) and Bitcoin uses ECDSA to sign transactions. 

- When user creates an account on Ethereum blockchain, the public key is generated from the private key using the ECDSA
- The account is made up of public and private key and the latter is the one used to sign transactions
- The private key gives the access to the Ethereum account and to the funds associated to the account
-  The public key can be derived from the signature and it’s used to proove the author of the signature
- User’s public address is the last 20 bytes of the Keccak-256 hash of the public key added after 0x

## **c) Hands on: Encrypt and sign a message**
[PGP](https://en.wikipedia.org/wiki/Pretty_Good_Privacy) (Pretty Good Privacy) is an cryptographic system used for   encrypting and decrypting emails and sensitive files. It's also used for confidentiality and verification. 

For the exercise I'm using PGP [GnuPG](https://gnupg.org) to encrypt the messages. The excersice was done on Ubuntu 18 virtual machine. GnuPG or GPG is an implementation of a public key cryptography. I followed these [instructions](https://www.digitalocean.com/community/tutorials/how-to-use-gpg-to-encrypt-and-sign-messages).

**Install GnuPG**

    $ sudo apt-get update
    $ sudo apt-get install gnupg

**Generate a key-pair**

    $ gpg --gen-key

This will ask your name and email address which will be assosiated with the key-pair. After it will ask you to enter a passphrase. 

**Import** someone's **public key** from the file. 

    $ gpg --import certkey.asc

**Encrypt a message** by using the receiver's (-r) public key and sign it with your own  private key. In this case, the receiver is same. 

    $ gpg --encrypt --sign --armor -r person@email.com file_name

**Decrypt the message** 

    $ gpg file_name.asc

**Verify** the sender's identity using a fingerprint of a public key.

    $ gpg --fingerprint person@email.com

You can **sign the key** to tell the software you trust the key you have been given and you have verified the person it's associated with. 

    $gpg --sign-key person@email.com

**List** all the keys with this command.

    $ gpg --list-keys



































