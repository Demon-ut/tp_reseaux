# TP5 : Un ptit LAN à nous
## I. Setup
### ☀️ Uniquement avec des commandes, prouvez-que :
- vous avez bien configuré les adresses IP demandées (un ip a suffit hein) :
    -   Routeur :
    ```ps
    [root@routeur ~]# ip a
    1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
    valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host
    valid_lft forever preferred_lft forever
    2: enp0s3: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 08:00:27:8f:5f:86 brd ff:ff:ff:ff:ff:ff
    inet 10.5.1.254/24 brd 10.5.1.255 scope global noprefixroute enp0s3
    valid_lft forever preferred_lft forever
    inet6 fe80::a00:27ff:fe8f:5f86/64 scope link
    valid_lft forever preferred_lft forever
    3: enp0s8: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 08:00:27:e2:d7:9e brd ff:ff:ff:ff:ff:ff
    inet 10.0.3.15/24 brd 10.0.3.255 scope global dynamic noprefixroute enp0s8
    valid_lft 81414sec preferred_lft 81414sec
    inet6 fe80::9f6c:31dc:1bb7:c55c/64 scope link noprefixroute
    valid_lft forever preferred_lft forever
    ```
    - Client 1 :
    ```ps
    amgoasdoue@client1:~$ ip a
    1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
    valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host noprefixroute
    valid_lft forever preferred_lft forever
    2: enp0s3: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast state UP group default qlen 1000
    link/ether 08:00:27:f0:8a:8a brd ff:ff:ff:ff:ff:ff
    inet 10.5.1.11/24 brd 10.5.1.255 scope global noprefixroute enp0s3
    valid_lft forever preferred_lft forever
    inet6 fe80::a00:27ff:fef0:8a8a/64 scope link
    valid_lft forever preferred_lft forever
    ```
    - Client 2 :
    ```ps
    amgoasdoue@client2:~$ ip a
    1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
    valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host noprefixroute
    valid_lft forever preferred_lft forever
    2: enp0s3: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast state UP group default qlen 1000
    link/ether 08:00:27:b3:a7:4a brd ff:ff:ff:ff:ff:ff
    inet 10.5.1.12/24 brd 10.5.1.255 scope global noprefixroute enp0s3
    valid_lft forever preferred_lft forever
    inet6 fe80::a00:27ff:feb3:a74a/64 scope link
    valid_lft forever preferred_lft forever
    ```
- vous avez bien configuré les hostnames demandés :
    - Routeur :
    ```ps
    [root@routeur ~]# hostnamectl
    Static hostname: routeur.tp5.b1
    Icon name: computer-vm
    Chassis: vm 🖴
    Machine ID: 8888159e802746da9449c95783656357
    Boot ID: 52f8e2a952724128ab7a7d3c00d0dc2e
    Virtualization: oracle
    Operating System: Rocky Linux 9.4 (Blue Onyx)
    CPE OS Name: cpe:/o:rocky:rocky:9::baseos
    Kernel: Linux 5.14.0-427.13.1.el9_4.x86_64
    Architecture: x86-64
    Hardware Vendor: innotek GmbH
    Hardware Model: VirtualBox
    Firmware Version: VirtualBox
    ```

    - Client 1 :

    ```ps
    amgoasdoue@client1:~$ hostnamectl
    Static hostname: client1.tp5.b1
    Icon name: computer-vm
    Chassis: vm 🖴
    Machine ID: 76b5ee21b2d74e768db189f71456d58d
    Boot ID: 05a2725eb13944c9aa6a7858d32d1d8f
    Virtualization: oracle
    Operating System: Ubuntu 24.04.1 LTS
    Kernel: Linux 6.8.0-45-generic
    Architecture: x86-64
    Hardware Vendor: innotek GmbH
    Hardware Model: VirtualBox
    Firmware Version: VirtualBox
    Firmware Date: Fri 2006-12-01
    Firmware Age: 17y 10month 2w
    ```

    - Client 2 :

    ```bash
    amgoasdoue@client2:~$ hostnamectl
    Static hostname: client2.tp5.b1
    Icon name: computer-vm
    Chassis: vm 🖴
    Machine ID: 76b5ee21b2d74e768db189f71456d58d
    Boot ID: 9bc0c3eba7844528b431c09b9a6519f1
    Virtualization: oracle
    Operating System: Ubuntu 24.04.1 LTS
    Kernel: Linux 6.8.0-45-generic
    Architecture: x86-64
    Hardware Vendor: innotek GmbH
    Hardware Model: VirtualBox
    Firmware Version: VirtualBox
    Firmware Date: Fri 2006-12-01
    Firmware Age: 17y 10month 2w 1d
    ```

