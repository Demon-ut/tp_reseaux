- GOASDOUÉ Anthony / B1 info
# TP2 : Hey yo tell a neighbor tell a friend

## I. Simplest LAN

### 🌞 Prouvez que votre configuration est effective
---

```
PS C:\Windows\system32> Get-NetIPAddress -InterfaceAlias "Ethernet"
>>


IPAddress         : fe80::8acd:293f:12c5:e87f%4
InterfaceIndex    : 4
InterfaceAlias    : Ethernet
AddressFamily     : IPv6
Type              : Unicast
PrefixLength      : 64
PrefixOrigin      : WellKnown
SuffixOrigin      : Link
AddressState      : Preferred
ValidLifetime     :
PreferredLifetime :
SkipAsSource      : False
PolicyStore       : ActiveStore

IPAddress         : 10.6.6.1
InterfaceIndex    : 4
InterfaceAlias    : Ethernet
AddressFamily     : IPv4
Type              : Unicast
PrefixLength      : 24
PrefixOrigin      : Manual
SuffixOrigin      : Manual
AddressState      : Preferred
ValidLifetime     :
PreferredLifetime :
SkipAsSource      : False
PolicyStore       : ActiveStore
```

### 🌞 Tester que votre LAN + votre adressage IP est fonctionnel
---
```
PS C:\Windows\system32> ping 10.6.6.2

Envoi d’une requête 'Ping'  10.6.6.2 avec 32 octets de données :
Réponse de 10.6.6.2 : octets=32 temps=4 ms TTL=128
Réponse de 10.6.6.2 : octets=32 temps=4 ms TTL=128
Réponse de 10.6.6.2 : octets=32 temps=3 ms TTL=128
Réponse de 10.6.6.2 : octets=32 temps=4 ms TTL=128

Statistiques Ping pour 10.6.6.2:
    Paquets : envoyés = 4, reçus = 4, perdus = 0 (perte 0%),
Durée approximative des boucles en millisecondes :
    Minimum = 3ms, Maximum = 4ms, Moyenne = 3ms
```

### 🌞 Capture de ping
---

```
PS C:\Windows\system32> ping -t 10.6.6.2

Envoi d’une requête 'Ping'  10.6.6.2 avec 32 octets de données :
Réponse de 10.6.6.2 : octets=32 temps=3 ms TTL=128
Réponse de 10.6.6.2 : octets=32 temps=3 ms TTL=128
Réponse de 10.6.6.2 : octets=32 temps=3 ms TTL=128
Réponse de 10.6.6.2 : octets=32 temps=3 ms TTL=128
Réponse de 10.6.6.2 : octets=32 temps=3 ms TTL=128
Réponse de 10.6.6.2 : octets=32 temps=4 ms TTL=128
Réponse de 10.6.6.2 : octets=32 temps=3 ms TTL=128
Réponse de 10.6.6.2 : octets=32 temps=3 ms TTL=128
Réponse de 10.6.6.2 : octets=32 temps=3 ms TTL=128
Réponse de 10.6.6.2 : octets=32 temps=3 ms TTL=128
Réponse de 10.6.6.2 : octets=32 temps=4 ms TTL=128
Réponse de 10.6.6.2 : octets=32 temps=3 ms TTL=128
Réponse de 10.6.6.2 : octets=32 temps=4 ms TTL=128
Réponse de 10.6.6.2 : octets=32 temps=3 ms TTL=128
Réponse de 10.6.6.2 : octets=32 temps=3 ms TTL=128
Réponse de 10.6.6.2 : octets=32 temps=14 ms TTL=128
Réponse de 10.6.6.2 : octets=32 temps=4 ms TTL=128
Réponse de 10.6.6.2 : octets=32 temps=3 ms TTL=128
Réponse de 10.6.6.2 : octets=32 temps=3 ms TTL=128
Réponse de 10.6.6.2 : octets=32 temps=3 ms TTL=128
Réponse de 10.6.6.2 : octets=32 temps=3 ms TTL=128
Réponse de 10.6.6.2 : octets=32 temps=3 ms TTL=128
Réponse de 10.6.6.2 : octets=32 temps=2 ms TTL=128
Réponse de 10.6.6.2 : octets=32 temps=3 ms TTL=128
Réponse de 10.6.6.2 : octets=32 temps=3 ms TTL=128
Réponse de 10.6.6.2 : octets=32 temps=3 ms TTL=128
Réponse de 10.6.6.2 : octets=32 temps=4 ms TTL=128
Réponse de 10.6.6.2 : octets=32 temps=3 ms TTL=128

Statistiques Ping pour 10.6.6.2:
    Paquets : envoyés = 28, reçus = 28, perdus = 0 (perte 0%),
Durée approximative des boucles en millisecondes :
    Minimum = 2ms, Maximum = 14ms, Moyenne = 3ms
Ctrl+C
```
+ le fichier `ping.pcap`

