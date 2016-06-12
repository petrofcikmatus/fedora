# Úvod

V tejto časti tutoriálu vám predstavím, čo to tá Fedora vlastne je, kde ju môžeme získať, a ako si vytvoriť inštalačné médium s Fedorou.

## Čo je to Fedora

Fedora je linuxová distribúcia založená na balíčkovacom systéme RPM, vyvíjaná za podpory komunity projektu [Fedora Project](https://fedoraproject.org/wiki/Overview).

Fedora Project je sponzorovaný spoločnosťou [Red Hat](https://www.redhat.com/en), a podľa jednotlivých vydaní Fedory potom Red Hat vytvára vlastný operačný systém Red Hat Enterprise Linux.

**Aktuálna verzia Fedory je Fedora 23**, nasledujúca Fedora 24 by mala byť vydaná 14. júna 2016.

Fedora je samozrejme **zadarmo** a delí sa na 3 verzie podľa použitia.

Pre nás zaujímavou verziu je verzia [Workstation](https://getfedora.org/en/workstation/), kde je východzím grafickým prostredím [GNOME 3](https://www.gnome.org/gnome-3/).

Z Fedory 23 Workstation existujú aj tzv. Fedora Spin-y s KDE Plasma Desktop, XFCE Desktop, LXDE Desktop, MATE-Compiz Desktop, Cinnamon Desktop a SOAS Desktop (Sugar on a Stick).

Ďalšími verziami sú [Server](https://getfedora.org/en/server/), [Cloud](https://getfedora.org/en/cloud/) (obrazy raw, vagrant, amazon, docker...), a ako bonus sú k dispozícii aj [ARM verzie](https://arm.fedoraproject.org/) všetkého čo som napísal.

Webstránka: [getfedora.org/en/](https://getfedora.org/en/)

## Stiahnutie inštalačného obrazu

Aby sme si Fedoru mohli nainštalovať (prípadne len vyskúšať), musíme si stiahnúť bootovateľný obraz systému (ISO súbor).

Na stránke [getfedora.org/en/workstation/download/](https://getfedora.org/en/workstation/download/) je na stiahnutie 64-bitový 1.4GB obraz Fedory 23 Workstation, a my si stiahneme práve ten.

Ak by niekto potreboval, sú tam aj linky pre 32-bitovú verziu, Netinstall obrazy oboch verzií, prípadne na stránke [torrents.fedoraproject.org](https://torrents.fedoraproject.org/) aj torrent súbory.

Ak sa niekomu nepáči grafické prostredie GNOME 3, môže siahnúť po jednom z viacerích spinov Fedory na stránke [spins.fedoraproject.org](https://spins.fedoraproject.org/).

## Vytvorenie inštalačného USB

Zatiaľ čo s CD/DVD je to jednoduché (stačí vypáliť ISO súbor), s USB-diskom to môže byť málinko komplikovanejšie.

Fedora Project odporúča použiť nástroj [LiveUSB Creator](https://fedorahosted.org/liveusb-creator/), ktorý je dostupný ako pre Linux, tak pre Windows.

Podľa mňa je však ideálnejšie vytvoriť si inštalačné USB Fedory cez známy multiplatformný program [Unetbootin](https://unetbootin.github.io/), ktorý je možné spustiť na Windows, Mac OS X, aj Linux-ových distribúciach.

U Fedory 23 môžeme Unetbootin nainštalovať pomocou príkazu:
```
sudo dnf install unetbootin
```

Program sa odporúča spustiť príkazom:
```
sudo unetbootin
```

Následne si vyberiete distribúciu na stiahnutie a inštalovanie, alebo rovno ISO súbor našej Fedory, ktorú sme si predtým stiahli :)

Vyberieme si zariadenie, na ktoré chceme obraz nakopírovať, a klineme na tlačítko OK. Program by mal skopírovať obsah ISO súboru na USB, a nastaviť USB ako bootovateľné médium.

V operačných systémoch Windows a Mac OS X som to moc neskúšal, ale predpokladám rovnaké chovanie.

Vo Windows-och mám pozitívne skúsenosti s programom [Power ISO](http://www.stahuj.centrum.cz/multimedia/ostatni/poweriso/)
a [Pendrive Universal USB Installer](http://www.pendrivelinux.com/universal-usb-installer-easy-as-1-2-3/) (dokáže nainštalovať viacero live systémov na jedno USB).
