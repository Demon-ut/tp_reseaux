#### GOASDOUÉ Anthony | B1 INFO
# TP6 : Des bo services dans des bo LANs
## I. Le setup
## 2. Marche à suivre
### ☀️ Prouvez que...

- une machine du LAN1 peut joindre internet (ping un nom de domaine)

```ps
[tp@dhcp network-scripts]$ ping www.ynov.com
PING www.ynov.com (172.67.74.226) 56(84) bytes of data.
64 bytes from 172.67.74.226 (172.67.74.226): icmp_seq=1 ttl=53 time=17.2 ms
64 bytes from 172.67.74.226 (172.67.74.226): icmp_seq=2 ttl=53 time=17.0 ms
64 bytes from 172.67.74.226 (172.67.74.226): icmp_seq=3 ttl=53 time=17.0 ms
64 bytes from 172.67.74.226 (172.67.74.226): icmp_seq=4 ttl=53 time=18.4 ms
^C
--- www.ynov.com ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 3007ms
rtt min/avg/max/mdev = 16.961/17.386/18.407/0.594 ms
```

- une machine du LAN2 peut joindre internet (ping nom de domaine)

```ps
[tp@web ~]$ ping www.ynov.com
PING www.ynov.com (104.26.11.233) 56(84) bytes of data.
64 bytes from 104.26.11.233 (104.26.11.233): icmp_seq=1 ttl=53 time=19.5 ms
64 bytes from 104.26.11.233 (104.26.11.233): icmp_seq=2 ttl=53 time=17.3 ms
64 bytes from 104.26.11.233 (104.26.11.233): icmp_seq=3 ttl=53 time=16.1 ms
64 bytes from 104.26.11.233 (104.26.11.233): icmp_seq=4 ttl=53 time=16.3 ms
^C
--- www.ynov.com ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 3009ms
rtt min/avg/max/mdev = 16.069/17.304/19.477/1.338 ms
```

- une machine du LAN1 peut joindre une machine du LAN2 (ping une adresse IP)

```ps
[tp@dhcp network-scripts]$ ping 10.6.2.11
PING 10.6.2.11 (10.6.2.11) 56(84) bytes of data.
64 bytes from 10.6.2.11: icmp_seq=1 ttl=63 time=2.02 ms
64 bytes from 10.6.2.11: icmp_seq=2 ttl=63 time=2.58 ms
64 bytes from 10.6.2.11: icmp_seq=3 ttl=63 time=2.66 ms
64 bytes from 10.6.2.11: icmp_seq=4 ttl=63 time=1.46 ms
^C
--- 10.6.2.11 ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 3007ms
rtt min/avg/max/mdev = 1.460/2.179/2.660/0.482 ms
```
## II. LAN clients 
### ☀️ Prouvez que...

- le client a bien récupéré une adresse IP en DHCP 

```ps
2: enp0s3: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast state UP group default qlen 1000
    link/ether 08:00:27:fd:63:9f brd ff:ff:ff:ff:ff:ff
    inet 10.6.1.37/24 metric 100 brd 10.6.1.255 scope global dynamic enp0s3
       valid_lft 415sec preferred_lft 415sec
    inet6 fe80::a00:27ff:fefd:639f/64 scope link
       valid_lft forever preferred_lft forever
```

- vous avez bien la bonne passerelle indiquée

```ps
amgoasdoue@client1:/etc/netplan$ ip r s
default via 10.6.1.254 dev enp0s3 proto dhcp src 10.6.1.37 metric 100
1.1.1.1 via 10.6.1.254 dev enp0s3 proto dhcp src 10.6.1.37 metric 100
10.6.1.0/24 dev enp0s3 proto kernel scope link src 10.6.1.37 metric 100
10.6.1.254 dev enp0s3 proto dhcp scope link src 10.6.1.37 metric 100
```

- vous avez bien 1.1.1.1 en DNS

```ps
amgoasdoue@client1:/etc/netplan$ resolvectl
Global
         Protocols: -LLMNR -mDNS -DNSOverTLS DNSSEC=no/unsupported
  resolv.conf mode: stub

Link 2 (enp0s3)
    Current Scopes: DNS
         Protocols: +DefaultRoute -LLMNR -mDNS -DNSOverTLS DNSSEC=no/unsupported
Current DNS Server: 1.1.1.1
       DNS Servers: 1.1.1.1
```

- que ça ping un nom de domaine public sans problème magueule 

```ps
amgoasdoue@client1:/etc/netplan$ ping www.ynov.com
PING www.ynov.com (104.26.10.233) 56(84) bytes of data.
64 bytes from 104.26.10.233: icmp_seq=1 ttl=53 time=16.8 ms
64 bytes from 104.26.10.233: icmp_seq=2 ttl=53 time=19.8 ms
64 bytes from 104.26.10.233: icmp_seq=3 ttl=53 time=16.7 ms
64 bytes from 104.26.10.233: icmp_seq=4 ttl=53 time=16.3 ms

^C--- www.ynov.com ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 3005ms
rtt min/avg/max/mdev = 16.279/17.394/19.843/1.426 ms
```

## III. LAN serveurzzzz

## III. 1. Serveur Web

### 3. Analyse et test

### ☀️ Déterminer sur quel port écoute le serveur NGINX