- tout le monde peut se ping au sein du réseau 10.5.1.0/24 :
    ```bash
    [root@routeur ~]# ping 10.5.1.11
    PING 10.5.1.11 (10.5.1.11) 56(84) bytes of data.
    64 bytes from 10.5.1.11: icmp_seq=1 ttl=64 time=0.621 ms
    64 bytes from 10.5.1.11: icmp_seq=2 ttl=64 time=0.538 ms
    64 bytes from 10.5.1.11: icmp_seq=3 ttl=64 time=1.05 ms
    64 bytes from 10.5.1.11: icmp_seq=4 ttl=64 time=0.689 ms
    ^C
    --- 10.5.1.11 ping statistics ---
    4 packets transmitted, 4 received, 0% packet loss, time 3005ms
    rtt min/avg/max/mdev = 0.538/0.724/1.048/0.194 ms  
    ```
    - Ping de routeur -> Client2 : 
    ```ps 
    [root@routeur ~]# ping 10.5.1.12
    PING 10.5.1.12 (10.5.1.12) 56(84) bytes of data.
    64 bytes from 10.5.1.12: icmp_seq=1 ttl=64 time=4.74 ms
    64 bytes from 10.5.1.12: icmp_seq=2 ttl=64 time=0.945 ms
    64 bytes from 10.5.1.12: icmp_seq=3 ttl=64 time=0.867 ms
    64 bytes from 10.5.1.12: icmp_seq=4 ttl=64 time=0.979 ms
    ^C
    --- 10.5.1.12 ping statistics ---
    4 packets transmitted, 4 received, 0% packet loss, time 3007ms
    rtt min/avg/max/mdev = 0.867/1.882/4.737/1.648 ms
    ```
## II. Accès internet pour tous
## 1. Accès internet routeur
### ☀️ Déjà, prouvez que le routeur a un accès internet
```ps
[root@routeur ~]# ping www.ynov.com
PING www.ynov.com (172.67.74.226) 56(84) bytes of data.
64 bytes from 172.67.74.226 (172.67.74.226): icmp_seq=1 ttl=52 time=35.0 ms
64 bytes from 172.67.74.226 (172.67.74.226): icmp_seq=2 ttl=52 time=32.2 ms
64 bytes from 172.67.74.226 (172.67.74.226): icmp_seq=3 ttl=52 time=68.6 ms
64 bytes from 172.67.74.226 (172.67.74.226): icmp_seq=4 ttl=52 time=83.9 ms
^C
--- www.ynov.com ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 3007ms
rtt min/avg/max/mdev = 32.242/54.926/83.935/22.028 ms
```
### ☀️ Activez le routage
```ps
[root@routeur ~] sudo firewall-cmd --add-masquerade --permanent
sudo firewall-cmd --reload
success
success
```

## 2. Accès internet clients
### ☀️ Prouvez que les clients ont un accès internet

```ps
amgoasdoue@client2:~$ ping 1.1.1.1
PING 1.1.1.1 (1.1.1.1) 56(84) bytes of data.
64 bytes from 1.1.1.1: icmp_seq=1 ttl=62 time=7.99 ms
64 bytes from 1.1.1.1: icmp_seq=2 ttl=62 time=5.80 ms
64 bytes from 1.1.1.1: icmp_seq=3 ttl=62 time=5.18 ms
64 bytes from 1.1.1.1: icmp_seq=4 ttl=62 time=8.84 ms
^C
--- 1.1.1.1 ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 3004ms
rtt min/avg/max/mdev = 5.184/6.950/8.836/1.506 ms
```

### ☀️ Montrez-moi le contenu final du fichier de configuration de l'interface réseau 

```ps
amgoasdoue@client2:~$ cat /etc/netplan/01-network-manager-all.yaml
#Let NetworkManager manage all devices on this system
network:
  version: 2
  renderer: NetworkManager
  ethernets:
    enp0s3:
      dhcp4: no
      addresses: [10.5.1.12/24]
      gateway4: 10.5.1.254
      nameservers:
        addresses: [1.1.1.1, 1.0.0.1]
```

## III. Serveur SSH
### ☀️ Sur routeur.tp5.b1, déterminer sur quel port écoute le serveur SSH

```ps
[root@routeur ~]# sudo ss -lnpt | grep 22
LISTEN 0      128          0.0.0.0:22        0.0.0.0:*    users:(("sshd",pid=704,fd=3))
LISTEN 0      128             [::]:22           [::]:*    users:(("sshd",pid=704,fd=4))
```

