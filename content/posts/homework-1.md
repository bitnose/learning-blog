+++
author = "Anniina Korkiakangas"
title = "Report 1: Cyber Kill Chain"
date = "2022-04-04"
description = "A writing based on given homework"
tags = [
    "cyber-kill-chain",
    "cyber-security",
    "homework",
]
categories = [
    "themes",
    "syntax",
]
series = ["Themes Guide"]
aliases = ["migrate-from-jekyl"]
+++

## **Report 1: Cyber Kill Chain**
### **Instructions**

This is a post based on the given homework at the course:
[ICT Security Basics from Trust to Blockchain ICT4HM103-3003, 2022 Spring](https://terokarvinen.com/2021/trust-to-blockchain-2022/)

 z) Read and summarize. Some bullets are enough for a summary.

- [Hutchins et al 2011: Intelligence-Driven Computer Network Defense Informed by Analysis of Adversary Campaigns and Intrusion Kill Chains](https://lockheedmartin.com/content/dam/lockheed-martin/rms/documents/cyber/LM-White-Paper-Intel-Driven-Defense.pdf) 
- [Darknet Diaries](https://darknetdiaries.com)
- [MITRE ATT&CK FAQ](https://attack.mitre.org/resources/faq/) explains [the ATT&CK Enterprise Matrix](https://attack.mitre.org/matrices/enterprise/). Explain tactic, technique, and procedure in the context of ATT&CK, and give an example of each. The enterprise matrix is big, you can just glimpse/browse it to see what's available instead of reading hundreds of pages.

a) How would you compare Cyber Kill Chain and ATT&CK Enterprise matrix? Who do you think could benefit from these models? (Bonus: Do you think anything is missing from either of these models?)

d) Install Debian on Virtualbox. Report your work, including the environment (including host OS, the real physical computer used).


## **Cyber Kill Chain**
### **Summary**
A Kill Chain model is used by the US military to target and engage an adversary to create desired effects
Roots on the kill chain model. Lockheed Martin, a US defense and technology company, created the Cyber Kill Chain as a framework for cyber defense.

- Cyber Kill Chain is a seven-stage systematic cyber-attack process and a defense model used for the identification and prevention of cyber-attacks on a computer network
- Each stage or chain is required to achieve the next one and a successful attack depends on stages in the right order
- Anyone deficiency will interrupt the entire process: The earlier the better!

### **The seven stages of the Cyber Kill Chain**

1. **Reconnaissance** Research, identification, and selection of targets.
2. **Weaponization** - Creating a malware weapon tailored for the vulnerable target
3. **Delivery** - Transmission of the weapon to the targeted environment 
4. **Exploitation** - After the weapon is delivered to the victim host, exploitation triggers intruders’ code using vulnerabilities on the target 
5. **Installation** - Installation of code/program on the target’s system allows the adversary to maintain persistence inside the environment. 
6. **Command and Control** -  Establishing a command and control channel to have access inside the target environment.
7. **Actions on Objectives** - Intruders take action to achieve their original objectives. For example, moving laterally inside the environment or violating the confidentiality, integrity, or availability of a system in the environment.

- The paper presents a new intrusion kill chain model to analyze intrusions and drive defensive courses of action
- The principle goal of the analysis is to determine the patterns and behaviors of the intruders, their tactics, techniques, and procedures to detect *“how”* they operate rather than specifically *“what”* they do
- Just one mitigation breaks the chain and thwarts the adversary, therefore any repetition by the adversary is a liability that defenders must recognize and leverage

### **Courses of Action**

- Defenders must be able to move their detection and analysis up the kill chain and more importantly implement courses of action across the kill chain
- **Detect**, **deny**, **disrupt**, **degrade**, **deceive**, and **destroy** are some courses of action that can be taken
- Some tools for courses of action: web analytics, network intrusion detection systems, denying access using firewall access control lists, audit logging, host intrusion detection systems, data execution prevention, honey potting, DNS redirecting

##### [Source: Hutchins et al 2011. Intelligence-Driven Computer Network Defense Informed by Analysis of Adversary Campaigns and Intrusion Kill Chains.](https://lockheedmartin.com/content/dam/lockheed-martin/rms/documents/cyber/LM-White-Paper-Intel-Driven-Defense.pdf)  Read 30.3.2022.

## **Darknet Diaries EP 100: NSO** 
##### Aug 31, 2021 

### **Summary**
An Israeli company, The NSO Group, created powerful spyware called Pegasus which gives access to the data on a mobile phone. The NSO Group sells spyware to government agencies around the world.
- Spyware like this is extremely sophisticated and expensive to buy, can be sold for hundreds of thousands of dollars or even millions
 The NSO Group claims they are selling Pegasus to governments and intelligence agencies to prevent crime and terror
- Nonetheless, if the software was used The NSO Group claims they only create and sell the spyware, don’t use them hence they are not held accountable for using the spyware 
- The malware can have an access to Whatsapp messages, listen to calls, track location, turn on the microphone and the camera, and then sends the data back to the attackers (government agencies) without the victim having a clue 
- The malware got access to mobile phones using zero-day exploits in Apple’s iPhones and using zero-click exploits against WhatsApp users
- The victims are cartel leaders, drug lords but also political leaders, human rights activists, journalists, people in power, scientists and their family members
- here is evidence of cases when the malware was used to attack civil society and innocent people
According to The NSO Group’s transparency report, the NSO - Group has sixty customers in forty countries and a list of fifty-five countries the NSO Group refuses to do business with due to moral or ethical reasons
- The host of the podcast, Jack Rhysider, says: 

*“But if they continue to do multi-million dollar deals with oppressive regimes who use the malware to attack civil society over and over, then the NSO Group needs to be held accountable for that.”* 
##### Darknet Diaries 2021. Jack Rhysider. Episode 100. https://darknetdiaries.com/episode/100/. Listened 1.4.2022.

## **ATT&CK** 
### **Summary**

[ATT&CK](https://attack.mitre.org/resources/faq/) "is a knowledge base of cyber adversary behavior and taxonomy for adversarial actions across their lifecycle."

### **Tactics**
- Adversary’s tactical goal: Tactics represent “why” an adversary performs an ATT&CK technique or sub-technique. The reason for performing an action. 
- [Initial Access tactic](https://attack.mitre.org/tactics/TA0001/): The adversary is trying to get into your network.
### **Techniques**
- Represents “how” an adversary achieves a tactical goal by performing an action.
- [Supply Chain Compromise tactic](https://attack.mitre.org/techniques/T1195/): Adversaries may manipulate products or product delivery mechanisms prior to receipt by a final consumer for data or system compromise. 
### **Procedure**
- The specific implementation the adversary uses for techniques or sub-techniques.
- APT29 group gained initial network access to some victims via a trojanized update of SolarWinds Orion software.

##### Mitre. Techniques. https://attack.mitre.org/techniques/T1195/002/. read: 30.3.2022.

## **Cyber Kill Chain vs ATT&CK Enterprise matrix**

A big difference between the two models is the way they approach the subject. Cyber Kill Chain approaches intrusions as a linear continuity of different procedures following each other after reaching the goal of each step. The focus is on identifying and stopping the intrusion, the earlier the better. 

Cyber Kill Chain is more theoretical and strategical approach. ATT&CK Enterprise matrix rather goes into detail and depth containing a lot of data regarding both adversarie's and defender's sides. ATT&CK Enterprise matrix is providing references and examples when Cyber Kill Chain is focusing more on the big picture.

ATT&CK Enterprise matrix is a toolbox containing a set of techniques used by adversaries to accomplish a specific objective. Cyber Kill Chain’s every stage is connected and adversaries’ strategy is seen as more rigid, following the same pattern in a specific order. 

The way the models are built is different. ATT&CK Enterprise Matrix is based on data that has been collected and regularly updated with the industry. Cyber Kill Chain is based on US Military’s Kill Chain model.

##### Macafee. What is mitre attack framework. https://www.mcafee.com/enterprise/en-us/security-awareness/cybersecurity/what-is-mitre-attack-framework.html. Read: 1.4.2022.

### **Who benefits?**

Both adversaries and cybersecurity teams can benefit from the models. Both can use the models as a framework for building strategies for attacking and defending. Adversaries can use the ATT&CK Enterprise matrix to create a strategy and procedure for the attack.

Defenders can use the model for testing purposes to orchestrate operations and penetration tests on their network. Targets and cybersecurity teams can benefit from using the same model for understanding and predicting the adversary’s strategy. 

##### Mitre. Getting started. https://attack.mitre.org/resources/getting-started/. Read 1.4.2022.
## **Install Linux virtual machine**
### **Report**
Installed Ubuntu to a Linux virtual machine with the Guest Additions using [Oracle’s Virtual Box]( https://www.virtualbox.org/wiki/Downloads) on macOS Big Sur 11. All good to go! 

- Client OS: Ubuntu
- Virtualization: Oracle VM & Vm Guest Additions
- Host OS: macOS Big Sur
- Machine: MacBook Pro 2015




