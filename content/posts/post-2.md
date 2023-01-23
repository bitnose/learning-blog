+++
author = "Anniina Korkiakangas"
title = "Reportti 2: Komentaja Pingviini"
date = "2023-01-23"
description = "Komentokehotteiden harjoittelua"
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

## **Raportti 2: Komentaja Pingviini**
- h2, Komentaja-Pingviini. Harjoitustehtäväraportti.
- Pohjana Tero Karvinen 2023: [Linux Palvelimet 2023 alkukevät, ICI003AS2A-3002](https://terokarvinen.com/2023/linux-palvelimet-2023-alkukevat/).

#### **x) Lue ja tiivistä: [Command Line Basics Revisited](https://terokarvinen.com/2020/command-line-basics-revisited/?fromSearch=command%20line%20basics%20revisited)**

**Linux Commnand Line Basics**

    # Tämä on kommentti
    $ pwd                   # Tulosta "working directory"                
    /home/anniinak                      

 **Liikkuminen**

    $ cd anniinadir/        # Liiku kansioon         
    $ cd ..                 # Mene +1 kansio ylös 
    $ less file.txt         # Näytä tekstitiedosto
    $ ls /etc|less          # Näytä tiedosto kerralla

**Tiedostojen muokkaus**

    $ nano file.txt         # Avaa tiedosto editorissa
    $ mkdir NEWFOLDER       # Uusi kansio
    $ mv OLDNAME NEWNAME    # Siirrä/uudelleennimeä 
    $ mv SOMEFILE NEWDIR/   # Siirrä/uudelleennimeä 


    $ cp -r ORIGINAL COPY   # Kopio ORIGINAL
    $ rmdir EMPTYDIR        # Poista tyhjä kansio
    $ rm JUNK               # Poista tiedosto
    $ rm -r FOLDEROFJUNK    # Poista tiedosto sisältöineen

**SSH Remote Control**

Avaa etäyhteys turvallisesti: 


    $ ssh anniina@example.com 
    anniina$ exit                  # Poistu etäkoneelta


Kopio FOLDER uuteen kansioon etäkoneelle : login@server:path_from_your_home_dir

    anniina$ exit
    $ scp -r FOLDER anniina@example.com:public_html/


**Apuja**

    $ man ls            # Näytä manuaali sivu
    $ ls --help         
    $ wget -h           


**Tab näppäin**
Näyttää mitä voidaan kirjoittaa: 

    $ ls /etc/re[tab][tab]
    reportbug.conf  resolvconf/     resolv.conf
    $ ls /etc/resolv.[tab]
    $ ls /etc/resolv.conf

    $ history               # Listaa syötetyt komennot

**Admin komennot**
- **Minimum priviledge** periaate: Anna vain tarvittavat käyttäoikeudet --> **sudo** vain kun vaaditaan laajat käyttöoikeudet
- Päivitä lista saatavista paketeista, "packages"

        $ sudo apt-get update 
- **Etsi** ladattavia ohjelmistoja avainsanoilla 

        $ apt-cache search dungeon adventure
- **Asenna** ohjelmisto

        $ sudo apt-get -y install nethack-console
- **Poista** ohjelmisto

        $ sudo apt-get purge nethack


### **Raportti h2: Perustiedot** 

Aloitin harjoituksen klo 11:07 ja lopetin 12:45.

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


### **Micro-editorin asennus**

#### **a) Micro.** Asenna micro-editori.

Käynnistin virtuaalikoneen, kirjauduin sisään ja avasin Terminalin. Syötin seuraavat komennot.

    $ sudo apt-get update 
    $ sudo apt-get -y dist-upgrade
    $ sudo apt-get install micro

Seuraavaksi testasin toimiiko editori. 

    $ micro

{{< figure src="/img/terminal-2.png" title="Toimii!" width="600">}}

### **Raudan tiedot** 

#### **a) Rauta.**  Listaa testaamasi koneen rauta (‘sudo lshw -short -sanitize’). Asenna lshw tarvittaessa. Selitä ja analysoi listaus..

     $ sudo lshw -short -sanitize
     sudo: lshw: command not found
     $ sudo apt-get install install
     $ sudo lshw -short -sanitize

{{< figure src="/img/rauta.png" title="" width="600">}}

Listauksessa selviää tietoja koneen raudasta. Virtuaalikone on asennettu VirtualBoxiin, listauksesta selviää prosessori, muisti, etc.

### **Ohjelmien asennus**

#### **c) Apt.**  Asenna kolme itsellesi uutta komentoriviohjelmaa. Kokeile kutakin ohjelmaa sen pääasiallisessa käyttötarkoituksessa. Ota ruutukaappaus. Kaikki terminaaliohjelmat kelpaavat, TUI (text user interface) ja CLI (command line interface). Osaatko tehdä apt-get komennon, joka asentaa nämä kolme ohjelmaa kerralla?

    $ sudo apt install nsnake tree git

### **nsnake - Klassinen matopeli** 

{{< figure src="/img/snake.png" title="" width="600">}}

### **tree - Navigoinnin helpottamiseksi** 

{{< figure src="/img/tree.png" title="" width="600">}}

### **Git - Versionhallinta**
Asensin gitin versionhallintaa varten. Syötin seuraavat komennot luodakseni uuden repositorion ja testatakseni versionhallintaa. 

    $ git version           # Versio
    $ mkdir Tarina          # Uusi kansio
    $ cd Tarina/            # Siirry kansioon
    $ git init              # Luo .git tiedosto
    $ git status            # Katso status
    $ micro luku_1.txt      # Luo uusi tiedosto
    $ git add .             # Lisää kaikki muutokset "stage"
    $ git commit -m "Init"  # Vahvista muutokset, viesti


{{< figure src="/img/git.png" title="" width="600">}}

### **Tärkeät tiedostot**
**d) FHS**. Esittele kansiot, jotka on listattu "Command Line Basics Revisited" kappaleessa "Important directories". Näytä kuvaava esimerkki kunkin tärkeän kansion sisältämästä tiedostosta tai kansiosta. Jos kyseessä on tiedosto, näytä siitä kuvaava esimerkkirivi. Työskentele komentokehotteessa ja näytä komennot, joilla etsit esimerkit.


- **/** Root directory (kaikki kansiot ovat tämän alla)
- **/home/** Sisältää kotikansiot kaikille käyttäjille
- **/home/anniina/** Käyttäjän kotiskansio
- **/etc/** Asetukset
- **/media/** Media, esim. /media/cdrom/ ja /media/usbdisk/
- **/var/log/** Loki 


{{< figure src="/img/home.png" title="" width="600">}}

{{< figure src="/img/etc.png" title="" width="600">}}

{{< figure src="/img/media.png" title="" width="600">}}

{{< figure src="/img/log.png" title="" width="600">}}

### **grep-komento**

**e) The Friendly M.** Näytä 2-3 kuvaavaa esimerkkiä grep-komennon käytöstä. Ohjeita löytyy 'man grep' ja tietysti verkosta.
