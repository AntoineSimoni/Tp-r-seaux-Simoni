# Tp réseaux Simoni
+# Plusieurs réseaux : Routage statique
## I.Création et utilisation simples d'une VM Centos
### 4. Configuration réseau d'une marchine CentOs
* A.Utilisez une commande pour prouver que vous avez internet depuis la VM.
Pour prouver que notre VM a internet, nous allons charger la page www.google.com via la commande `curl www.google.com`, ce qui donne :
```
[root@localhost ~]$ curl google.com
<HTML><HEAD><meta http-equiv="content-type" content="text/html;charset=utf-8">
<TITLE>301 Moved</TITLE></HEAD><BODY>
<H1>301 Moved</H1>
The document has moved
<A HREF="http://www.google.com/">here</A>.
</BODY></HTML>
```
* B.Prouvez que votre PC hôte et la VM peuvent communiquer
Pour tester la communication entre nos deux machines, on utilise : 
                sur la VM : `ping 192.168.127.1`,                   sur le PC hôte : `ping 192.168.127.10`
* C.Affichez votre table de routage sur la VM et expliquez chacune de ses lignes
Pour afficher la table de routage sur la VM, on utilise la commande `ip route` :
```
[root@localhost ~]$ ip route
default via 10.0.2.2 dev enp0s3 proto dhcp metric 100
10.0.2.0/24 dev enp0s3 proto kernel scope link src 10.0.2.15 metric 100
192.168.127.0/24 dev enp0s8 proto kernel scope link src 192.168.127.10 metric 101
```
* Ligne 1 : Indique sur quel réseau nous sommes connectés, ici : '10.0.2.2/24'.
* Ligne 2 : Indique le réseau sur lequel est la première carte réseau et l'ip que l'on a, ici : '10.0.2.15'
* Ligne 3 : Indique le réseau sur lequel est connectée la seconde carte réseau de notre VM, ici : '192.168.127.0/24', puis l'adresse ici : '192.168.127.10'.

### 5. Faire joujou avec quelques commandes
* Faire des pings :
    * Ping hôte > VM :
    ```
    C:\Users\User>ping 192.168.127.10

    Envoi d’une requête 'Ping'  192.168.127.10 avec 32 octets de données :
    Réponse de 192.168.127.10 : octets=32 temps<1ms TTL=64
    Réponse de 192.168.127.10 : octets=32 temps<1ms TTL=64
    Réponse de 192.168.127.10 : octets=32 temps<1ms TTL=64
    Réponse de 192.168.127.10 : octets=32 temps<1ms TTL=64

    Statistiques Ping pour 192.168.127.10:
        Paquets : envoyés = 4, reçus = 4, perdus = 0 (perte 0%),
    Durée approximative des boucles en millisecondes :
        Minimum = 0ms, Maximum = 0ms, Moyenne = 0ms
    ```
    * Ping VM > hôte :
    ```
    [root@localhost ~]$ ping 192.168.127.1
    PING 192.168.127.1 (192.168.127.1) 56(84) bytes of data.
    64 bytes from 192.168.127.1: icmp_seq=1 ttl=128 time=0.348 ms
    64 bytes from 192.168.127.1: icmp_seq=2 ttl=128 time=0.476 ms
    64 bytes from 192.168.127.1: icmp_seq=3 ttl=128 time=0.259 ms
    64 bytes from 192.168.127.1: icmp_seq=4 ttl=128 time=0.406 ms
    ^C
    --- 192.168.127.1 ping statistics ---
    4 packets transmitted, 4 received, 0% packet loss, time 2999ms
    rtt min/avg/max/mdev = 0.259/0.372/0.476/0.080 ms
    ```