## II. Utilisation des ports
## Client

### 🌞 Sur le PC client
---
```
PS C:\Users\amgoa\Desktop\Appli réseaux\netcat-win32-1.11\netcat-1.11> ./nc64.exe 10.6.6.2 9999
```

### 🌞 Echangez-vous des messages
---

```
PS C:\Users\amgoa\Desktop\Appli réseaux\netcat-win32-1.11\netcat-1.11> ./nc64.exe 10.6.6.2 9999
Salut ?
HAAA AAAU SECOURS TES QUI FRERE TU FAIS QUOI CHEZ WAM
je suis modo ;)
OK MEN FOUS
```

### 🌞 Utilisez une commande qui permet de voir la connexion en cours
---
```
PS C:\Users\amgoa\Desktop\Appli réseaux\netcat-win32-1.11\netcat-1.11> netstat -a -n -b | Select-String nc64.exe -Context 1,0

    TCP    10.6.6.1:15032         10.6.6.2:9999          ESTABLISHED
>  [nc64.exe]
```

### 🌞 Faites une capture Wireshark complète d'un échange
--- 
```
Netcat1.pcap
```


# 🌞 Inversez les rôles
## Serveur
### 🌞 Sur le PC serveur
--- 
```
PS C:\Users\amgoa\Desktop\Appli réseaux\netcat-win32-1.11\netcat-1.11> ./nc64.exe -l -p 9999
```
### 🌞 Sur le PC serveur toujours
```powershell
TCP    10.6.6.1:9999          10.6.6.2:9002          ESTABLISHED
[nc64.exe]
```

### 🌞 Utilisez une commande qui permet de voir la connexion en cours
--- 

```powershell
PS C:\Windows\system32> 

 -a -n -b | Select-String nc64.exe -Context 1,0

    TCP    10.6.6.1:9999          10.6.6.2:9078          ESTABLISHED
>  [nc64.exe]
```

### 🌞 Faites une capture Wireshark complète d'un échange
---

[coucoucuuuuuu](./netcat2.pcap)

## III. Analyse de vos applications usuelles

### 🌞 Utilisez Wireshark pour capturer du trafic HTTP
---
[http](./http.pcap)
### 🌞 Pour les 5 applications
---


#### Minecraft
```
PS C:\Windows\system32> netstat -a -n -b | Select-String Minec -Context 1,0

    TCP    10.33.79.11:18930      13.95.168.57:443       CLOSE_WAIT
>  [Minecraft.exe]
    TCP    10.33.79.11:18933      13.107.246.42:443      CLOSE_WAIT
>  [Minecraft.exe]
    TCP    10.33.79.11:18989      8.8.8.8:443            ESTABLISHED
>  [Minecraft.exe]
    TCP    10.33.79.11:18990      162.159.61.3:443       ESTABLISHED
>  [Minecraft.exe]
    TCP    10.33.79.11:19041      74.125.206.94:443      ESTABLISHED
>  [Minecraft.exe]
    TCP    10.33.79.11:19046      13.107.246.42:443      ESTABLISHED
>  [Minecraft.exe]
    TCP    10.33.79.11:19048      13.107.246.42:443      ESTABLISHED
>  [Minecraft.exe]
```
[service1](./service1.pcap)

