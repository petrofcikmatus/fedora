# O Fedore #

V tomto súbore sú informácie a návod na inštaláciu Linux Fedora 23 Workstation.

## Čo je to Fedora ##

Fedora je linuxová distribúcia založená na balíčkovacom systéme RPM, vyvíjaná za podpory komunity projektu Fedora Project.

Fedora Project je sponzorovaný spoločnosťou Red Hat a podľa jednotlivých vydaní Fedory potom Red Hat vytvára vlastný operačný systém Red Hat Enterprise Linux.

**Aktuálna verzia Fedory je Fedora 23**, nasledujúca Fedora 24 by mala byť vydaná 7. júna 2016, a 29. marca 2016 bola sprístupnená Fedora 24 Alpha.

Hlavnou verziou je [Fedora 23 Workstation](https://getfedora.org/en/workstation/), kde **východzím grafickým prostredím je GNOME 3**.

Z Fedory 23 Workstation existujú aj tzv. Fedora Spin-y s KDE Plasma Desktop, XFCE Desktop, LXDE Desktop, MATE-Compiz Desktop, Cinnamon Desktop a SOAS Desktop (Sugar on a Stick).

Ďalšími verziami sú [Fedora 23 Server](https://getfedora.org/en/server/), [Fedora 23 Cloud](https://getfedora.org/en/cloud/) (obrazy raw, vagrant, amazon, docker...), nakoniec sú k dispozícii aj [ARM verzie](https://arm.fedoraproject.org/) všetkého čo som napísal.

Webstránka: [https://getfedora.org/en/](https://getfedora.org/en/)

## Stiahnutie inštalačného obrazu ##

Na stránke [https://getfedora.org/en/workstation/download/](https://getfedora.org/en/workstation/download/) je na stiahnutie 64-bitový 1.4GB obraz Fedory 23 Workstation, a my si stiahneme práve ten.

Ak by niekto potreboval, sú tam aj linky pre 32-bitovú verziu, Netinstall obrazy oboch verzií, prípadne na stránke [https://torrents.fedoraproject.org/](https://torrents.fedoraproject.org/) aj torrent súbory.

## Vytvorenie inštalačného USB ##

Najideálnešie je vytvoriť si inštalačné USB Fedory 23 Workstation cez známy multiplatformný program [Unetbootin](https://unetbootin.github.io/), ktorý je možné spustiť na Windows, Mac OS X, aj Linux-ových distribúciach.

U Fedory 23 môžeme Unetbootin nainštalovať pomocou príkazu:
```
sudo dnf install unetbootin
```

Program sa odporúča spustiť príkazom:
```
sudo unetbootin
```

Následne si vyberiete distribúciu na stiahnutie a inštalovanie, alebo rovno ISO súbor našej Fedory 23 Workstation, ktorú sme si predtým stiahli :)
Vyberieme si zariadenie, na ktoré chceme obraz nakopírovať, a klineme na tlačítko OK. Program by mal skopírovať obsah ISO súboru na USB, a nastaviť USB ako bootovateľné médium.

V operačných systémoch Windows a Mac OS X som to moc neskúšal, ale predpokladám rovnaké chovanie.

Vo Windows-och mám pozitívne skúsenosti aj s programom [Power ISO](http://www.stahuj.centrum.cz/multimedia/ostatni/poweriso/) a s [Pendrive Universal USB Installer](http://www.pendrivelinux.com/universal-usb-installer-easy-as-1-2-3/)(dokáže nainštalovať viacero live systémov na jedno USB).

Ak má niekto alternatívy, poprosím napísať do komentárov.