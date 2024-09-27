# I. Récolte d'informations

## 🌞 Adresses IP de ta machine

1. **Affiche l'adresse IP que ta machine a sur sa carte réseau WiFi :**

    - Ma commande :
    `ipconfig`
    
    - Résultat :
    ```
    Carte réseau sans fil Wi-Fi :
       Adresse IPv4. . . . . . . . . . . . . .: 10.33.79.11
    ```

2. **Affiche l'adresse IP que ta machine a sur sa carte réseau Ethernet :**

    - Ma commande :
    `ipconfig`
    
    - Résultat :
    ```
    Carte Ethernet Ethernet 2 :

   Suffixe DNS propre à la connexion. . . :
   Adresse IPv6 de liaison locale. . . . .: fe80::fc74:5e6e:9008:decc%11
   Adresse IPv4. . . . . . . . . . . . . .: 192.168.56.1
   Masque de sous-réseau. . . . . . . . . : 255.255.255.0
    ```
## 🌞 Si t'as un accès internet normal, d'autres infos sont forcément dispos...

1. **affiche l'adresse IP de la passerelle du réseau local**
    
    - Ma commande : `ipconfig`

    - Résultat : 
    ```
    Carte réseau sans fil Wi-Fi :

     Passerelle par défaut. . . . . . . . . : 10.33.79.254
    ```
2. **affiche l'adresse IP du serveur DNS que connaît ton PC**

    - Ma commande : `ipconfig /all`

    - Le Résultat : 
    ```
    Carte réseau sans fil Wi-Fi :
    
     Serveurs DNS. . .  . . . . . . . . . . : 8.8.8.8
                                       1.1.1.1
    ```
3. **affiche l'adresse IP du serveur DHCP que connaît ton PC**

    - Ma commande : `ipconfig /all`

    - Le Résultat : 
    ```
    Carte réseau sans fil Wi-Fi :

     Serveur DHCP . . . . . . . . . . . . . : 10.33.79.254
    ```
## 🌟 BONUS : Détermine s'il y a un pare-feu actif sur ta machine

1. **détermine s'il exise un pare-feu actif sur votre machine**
    
    - Ma commande : `Get-NetFirewallProfile | Format-Table Name, Enabled`

    - Le Résultat : 
```
Name    Enabled
----    -------
Domain     True
Private    True
Public     True
```  

2. **si oui, je veux aussi voir une commande pour lister les règles du pare-feu**
    
    - Ma commande : `Get-NetFirewallRule`

    - Le Résultat : 
```
Name                          : NETDIS-SSDPSrv-Out-UDP
DisplayName                   : Découverte de réseau (SSDP-Sortie)
Description                   : Règle de trafic sortant pour la découverte de réseau
                            pour autoriser l’utilisation du protocole SSDP
                            (Simple Service Discovery Protocol). [UDP 1900]
DisplayGroup                  : Recherche du réseau
Group                         : @FirewallAPI.dll,-32752
Enabled                       : False
Profile                       : Domain, Public
Platform                      : {}
Direction                     : Outbound
Action                        : Allow
EdgeTraversalPolicy           : Block
LooseSourceMapping            : False
LocalOnlyMapping              : False
Owner                         :
PrimaryStatus                 : OK
Status                        : La règle a été analysée à partir de la banque. (65536)
EnforcementStatus             : NotApplicable
PolicyStoreSource             : PersistentStore
PolicyStoreSourceType         : Local
RemoteDynamicKeywordAddresses : {}
PolicyAppId                   :
```

 # II. Utiliser le réseau

## 🌞 Envoie un ping vers...

1. **toi-même !**

    - Ma commande : `ping 10.33.79.11`
    
    - Résultat :
```
Envoi d’une requête 'Ping'  10.33.79.11 avec 32 octets de données :
Réponse de 10.33.79.11 : octets=32 temps<1ms TTL=128
Réponse de 10.33.79.11 : octets=32 temps<1ms TTL=128
Réponse de 10.33.79.11 : octets=32 temps<1ms TTL=128
Réponse de 10.33.79.11 : octets=32 temps<1ms TTL=128

Statistiques Ping pour 10.33.79.11:
Paquets : envoyés = 4, reçus = 4, perdus = 0 (perte 0%),
Durée approximative des boucles en millisecondes :
Minimum = 0ms, Maximum = 0ms, Moyenne = 0ms
```