### Spotify
```
PS C:\Windows\system32> netstat -a -n -b | Select-String Spot -Context 1,0

    TCP    0.0.0.0:19228          0.0.0.0:0              LISTENING
>  [Spotify.exe]
    TCP    0.0.0.0:57621          0.0.0.0:0              LISTENING
>  [Spotify.exe]
    TCP    10.33.79.11:19238      104.199.65.9:4070      ESTABLISHED
>  [Spotify.exe]
    TCP    10.33.79.11:19248      35.186.224.41:443      ESTABLISHED
>  [Spotify.exe]
    TCP    10.33.79.11:19260      35.186.224.41:443      ESTABLISHED
>  [Spotify.exe]
    TCP    10.33.79.11:19284      35.186.224.26:443      ESTABLISHED
>  [Spotify.exe]
    TCP    10.33.79.11:19291      216.58.213.74:443      ESTABLISHED
>  [Spotify.exe]
    TCP    10.33.79.11:19292      35.186.224.26:443      ESTABLISHED
>  [Spotify.exe]
    TCP    10.33.79.11:19297      34.120.195.249:443     ESTABLISHED
>  [Spotify.exe]
    TCP    10.33.79.11:19308      74.125.206.94:443      ESTABLISHED
>  [Spotify.exe]
    UDP    0.0.0.0:1900           *:*
>  [Spotify.exe]
    UDP    0.0.0.0:1900           *:*
>  [Spotify.exe]
    UDP    0.0.0.0:5353           *:*
>  [Spotify.exe]
    UDP    0.0.0.0:5353           *:*
>  [Spotify.exe]
    UDP    0.0.0.0:5353           *:*
>  [Spotify.exe]
    UDP    0.0.0.0:5353           *:*
>  [Spotify.exe]
    UDP    0.0.0.0:5353           *:*
>  [Spotify.exe]
    UDP    0.0.0.0:5353           *:*
>  [Spotify.exe]
    UDP    0.0.0.0:49824          34.120.195.249:443
>  [Spotify.exe]
    UDP    0.0.0.0:53361          8.8.4.4:443
>  [Spotify.exe]
    UDP    0.0.0.0:57189          *:*
>  [Spotify.exe]
    UDP    0.0.0.0:57190          *:*
>  [Spotify.exe]
    UDP    0.0.0.0:57621          *:*
>  [Spotify.exe]
    UDP    0.0.0.0:60608          35.186.224.26:443
>  [Spotify.exe]
    UDP    0.0.0.0:63003          8.8.4.4:443
>  [Spotify.exe]
    UDP    0.0.0.0:63029          35.186.224.26:443
>  [Spotify.exe]
    UDP    [::]:5353              *:*
>  [Spotify.exe]
    UDP    [::]:5353              *:*
>  [Spotify.exe]
    UDP    [::]:5353              *:*
>  [Spotify.exe]
    UDP    [::]:5353              *:*
>  [Spotify.exe]
```
[service2](./service2.pcap)

### Teams
```powershell
PS C:\Windows\system32> netstat -a -n -b | Select-String team -Context 1,0

    TCP    10.33.79.11:18205      57.153.124.213:443     ESTABLISHED
>  [ms-teams.exe]
    TCP    10.33.79.11:18206      52.123.200.56:443      ESTABLISHED
>  [ms-teams.exe]
    TCP    10.33.79.11:20299      20.50.80.213:443       ESTABLISHED
>  [ms-teams.exe]
    TCP    10.33.79.11:20301      20.50.80.213:443       ESTABLISHED
>  [ms-teams.exe]
    UDP    0.0.0.0:50089          *:*
>  [ms-teams.exe]
    UDP    0.0.0.0:55857          *:*
>  [ms-teams.exe]
    UDP    0.0.0.0:59540          *:*
>  [ms-teams.exe]
    UDP    [::]:50089             *:*
>  [ms-teams.exe]
    UDP    [::]:55857             *:*
>  [ms-teams.exe]
    UDP    [::]:59540             *:*
>  [ms-teams.exe]

```
[service3](./service3.pcap)

