+++
author = "Anniina Korkiakangas"
title = "Reportti h5: Hello Web"
date = "2023-02-03"
description = "Apachen asentaminen Linuxiin."
tags = [
    "linux",
    "virtualmachine",
    "debian",
    "apache",
    "command-line"
]
categories = [
    "themes",
    "syntax",
]
series = ["Themes Guide"]
aliases = ["migrate-from-jekyl"]
+++

## **Raportti h5: Hello Web**
- h5 Hello Web. Harjoitustehtäväraportti.
- Pohjana Tero Karvinen 2023: [Linux Palvelimet 2023 alkukevät, ICI003AS2A-3002](https://terokarvinen.com/2023/linux-palvelimet-2023-alkukevat/).

#### **x) Kuuntele ja tiivistä**  

Valitsin Indie Hackersin jakson [#265 - From Full-Time Job to $30k/Month with Damon Chen of Testimonial]().

- Vieraana Damon Chen, joka on "indie hakkeri", [Testimonialin](https://testimonial.to/resources/damon) perustaja
- Testimonial tarjoaa asiakkaille/yrityksille markkinoinnintyökaluja, subscription based
- Jaksossa puhutaan yleisellä tasolla mm. epäonnistuneista projekteista ennen läpimurtoa, ideoista ja hyväksynnänhakemista omille ideoille, mitä on olla indie hakkeri
- Miksi Damon Chen lähti tekemään omaa bisnestä sen sijaan, että olisi ollut rivityöntekijä: Oma motivaatio ja halu työskennelle itselle
- Sosiaalinen media, Twitter sekä oma **aktiivinen** verkottuminen, kun rakennetaan yhteisöä/asiakaskuntaa tuotteelle 
- Keskittyy asiakkaisiin ja asiakaspalautteeseen sen sijaan, että keskittyisi kilpailijoihin
- Jaksossa puhutaan työn laskuttamisesta ja sen tuomista haasteista: kuinka voi olla hankalaa laskuttaa suurempia hintoja, mutta loppu peleissä se saattaa kannattaa: Ammattiylpeys ja oman työn/ajan arvostaminen näkyvät ulospäin, kuin itseään toteuttava ennustus

## **Linux: Hands on**
### **Perustiedot** 

**Host kone:**
- Rauta: MacBook Pro Retina, 2015
- Ohjelmistojärjestelmä: macOS Big Sur 11.7
- Prosessori: Intel Core i7

**Virtuaali kone:**
- VM: debian-live-11.6.0-amd64-xfce-nonfree.iso
- Operating System: Debian (64-bit)
- Type: Linux
- Memory size: 4000 MB
- File size: 60 GB
- Hard disk file type: VDI

##### Tehtävien tekemiseen kului noin tunti.

**a) Vaihda Apachen** esimerkkisivu johonkin lyheen sivuun niin, että vanha esimerkkisivu ei näy. (Tämä lienee ainoa kohta, jossa ikinä muokkaat weppisivua pääkäyttäjän oikeuksin. /var/www/html/index.html)


Poistin vanhan asennuksen ja tiedostot aloittaakseni harjoituksen puhtaalta pöydältä. Poistin public_html kansion myös. 

    anniinak$ sudo apt-get update   
    anniinak$ sudo apt-get -y dist-upgrade
    anniinak$ sudo systemctl stop apache2
    anniinak$ sudo apt-get purge apache2 apache2-bin
    anniinak$ rm -r /public_html

{{< figure src="/img/h5/start.png" title="" width="600">}}

Asensin Apachen uudelleen. Jostain syystä selain (ja curl) näyttivät tekstin edellisestä Apachen asennuksesta.

    anniinak$ sudo apt-get -y install apache2
    anniinak$ sudo systemctl start apache2
    anniinak$ curl http://localhost/

Komento esimerkkisivun vaihtamiseen: 

    anniinak$ echo "Hello"|sudo tee /var/www/html/index.html

**b) käyttäjien kotisivut** (http://example.com/~tero) toimimaan. Testaa esimerkkikotisivulla.

Seuraavaksi loin käyttäjän kotisivut: 

    anniinak$ sudo a2enmod userdir
    anniinak$ systemctl restart apache2

{{< figure src="/img/h5/auth_reg.png" title="" width="600">}}

Menin käyttäjän kotikansioon, loin uuden kansion ja lisäsin sinne hieman HTML:

    anniinak$ mkdir public_html
    anniinak$ micro index.html
    anniinak$ curl ‘http://localhost/~anniinak’

Päivitin selaimen ja:

{{< figure src="/img/h5/homepage.png" title="" width="600">}}

Yritin laittaa example.com toimimaan siirtämällä public_html example.com kansioon:

    anniinak$ mkdir example.com
    anniinak$ mv public_html example.com
    anniinak$ sudo systemctl restart apache2
    anniinak$ curl ‘http://example.com/~anniinak/’

Sain näkymään uuden esimerkkisivun, mutta samalla "hukkasin" pääsyn index.hmtl (kotisivut).

Löysin  [artikkelin](https://httpd.apache.org/docs/2.2/mod/mod_userdir.html), jossa kerrotaan enemmän UserDir toiminnasta usealle käyttäjälle. Tarkistan/korjaan tämän myöhemmin.

**c) Tee uusi käyttäjä**. Kirjaudu ulos omastasi ja sisään uutena käyttäjänä. Tee uudellekin käyttäjälle kotisivu.

Syötin seuraavat komennot luodakseni testi käyttäjän ja [kirjautuakseni](https://unix.stackexchange.com/questions/3568/how-to-switch-between-users-on-one-terminal) tilille: 

    anniinak$ sudo adduser testianniinak
    anniinak$ su testianniinak
    testianniinak$ whoami

{{< figure src="/img/h5/newuser.png" title="" width="600">}}

Tarkistin, että testikäyttäjällä ei ole kotisivuja:

{{< figure src="/img/h5/no_page.png" title="" width="600">}}

Loin testikäyttäjälle kotisivut (testikäyttäjän kotikansiossa):

    testianniinak$ mkdir public_html
    testianniinak$ micro index.html

Toisella käyttäjällä (kenellä on sudo oikeudet):

    anniinak$ sudo systemctl restart apache2
    anniinak$ curl ‘http://localhost/~testianniinak/’
    anniinak$ curl ‘http://localhost/~anniinak/’

Lähteet: https://superuser.com/questions/635289/what-is-the-recommended-directory-to-store-website-content

**d) Tee validi HTML5 sivu.**

Tein validit HTML5 sivut, minimaaliset: 

{{< figure src="/img/h5/end.png" title="" width="600">}}






