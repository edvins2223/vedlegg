Alle maskiner kjører på VmWare

# Oppsett av Linux

Vi kjører Debian GNU/Linux 11.6.0 x86_64 med standardinstillinger 




| Bruker | Privilegie |
| ----------- | ----------- |
| root | super-user |
| jb | super-user |

## Leserveiledning:
I den påfølgende tekst vil vi bruke "$"- og "#"-symbolet for å vise en kommando slik den skal skrives inn i CMD-konsollet. Disse symbolene skal altså ikke skrives inn. "$"-symbolet representerer kommandoer skrevet av jb brukeren, mens "#"-symbolet representerer kommandoer skrevet av root.


## For å gi brukeren på Linux sudo rettigheter:
```
  $ su #kjør som root
  # sudo visudo
```
Under root i "# User privilege specification" legg til linjen:
```
jb  ALL=(ALL:ALL) ALL
```
og lagre filen.
Deretter tester man om brukeren har fått sudo rettigheter:
```
  # exit
  $ sudo ls -la /root #brukeren jb har sudo privilegier dersom kommandoen viser listen
```

## Oppsett av Docker på Linux
For installasjon av Docker ble installasjonsguiden https://docs.docker.com/engine/install/debian/#prerequisites til Docker Inc fulgt. 