### Épic game luncher
```
PS C:\Windows\system32> netstat -a -n -b | Select-String epic -Context 1,0

    TCP    10.33.79.11:20556      3.215.246.152:443      ESTABLISHED
>  [EpicGamesLauncher.exe]
    TCP    10.33.79.11:20557      44.206.185.128:443     ESTABLISHED
>  [EpicGamesLauncher.exe]
    TCP    10.33.79.11:20573      104.18.21.94:443       ESTABLISHED
>  [EpicWebHelper.exe]
    TCP    10.33.79.11:20574      18.244.28.75:443       ESTABLISHED
>  [EpicGamesLauncher.exe]
    TCP    10.33.79.11:20577      3.214.46.187:443       ESTABLISHED
>  [EpicGamesLauncher.exe]
    TCP    10.33.79.11:20579      104.18.3.64:443        ESTABLISHED
>  [EpicWebHelper.exe]
    TCP    10.33.79.11:20588      8.8.8.8:443            ESTABLISHED
>  [EpicWebHelper.exe]
    TCP    10.33.79.11:20589      8.8.8.8:443            ESTABLISHED
>  [EpicWebHelper.exe]
    TCP    10.33.79.11:20590      8.8.8.8:443            ESTABLISHED
>  [EpicWebHelper.exe]
    TCP    10.33.79.11:20591      172.64.41.3:443        ESTABLISHED
>  [EpicWebHelper.exe]
    TCP    10.33.79.11:20592      172.64.41.3:443        ESTABLISHED
>  [EpicWebHelper.exe]
    TCP    10.33.79.11:20593      172.64.41.3:443        ESTABLISHED
>  [EpicWebHelper.exe]
    TCP    10.33.79.11:20594      18.155.129.100:443     ESTABLISHED
>  [EpicWebHelper.exe]
    TCP    10.33.79.11:20595      2.19.201.90:443        ESTABLISHED
>  [EpicWebHelper.exe]
    TCP    10.33.79.11:20596      34.200.200.56:443      ESTABLISHED
>  [EpicWebHelper.exe]
    TCP    10.33.79.11:20597      2.19.201.90:443        ESTABLISHED
>  [EpicWebHelper.exe]
    TCP    10.33.79.11:20599      3.225.179.124:443      ESTABLISHED
>  [EpicWebHelper.exe]
    TCP    10.33.79.11:20600      23.65.196.61:443       ESTABLISHED
>  [EpicWebHelper.exe]
    TCP    10.33.79.11:20602      34.196.117.32:443      ESTABLISHED
>  [EpicWebHelper.exe]
    TCP    10.33.79.11:20604      54.159.61.166:443      ESTABLISHED
>  [EpicWebHelper.exe]
    TCP    10.33.79.11:20605      44.218.56.236:443      ESTABLISHED
>  [EpicWebHelper.exe]
    TCP    10.33.79.11:20607      2.19.201.90:443        ESTABLISHED
>  [EpicGamesLauncher.exe]
    TCP    10.33.79.11:20608      104.18.2.64:443        ESTABLISHED
>  [EpicWebHelper.exe]
    UDP    0.0.0.0:6666           *:*
>  [EpicGamesLauncher.exe]
    UDP    0.0.0.0:54386          *:*
>  [EpicGamesLauncher.exe]
    UDP    0.0.0.0:56860          8.8.8.8:443
>  [EpicWebHelper.exe]
```
[service4](./service4.pcap)