* Afficher la table de routage :
    * de l'hôte :
    ```
    C:\Users\User>route print
    ===========================================================================
    Liste d'Interfaces
    17...4c cc 6a e2 e3 63 ......Killer E2500 Gigabit Ethernet Controller
    48...0a 00 27 00 00 30 ......VirtualBox Host-Only Ethernet Adapter #2
    10...9e b6 d0 1e d1 17 ......Microsoft Wi-Fi Direct Virtual Adapter
    20...ae b6 d0 1e d1 17 ......Microsoft Wi-Fi Direct Virtual Adapter #2
    8...9c b6 d0 1e d1 17 ......Killer Wireless-n/a/ac 1535 Wireless Network Adapter
    19...9c b6 d0 1e d1 18 ......Bluetooth Device (Personal Area Network)
    1...........................Software Loopback Interface 1
    ===========================================================================

    IPv4 Table de routage
    ===========================================================================
    Itinéraires actifs :
    Destination réseau    Masque réseau  Adr. passerelle   Adr. interface Métrique
            0.0.0.0          0.0.0.0      10.33.3.253      10.33.1.134     35
            10.33.0.0    255.255.252.0         On-link       10.33.1.134    291
        10.33.1.134  255.255.255.255         On-link       10.33.1.134    291
        10.33.3.255  255.255.255.255         On-link       10.33.1.134    291
            127.0.0.0        255.0.0.0         On-link         127.0.0.1    331
            127.0.0.1  255.255.255.255         On-link         127.0.0.1    331
    127.255.255.255  255.255.255.255         On-link         127.0.0.1    331
        192.168.127.0    255.255.255.0         On-link     192.168.127.1    330
        192.168.127.1  255.255.255.255         On-link     192.168.127.1    330
    192.168.127.255  255.255.255.255         On-link     192.168.127.1    330
            224.0.0.0        240.0.0.0         On-link         127.0.0.1    331
            224.0.0.0        240.0.0.0         On-link       10.33.1.134    291
            224.0.0.0        240.0.0.0         On-link     192.168.127.1    330
    255.255.255.255  255.255.255.255         On-link         127.0.0.1    331
    255.255.255.255  255.255.255.255         On-link       10.33.1.134    291
    255.255.255.255  255.255.255.255         On-link     192.168.127.1    330
    ===========================================================================
    Itinéraires persistants :
    Aucun

    IPv6 Table de routage
    ===========================================================================
    Itinéraires actifs :
    If Metric Network Destination      Gateway
    1    331 ::1/128                  On-link
    8    291 fe80::/64                On-link
    48    281 fe80::/64                On-link
    8    291 fe80::dc78:3246:947c:3437/128
                                        On-link
    48    281 fe80::dd63:af33:a449:447c/128
                                        On-link
    1    331 ff00::/8                 On-link
    8    291 ff00::/8                 On-link
    48    281 ff00::/8                 On-link
    ===========================================================================
    Itinéraires persistants :
    Aucun
    ```
    * de la VM :
    ```
    [root@localhost ~]$ ip route
    default via 10.0.2.2 dev enp0s3 proto dhcp metric 100
    10.0.2.0/24 dev enp0s3 proto kernel scope link src 10.0.2.15 metric 100
    192.168.127.0/24 dev enp0s8 proto kernel scope link src 192.168.127.10 metric 101
    ```

* Depuis la VM, utilisez `curl` pour télécharger un fichier sur internet
    ```
    [root@localhost ~]$ curl google.com
    <HTML><HEAD><meta http-equiv="content-type" content="text/html;charset=utf-8">
    <TITLE>301 Moved</TITLE></HEAD><BODY>
    <H1>301 Moved</H1>
    The document has moved
    <A HREF="http://www.google.com/">here</A>.
    </BODY></HTML>
    ```

