# Rozległe sieci komputerowe

## Sprawozdanie z laboratorium

Data | Tytuł zajęć | Uczestnicy
:-:|:-:|:-:
12.03.2018 07:30	| Podstawowa konfiguracja routera z użyciem IOS CLI	| Bartosz Rodziewicz (226105)

### Wyniki realizacji zadań

#### Output komendy `show version`

```
Cisco IOS Software, C2900 Software (C2900-UNIVERSALK9-M), Version 15.4(3)M1, RELEASE SOFTWARE (fc1)
Technical Support: http://www.cisco.com/techsupport
Copyright (c) 1986-2014 by Cisco Systems, Inc.
Compiled Sat 25-Oct-14 03:34 by prod_rel_team

ROM: System Bootstrap, Version 15.0(1r)M16, RELEASE SOFTWARE (fc1)

R1_Rodziewicz uptime is 54 minutes
System returned to ROM by power-on
System restarted at 07:43:25 CET Mon Mar 12 2018
System image file is "flash0:c2900-universalk9-mz.SPA.154-3.M1.bin"
Last reload type: Normal Reload
Last reload reason: power-on



This product contains cryptographic features and is subject to United
States and local country laws governing import, export, transfer and
use. Delivery of Cisco cryptographic products does not imply
third-party authority to import, export, distribute or use encryption.
Importers, exporters, distributors and users are responsible for
compliance with U.S. and local country laws. By using this product you
agree to comply with applicable laws and regulations. If you are unable
to comply with U.S. and local laws, return this product immediately.

A summary of U.S. laws governing Cisco cryptographic products may be found at:
http://www.cisco.com/wwl/export/crypto/tool/stqrg.html

If you require further assistance please contact us by sending email to
export@cisco.com.

Cisco CISCO2901/K9 (revision 1.0) with 446464K/77824K bytes of memory.
Processor board ID FCZ1911C3B2
2 Gigabit Ethernet interfaces
2 Serial(sync/async) interfaces
1 terminal line
1 Virtual Private Network (VPN) Module
DRAM configuration is 64 bits wide with parity enabled.
255K bytes of non-volatile configuration memory.
255488K bytes of ATA System CompactFlash 0 (Read/Write)


License Info:

License UDI:

-------------------------------------------------
Device#   PID                   SN
-------------------------------------------------
*1        CISCO2901/K9          FCZ1911C3B2



Technology Package License Information for Module:'c2900'

------------------------------------------------------------------------
Technology    Technology-package                  Technology-package
              Current              Type           Next reboot
------------------------------------------------------------------------
ipbase        ipbasek9             Permanent      ipbasek9
security      securityk9           Permanent      securityk9
uc            None                 None           None
data          None                 None           None
NtwkEss       None                 None           None
CollabPro     None                 None           None

Configuration register is 0x2102
```

#### Output komendy `show startup-config`

```
Using 1810 out of 262136 bytes
!
! Last configuration change at 08:38:15 CET Mon Mar 12 2018 by admin
! NVRAM config last updated at 08:39:26 CET Mon Mar 12 2018 by admin
!
version 15.4
service timestamps debug datetime msec
service timestamps log datetime msec
service password-encryption
!
hostname R1_Rodziewicz
!
boot-start-marker
boot-end-marker
!
!
security passwords min-length 10
enable secret 5 $1$lpJZ$Fd1fPSL9guZgE93ppQ5Th.
!
no aaa new-model
memory-size iomem 15
clock timezone CET 1 0
clock summer-time CET recurring
!
!
!
!
!
!
!
!
!
!
!
!
!
!
no ip domain lookup
ip domain name CCNA-lab.com
ip cef
no ipv6 cef
!
multilink bundle-name authenticated
!
!
cts logging verbose
!
!
license udi pid CISCO2901/K9 sn FCZ1911C3B2
!
!
username admin privilege 15 secret 5 $1$d1jH$HrbH/XzrhJiUUsdemGWuB0
!
redundancy
!
!
!
!
!
!
!
!
!
!
!
!
!
!
!
interface Embedded-Service-Engine0/0
 no ip address
 shutdown
!
interface GigabitEthernet0/0
 description PC
 ip address 192.168.0.1 255.255.255.0
 duplex auto
 speed auto
!
interface GigabitEthernet0/1
 description Switch
 ip address 192.168.1.1 255.255.255.0
 duplex auto
 speed auto
!
interface Serial0/0/0
 no ip address
 shutdown
 clock rate 2000000
!
interface Serial0/0/1
 no ip address
 shutdown
 clock rate 2000000
!
ip forward-protocol nd
!
no ip http server
no ip http secure-server
!
!
!
!
!
control-plane
!
!
banner motd ^CNieautoryzowany dostep zabroniony!^C
!
line con 0
 exec-timeout 300 0
 password 7 03075218050022434019181604
 logging synchronous
 login
line aux 0
line 2
 no activation-character
 no exec
 transport preferred none
 transport output pad telnet rlogin lapb-ta mop udptn v120 ssh
 stopbits 1
line vty 0 4
 exec-timeout 300 0
 password 7 121A0C0411041A10333B253B20
 logging synchronous
 login local
 transport input ssh
!
scheduler allocate 20000 1000
!
end
```

#### Output komendy `show ip route`

```
Codes: L - local, C - connected, S - static, R - RIP, M - mobile, B - BGP
       D - EIGRP, EX - EIGRP external, O - OSPF, IA - OSPF inter area
       N1 - OSPF NSSA external type 1, N2 - OSPF NSSA external type 2
       E1 - OSPF external type 1, E2 - OSPF external type 2
       i - IS-IS, su - IS-IS summary, L1 - IS-IS level-1, L2 - IS-IS level-2
       ia - IS-IS inter area, * - candidate default, U - per-user static route
       o - ODR, P - periodic downloaded static route, H - NHRP, l - LISP
       a - application route
       + - replicated route, % - next hop override

Gateway of last resort is not set

      192.168.0.0/24 is variably subnetted, 2 subnets, 2 masks
C        192.168.0.0/24 is directly connected, GigabitEthernet0/0
L        192.168.0.1/32 is directly connected, GigabitEthernet0/0
      192.168.1.0/24 is variably subnetted, 2 subnets, 2 masks
C        192.168.1.0/24 is directly connected, GigabitEthernet0/1
L        192.168.1.1/32 is directly connected, GigabitEthernet0/1
```

#### Output komendy `show ip interface brief`

```
Interface                  IP-Address      OK? Method Status                Protocol
Embedded-Service-Engine0/0 unassigned      YES unset  administratively down down
GigabitEthernet0/0         192.168.0.1     YES manual up                    up
GigabitEthernet0/1         192.168.1.1     YES manual up                    up
Serial0/0/0                unassigned      YES unset  administratively down down
Serial0/0/1                unassigned      YES unset  administratively down down
```

#### Output komendy `show ipv6 int brief`

```
Em0/0                  [administratively down/down]
    unassigned
GigabitEthernet0/0     [up/up]
    FE80::1
    2001:DB8:ACAD:A::1
GigabitEthernet0/1     [up/up]
    unassigned
Serial0/0/0            [administratively down/down]
    unassigned
Serial0/0/1            [administratively down/down]
    unassigned
```
