### GOASDOUÉ Anthony | B1 INFO

# TP7 : On dit chiffrer pas crypter

## II. Serveur Web

## 1. HTTP

### B. Configuration

---

#### 🌞 **Lister les ports en écoute sur la machine**

```ps
[tp@web sitedefou.tp7.b1]$ sudo ss -lnpt | grep 80
LISTEN 0      511          0.0.0.0:80        0.0.0.0:*    users:(("nginx",pid=11610,fd=6),("nginx",pid=11609,fd=6))
LISTEN 0      511             [::]:80           [::]:*    users:(("nginx",pid=11610,fd=7),("nginx",pid=11609,fd=7))
```

#### 🌞 **Ouvrir le port dans le firewall de la machine**

```ps
[tp@web sitedefou.tp7.b1]$ sudo firewall-cmd --permanent --add-port=80/tcp
success
[tp@web sitedefou.tp7.b1]$ sudo firewall-cmd --reload
success
```

### C. Tests client

---

#### 🌞 **Vérifier que ça a pris effet**

* faites un `ping` vers `sitedefou.tp7.b1`
  ```ps
  amgoasdoue@client1:~$ ping sitedefou.tp7.b1
  PING sitedefou.tp7.b1 (10.7.1.11) 56(84) bytes of data.
  64 bytes from sitedefou.tp7.b1 (10.7.1.11): icmp_seq=1 ttl=64 time=4.12 ms
  64 bytes from sitedefou.tp7.b1 (10.7.1.11): icmp_seq=2 ttl=64 time=1.08 ms
  64 bytes from sitedefou.tp7.b1 (10.7.1.11): icmp_seq=3 ttl=64 time=2.14 ms
  64 bytes from sitedefou.tp7.b1 (10.7.1.11): icmp_seq=4 ttl=64 time=0.872 ms
  ^C
  --- sitedefou.tp7.b1 ping statistics ---
  4 packets transmitted, 4 received, 0% packet loss, time 3006ms
  rtt min/avg/max/mdev = 0.872/2.050/4.115/1.284 ms
  ```
* visitez `http://sitedefou.tp7.b1`

```ps
amgoasdoue@client1:~$ curl http://sitedefou.tp7.b1
meow !
```

### D. Analyze

---

#### 🌞 **Capture `tcp_http.pcap`**

[http](.\tcp_http.pcap)

#### 🌞 **Voir la connexion établie**

```ps
amgoasdoue@client1:/etc$ ss | grep tcp
tcp   SYN-SENT 0      1                                                  10.7.1.101:53238           1.1.1.1:domain
```

## 2. On rajoute un S

### B. Configuration

---

🌞 **Lister les ports en écoute sur la machine**

```ps
[tp@web ~]$ sudo ss -lnpt | grep nginx
LISTEN 0      511          0.0.0.0:80        0.0.0.0:*    users:(("nginx",pid=1460,fd=7),("nginx",pid=1459,fd=7))
LISTEN 0      511        10.7.1.11:443       0.0.0.0:*    users:(("nginx",pid=1460,fd=6),("nginx",pid=1459,fd=6))
LISTEN 0      511             [::]:80           [::]:*    users:(("nginx",pid=1460,fd=8),("nginx",pid=1459,fd=8))
```

#### 🌞 **Gérer le firewall**

```ps
[tp@web ~]$ sudo firewall-cmd --permanent --add-port=443/tcp
success
[tp@web ~]$ sudo firewall-cmd --reload
success
```

### B. Test test test analyyyze

---

#### 🌞 **Capture `tcp_https.pcap`**

[https](.\tcp_https.pcap)

## III. Serveur VPN

## 1. Install et conf Wireguard

#### 🌞 **Prouvez que vous avez bien une nouvelle carte réseau `wg0`**

```ps
[tp@vpn ~]$ ip a
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host
       valid_lft forever preferred_lft forever
2: enp0s3: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 08:00:27:d1:f6:6f brd ff:ff:ff:ff:ff:ff
    inet 10.7.1.111/24 brd 10.7.1.255 scope global noprefixroute enp0s3
       valid_lft forever preferred_lft forever
    inet6 fe80::a00:27ff:fed1:f66f/64 scope link
       valid_lft forever preferred_lft forever
3: enp0s8: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 08:00:27:f4:fd:da brd ff:ff:ff:ff:ff:ff
    inet 10.7.2.111/24 brd 10.7.2.255 scope global noprefixroute enp0s8
       valid_lft forever preferred_lft forever
    inet6 fe80::a00:27ff:fef4:fdda/64 scope link
       valid_lft forever preferred_lft forever
4: wg0: <POINTOPOINT,NOARP,UP,LOWER_UP> mtu 1420 qdisc noqueue state UNKNOWN group default qlen 1000
    link/none
    inet 10.7.200.1/24 scope global wg0
       valid_lft forever preferred_lft forever
```

#### 🌞 **Déterminer sur quel port écoute Wireguard**

```ps
[tp@vpn ~]$ sudo ss -lnpu | grep 51820
UNCONN 0      0            0.0.0.0:51820      0.0.0.0:*

UNCONN 0      0               [::]:51820         [::]:*
```

#### 🌞 **Ouvrez ce port dans le firewall**

```ps
   [tp@vpn ~]$ sudo firewall-cmd --permanent --add-port=51820/tcp
sudo firewall-cmd --reload
Warning: ALREADY_ENABLED: 51820:tcp
success
success
[tp@vpn ~]$ sudo firewall-cmd --list-all
public (active)
  target: default
  icmp-block-inversion: no
  interfaces: enp0s3 enp0s8
  sources:
  services: ssh
  ports: 51820/tcp
  protocols:
  forward: yes
  masquerade: no
  forward-ports:
  source-ports:
  icmp-blocks:
  rich rules:
```

## 3. Proofs

#### 🌞 **Ping ping ping !**

```ps
amgoasdoue@client1:~$ ping 10.7.200.1
PING 10.7.200.1 (10.7.200.1) 56(84) bytes of data.
64 bytes from 10.7.200.1: icmp_seq=1 ttl=64 time=4.66 ms
64 bytes from 10.7.200.1: icmp_seq=2 ttl=64 time=2.08 ms
64 bytes from 10.7.200.1: icmp_seq=3 ttl=64 time=0.830 ms
64 bytes from 10.7.200.1: icmp_seq=4 ttl=64 time=3.39 ms
^C
--- 10.7.200.1 ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 3005ms
rtt min/avg/max/mdev = 0.830/2.740/4.657/1.429 ms
```

#### 🌞 **Capture `ping1_vpn.pcap`**

[ping1_vpn](.\ping1_vpn.pcap)

#### 🌞 **Capture `ping2_vpn.pcap`**

[ping2_vpn](.\ping2_vpn.pcap)

#### 🌞 **Prouvez que vous avez toujours un accès internet**

```ps
amgoasdoue@client1:~$ traceroute 1.1.1.1
traceroute to 1.1.1.1 (1.1.1.1), 30 hops max, 60 byte packets
 1  _gateway (10.7.200.1)  5.831 ms  6.764 ms  8.954 ms
 2  _gateway (10.7.1.254)  12.885 ms  17.345 ms  18.850 ms
 3  10.0.3.2 (10.0.3.2)  26.984 ms  28.530 ms  30.133 ms
 4  * * *
 5  * * *
```

## 4.Private service

#### 🌞 **Visitez le service Web à travers le VPN**

```ps
amgoasdoue@client1:~$ curl https://sitedefou.tp7.b1
meow !
```
