# Vedlegg A - systemkonfigurasjon

**Innhold:**
1. [Generelt](#1-generelt)
2. [Linux](#2-linux)  
2.1. [For å gi brukeren på Linux sudo rettigheter:](#21-for-å-gi-brukeren-på-linux-sudo-rettigheter)  
2.2. [Oppsett av Docker på Linux:](#22-oppsett-av-docker-på-linux)  
3. [Windows](#3-windows)

<br>
<br>

# 1 Generelt

Alle maskiner kjører på VmWare
<br>

# 2 Linux

> **MERK:** _I den påfølgende tekst vil vi bruke "$"- og "#"-symbolet for å vise en kommando slik den skal skrives inn i CMD-konsollet. Disse symbolene skal altså ikke skrives inn. "$"-symbolet representerer kommandoer skrevet av jb brukeren, mens "#"-symbolet representerer kommandoer skrevet av root_

Vi kjører Debian GNU/Linux 11.6.0 x86_64 med standardinstillinger 




| Bruker | Privilegie |
| ----------- | ----------- |
| root | super-user |
| jb | super-user |

<br>

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
<br>
Deretter tester man om brukeren har fått sudo rettigheter:
```shell
  # exit
  $ sudo ls -la /root
```
Dersom siste linje printer ut en liste har brukeren sudo rettigheter.
<br>

## 2.2 Oppsett av Docker på Linux:
Installer Docker gjennom et script fra get.docker.com gjennom å skrive 
```shell
$ curl -fsSL https://get.docker.com -o get-docker.sh
$ sudo sh ./get-docker.sh 
```
Nå er Docker version 23.0.1, build a5ee5b1 installert.

Laster ned konteineren Portainer som er en administrasjonsverktøy med GUI.

Åpner portainer i nettleseren på https://localhost:9443

Velger brukernavn (jb) og passord (jb1234567890)

Hopper over installasjonsveiviseren.

Setter opp en GitLab regestry i Porteiner:
I App Templates søker vi opp GitLab CE. Fyller ut "Name" til "gitlab" og resten er standard. 

Starter gitlab konteineren i Portainer. 

Åpner konsollet til konteineren gjennom Portainer (tilsvarende ```sudo docker exec -it gitlab```) og kjører kommando ```grep 'Password:' /etc/gitlab/initial_root_password ```. Kopierer passordet. 

Åpner gitlab konteineren i web-konsoll med root som brukernavn og passordet som ble kopiert og endrer passsord til jb1234567890. 

Lager Access Token på Settings. Kaller den "portainer". 
Tillater alle read funksjonaliteter. Kopierer token som er lagd.
Limer inn token i gitlab registry. 






Installerer Watchtower i GitLab registry:
containrrr/watchtower fra docker.io
med volume /var/run/docker.sock både på ontainer og host med bind og witable. Dette deler Docker prosessen mellom Watchtower og klienten og gjør derfor at Watchtower får tillatelse til å administrere Docker. Dette er for eks. hente nye images og oppdatering av conteinere automatisk.



nginx

For installasjon av Docker ble [installasjonsguiden _(https://docs.docker.com/engine/install/debian/)_](https://docs.docker.com/engine/install/debian/) til Docker Inc fulgt. 

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

# Windows
Vi kjører Windows Enterprise 10 OS-build 1........ 64-bit med standardinstillinger 

RAM: 8 GB
Hard Disk: 128 GB
CPU: 4
Cores per Socket: 2
Skrur på "Exposure hardware assisted viritualization to the guest OS" i vSphere Client for Windows maskinen.



| Bruker | Privilegie |
| ----------- | ----------- |
| FIH | administrator |
| fihuser | bruker |

<br>

## 3.1 Oppsett av Docker på Windows:
For installasjon av Docker ble [installasjonsguiden _(https://docs.docker.com/desktop/install/windows-install/)_](https://docs.docker.com/desktop/install/windows-install/) til Docker Inc fulgt. 

Skrur på WSL ved å kjøre kommandoen ```wsl --install``` i Powershell.

Åpner REGEDIT og endrer HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\LxssManager\Start til 2 og starter maskinen på nytt. 

Åpner Powershell som administrator og kjører ```
Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Windows-Subsystem-Linux```


Vi installerte Docker Desktop ved å laste ned og kjøre "Docker Desktop Installer.exe" fra [installasjonsguiden _(https://docs.docker.com/desktop/install/windows-install/)_]. 