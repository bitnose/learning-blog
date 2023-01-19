+++
author = "Anniina Korkiakangas"
title = "Reportti 1: Virtuaali-Linux"
date = "2023-01-19"
description = "Linuxin asentaminen virtuaalikoneeseen"
tags = [
    "linux",
    "virtualmachine",
    "läksyt",
    "debian",
    "virtualbox"
]
categories = [
    "themes",
    "syntax",
]
series = ["Themes Guide"]
aliases = ["migrate-from-jekyl"]
+++

## **Raportti 1: Virtuaali-Linux**
- h1, Virtuaali-Linux. Harjoitustehtäväraportti.
- Pohjana Tero Karvinen 2023: [Linux Palvelimet 2023 alkukevät, ICI003AS2A-3002](https://terokarvinen.com/2023/linux-palvelimet-2023-alkukevat/).

#### **x) Lue ja tiivistä: [Raportin kirjoittaminen](https://terokarvinen.com/2006/raportin-kirjoittaminen-4/)**

Tietokoneiden teknisten testien raportointi pähkinänkuoressa:
- Vastaa kysymykseen **mitä** teit, **mitä** tapahtui ja **missä** ympäristössä 
- Kirjoita tapahtumia **samalla**, kun testaat
- **Toistettavuus**: Raportoi niin, että ulkopuolinen pääsee samaan tulokseen samassa ympäristössä
- Raportoi **imperfektissä**: "Klikkasin..." 
- **Täsmällinen**: komennot, klikkaukset, kellonajat, yllätykset, viat ylös
- **Helppolukuinen**: väliotsikot, oikoluku, alkutiivistelmä 
- **Lähdeviitteet** (ja lisenssit)
- **EI** sisällä sepitystä, plagiointia tai kuvien luvatonta kopiointia

#### **a) Asenna Linux virtuaalikoneeseen.** 

Tein harjoituksen, klo 11:15:
- Ohjelmistojärjestelmä: macOS Big Sur 11.7
- Kone: MacBook Pro Retina, 2015
- Perustuen: [Install Debian on Virtualbox - Updated 2023](https://terokarvinen.com/2021/install-debian-on-virtualbox/) by Tero Karvinen

Ensimmäiseksi latasin Debian 11 *debian-live-11.6.0-amd64-xfce-nonfree.iso* tiedoston [Debianin sivustolta](https://cdimage.debian.org/images/unofficial/non-free/images-including-firmware/current-live/amd64/iso-hybrid/).

**Oracle VirtualBox**

[Oracle VirtualBox 6.1](https://www.virtualbox.org/wiki/Downloads) macOS:lle oli valmiiksi asennettuna koneelle. 

Lisäsin uuden virtuaalikoneen VirtualBoxissa: 
        
##### Machine > New...

- Name: Debian
- Operating System: Debian (64-bit)
- Type: Linux
- Memory size: 4000 MB
- File size: 60 GB
- Hard disk file type: VDI

Seuraavaksi: 
##### Settings > Storage > Controller: IDE > Optical Drive 
- Etsin lataamani ISO tiedoston *debian-live-11.6.0-amd64-xfce-nonfree.iso* ja lisäsin sen *Virtual Optical Desk File*

**Debian virtuaalikone**

Klikkasin **Start** käynnistääkseni virtuaalikoneen.
Vituaalikone käynnistyi onnistuneesti! Seuraavaksi valitsin Main Menun vaihtoehdoista Debian GNU/Linux Live (kernel 4.19.0-13-amd64). Debian työpöytä live versio avautui, seuraavaksi klikkasin **Install Debian kuvaketta** aloittaakseni asennuksen. 

**Installer** avautui ja lisäsin seuraavat tiedot:
- Language > American English
- Location > Finland (valitsin kartalta)
- Keyboard > Keyboard model: Generic 105-key PC (intl.), Finnish & Finnish (Machintosh)
- Partitions > Erase Disk: yes
- Partitions > Encryption: no
- Partitions > Master Boot Record

Lisäsin **käyttäjätiedot**:
- Etunimi + Sukunimi
- Käyttäjänimi kirjautumiseen
- Koneen nimi 
- Salasana
- Login automatically: No

Seuraavaksi tarkistin tiedot yhteenvedosta ja klikkasins **Install** - asennus alkoi onnistuneesti. 

{{< figure src="/img/debian-1.png" title="All done!" width="600">}}

Klikkasin **Restart**.  
Sisäänkirjaudun juuri luomillani käyttäjätunnuksilla onnistuneesti. Asennus onnistui!

{{< figure src="/img/debian.png" title="Toimii" width="600">}}

Aukaisin terminaalin ja syötin komennon:

    $ sudo apt-get update


- **sudo** käytä superuser oikeuksia
- **apt-get** package manager
- **update** Update komento

Päivitin ja asensin uusimmat versiot kaikista ohjelmista:

        $ sudo apt-get -y dist-upgrade

- **-y** Kyllä vastaus
- **dist-upgrade** Päivitä kaikki 

Asensin ja käynnistin palomuurin:

        $ sudo apt-get -y install ufw
        $ sudo ufw enable

- **install** asenna
- **ufw** Palomuuri
- **enable** aloita

{{< figure src="/img/debian-3.png" title="Terminal" width="600">}}

Uudelleenkäynnistin koneen klikkaamalla vasempaan yläkulmaan:
##### Applications > Log out > Restart 

Kone uudelleenkäynnistyi ja kirjauduin sisään. 


**Virtuaali-Linux asennettu!**
