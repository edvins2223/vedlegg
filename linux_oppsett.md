# Vi har bruker med navn jb og root med navn jb


## For å gi brukeren på Linux sudo rettigheter:
`code`
$ su #kjør som root
# sudo usermod -aG sudo jb
# exit
`code`

Fra nå av: dersom du skriver 
`code`
$ su jb
`code`
vil du få sudo rettigheter med brukeren jb

sudo visudo /etc/sudoers