### ☀️ Sur routeur.tp5.b1, vérifier que ce port est bien ouvert

```ps
[root@routeur ~]# sudo firewall-cmd --list-all
public (active)
target: default
icmp-block-inversion: no
interfaces: enp0s3 enp0s8
sources:
services: cockpit dhcpv6-client ssh
ports:
protocols:
forward: yes
masquerade: yes
forward-ports:
source-ports:
icmp-blocks:
rich rules:
```

## IV. Serveur DHCP
## 3. Rendu attendu
### ☀️ Installez et configurez un serveur DHCP sur la machine routeur.tp5.b1

```ps 
[root@routeur ~]# sudo dnf install dhcp-server -y
Last metadata expiration check: 1:53:56 ago on Tue 15 Oct 2024 09:53:14 PM CEST.
Dependencies resolved.
=======================================================================================
 Package             Architecture   Version                       Repository      Size
=======================================================================================
Installing:
 dhcp-server         x86_64         12:4.4.2-19.b1.el9            baseos         1.2 M
Installing dependencies:
 dhcp-common         noarch         12:4.4.2-19.b1.el9            baseos         128 k

Transaction Summary
=======================================================================================
Install  2 Packages

Total download size: 1.3 M
Installed size: 4.2 M
Downloading Packages:
(1/2): dhcp-common-4.4.2-19.b1.el9.noarch.rpm          486 kB/s | 128 kB     00:00
(2/2): dhcp-server-4.4.2-19.b1.el9.x86_64.rpm          2.9 MB/s | 1.2 MB     00:00
---------------------------------------------------------------------------------------
Total                                                  1.7 MB/s | 1.3 MB     00:00
Running transaction check
Transaction check succeeded.
Running transaction test
Transaction test succeeded.
Running transaction
  Preparing        :                                                               1/1
  Installing       : dhcp-common-12:4.4.2-19.b1.el9.noarch                         1/2
  Running scriptlet: dhcp-server-12:4.4.2-19.b1.el9.x86_64                         2/2
  Installing       : dhcp-server-12:4.4.2-19.b1.el9.x86_64                         2/2
  Running scriptlet: dhcp-server-12:4.4.2-19.b1.el9.x86_64                         2/2
  Verifying        : dhcp-server-12:4.4.2-19.b1.el9.x86_64                         1/2
  Verifying        : dhcp-common-12:4.4.2-19.b1.el9.noarch                         2/2

Installed:
  dhcp-common-12:4.4.2-19.b1.el9.noarch      dhcp-server-12:4.4.2-19.b1.el9.x86_64

Complete!
[root@routeur ~]# sudo nano /etc/dhcp/dhcpd.conf
[root@routeur ~]# sudo systemctl start dhcpd
sudo systemctl enable dhcpd
Created symlink /etc/systemd/system/multi-user.target.wants/dhcpd.service → /usr/lib/systemd/system/dhcpd.service.
[root@routeur ~]# sudo nano /etc/dhcp/dhcpd.conf
[root@routeur ~]# sudo systemctl status dhcpd
● dhcpd.service - DHCPv4 Server Daemon
     Loaded: loaded (/usr/lib/systemd/system/dhcpd.service; enabled; preset: disabled)
     Active: active (running) since Tue 2024-10-15 23:49:06 CEST; 2min 8s ago
       Docs: man:dhcpd(8)
             man:dhcpd.conf(5)
   Main PID: 1594 (dhcpd)
     Status: "Dispatching packets..."
      Tasks: 1 (limit: 11099)
     Memory: 5.2M
        CPU: 28ms
     CGroup: /system.slice/dhcpd.service
             └─1594 /usr/sbin/dhcpd -f -cf /etc/dhcp/dhcpd.conf -user dhcpd -group dhc>

Oct 15 23:49:06 routeur.tp5.b1 dhcpd[1594]: ** Ignoring requests on enp0s8.  If this i>
Oct 15 23:49:06 routeur.tp5.b1 dhcpd[1594]:    you want, please write a subnet declara>
Oct 15 23:49:06 routeur.tp5.b1 dhcpd[1594]:    in your dhcpd.conf file for the network>
Oct 15 23:49:06 routeur.tp5.b1 dhcpd[1594]:    to which interface enp0s8 is attached. >
Oct 15 23:49:06 routeur.tp5.b1 dhcpd[1594]:
Oct 15 23:49:06 routeur.tp5.b1 dhcpd[1594]: Listening on LPF/enp0s3/08:00:27:8f:5f:86/>
Oct 15 23:49:06 routeur.tp5.b1 dhcpd[1594]: Sending on   LPF/enp0s3/08:00:27:8f:5f:86/>
Oct 15 23:49:06 routeur.tp5.b1 dhcpd[1594]: Sending on   Socket/fallback/fallback-net
Oct 15 23:49:06 routeur.tp5.b1 dhcpd[1594]: Server starting service.
Oct 15 23:49:06 routeur.tp5.b1 systemd[1]: Started DHCPv4 Server Daemon.
lines 1-23/23 (END)
```

