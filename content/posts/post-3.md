+++
author = "Anniina Korkiakangas"
title = "Linux 3: Vapaus!"
date = "2023-01-26"
description = "Lisenssit ja "
tags = [
    "linux",
    "virtualmachine",
    "debian",
    "virtualbox",
    "command-line"
]
categories = [
    "themes",
    "syntax",
]
series = ["Themes Guide"]
aliases = ["migrate-from-jekyl"]
+++

## **Linux 3: Vapaus!**
- h3, Vapaus!. Harjoitustehtäväraportti.
- Pohjana Tero Karvinen 2023: [Linux Palvelimet 2023 alkukevät, ICI003AS2A-3002](https://terokarvinen.com/2023/linux-palvelimet-2023-alkukevat/).

#### **a) Kolmen ohjelman lisenssit.** Tarkastele kolmen edellisessä harjoituksessa asentamasi ohjelman lisenssejä. Selvitä kustakin ohjelmasta:

- Mitä lisenssiä kyseinen ohjelma käyttää?
- Mistä päättelit lisenssin?
- Onko kyseessä vapaa lisenssi?
- Mitkä ovat tämän lisenssin **tärkeimmät** oikeusvaikutukset?

**Git**
- GNU General Public License version 2.0
- Kyseessä on vapaa lisenssi
- [Trademark Policy](https://git-scm.com/about/trademark): Rajoittaa termin "Git", logon ja sloganin käyttöä "the stupid content tracker" 
- Lähteet: https://git-scm.com/about/free-and-open-source 

**Nsnake**
- GNU General Public License version 3.0
- Kaupallinen käyttö, muokkaus, jakelu, yksityinen käyttö 
- Kyseessä on vapaa lisenssi
- Lähteet: https://github.com/alexdantas/nsnake/

**Tree**
- GNU General Public License version 2.0
- Kyseessä on vapaa lisenssi
- Lähteet: https://gitlab.com/OldManProgrammer/unix-tree/-/blob/master/LICENSE

**Ota selvää**: Mitä eroa on GNU 2.0 ja 3.0? 

## **Linux: Hands on**
### **Perustiedot** 

Host kone:
- Rauta: MacBook Pro Retina, 2015
- Ohjelmistojärjestelmä: macOS Big Sur 11.7
- Prosessori: Intel Core i7

Virtuaali kone: 
- VM: debian-live-11.6.0-amd64-xfce-nonfree.iso
- Operating System: Debian (64-bit)
- Type: Linux
- Memory size: 4000 MB
- File size: 60 GB
- Hard disk file type: VDI

### **Grep komento**

#### **b) Säännöllistä.** Poimi tekstitiedostosta tietoa grep-komennolla käyttäen säännöllisiä lausekkeita (regexp, regular expressions).

Käynnistin virtuaalikoneen, kirjauduin sisään ja avasin Terminalin. Syötin seuraavat komennot tarkistaakseni ja ladatakseni päivitykset.

    $ sudo apt-get update 
    $ sudo apt-get -y dist-upgrade

Loin ensiksi tekstitiedoston /Documents/Tarina kansioon ja lisäsin tekstiä.

    $ cd Documents/Tarina/
    $ micro tarina
    
Seuraavaksi syötin grep komentoja:

    $ grep -w "qui" tarina
    $ grep -c 'qui' tarina
    $ grep -w '[0-9].[0-9][0-9].[0-9][0-9]' tarina

- **-w** tarkoittaa sana/word
- **-c** count/kpl määrä
- **[0-9]** Luku 0:n ja 9:n välillä

{{< figure src="/img/grep.png" title="" width="600">}}

### **Pipes** 

#### **c) Pipe.** Näytä esimerkki putkista (pipes).

Etsin komentokerrat, jolloin käytin greppiä. 

    $ history|grep grep

Tutkin lisää tiedostoa:

    $ cat tarina|grep -w -i 'qui'|grep -w 'sequi'  

{{< figure src="/img/pipes.png" title="" width="600">}}

