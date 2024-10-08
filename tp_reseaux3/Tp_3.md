 - GOASDOUÉ Anthony | B1 INFO
 
# TP3 : 32°13'34"N 95°03'27"W

## I. ARP basics

### ☀️ Avant de continuer...
```powershell
PS C:\Windows\system32> ipconfig /all

Carte réseau sans fil Connexion au réseau local* 1 :

Carte réseau sans fil Wi-Fi :
   Adresse physique . . . . . . . . . . . : D0-65-78-A2-A1-20
```

### ☀️ Affichez votre table ARP
```powershell
PS C:\Windows\system32> arp -a

Interface : 192.168.56.1 --- 0xb
  Adresse Internet      Adresse physique      Type
  192.168.56.255        ff-ff-ff-ff-ff-ff     statique
  224.0.0.22            01-00-5e-00-00-16     statique
  224.0.0.251           01-00-5e-00-00-fb     statique
  224.0.0.252           01-00-5e-00-00-fc     statique
  230.0.0.1             01-00-5e-00-00-01     statique
  239.255.255.250       01-00-5e-7f-ff-fa     statique

Interface : 10.33.79.11 --- 0xe
  Adresse Internet      Adresse physique      Type
  10.33.65.63           44-af-28-c3-6a-9f     dynamique
  10.33.66.78           e4-b3-18-48-36-68     dynamique
  10.33.79.254          7c-5a-1c-d3-d8-76     dynamique
  10.33.79.255          ff-ff-ff-ff-ff-ff     statique
  224.0.0.22            01-00-5e-00-00-16     statique
  224.0.0.251           01-00-5e-00-00-fb     statique
  224.0.0.252           01-00-5e-00-00-fc     statique
  230.0.0.1             01-00-5e-00-00-01     statique
  239.255.255.250       01-00-5e-7f-ff-fa     statique
  255.255.255.255       ff-ff-ff-ff-ff-ff     statique
```
### ☀️ Déterminez l'adresse MAC de la passerelle du réseau de l'école
```powershell
PS C:\Windows\system32> arp -a

Interface : 10.33.79.11 --- 0xe
  Adresse Internet      Adresse physique      Type
  10.33.79.254          7c-5a-1c-d3-d8-76     dynamique
```

### ☀️ Supprimez la ligne qui concerne la passerelle
```powershell 
PS C:\Windows\system32> arp -d 10.33.79.254
```

### ☀️ Prouvez que vous avez supprimé la ligne dans la table ARP
```powershell
PS C:\Windows\system32> arp -a

Interface : 192.168.56.1 --- 0xb
  Adresse Internet      Adresse physique      Type
  192.168.56.255        ff-ff-ff-ff-ff-ff     statique
  224.0.0.22            01-00-5e-00-00-16     statique
  224.0.0.251           01-00-5e-00-00-fb     statique
  224.0.0.252           01-00-5e-00-00-fc     statique
  230.0.0.1             01-00-5e-00-00-01     statique
  239.255.255.250       01-00-5e-7f-ff-fa     statique
```

### ☀️ Wireshark
[arp1](./arp1.pcap)

## II. ARP dans un réseau local