### ☀️ Créez une nouvelle machine client client3.tp5.b1

- définissez son hostname

```ps
amgoasdoue@client:~$ hostname
client.tp5.b1
```

- définissez une IP en DHCP
vérifiez que c'est bien une adresse IP entre .137 et .237

```ps
amgoasdoue@client:~$ ip a
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host noprefixroute
       valid_lft forever preferred_lft forever
2: enp0s3: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast state UP group default qlen 1000
    link/ether 08:00:27:e1:b7:cb brd ff:ff:ff:ff:ff:ff
    inet 10.5.1.137/24 brd 10.5.1.255 scope global dynamic noprefixroute enp0s3
       valid_lft 43048sec preferred_lft 43048sec
    inet6 fe80::a00:27ff:fee1:b7cb/64 scope link
       valid_lft forever preferred_lft forever
```

- prouvez qu'il a immédiatement un accès internet

```ps
amgoasdoue@client:~$ ping 8.8.8.8
PING 8.8.8.8 (8.8.8.8) 56(84) bytes of data.
64 bytes from 8.8.8.8: icmp_seq=1 ttl=114 time=38.2 ms
64 bytes from 8.8.8.8: icmp_seq=2 ttl=114 time=22.1 ms
64 bytes from 8.8.8.8: icmp_seq=3 ttl=114 time=22.3 ms
64 bytes from 8.8.8.8: icmp_seq=4 ttl=114 time=23.3 ms
^C
--- 8.8.8.8 ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 3005ms
rtt min/avg/max/mdev = 22.139/26.480/38.179/6.769 ms
amgoasdoue@client:~$ ping www.google.com
PING www.google.com (142.250.179.100) 56(84) bytes of data.
64 bytes from par21s20-in-f4.1e100.net (142.250.179.100): icmp_seq=1 ttl=113 time=21.6 ms
64 bytes from par21s20-in-f4.1e100.net (142.250.179.100): icmp_seq=2 ttl=113 time=23.1 ms
64 bytes from par21s20-in-f4.1e100.net (142.250.179.100): icmp_seq=3 ttl=113 time=21.2 ms
64 bytes from par21s20-in-f4.1e100.net (142.250.179.100): icmp_seq=4 ttl=113 time=21.2 ms
64 bytes from par21s20-in-f4.1e100.net (142.250.179.100): icmp_seq=5 ttl=113 time=21.6 ms
^C
--- www.google.com ping statistics ---
5 packets transmitted, 5 received, 0% packet loss, time 4006ms
rtt min/avg/max/mdev = 21.155/21.738/23.097/0.707 ms
```

### ☀️ Consultez le bail DHCP qui a été créé pour notre client

```ps
[root@routeur ~]# sudo cat /var/lib/dhcpd/dhcpd.leases
# The format of this file is documented in the dhcpd.leases(5) manual page.
# This lease file was written by isc-dhcp-4.4.2b1

# authoring-byte-order entry is generated, DO NOT DELETE
authoring-byte-order little-endian;

lease 10.5.1.137 {
  starts 2 2024/10/15 22:55:55;
  ends 3 2024/10/16 10:55:55;
  cltt 2 2024/10/15 22:55:55;
  binding state active;
  next binding state free;
  rewind binding state free;
  hardware ethernet 08:00:27:e1:b7:cb;
  uid "\001\010\000'\341\267\313";
  client-hostname "client";
}
```

### ☀️ Confirmez qu'il s'agit bien de la bonne adresse MAC

```ps
amgoasdoue@client:~$ ip a
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host noprefixroute
       valid_lft forever preferred_lft forever
2: enp0s3: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast state UP group default qlen 1000
    link/ether 08:00:27:e1:b7:cb brd ff:ff:ff:ff:ff:ff
    inet 10.5.1.137/24 brd 10.5.1.255 scope global dynamic noprefixroute enp0s3
       valid_lft 42687sec preferred_lft 42687sec
    inet6 fe80::a00:27ff:fee1:b7cb/64 scope link
       valid_lft forever preferred_lft forever
```