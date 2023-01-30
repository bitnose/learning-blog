+++
author = "Anniina Korkiakangas"
title = "Reportti 4: Tukki"
date = "2023-01-30"
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

## **Raportti 4: Tukki**
- h4, Tukki. Harjoitustehtäväraportti.
- Pohjana Tero Karvinen 2023: [Linux Palvelimet 2023 alkukevät, ICI003AS2A-3002](https://terokarvinen.com/2023/linux-palvelimet-2023-alkukevat/).

#### **z) Lue ja tiivistä**  

Valitsin artikkelin [An Introduction to Data Science On The Linux Command Line](https://blog.robertelder.org/data-science-linux-command-line/).

- Vastaa kysymykseen kuinka käyttää komentoriviä tiedon analysointiin
- Artikkile korostaa | tai putkien (pipes) merkitystä kommentorivillä: sen avulla voidaan luoda erittäin tehokkaita, räätälöityjä komentoja yhdistäen eri ohjelmien input ja output dataa 
- **grep**: Tiedon suodattamasiseen tekstitiedostoista (txt, csv), mm. säännöllisen lausekkeen avulla
- **sed**: Työkalu etsi ja korvaa toiminnolle, tiedon formatisointiin
- **awk**: Suorittaa edistyneempiä etsi ja korvaa toimintoja
- **sort**: jaotteluun
- **comm**: laskentaan(set operations) kuten päällekkäisyyksien löytämiseen tekstitiedoissa
- **uniq**: uniikkien/kerran esiintyvien rivien tutkimiseen tekstitiedossa 
- **tr**: poista tai korvaa yksittäisiä merkkejä tai merkkijonoja
- **cat**: tiedoston/tiedostoiden ketjuttamiseen ja tulostamiseen konsolissa
- **head**: tulosta tiedoston ensimmäiset rivit/tavut
- **tail**: tulostaa tiedoston viimeiset rivit/tavut
- **wc**: sanan, merkkien lukumäärät, rivimäärät
- **find**: etsi tiedostoja, suorita komentoja
- **tsort**: [Topologinen lajittelu](https://en.wikipedia.org/wiki/Topological_sorting)
- **tee**: jaa tiedontulva tiedostoihin ja samalla tulosta konsoliin
- **<**: outputin uudelleenohjaus (esim. konsolin sijasta tiedostoon)
- **>** : tiedoston sisällön uudelleenohjaus ohjelmaan inputtiin
- Huomio onko kyseessä **UTF-8** vai **UTF-16** 
- Putkien käyttö **tietokantojen** (kuten psql, mysql) kanssa onnistuu

[Kommenteissa](https://news.ycombinator.com/item?id=21605077) tulee esille erilaisia työkaluja datan analysointiin, käsittelyyn (data science) ja myös visualisointiin. Lisäksi esim. kysymys miksi analysoida tietoa komennoilla kun voi hyödyntää Pythonia tai R kieltä. Komentirivin etuna on automaation helppous ja kätevyys.


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

##### Kellonaika: 11:10 

#### a) **Tukki.** Analysoi yksi esimerkkirivi kustakin näistä lokeista:


### **/var/log/syslog** - Yleisloki, tänne kaikki joilla ei ole omaa lokia

    $ sudo head /var/log/syslog

    {{< figure src="/img/sighup.png" title="" width="600">}}

- Päivämäärä ja kelllonaika
- [systemd](https://fi.wikipedia.org/wiki/Systemd): Käynnistää tärkeimmät ohjelmat, ajurit sekä aloittaa lokitietojen keräämisen
- [rsyslog](https://github.com/rsyslog/rsyslog): Lokien tehokkaaseen käsittelyyn --> Esim. ottaa vastaan inputin ja syöttää outputin haluttuun kohteeseen
- [SIGHUP](https://en.wikipedia.org/wiki/SIGHUP) ("signal hang up"): Signaali, joka lähetetään prosesseille kun terminaali suljetaan (ymmärtääkseni?)
- Ymmärtääkseni loki kirjaa tiedon, että terminaali on suljetaan.


### **/var/log/auth.log** - Kirjatumiset, sudo:n käyttö

    $ sudo head /var/log/auth.log

    {{< figure src="/img/auth.png" title="" width="600">}}

- Päivämäärä ja kelllonaika
- CRON: suorittaa ajastettuja komentoja
- pam_unix: Moduuli, joka hoitaa käyttäjän tunnistautumisen, tarkistaa salasanan.
- Loki kirjaa tiedon, että sessio on avattu root käyttäjälle

### **/var/log/apache2/access.log** - Onnistunut surffailu 2xx, 3xx; käyttäjän virheet 4xx client error

Jostain syystä kyseinen tiedosto on tyhjä, mutta sen sijaan löysin toisen tiedoston nimellä 
joten tarkastelen kyseistä tiedostoa.

**Onnistunut** surffailu:

    $ sudo cat /var/log/apache2/access.log|grep -w --color '200'

    {{< figure src="/img/access.png" title="" width="600">}}

- **127.0.0.1.** IP-osoite, josta pyyntö tuli (client)
- **'- -'** käyttäjän (client) tunnus
- **[30/Jan/2023:12:05:54 +0200]** Pyynnön päivämäärä, kellonaika ja aikavyöhyke
- **"GET / HTTP/1.1"** GET pyyntö serverille tiettyyn kohteeseen (API ?)
- **URL**
- **200** Vastaus serveriltä, onnistunut pyyntö. HTTP response status koodi.
- **3380** Käyttäjälle palautetun objektin koko
- **Loppuosa** User Agent, joka tunnistaa tietoa selaimesta, jota käytettiin pyynnön tekemiseksi 

**Epäonnistunut** surffailu:

    $ sudo cat /var/log/apache2/access.log|grep -w --color '404'

{{< figure src="/img/error_404.png" title="" width="600">}}

Tiedot ovat samankaltaisia kuin onnistuneessa surffailussa muutamalla erolla:
- 404: Vastaus serveriltä, epäonnistunut pyyntö. HTTP response status koodi.
Pyyntö oli GET request ja sillä pyydettiin [faviconia](https://stackoverflow.com/questions/13154603/how-to-resolve-favicon-ico-not-found-error-on-apache), mikä on selaimessa, URL vieressä näkyvä pieni kuvake verkkosivustolle. Selaimet pyytävät faviconia automaattisesti ja, jos sitä ei ole pyyntö palauttaa 404 HTTP status kooodin. 

##### Lähteet: https://www.sumologic.com/blog/apache-access-log/

##### *Olen kuluttanut tehtävien tekoon noin tunnin tähän mennessä.*

### **/var/log/apache2/error.log**

Tämä tiedosto sisältää lokeja Apachen omista virheilmoituksista.

    $ sudo cat /var/log/apache2/error.log

Tämä tiedosto oli tyhjä, lokeja ei löytynyt. Sen sijaan listaamalla apache2 kansion tiedostot, selvisi että siellä on error.log.1 tiedosto. En tiedä, miksi lokit on tallennettu error.log.1 tiedostoon eikä error.log tiedostoon. 

    $ sudo cat /var/log/apache2/error.log.1

{{< figure src="/img/error.png" title="" width="600">}}

- Päivämäärä, ajankonta, timestamp 
- mpm_event:notice viestin tyyppi
- pid: prosessi pid 
- Loki tarkoittaa, että uusi processi käynnistyi kyseisellä pid:llä

Käytin **man** komentoa selvittääkseni tietoa lokissa esiintyvistä komennoista. 

##### Lähteet: https://serverfault.com/questions/607873/apache-is-ok-but-what-is-this-in-error-log-mpm-preforknotice

#### b) **Aiheuta.** Aiheuta lokiin kaksi eri tapahtumaa: yksi esimerkki **onnistuneesta** ja yksi esimerkki **epäonnistuneesta** tai kielletystä toimenpiteestä. Analysoi rivit yksityiskohtaisesti.









Lokin analysoiminen tarkoittaa, että selität **kaiken**
Vähän lokia, paljon selitystä
**Kello** - onko oikeassa, mikä aikavyöhyke
Mitä kukin osa tarkoittaa
Mitä numerot merkitsevät
Mitä tämä kokonaisuutena tarkoittaa
Mitä puuttuu
Mitä osia et vielä ymmärtänyt tai selvittänyt tässä yhteydessä
Kerro se itsellesi ilmeinen asia ensin

Lähteet:
https://askubuntu.com/questions/465544/why-do-i-see-a-cron-session-opening-and-closing-every-hour-in-var-log-auth-log