* Depuis la VM, utilisez `dig` pour connaître l'IP de :
    * ynov.com
    ```
    [root@localhost ~]$ dig ynov.com

    ; <<>> DiG 9.9.4-RedHat-9.9.4-72.el7 <<>> ynov.com
    ;; global options: +cmd
    ;; Got answer:
    ;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 39992
    ;; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 13, ADDITIONAL: 27

    ;; OPT PSEUDOSECTION:
    ; EDNS: version: 0, flags:; udp: 4096
    ;; QUESTION SECTION:
    ;ynov.com.                      IN      A

    ;; ANSWER SECTION:
    ynov.com.               3610    IN      A       217.70.184.38

    ;; AUTHORITY SECTION:
    com.                    76355   IN      NS      a.gtld-servers.net.
    com.                    76355   IN      NS      i.gtld-servers.net.
    com.                    76355   IN      NS      j.gtld-servers.net.
    com.                    76355   IN      NS      m.gtld-servers.net.
    com.                    76355   IN      NS      g.gtld-servers.net.
    com.                    76355   IN      NS      h.gtld-servers.net.
    com.                    76355   IN      NS      e.gtld-servers.net.
    com.                    76355   IN      NS      f.gtld-servers.net.
    com.                    76355   IN      NS      d.gtld-servers.net.
    com.                    76355   IN      NS      c.gtld-servers.net.
    com.                    76355   IN      NS      b.gtld-servers.net.
    com.                    76355   IN      NS      l.gtld-servers.net.
    com.                    76355   IN      NS      k.gtld-servers.net.

    ;; ADDITIONAL SECTION:
    a.gtld-servers.net.     76355   IN      A       192.5.6.30
    a.gtld-servers.net.     76355   IN      AAAA    2001:503:a83e::2:30
    b.gtld-servers.net.     76355   IN      A       192.33.14.30
    b.gtld-servers.net.     76355   IN      AAAA    2001:503:231d::2:30
    c.gtld-servers.net.     76355   IN      A       192.26.92.30
    c.gtld-servers.net.     76355   IN      AAAA    2001:503:83eb::30
    d.gtld-servers.net.     76355   IN      A       192.31.80.30
    d.gtld-servers.net.     76355   IN      AAAA    2001:500:856e::30
    e.gtld-servers.net.     76355   IN      A       192.12.94.30
    e.gtld-servers.net.     76355   IN      AAAA    2001:502:1ca1::30
    f.gtld-servers.net.     76355   IN      A       192.35.51.30
    f.gtld-servers.net.     76355   IN      AAAA    2001:503:d414::30
    g.gtld-servers.net.     76355   IN      A       192.42.93.30
    g.gtld-servers.net.     76355   IN      AAAA    2001:503:eea3::30
    h.gtld-servers.net.     76355   IN      A       192.54.112.30
    h.gtld-servers.net.     76355   IN      AAAA    2001:502:8cc::30
    i.gtld-servers.net.     76355   IN      A       192.43.172.30
    i.gtld-servers.net.     76355   IN      AAAA    2001:503:39c1::30
    j.gtld-servers.net.     76355   IN      A       192.48.79.30
    j.gtld-servers.net.     76355   IN      AAAA    2001:502:7094::30
    k.gtld-servers.net.     76355   IN      A       192.52.178.30
    k.gtld-servers.net.     76355   IN      AAAA    2001:503:d2d::30
    l.gtld-servers.net.     76355   IN      A       192.41.162.30
    l.gtld-servers.net.     76355   IN      AAAA    2001:500:d937::30
    m.gtld-servers.net.     76355   IN      A       192.55.83.30
    m.gtld-servers.net.     76355   IN      AAAA    2001:501:b1f9::30

    ;; Query time: 6 msec
    ;; SERVER: 10.33.10.20#53(10.33.10.20)
    ;; WHEN: Tue Jan 15 11:05:00 CET 2019
    ;; MSG SIZE  rcvd: 849
    ```
    * google.com
    ```
    [root@localhost ~]$ dig google.com

    ; <<>> DiG 9.9.4-RedHat-9.9.4-72.el7 <<>> google.com
    ;; global options: +cmd
    ;; Got answer:
    ;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 5523
    ;; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 13, ADDITIONAL: 27

    ;; OPT PSEUDOSECTION:
    ; EDNS: version: 0, flags:; udp: 4096
    ;; QUESTION SECTION:
    ;google.com.                    IN      A

    ;; ANSWER SECTION:
    google.com.             220     IN      A       216.58.209.238

    ;; AUTHORITY SECTION:
    com.                    76274   IN      NS      c.gtld-servers.net.
    com.                    76274   IN      NS      e.gtld-servers.net.
    com.                    76274   IN      NS      f.gtld-servers.net.
    com.                    76274   IN      NS      g.gtld-servers.net.
    com.                    76274   IN      NS      j.gtld-servers.net.
    com.                    76274   IN      NS      i.gtld-servers.net.
    com.                    76274   IN      NS      d.gtld-servers.net.
    com.                    76274   IN      NS      l.gtld-servers.net.
    com.                    76274   IN      NS      h.gtld-servers.net.
    com.                    76274   IN      NS      k.gtld-servers.net.
    com.                    76274   IN      NS      a.gtld-servers.net.
    com.                    76274   IN      NS      b.gtld-servers.net.
    com.                    76274   IN      NS      m.gtld-servers.net.

    ;; ADDITIONAL SECTION:
    a.gtld-servers.net.     76274   IN      A       192.5.6.30
    a.gtld-servers.net.     76274   IN      AAAA    2001:503:a83e::2:30
    b.gtld-servers.net.     76274   IN      A       192.33.14.30
    b.gtld-servers.net.     76274   IN      AAAA    2001:503:231d::2:30
    c.gtld-servers.net.     76274   IN      A       192.26.92.30
    c.gtld-servers.net.     76274   IN      AAAA    2001:503:83eb::30
    d.gtld-servers.net.     76274   IN      A       192.31.80.30
    d.gtld-servers.net.     76274   IN      AAAA    2001:500:856e::30
    e.gtld-servers.net.     76274   IN      A       192.12.94.30
    e.gtld-servers.net.     76274   IN      AAAA    2001:502:1ca1::30
    f.gtld-servers.net.     76274   IN      A       192.35.51.30
    f.gtld-servers.net.     76274   IN      AAAA    2001:503:d414::30
    g.gtld-servers.net.     76274   IN      A       192.42.93.30
    g.gtld-servers.net.     76274   IN      AAAA    2001:503:eea3::30
    h.gtld-servers.net.     76274   IN      A       192.54.112.30
    h.gtld-servers.net.     76274   IN      AAAA    2001:502:8cc::30
    i.gtld-servers.net.     76274   IN      A       192.43.172.30
    i.gtld-servers.net.     76274   IN      AAAA    2001:503:39c1::30
    j.gtld-servers.net.     76274   IN      A       192.48.79.30
    j.gtld-servers.net.     76274   IN      AAAA    2001:502:7094::30
    k.gtld-servers.net.     76274   IN      A       192.52.178.30
    k.gtld-servers.net.     76274   IN      AAAA    2001:503:d2d::30
    l.gtld-servers.net.     76274   IN      A       192.41.162.30
    l.gtld-servers.net.     76274   IN      AAAA    2001:500:d937::30
    m.gtld-servers.net.     76274   IN      A       192.55.83.30
    m.gtld-servers.net.     76274   IN      AAAA    2001:501:b1f9::30

    ;; Query time: 10 msec
    ;; SERVER: 10.33.10.20#53(10.33.10.20)
    ;; WHEN: Tue Jan 15 11:06:20 CET 2019
    ;; MSG SIZE  rcvd: 851
    ```