### Steam
```
PS C:\Windows\system32> netstat -a -n -b | Select-String stea -Context 1,0

    TCP    0.0.0.0:27036          0.0.0.0:0              LISTENING
>  [Steam.exe]
    TCP    10.33.79.11:20887      92.122.166.120:443     ESTABLISHED
>  [Steam.exe]
    TCP    10.33.79.11:20888      2.21.34.18:80          ESTABLISHED
>  [Steam.exe]
    TCP    10.33.79.11:20908      8.8.4.4:443            ESTABLISHED
>  [steamwebhelper.exe]
    TCP    10.33.79.11:20909      162.159.61.3:443       ESTABLISHED
>  [steamwebhelper.exe]
    TCP    10.33.79.11:20911      162.159.61.3:443       ESTABLISHED
>  [steamwebhelper.exe]
    TCP    10.33.79.11:20912      8.8.4.4:443            ESTABLISHED
>  [steamwebhelper.exe]
    TCP    10.33.79.11:20952      23.217.238.254:443     ESTABLISHED
>  [Steam.exe]
    TCP    10.33.79.11:20953      192.229.221.95:80      ESTABLISHED
>  [Steam.exe]
    TCP    10.33.79.11:20957      155.133.248.42:27018   ESTABLISHED
>  [Steam.exe]
    TCP    10.33.79.11:20958      95.100.252.32:80       ESTABLISHED
>  [Steam.exe]
    TCP    10.33.79.11:20971      23.72.250.72:80        ESTABLISHED
>  [Steam.exe]
    TCP    10.33.79.11:20972      23.72.250.72:80        ESTABLISHED
>  [Steam.exe]
    TCP    10.33.79.11:20973      23.72.250.72:80        ESTABLISHED
>  [Steam.exe]
    TCP    10.33.79.11:20974      23.72.250.72:80        ESTABLISHED
>  [Steam.exe]
    TCP    10.33.79.11:20975      23.72.250.72:80        ESTABLISHED
>  [Steam.exe]
    TCP    10.33.79.11:20976      23.72.250.72:80        ESTABLISHED
>  [Steam.exe]
    TCP    10.33.79.11:20977      23.72.250.72:80        ESTABLISHED
>  [Steam.exe]
    TCP    10.33.79.11:20978      23.72.250.72:80        ESTABLISHED
>  [Steam.exe]
    TCP    10.33.79.11:20982      185.25.182.9:443       ESTABLISHED
>  [Steam.exe]
    TCP    10.33.79.11:20983      23.72.250.143:443      ESTABLISHED
>  [Steam.exe]
    TCP    10.33.79.11:20984      23.72.250.157:443      ESTABLISHED
>  [Steam.exe]
    TCP    10.33.79.11:20985      23.72.250.143:443      ESTABLISHED
>  [Steam.exe]
    TCP    10.33.79.11:20986      23.72.250.143:443      ESTABLISHED
>  [Steam.exe]
    TCP    10.33.79.11:20987      23.72.250.157:443      ESTABLISHED
>  [Steam.exe]
    TCP    10.33.79.11:20988      23.72.250.157:443      ESTABLISHED
>  [Steam.exe]
    TCP    10.33.79.11:20989      23.217.238.254:443     ESTABLISHED
>  [Steam.exe]
    TCP    10.33.79.11:20990      23.217.238.254:443     ESTABLISHED
>  [Steam.exe]
    TCP    10.33.79.11:20991      23.217.238.254:443     ESTABLISHED
>  [Steam.exe]
    TCP    10.33.79.11:20992      23.41.213.48:443       ESTABLISHED
>  [steamwebhelper.exe]
    TCP    10.33.79.11:20993      23.41.213.48:443       ESTABLISHED
>  [steamwebhelper.exe]
    TCP    10.33.79.11:20994      23.41.213.48:443       ESTABLISHED
>  [steamwebhelper.exe]
    TCP    10.33.79.11:20995      23.72.250.139:443      ESTABLISHED
>  [steamwebhelper.exe]
    TCP    10.33.79.11:20996      23.217.238.254:443     ESTABLISHED
>  [steamwebhelper.exe]
    TCP    10.33.79.11:20997      23.72.250.134:443      ESTABLISHED
>  [steamwebhelper.exe]
    TCP    10.33.79.11:20998      23.72.250.134:443      ESTABLISHED
>  [steamwebhelper.exe]
    TCP    10.33.79.11:20999      23.72.250.134:443      ESTABLISHED
>  [steamwebhelper.exe]
    TCP    10.33.79.11:21000      23.217.238.254:443     ESTABLISHED
>  [steamwebhelper.exe]
    TCP    10.33.79.11:21001      23.72.250.136:443      ESTABLISHED
>  [steamwebhelper.exe]
    TCP    10.33.79.11:21014      23.72.250.156:443      ESTABLISHED
>  [steamwebhelper.exe]
    TCP    10.33.79.11:21022      185.25.182.36:443      ESTABLISHED
>  [Steam.exe]
    TCP    10.33.79.11:21023      185.25.182.37:443      ESTABLISHED
>  [Steam.exe]
    TCP    10.33.79.11:21024      2.21.34.73:80          ESTABLISHED
>  [Steam.exe]
    TCP    127.0.0.1:20892        0.0.0.0:0              LISTENING
>  [Steam.exe]
    TCP    127.0.0.1:20892        127.0.0.1:20919        ESTABLISHED
>  [Steam.exe]
    TCP    127.0.0.1:20894        0.0.0.0:0              LISTENING
>  [Steam.exe]
    TCP    127.0.0.1:20894        127.0.0.1:20918        ESTABLISHED
>  [Steam.exe]
    TCP    127.0.0.1:20918        127.0.0.1:20894        ESTABLISHED
>  [steamwebhelper.exe]
    TCP    127.0.0.1:20919        127.0.0.1:20892        ESTABLISHED
>  [steamwebhelper.exe]
    TCP    127.0.0.1:27060        0.0.0.0:0              LISTENING
>  [Steam.exe]
    UDP    0.0.0.0:27036          *:*
>  [Steam.exe]
    UDP    0.0.0.0:63592          8.8.4.4:443
>  [steamwebhelper.exe]
```
[service5](./service5.pcap)