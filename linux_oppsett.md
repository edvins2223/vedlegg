# Oppsett av Linux
Vi kjører Debian 11.6.0 64-bit med standardinstillinger

| Bruker | Privilegie |
| ----------- | ----------- |
| root | super-user |
| jb | super-user |


## For å gi brukeren på Linux sudo rettigheter:
```
  $ su #kjør som root
  # sudo usermod -aG sudo jb
  # exit
```

### Fra nå av: 
dersom du skriver 
```
  $ su jb
```
vil du få sudo rettigheter med brukeren jb

```
  sudo visudo /etc/sudoers
```