2. **vers l'adresse IP**

    - Ma commande : `ping 127.0.0.1`
    
    - Résultat :
```
Envoi d’une requête 'Ping'  127.0.0.1 avec 32 octets de données :
Réponse de 127.0.0.1 : octets=32 temps<1ms TTL=128
Réponse de 127.0.0.1 : octets=32 temps<1ms TTL=128
Réponse de 127.0.0.1 : octets=32 temps<1ms TTL=128
Réponse de 127.0.0.1 : octets=32 temps<1ms TTL=128

Statistiques Ping pour 127.0.0.1:
Paquets : envoyés = 4, reçus = 4, perdus = 0 (perte 0%),
Durée approximative des boucles en millisecondes :
Minimum = 0ms, Maximum = 0ms, Moyenne = 0ms
```
## 🌞 On continue avec ping. Envoie un ping vers...

1. **ta passerelle**

```
PS C:\Users\amgoa> ipconfig

Configuration IP de Windows

Carte réseau sans fil Wi-Fi :

Suffixe DNS propre à la connexion. . . :
Adresse IPv6 de liaison locale. . . . .: fe80::eb8d:747e:4b86:3414%14
Adresse IPv4. . . . . . . . . . . . . .: 10.33.79.11
Masque de sous-réseau. . . . . . . . . : 255.255.240.0
Passerelle par défaut. . . . . . . . . : 10.33.79.254

Carte Ethernet Connexion réseau Bluetooth :

Statut du média. . . . . . . . . . . . : Média déconnecté
Suffixe DNS propre à la connexion. . . :

PS C:\Users\amgoa> ping 10.33.79.254

Envoi d’une requête 'Ping'  10.33.79.254 avec 32 octets de données :
Délai d’attente de la demande dépassé.

Statistiques Ping pour 10.33.79.254:
    Paquets : envoyés = 1, reçus = 0, perdus = 1 (perte 100%),
```
2. **un(e) pote sur le réseau**
```
PS C:\Users\amgoa> ping 10.33.66.78

Envoi d’une requête 'Ping'  10.33.66.78 avec 32 octets de données :
Réponse de 10.33.66.78 : octets=32 temps=49 ms TTL=64
Réponse de 10.33.66.78 : octets=32 temps=64 ms TTL=64
Réponse de 10.33.66.78 : octets=32 temps=82 ms TTL=64
Réponse de 10.33.66.78 : octets=32 temps=89 ms TTL=64

Statistiques Ping pour 10.33.66.78:
    Paquets : envoyés = 4, reçus = 4, perdus = 0 (perte 0%),
Durée approximative des boucles en millisecondes :
    Minimum = 49ms, Maximum = 89ms, Moyenne = 71ms
```
3. **un site internet**
```
PS C:\Users\amgoa> ping www.thinkerview.com

Envoi d’une requête 'ping' sur www.thinkerview.com [188.114.97.7] avec 32 octets de données :
Réponse de 188.114.97.7 : octets=32 temps=17 ms TTL=55
Réponse de 188.114.97.7 : octets=32 temps=19 ms TTL=55
Réponse de 188.114.97.7 : octets=32 temps=15 ms TTL=55
Réponse de 188.114.97.7 : octets=32 temps=16 ms TTL=55

Statistiques Ping pour 188.114.97.7:
    Paquets : envoyés = 4, reçus = 4, perdus = 0 (perte 0%),
Durée approximative des boucles en millisecondes :
    Minimum = 15ms, Maximum = 19ms, Moyenne = 16ms
```
## 🌞 Faire une requête DNS à la main 

