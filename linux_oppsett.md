# Vedlegg A - systemkonfigurasjon

**Innhold:**
1. [Generelt](#1-generelt)
2. [Linux](#2-linux)
2.1. [For å gi brukeren på Linux sudo rettigheter:](#21-for-å-gi-brukeren-på-linux-sudo-rettigheter)  
2.2. [Oppsett av Docker på Linux:](#22-oppsett-av-docker-på-linux)  

<br>
<br>

# 1 Generelt

Alle maskiner kjører på VmWare

# 2 Linux

> **MERK:** _I den påfølgende tekst vil vi bruke "$"- og "#"-symbolet for å vise en kommando slik den skal skrives inn i CMD-konsollet. Disse symbolene skal altså ikke skrives inn. "$"-symbolet representerer kommandoer skrevet av jb brukeren, mens "#"-symbolet representerer kommandoer skrevet av root_

Vi kjører Debian GNU/Linux 11.6.0 x86_64 med standardinstillinger 




| Bruker | Privilegie |
| ----------- | ----------- |
| root | super-user |
| jb | super-user |


## 2.1 For å gi brukeren på Linux sudo rettigheter:
```shell
  $ su
  # sudo visudo
```
Under root i "# User privilege specification" legg til linjen:
```
jb  ALL=(ALL:ALL) ALL
```
og lagre filen.
Deretter tester man om brukeren har fått sudo rettigheter:
```shell
  # exit
  $ sudo ls -la /root
```

## 2.2 Oppsett av Docker på Linux:
For installasjon av Docker ble installasjonsguiden https://docs.docker.com/engine/install/debian/#prerequisites til Docker Inc fulgt. 

Vi installerte Docker med et repo. Med de neste kommandoene oppdateres og installeres det pakker som gjør det mulig å tillate repo over HTTPS.
```shell
$ sudo apt-get update
$ sudo apt-get install \
    ca-certificates \
    curl \
    gnupg \
    lsb-release
```
<br>

Her legges Docker Inc sin offisielle GPG-nøkkel til maskinen:
```shell
$ sudo mkdir -m 0755 -p /etc/apt/keyrings
$ curl -fsSL https://download.docker.com/linux/debian/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
```
<br>

Så eksekveres en kommando for å sette opp et stabilt repo og gjør det klart til installering:
```shell
$ echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/debian \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```
<br>

Til slutt installeres siste versjon av Docker Engine med følgende kommandoer:  
> **MERK:** _Skal testen etterprøves, bør det spesifiseres hvilken versjon som skal lastes ned her, for å få samme versjon som ble benyttet under forsøket i dette prosjektet. Dette er for å skape et likt testmiljø_
```shell
$ sudo apt-get update
$ sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```
<br>
Nå er Docker installert på maskinen.


<br>

