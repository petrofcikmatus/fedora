# LAMP #

V tomto súbore je návod na inštaláciu LAMP-stacku.

## Čo je to LAMP ##

LAMP je skratka pre sadu nástrojov pre vývoj a prevádzkovanie webových aplikácií. Najčastejšie skratka LAMP reprezentuje nasledovné súčasti:

1. **L ako Linux.** Ide o operačný systém, v ktorom pracujeme. Môže byť aj MAMP pre Mac OS X, alebo WAMP pre Windows.
1. **A ako Apache.** Ide o serverový softvér, a je možné použiť aj Nginx.
1. **M ako MySQL/MariaDB.** Ide o systém riadenia bázy dát (databázu), a kľudne to môže byť aj PostgreSQL (LAPP).
1. **P ako PHP/Perl/Python.** Tie sa používajú často spolu na prevádzkovanie dynamických webových stránok.

## 1 Inštalácia Apache (httpd) ##

Apache nainštalujeme príkazom:
```
sudo dnf install httpd
```

Nastavíme spustenie Apache serveru po spustení PC a tiež si ho manuálne spustíme:
```
sudo systemctl enable httpd
sudo systemctl start httpd
```

Odporúčam zmeniť užívateľa, pod ktorým sa Apache (httpd) spúšťa, a to z toho dôvodu, aby sme moholi narábať so súbormi, ktoré vytvorí PHP skript, a naopak, aby PHP mohlo narábať so súbormi, ktoré sme vytvorili my.
Napr. ak ja som užívateľ **matusko**, tak chcem aby sa Apache (httpd) spúšťal pod užívateľom **matusko**. Tejto zmeny docielime v súbore **/etc/httpd/conf/httpd.conf**:
```
sudo vi /etc/httpd/conf/httpd.conf
```
kde je potrebné zmeniť približne na riadkoch 66 a 67, údaje:
```
User apache
Group apache
```
na
```
User matusko
Group matusko
```

Po každej zmene v konfiguráku httpd.conf je potrebné reštartovať httpd:
```
sudo systemctl restart httpd
```

Taktiež je potrebné pridať užívateľa, u mňa **matusko**, do skupiny **apache**, a to z toho dôvodu, aby sme mohli modifikovať zložky patriace skupine **apache**, a aby nám neskôr fungovalo session v PHP:
```
sudo usermod -a -G apache matusko
```

**Poznámka:** Ak chceme aby boli naše stránky dostupné aj vzdialene, musíme firewall-u pridať výnimky:
```
sudo firewall-cmd --permanent --add-service=http
sudo firewall-cmd --permanent --add-service=https
```

A následne reštartovať firewalld:
```
sudo firewall-cmd --reload
```

## 2 Inštalácia PHP ##

PHP nainštalujeme príkazom:
```
sudo dnf install php
```

Je vhodné si nastaviť PHP (napr. zapnúť zobrazovanie chýb) v súbore **/etc/php.ini**:
```
sudo vi /etc/php.ini
```

Pre zistenie, kde sa php.ini nachádza, je možné použiť príkaz:
```
php --ini
```

Pre zistenie verzie PHP je možné použiť príkaz:
```
php --version
```

Po každej zmene v konfiguráku php.ini je potrebné reštartovať httpd:
```
sudo systemctl restart httpd
```

Naše webové stránky sa budú nachádzať v zložke **/var/www/html**.

V prípade potreby meniť práva (vlastníctvo) zložiek v **/var/www** môžeme použiť nasledujúce príkazy:
```
sudo chown -R matusko /var/www
sudo chgrp -R matusko /var/www
```

**Poznámka:** Môžeme si vytvoriť testovací súbor:
```
echo "<?php phpinfo() ?>" >> /var/www/html/phpinfo.php
```

ktorý si zobrazíme na adrese:
```
http://localhost/phpinfo.php
```

**Poznámka 2:** V prípade potreby je dostupný aj grafický nástroj na spravovanie užívateľov a užívateľských skupín. Stačí do terminálu zadať:
```
sudo system-config-users
```
Ak by sme ho v systéme ešte nemali, terminál nás na to upozorní a ponúkne inštaláciu.

## 3 Inštalácia MariaDB ##

MariaDB server a klienta nainštalujeme príkazom:
```
sudo dnf install mariadb mariadb-server
```

Nastavíme spustenie MariaDB serveru po spustení PC a tiež si ju manuálne spustíme:
```
sudo systemctl enable mariadb
sudo systemctl start mariadb
```

Je dôležité prejsť si nastavenia databázy, kde si môžeme nastaviť heslo užívateľa `root` do databázy, či má byť databáza dostupná aj vzdialene, či chceme vymazať testovaciu tabuľku a podobne. Použite preto príkaz:
```
mysql_secure_installation
```

## 4 Inštalácia phpMyAdmin-u ##

PhpMyAdmin nainštalujeme príkazom:
```
sudo dnf install phpMyAdmin
```

Následne je potrebné reštartovať httpd:
```
sudo systemctl restart httpd
```

Dostupný by mal byť na adrese:
```
http://localhost/phpmyadmin
```

## 5 Inštalácia XDebug-u - voliteľné ##

XDebug nainštalujeme príkazom:
```
sudo dnf install php-pecl-xdebug
```

Následne je potrebné reštartovať httpd:
```
sudo systemctl restart httpd
```

Ak sme všetko spravili správne, môžeme zadať príkaz:
```
php --version
```
kde by nám mala pribudnúť informácia o XDebug-u:
```
PHP 5.6.19 (cli) (built: Mar  3 2016 06:29:24)
Copyright (c) 1997-2016 The PHP Group
Zend Engine v2.6.0, Copyright (c) 1998-2016 Zend Technologies
    with Xdebug v2.3.3, Copyright (c) 2002-2015, by Derick Rethans
```

**Poznámka:** Pri spustenom XDebug bude Composer hlásiť, že ho to spomaľuje.