## 1. Basics
### ☀️ Déterminer
```ps
PS C:\Windows\system32> arp -a

Interface : 192.168.28.16 --- 0xe
  Adresse Internet      Adresse physique      Type
  192.168.28.249        6a-b2-90-ea-ae-be     dynamique
```
### ☀️ DIY
```ps
PS C:\Windows\system32> ipconfig

Carte réseau sans fil Wi-Fi :

   Suffixe DNS propre à la connexion. . . :
   Adresse IPv6 de liaison locale. . . . .: fe80::eb8d:747e:4b86:3414%14
   Adresse IPv4. . . . . . . . . . . . . .: 192.168.28.1
   Masque de sous-réseau. . . . . . . . . : 255.255.255.0
   Passerelle par défaut. . . . . . . . . : 192.168.28.249
```
### ☀️ Pingz !
- Adrien : 
```ps
PS C:\Windows\system32> ping 192.168.28.69

Envoi d’une requête 'Ping'  192.168.28.69 avec 32 octets de données :
Réponse de 192.168.28.69 : octets=32 temps=8 ms TTL=128
Réponse de 192.168.28.69 : octets=32 temps=14 ms TTL=128
Réponse de 192.168.28.69 : octets=32 temps=8 ms TTL=128
Réponse de 192.168.28.69 : octets=32 temps=17 ms TTL=128

Statistiques Ping pour 192.168.28.69:
    Paquets : envoyés = 4, reçus = 4, perdus = 0 (perte 0%),
Durée approximative des boucles en millisecondes :
    Minimum = 8ms, Maximum = 17ms, Moyenne = 11ms
```
- Johann :
```ps
PS C:\Windows\system32> ping 192.168.28.33

Envoi d’une requête 'Ping'  192.168.28.33 avec 32 octets de données :
Réponse de 192.168.28.33 : octets=32 temps=181 ms TTL=128
Réponse de 192.168.28.33 : octets=32 temps=18 ms TTL=128
Réponse de 192.168.28.33 : octets=32 temps=33 ms TTL=128
Réponse de 192.168.28.33 : octets=32 temps=132 ms TTL=128

Statistiques Ping pour 192.168.28.33:
    Paquets : envoyés = 4, reçus = 4, perdus = 0 (perte 0%),
Durée approximative des boucles en millisecondes :
    Minimum = 18ms, Maximum = 181ms, Moyenne = 91ms
```
- Baptiste :
```ps
PS C:\Windows\system32> ping 192.168.28.66

Envoi d’une requête 'Ping'  192.168.28.66 avec 32 octets de données :
Réponse de 192.168.28.66 : octets=32 temps=135 ms TTL=128
Réponse de 192.168.28.66 : octets=32 temps=33 ms TTL=128
Réponse de 192.168.28.66 : octets=32 temps=254 ms TTL=128
Réponse de 192.168.28.66 : octets=32 temps=158 ms TTL=128

Statistiques Ping pour 192.168.28.66:
    Paquets : envoyés = 4, reçus = 4, perdus = 0 (perte 0%),
Durée approximative des boucles en millisecondes :
    Minimum = 33ms, Maximum = 254ms, Moyenne = 145ms
```
- xkcd.com
```ps
PS C:\Windows\system32> ping xkcd.com

Envoi d’une requête 'ping' sur xkcd.com [151.101.64.67] avec 32 octets de données :
Réponse de 151.101.64.67 : octets=32 temps=10 ms TTL=57
Réponse de 151.101.64.67 : octets=32 temps=36 ms TTL=57
Réponse de 151.101.64.67 : octets=32 temps=19 ms TTL=57
Réponse de 151.101.64.67 : octets=32 temps=12 ms TTL=57

Statistiques Ping pour 151.101.64.67:
    Paquets : envoyés = 4, reçus = 4, perdus = 0 (perte 0%),
Durée approximative des boucles en millisecondes :
    Minimum = 10ms, Maximum = 36ms, Moyenne = 19ms
```
## 2. ARP
### ☀️ Affichez votre table ARP !
```ps
PS C:\Windows\system32> arp -a

Interface : 192.168.56.1 --- 0xb
  Adresse Internet      Adresse physique      Type
  192.168.56.255        ff-ff-ff-ff-ff-ff     statique
  224.0.0.22            01-00-5e-00-00-16     statique
  224.0.0.251           01-00-5e-00-00-fb     statique
  224.0.0.252           01-00-5e-00-00-fc     statique
  230.0.0.1             01-00-5e-00-00-01     statique
  239.255.255.250       01-00-5e-7f-ff-fa     statique

Interface : 192.168.28.1 --- 0xe
  Adresse Internet      Adresse physique      Type
  192.168.28.33         a8-41-f4-ea-29-b5     dynamique
  192.168.28.66         3a-8b-bb-d2-40-03     dynamique
  192.168.28.69         58-96-71-9c-c7-6e     dynamique
  192.168.28.249        6a-b2-90-ea-ae-be     dynamique
  192.168.28.255        ff-ff-ff-ff-ff-ff     statique
  224.0.0.22            01-00-5e-00-00-16     statique
  224.0.0.251           01-00-5e-00-00-fb     statique
  224.0.0.252           01-00-5e-00-00-fc     statique
  239.255.255.250       01-00-5e-7f-ff-fa     statique
  255.255.255.255       ff-ff-ff-ff-ff-ff     statique
```
### ☀️ Capture arp2.pcap
[arp2](./arp2.pcap)
