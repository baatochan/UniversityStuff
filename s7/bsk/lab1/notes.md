# 1. 
nr 8

router 10.0.0.1  
pc iwo 10.0.0.2  
pc baato 10.0.0.3  

# 2.

```
Active Connections

  Proto  Local Address          Foreign Address        State
  TCP    10.0.0.3:65132         10.0.0.1:telnet        ESTABLISHED
  TCP    10.0.0.3:65134         KSSK4:http             ESTABLISHED
  TCP    127.0.0.1:49190        KSSK:49191             ESTABLISHED
  TCP    127.0.0.1:49191        KSSK:49190             ESTABLISHED
  TCP    127.0.0.1:49194        KSSK:49195             ESTABLISHED
  TCP    127.0.0.1:49195        KSSK:49194             ESTABLISHED
  TCP    127.0.0.1:49216        KSSK:49217             ESTABLISHED
  TCP    127.0.0.1:49217        KSSK:49216             ESTABLISHED
  TCP    127.0.0.1:49225        KSSK:49226             ESTABLISHED
  TCP    127.0.0.1:49226        KSSK:49225             ESTABLISHED
  TCP    127.0.0.1:65038        KSSK:65039             ESTABLISHED
  TCP    127.0.0.1:65039        KSSK:65038             ESTABLISHED
  TCP    127.0.0.1:65071        KSSK:65072             ESTABLISHED
  TCP    127.0.0.1:65072        KSSK:65071             ESTABLISHED
  TCP    127.0.0.1:65130        KSSK:65131             ESTABLISHED
  TCP    127.0.0.1:65131        KSSK:65130             ESTABLISHED
```

# 3. 
## synscan cala siec

```
C:\Users\Student>nmap -sS 10.0.0.0/16
Starting Nmap 7.70 ( https://nmap.org ) at 2018-10-26 11:37 Central European Day
light Time
mass_dns: warning: Unable to determine any DNS servers. Reverse DNS is disabled.
 Try using --system-dns or specify valid servers with --dns-servers
Nmap scan report for 10.0.0.1
Host is up (0.00032s latency).
Not shown: 999 closed ports
PORT   STATE SERVICE
23/tcp open  telnet
MAC Address: A0:EC:F9:D8:1F:90 (Cisco Systems)

Nmap scan report for 10.0.0.2
Host is up (0.0059s latency).
Not shown: 999 closed ports
PORT   STATE SERVICE
80/tcp open  http
MAC Address: 08:00:27:1C:14:28 (Oracle VirtualBox virtual NIC)

^C
```
## xmas router

```
C:\Users\Student>nmap -sX -p1-65535 10.0.0.1
Starting Nmap 7.70 ( https://nmap.org ) at 2018-10-26 11:50 Central European Day
light Time
mass_dns: warning: Unable to determine any DNS servers. Reverse DNS is disabled.
 Try using --system-dns or specify valid servers with --dns-servers
Nmap scan report for 10.0.0.1
Host is up (0.014s latency).
All 65535 scanned ports on 10.0.0.1 are closed
MAC Address: A0:EC:F9:D8:1F:90 (Cisco Systems)

Nmap done: 1 IP address (1 host up) scanned in 18.23 seconds
```
## wybrane porty syn scan iwo pc

```
C:\Users\Student>nmap -sS -p T:21-25,80,443,2137,8080,27015 10.0.0.2
Starting Nmap 7.70 ( https://nmap.org ) at 2018-10-26 11:55 Central European Day
light Time
mass_dns: warning: Unable to determine any DNS servers. Reverse DNS is disabled.
 Try using --system-dns or specify valid servers with --dns-servers
Nmap scan report for 10.0.0.2
Host is up (0.00s latency).

PORT      STATE  SERVICE
21/tcp    closed ftp
22/tcp    closed ssh
23/tcp    closed telnet
24/tcp    closed priv-mail
25/tcp    closed smtp
80/tcp    open   http
443/tcp   closed https
2137/tcp  closed connect
8080/tcp  closed http-proxy
27015/tcp closed unknown
MAC Address: 08:00:27:1C:14:28 (Oracle VirtualBox virtual NIC)

Nmap done: 1 IP address (1 host up) scanned in 2.00 seconds
```