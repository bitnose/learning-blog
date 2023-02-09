+++
author = "Anniina Korkiakangas"
title = "Reportti h6: Based"
date = "2023-02-06"
description = "Apachen asentaminen Linuxiin."
tags = [
    "linux",
    "virtualmachine",
    "debian",
    "dns",
    "name-server",
    "web",
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

## **Raportti h6: Based**
- Perustuu Tero Karvinen 2023: [Linux Palvelimet 2023 alkukevät, ICI003AS2A-3002](https://terokarvinen.com/2023/linux-palvelimet-2023-alkukevat/).

#### **x) Lue ja tiivistä.** 
 
#### **Apache Software Foundation 2023**: [Getting Started](https://httpd.apache.org/docs/2.4/getting-started.html)

Apachen virallinen dokumentti, joka pitää sisällään Apachen perusteet.

**URL:in anatomiaa:**

    https://httpd.apache.org/docs/2.4/getting-started.html?arg=value

- **https**: Käytetty protokolla
- **httpd.apache.org**: Serverin nimi
- **/docs/2.4/getting-started.html?**: URL-polku pyydettyyn tiedostoon
- **arg=value**: Query string/argumentit; sisältää parametreja, joita lähetetään palvelimelle pyynnön (requestin) mukana
- CLIENT (web browser) --> REQUEST --> SERVER (Apache Server)
- CLIENT (web browser) <-- RESPONSE <-- SERVER (Apache Server)
 - **Response** Koostuu [http status koodista](https://cwiki.apache.org/confluence/display/HTTPD/CommonHTTPStatusCodes) ja mahdollisesta response bodystä.

**DNS, Domain Name System:**

- DNS tallentaa serverin nimen, joka vastaa julkista IP osoitetta -> kertoo serverin osoitteen nimen perusteella 
- Client selvittää DNS kautta, mikä serveri osoite vastaa mitäkin IP osoitetta
- Virtual hostien avulla yksi fyysinen serveri voi ajaa useita verkkosivustoja
    
**Apache Configuration -tiedostot**

- Apache HTTP serveri konfiguroidaan tekstitiedostojen avulla
- Default tiedostot sijaitsevat yleensä polussa **/usr/local/apache2/conf** ja on nimeltään **httpd.conf** (sijainti ja nimet saattavat vaihdella)
- Konfiguroidaan [configuration directivies](https://httpd.apache.org/docs/2.4/mod/quickreference.html) avulla (avainsana + argumentteja)

**Web sivujen sisältö**

- **Staattinen** sisältö: HTML, css, kuvat. DocumentRoot directive määrittää missä sisältö sijaitsee
- **Dynaaminen** sisältö: Generoidaan pyyntöä tehdessä, esimerkiksi [handlerien](https://httpd.apache.org/docs/2.4/handler.html) avulla 
- **ErrorLog** ja **log** tiedostot apuna ongelmienratkaisuun

#### **Apache Software Foundation 2023**: [Name-based Virtual Host Support](https://httpd.apache.org/docs/current/vhosts/name-based.html)**

- Apachen virallinen dokumentti kertoo miten ja milloin käytetään nimipohjaisia virtuaali hosteja
- IP-pohjaiset(IP-based) virtuaali hostit käyttävät IP osoitetta määrittääkseen, mikä on osoite kun taas nimi -pohjaiset (name-based) käyttävät nimiä osoitteen määrittämiseen DNS kautta 

**Name-based: Käyttö**

-  Ensin rekisteröidään ja konfiguroidaan serverin nimi vastaamaan IP-osoitetta DNS palvelimella, ja sitten konfiguroidaan Apache
- Tietty virtuaali host määritellään **VirtualHost** blokissa
    - **ServerName** Määrittää mikä host
    - **DocumentRoot** Missä sisältö sijaitsee
    - **ServerAlias** Alias, toinen nimi samalle sivustolle
- Lisäämällä [direktiivejä](https://httpd.apache.org/docs/2.4/mod/quickreference.html)  sivustoa voidaan räätälöidä ja optimoida haluttuun käyttötarkoitukseen

**Esimerkki tiedosto:** 

    <VirtualHost *:80>
        # This first-listed virtual host is also the default for *:80
        ServerName www.example.com
        ServerAlias example.com 
        DocumentRoot "/www/domain"
    </VirtualHost>
    <VirtualHost *:80>
        ServerName other.example.com
        DocumentRoot "/www/otherdomain"
    </VirtualHost>

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

### **a) Vaihda Apachelle uusi etusivu.** 

Selaimella Apachen etusivu: 

{{< figure src="/img/h6/start.png" title="" width="600">}}

Komentorivillä:

    $ sudo apt-get update   
    $ sudo apt-get -y dist-upgrade
    $ sudo systemctl status apache2
    $ curl ‘http://localhost/’

{{< figure src="/img/h6/start_curl.png" title="" width="600">}}

Seuraavaksi tarkistin, että sites-available on konfiguroitu oikein:

    $ cat /etc/apache2/sites-available/frontpage.conf

{{< figure src="/img/h6/config.png" title="" width="600">}}

Kaikki kuten piti. Sirryin luomaan käyttäjälle kotikansioon ja seuraavaksi päivitin hieman etusivua (ilman sudoa):

    $ micro public_sites/index.html
    $ curl ‘http://localhost/’

{{< figure src="/img/h6/after_terminal.png" title="" width="600">}}
 
{{< figure src="/img/h6/end.png" title="" width="600">}}

Täysin uuden frontpage.conf tiedoston luonti ja konfigurointi sekä vanhan default tiedoston hylkääminen (000-default.conf):

    $ sudoedit /etc/apache2/sites-available/frontpage.conf
    $ cat /etc/apache2/sites-available/frontpage.conf
    $ sudo a2ensite frontpage.conf
    $ sudo a2dissite 000-default.conf 
    $ sudo systemctl restart apache2
    
Uuden sivuston luonti käyttäjän **kotikansiossa** (ilman sudoa):

    $ mkdir sites-available
    $ micro index.html

### **Päätelmä**
Kaikki meni kuten piti, ei mitään erityistä. Tehtävän tekemiseen kului noin 30 minuuttia.

**b) Tee Apachen asetustiedostoon kirjoitusvirhe.** Etsi se työkalujen avulla. Vertaa 'apache2ctl configtest' ja virhelokin /var/log/apache2/error.log virheilmoituksia.

Ensimmäiseksi listasin mitä kansiossa on: 

    $ ls /etc/apache2/sites-available/

Seuraavaksi muokkasin frontpage.conf tiedostoa ja lisäsin sinne virheen ja käynnistin apachen uudelleen: 

    $ sudoedit /etc/apache2/sites-available/frontpage.conf
    $ cat /etc/apache2/sites-available/frontpage.conf
    $ sudo systemctl restart apache2
    $ sudo systemctl restart apache2.service

{{< figure src="/img/h6/error_start.png" title="" width="600">}}

Seuraavaksi tarkastelin virheilmoituksia. Ajoin configtestin, joka tarkistaa konfigurointi -tiedostot kirjoitusvirheiden varalta. Luin ensin lisätietoa apache2tl:n configtestistä, jonka jälkeen testasin komentoa:

    $ man apache2ctl
    $ /usr/sbin/apache2ctl configtest

Viestistä ilmenee selkeästi **mikä** meni vikaan (syntax error, puuttuu '>'), **missä** tiedostossa (/etc/apache2/sites-enabled/frontpage.conf) ja **millä** rivillä (line of 5) kirjoitusvirhe on.  Kertoo testin **tuloksen** (failed) sekä **mistä**(Apache error log) voi löytyä lisää tietoa.

Toisaalta  teksti osoittaa kohteeseen /etc/apache2/**sites-enabled**/frontpage.conf eikä /etc/apache2/**sites-available**/frontpage.conf osoitteeseen, jossa tiedostoa muokataan (ymmärtääkseni). Hieman hämmentävää. 

{{< figure src="/img/h6/syntax_error.png" title="" width="600">}}

Seuraavaksi tarkistin virhelokin:

    $ sudo cat /var/log/apache2/error.log

{{< figure src="/img/h6/error_log.png" title="" width="600">}}

Tämä ei kerro paljon mitään, ainakaan kirjoitusvirheestä. 

**Päätelmä**: Kirjoitusvirheiden tarkistamiseen configtest on hyödyllinen työkalu. Tehtävän tekemiseen kului noin 30 minuuttia. 