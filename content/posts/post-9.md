+++
author = "Anniina Korkiakangas"
title = "Linux h9 Sequel"
date = "2023-02-16"
description = "PostgreSQL on Linux"
tags = [
    "linux",
    "virtualmachine",
    "debian",
    "cloud",
    "postgresql",
    "sql"
]
categories = [
    "themes",
    "syntax",
]
series = ["Themes Guide"]
aliases = ["migrate-from-jekyl"]
+++

## **Linux h9 Sequel**
- Based on Tero Karvinen 2023: [Linux Palvelimet 2023 alkukevät, ICI003AS2A-3002](https://terokarvinen.com/2023/linux-palvelimet-2023-alkukevat/).

#

**x) Yrityssoftaa.** Keksi esimerkki palvelusta, jota käytetään wepissä selaimella, koodi ajetaan palvelimella ja taustalla on tietokanta. Mitä etuja tällä toteutustavalla on vaihtoehtoisiin toteutustapoihin verrattuna? (Tässä x-alakohdassa ei tarvitse tehdä testejä koneella tai toteuttaa mitään, pelkkä kuvittelu ja vastauksen kirjoittaminen riittää)

**Online Shop**
- Customer uses the service on the web: The web is the interface for the customer (comparing and buying products, placing the order, getting information about the company)
- Customer's userdata is saved on database, as well as the order and product information
- The code is run on linux server, website is served by Apache
- Communication between the database and the website could be handled by some back-end library (Django (Python), Vapor (Swift), etc)
- **Benefits:**
    - The back-end and the frontend is separated: increased security
    - The data will be saved permanently in common format (unless someone deletes the db)
    - The data can be accessible for several websites 
    - Increased scalability and availability when parts are broken into smaller (micro)services --> Easier to managed and apply changes compared to monolith systems
    - In larger projects, the people who work with the project could focus on certain skillsets rather than mastering the whole fullstack

#
## **Linux: Hands on**

**Host Machine**
- MacBook Pro Retina, 2015
- OS: macOS Big Sur 11.7
- Intel Core i7

**Virtual Box (local)**
- VM: debian-live-11.6.0-amd64-xfce-nonfree.iso
- Operating System: Debian (64-bit)
- Type: Linux
- Memory size: 4000 MB
- File size: 60 GB
- Hard disk file type: VDI

**Virual Cloud Server** 
- Debian 11 Image
-  (should be more than enough)
- Region: Frankfurt, DE
- Linode Plan > Shared CPU > 1 GB RAM (Nanode)
- 5$/month (Free credits)
- domain: www.korkiakangas.com

#

**a) Postgre.** Install PostgreSQL and test it by executing SQL-command. (If you did it during the lesson, create a new Linux-user and a new database and db user for him.)


##### **Started at 11:43**
I connected to my virtual cloud server. I did already install PostgreSQL during the previous lesson.

    anniinak$ ssh anniina@<IP-address>         
    anniina$ whoami
    anniina$ sudo apt-get update
    anniina$ sudo apt-get -y dist-upgrade
    anniina$ sudo systemctl status postgresql

{{< figure src="/img/h9/active.png" title="" width="600">}}

    # Create new user, login
    anniina$ sudo adduser testianniina
    anniina$ su testianniina
    testianniina$ cd /home/testianniina

I tried to create database for testianniina with testianniina but it failed like I expected: to create a database the user need to have sudo rights. Didn't want to give the sudo rights to testianniina hence I changed back to anniina and created a new database and user for postgresql: 

    testianniina$ su anniina
    # Create new database and user
    anniina$ sudo -u postgres createdb testianniina 
    anniina$ sudo -u postgres createuser testianniina
    # Change user
    anniina$ su testianniina

    # Start psql with the user 
    testianniina$ psql

    # PSQL
    testianniina=> SELECT coucou;

**It worked!**

{{< figure src="/img/h9/new_user.png" title="" width="600">}}

##### **Finished at 12:05**

#

**b) Crud.** Try CRUD (create, read, update, delete) writing SQL. 

##### **Started at 12:12**


### **CREATE**

**Create table**

    testianniina$ psql 
    testianniina=> CREATE TABLE students (id SERIAL PRIMARY KEY, name VARCHAR(200));

where:
- **CREATE TABLE students:** creates a new table students
- **id SERIAL PRIMARY KEY:** Represent's student's id. SERIAL tells that the ids are handled/counted automatically by PostgeSQL
- **name VARCHAR(200):** Represents student's name. kind of a string with length of 200 characteus. 

**List tables**

List tables:

    testianniina=> \d

List table 'students':

    testianniina=> \d students    

{{< figure src="/img/h9/tables.png" title="" width="600">}}

**Create records: INSERT**

Created a new record on students table (single quotes are must). Returning returned the id and name of the record what was created.

    testianniina=> INSERT INTO students(name) VALUES ('Anniina');
    testianniina=> INSERT INTO students(name) VALUES ('Matti');
    testianniina=> INSERT INTO students(name) VALUES ('Maija');
    testianniina=> INSERT INTO students(name) VALUES ('Tarja') RETURNING id, name;

{{< figure src="/img/h9/insert.png" title="" width="600">}}


#

### **READ**
Read/printed all (*) records from table students: 
    
    testianniina=> SELECT * from students;


Read/printed all (*) records from table students which name starts 'Ma':

    Read/print all (*) records from table students.  SELECT * FROM students WHERE name LIKE 'Ma%';

{{< figure src="/img/h9/read.png" title="" width="600">}}


#

### **UPDATE**

Updated a field of a record:

    testianniina=> UPDATE students SET name='Anniina Korkiakangas' WHERE name='Anniina';

Checked the updated record:

    testianniina=> SELECT * FROM students;

{{< figure src="/img/h9/update.png" title="" width="600">}}

# 

### **DELETE**
Deleted a record: 

    testianniina=> DELETE FROM students WHERE name='Tarja';

Checked the record was deleted:

    testianniina=> SELECT * FROM students;

{{< figure src="/img/h9/delete.png" title="" width="600">}}

##### **Finished at 12:45**

#

**n) Volunteer: Maria.** Install MariaDB and try the CRUD.


Karvinen 2016-2023: Install PostgreSQL on Ubuntu – New user and database in 3 commands
Karvinen 2016-2023: PostgreSQL Install and One Table Database – SQL CRUD tutorial for Ubuntu
'sudo adduser tero'
Karvinen 2018: Install MariaDB on Ubuntu 18.04 – Database Management System, the New MySQL