## II.Notion de ports et SSH
### 1.Exploration des ports locaux
Après quelques recherche sur la commande `ss` on se retrouve avec la commande `ss -n -t` ce qui nous donne :
```
[root@localhost ~]$ ss -t -n
State      Recv-Q Send-Q Local Address:Port               Peer Address:Port         
ESTAB      0      64     192.168.127.10:22                 192.168.127.1:6121       
```

### 2.SSH
### 3.Firewall
##### * A.SSH :
Modifier le fichier `/etc/ssh/sshd_config`
Redémarrer le système avec `systemctl restart sshd`
Vérifier que votre serveur SSH écoute sur un port différent que le 22 grace a la commande : `ss -4tln`
Connexion au serveur via le client :
```
C:\Users\User>ssh root@192.168.102.10
ssh: connect to host 192.168.102.10 port 22: Connection refused
```
L'erreur qui parvient nous montre que la connexion est tentée sur le port 22 de la VM, il faut donc préciser sur quel port se connecter via l'option `-p 2222`
##### * B.`netcat` :
On lance le netcat "serveur" grace a la commande `[root@localhost ~]$ nc -l 5454`
puis dans la VM on lance un client grace a la commande `C:\Users\User\Desktop\netcat-win32-1.11\netcat-1.11>nc 192.168.102.10 5454`

## III.Routage Statique
L'objectif de cette partie est de transformer nos PC en routeurs et de permettre au deuxième PC de se connecter à la machine du premier, et inversement.
```
Internet            Internet
    |                    |
  WiFi                  WiFi
    |                    |
   PC 1  ---Ethernet--- PC 2
    |                    |
Host-only 1          Host-only 2
    |                    |
   VM 1                 VM 2
```

Une fois les configurations faites, les ping ne fonctionnaient que :
* De la VM1 au PC1 et PC2
* De la VM2 au PC1 et PC2
* Du PC1 au PC2