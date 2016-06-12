# Composer

V tejto časti tutoriálu sa budeme venovať inštalácii Composer-u a v krátkosti si ukážeme, ako s ním pracovať.

## Čo je to Composer

[Composer](https://getcomposer.org/) je správca balíčkov (závislostí) pre PHP,
ktoré si môžeme prezrieť na stránke [Packagist.org](https://packagist.org/).
V dnešnej dobe pri programovaní systémov PHP už takmer málokto nepracuje Composer-om.

**Poznámka:** Pri spustenom XDebug bude Composer hlásiť, že ho to spomaľuje.

## Inštalácia Composer-u

Všetky informácie ako nainštalovať Composer sú dostupné priamo v [dokumentácii getcomposer.org](https://getcomposer.org/doc/00-intro.md#installation-linux-unix-osx).

V zásade sú tu dve možnosti ako nainštalovať Composer. Buď lokálne ako súčasť nášho projektu,
alebo globálne ako príkaz spustiteľný naprieč systémom.

### Inštalácia z repozitárov Fedory - globálne, odporúčané

Stačí spustiť v termináli nasledujúci príkaz:

```
sudo dnf install composer
```

Composer je dostupný ako `/usr/bin/composer` a je ho možné spustiť z ľubovoľnej zložky.
Takto nainštalovaný Composer sa nám bude aktualizovať rovnako ako zvyšok systému, a nemusíme sa o nič starať.

**Poznámka:** Nevýhodou môže byť staršia verzia, no osobne som sa so žiadnym problémom nestretol.

Po spustení príkazu:

```
composer --version
```

som dostal nasledujúci výpis:

```
Composer version 1.1.2 2016-05-31 19:48:11
```

čo je v dobe písania tohto textu najnovšia verzia.

**Poznámka 2:** Oproti inštalácií zo stránok getcomposer.org takto nainštalovaný
Composer nemá možnosť "sebaaktualizovania", a preto nasledujúci príkaz nespustíme:

```
composer self-update
```

Nám to ale nevadí, o aktualizáciu sa starajú repozitáre Fedory :)

### Inštalácia zo stránok getcomposer.org - lokálne

Inštalácia Composer-u lokálne je skôr záležitosťou stiahnutia Composer-u k jednomu projektu.
Hodí sa v prípadoch, ak na serveri nemáme globálne nainštalovaný Composer, ak ho tam nechceme
inštalovať globálne, alebo ak nemáme práva na inštaláciu Composer-u globálne.

V tomto prípade odporúčam sledovať [Download stránku Composer-u](https://getcomposer.org/download/),
kde je možné stiahnúť `composer.phar` (PHP Archive) manuálne, alebo cez ich inštalátor.

Pri manuálnom stiahnutí je potrebné skopírovať `composer.phar` do koreňovej zložky
našej webovej aplikácie, a spúšťať ho cez terminál za použitia PHP ako napr.:

```
php composer.phar --version
```

Pri použití inštalátoru je používanie rovnaké. Inštalátor navyše kontroluje niektoré
nastavenia PHP a následne stiahne najnovšiu verziu `composer.phar` archívu.

Aj lokálnu inštaláciu Composer-u je možné aktualizovať, a to príkazom:

```
php composer.phar self-update
```

### Inštalácia zo stránok getcomposer.org - globálne

Jednoducho stačí premiestniť súbor composer.phar z lokálnej inštalácie Composer-u do nejakej zložky,
z ktorej sa spúšťajú programy v termináli. Typicky sa jedná o zložku `/usr/local/bin`, takže môžeme použiť príkaz:

```
mv composer.phar /usr/local/bin/composer
```

Súbor `composer.phar` sme rovno premenovali na `composer`, a už nám stačí program spúšťať bez php na začiatku:

```
composer --version
```

**Poznámka:** Osobne túto možnosť nepoužívam, pretože z repozitárov Fedory mi to príde jednoduchšie.

## Použitie Composer-u

V tejto sekcii budem predpokladať, že máme Composer nainštalovaný globálne, a pri práci s Composer-om
sme v koreňovej zložke nášho projektu (tam kde je `composer.json` súbor).

V prípade, že ho máte len lokálne, stačí adekvátne upraviť príkaz podľa príkladu:

```
composer --version
```

má lokálne tvar

```
php composer.phar --version
```

### Pridanie závislosti do našej aplikácie

V koreňovej zložke našej aplikácie by sme mali mať súbor `composer.json`,
ktorý si tam môžeme vygenerovať príkazom:

```
composer init
```

alebo si ho tam pridáme sami. Ten obsahuje závislosti našej aplikácie v JSON formáte:

```json
{
    "require": {
        "vendor/package": "1.3.2",
        "vendor/package2": "1.*",
        "vendor/package3": "^2.0.3"
    }
}
```

V jednoduchosti ide o to, že si nadefinujeme jeden alebo viac dvojíc `"vyvojar/balicek": "verzia"`.
Ako príklad uvediem [Swift Mailer](https://packagist.org/packages/swiftmailer/swiftmailer) vo verzii 5.4.1:

```json
{
    "require": {
        "swiftmailer/swiftmailer": "5.4.1"
    }
}
```

Toto môžeme spraviť aj pomocou terminálu príkazom (ak sa nachádzame v zložke s našim projektom,
máme nainštalovaný composer globálne, a máme vytvorený composer.json súbor):

```
composer require swiftmailer/swiftmailer
```

Takto sme nadefinovali závislosti, ale teraz ich potrebujeme stiahnúť/aktualizovať v projekte.

Príkaz pre stiahnutie závislostí je:

```
composer install
```

a pre aktualizáciu:

```
composer update
```

Hotovo, závislosti sa nám posťahovali do zložky `vendor` a my ich môžeme s radosťou používať.

### Použitie závislosti v našej aplikácii

Kľúčové je "requirnúť" si cudzie kódy do našej aplikácie. Nebudeme to však robiť ručne, ale použijeme autoloader.

V našej aplikácii si teda "requirneme" Composer-ovský `autload.php` nachádzajúci sa v zložke `vendor` (cestu si upravte podľa seba):

```php
// require composer autoload, if any
if (file_exists($composerAutoload = "vendor/autoload.php")) {
    require($composerAutoload);
}
```

Teraz už len stačí použiť cudzí kód, a o nič sa nemusíme starať :)

### Odstránenie závislosti

Závislosti odstraňujeme podobne ako sme ich pridávali.

Buď manuálne upravíme súbor `composer.json`, v ktorom vymažeme už nepotrebnú závislosť, alebo príkazom (napr. ten Swift Mailer):

```
composer remove swiftmailer/swiftmailer
```

a spustíme príkaz:

```
composer update
```