1. **effectue une requête DNS à la main pour obtenir l'adresse IP qui correspond aux noms de domaine suivants: www.thinkerview.com www.wikileaks.org www.torproject.org**
```
PS C:\Users\amgoa>  nslookup www.thinkerview.com
Serveur :   dns.google
Address:  8.8.8.8

Réponse ne faisant pas autorité :
Nom :    www.thinkerview.com
Addresses:  2a06:98c1:3121::7
          2a06:98c1:3120::7
          188.114.97.7
          188.114.96.7

PS C:\Users\amgoa> nslookup www.wikileaks.org
Serveur :   dns.google
Address:  8.8.8.8

Réponse ne faisant pas autorité :
Nom :    wikileaks.org
Addresses:  51.159.197.136
          80.81.248.21
Aliases:  www.wikileaks.org

PS C:\Users\amgoa> nslookup www.torproject.org
Serveur :   dns.google
Address:  8.8.8.8

Réponse ne faisant pas autorité :
Nom :    www.torproject.org
Addresses:  2a01:4f9:c010:19eb::1
          2a01:4f8:fff0:4f:266:37ff:fe2c:5d19
          2620:7:6002:0:466:39ff:fe7f:1826
          2a01:4f8:fff0:4f:266:37ff:feae:3bbc
          2620:7:6002:0:466:39ff:fe32:e3dd
          116.202.120.165
          204.8.99.144
          95.216.163.36
          204.8.99.146
          116.202.120.166
```
# III. Sniffer le réseau

## 🌞 J'attends dans le dépôt git de rendu un fichier ping.pcap
## 🌞 Livrez un deuxième fichier : dns.pcap
# IV. Network scanning et adresses IP

## 🌞 Effectue un scan du réseau auquel tu es connecté
```
PS C:\Users\amgoa> nmap.exe -sn -PR 10.33.79.11/20
Starting Nmap 7.95 ( https://nmap.org ) at 2024-09-27 12:04 Paris, Madrid (heure dÆÚtÚ)
Nmap scan report for 10.33.66.78
Host is up (0.063s latency).
MAC Address: E4:B3:18:48:36:68 (Intel Corporate)
Nmap scan report for 10.33.67.113
Host is up (0.14s latency).
MAC Address: D2:91:DE:DF:9A:6E (Unknown)
Nmap scan report for 10.33.69.68
Host is up (0.33s latency).
MAC Address: EE:E8:D9:89:3F:F1 (Unknown)
Nmap scan report for 10.33.69.69
Host is up (0.0060s latency).
MAC Address: 98:BD:80:8B:C9:FA (Intel Corporate)
Nmap scan report for 10.33.69.89
Host is up (0.88s latency).
MAC Address: AC:C9:06:10:14:B6 (Apple)
Nmap scan report for 10.33.69.90
Host is up (0.011s latency).
MAC Address: 60:E9:AA:DD:EE:4D (Cloud Network Technology Singapore PTE.)
Nmap scan report for 10.33.69.92
Host is up (0.089s latency).
```
## 🌞 Changer d'adresse IP
```
PS C:\Users\amgoa> ipconfig /all

Carte réseau sans fil Wi-Fi :
Suffixe DNS propre à la connexion. . . :
Description. . . . . . . . . . . . . . : Intel(R) Wi-Fi 6E AX211 160MHz
Adresse physique . . . . . . . . . . . : D0-65-78-A2-A1-20
DHCP activé. . . . . . . . . . . . . . : Non
Configuration automatique activée. . . : Oui
Adresse IPv6 de liaison locale. . . . .: fe80::eb8d:747e:4b86:3414%14(préféré)
Adresse IPv4. . . . . . . . . . . . . .: 10.33.77.1(préféré)
Masque de sous-réseau. . . . . . . . . : 255.255.240.0
Passerelle par défaut. . . . . . . . . : 10.33.79.254
IAID DHCPv6 . . . . . . . . . . . : 147875192
DUID de client DHCPv6. . . . . . . . : 00-01-00-01-2E-3B-02-FD-CC-28-AA-BA-CD-5C
Serveurs DNS. . .  . . . . . . . . . . : 8.8.8.8
NetBIOS sur Tcpip. . . . . . . . . . . : Activé
```