```ps
[tp@web network-scripts]$ sudo ss -lnpt | grep 80
LISTEN 0      511          0.0.0.0:80        0.0.0.0:*    users:(("nginx",pid=1614,fd=6),("nginx",pid=1613,fd=6))
LISTEN 0      511             [::]:80           [::]:*    users:(("nginx",pid=1614,fd=7),("nginx",pid=1613,fd=7))
```

### ☀️ Ouvrir ce port dans le firewall

```ps
[tp@web network-scripts]$ sudo firewall-cmd --permanent --add-port=80/tcp
success

[tp@web network-scripts]$ sudo firewall-cmd --reload
success

[tp@web network-scripts]$ sudo firewall-cmd --list-all
public (active)
  target: default
  icmp-block-inversion: no
  interfaces: enp0s3
  sources:
  services: cockpit dhcpv6-client ssh
  ports: 80/tcp
  protocols:
  forward: yes
  masquerade: no
  forward-ports:
  source-ports:
  icmp-blocks:
  rich rules:
```

### ☀️ Visitez le site web !

```ps
amgoasdoue@client1:~$ curl -s http://10.6.2.11 | head -n10
<!doctype html>
<html>
  <head>
    <meta charset='utf-8'>
    <meta name='viewport' content='width=device-width, initial-scale=1'>
    <title>HTTP Server Test Page powered by: Rocky Linux</title>
    <style type="text/css">
      /*<![CDATA[*/

      html {
```

## III. 2. Serveur DNS

### 4. Analyse du service

### ☀️ Déterminer sur quel(s) port(s) écoute le service BIND9

```ps
[tp@dns ~]$ sudo ss -lnpt | grep 53
LISTEN 0      10         127.0.0.1:53        0.0.0.0:*    users:(("named",pid=729,fd=22))
LISTEN 0      4096       127.0.0.1:953       0.0.0.0:*    users:(("named",pid=729,fd=26))
LISTEN 0      10         10.6.2.12:53        0.0.0.0:*    users:(("named",pid=729,fd=28))
LISTEN 0      4096           [::1]:953          [::]:*    users:(("named",pid=729,fd=27))
LISTEN 0      10             [::1]:53           [::]:*    users:(("named",pid=729,fd=25))
```

### ☀️ Ouvrir ce(s) port(s) dans le firewall

```ps
[tp@dns ~]$ sudo firewall-cmd --permanent --add-port=53/tcp
success
[tp@dns ~]$ sudo firewall-cmd --reload
success
[tp@dns ~]$ sudo firewall-cmd --list-all
public (active)
  target: default
  icmp-block-inversion: no
  interfaces: enp0s3
  sources:
  services: cockpit dhcpv6-client ssh
  ports: 53/tcp
  protocols:
  forward: yes
  masquerade: yes
  forward-ports:
  source-ports:
  icmp-blocks:
  rich rules:
```

### ☀️ Effectuez des requêtes DNS manuellement depuis le serveur DNS lui-même dans un premier temps


```ps
[tp@dns ~]$ dig ynov.com

; <<>> DiG 9.16.23-RH <<>> ynov.com
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 31176
;; flags: qr rd ra; QUERY: 1, ANSWER: 3, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 1232
;; QUESTION SECTION:
;ynov.com.                      IN      A

;; ANSWER SECTION:
ynov.com.               300     IN      A       172.67.74.226
ynov.com.               300     IN      A       104.26.11.233
ynov.com.               300     IN      A       104.26.10.233

;; Query time: 35 msec
;; SERVER: 1.1.1.1#53(1.1.1.1)
;; WHEN: Mon Oct 21 23:48:23 CEST 2024
;; MSG SIZE  rcvd: 85

```

### ☀️ Effectuez une requête DNS manuellement depuis client1.tp6.b1


```ps
amgoasdoue@client1:~$ dig www.ynov.com

; <<>> DiG 9.18.28-0ubuntu0.24.04.1-Ubuntu <<>> www.ynov.com
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 56392
;; flags: qr rd ra; QUERY: 1, ANSWER: 3, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 65494
;; QUESTION SECTION:
;www.ynov.com.                  IN      A

;; ANSWER SECTION:
www.ynov.com.           300     IN      A       104.26.11.233
www.ynov.com.           300     IN      A       172.67.74.226
www.ynov.com.           300     IN      A       104.26.10.233

;; Query time: 30 msec
;; SERVER: 127.0.0.53#53(127.0.0.53) (UDP)
;; WHEN: Tue Oct 22 00:26:45 CEST 2024
;; MSG SIZE  rcvd: 89
```

### ☀️ Capturez une requête DNS et la réponse de votre serveur  

-> ouvrir : ``chaussette.pcap``

### ☀️ Créez un nouveau client client2.tp6.b1 vitefé

```ps
amgoasdoue@client2:~$ resolvectl
Global
         Protocols: -LLMNR -mDNS -DNSOverTLS DNSSEC=no/unsupported
  resolv.conf mode: stub

Link 2 (enp0s3)
    Current Scopes: DNS
         Protocols: +DefaultRoute -LLMNR -mDNS -DNSOverTLS DNSSEC=no/unsupported
       DNS Servers: 10.6.2.12
```