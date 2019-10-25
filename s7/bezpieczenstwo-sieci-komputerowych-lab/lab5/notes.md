# 1.

before
```
S09#show port-security address
               Secure Mac Address Table
-----------------------------------------------------------------------------
Vlan    Mac Address       Type                          Ports   Remaining Age
                                                                   (mins)
----    -----------       ----                          -----   -------------
   1    bc5f.f41b.60b6    SecureSticky                  Fa0/4        -
-----------------------------------------------------------------------------
Total Addresses in System (excluding one mac per port)     : 0
Max Addresses limit in System (excluding one mac per port) : 8192
S09#show port-security interface f0/4
Port Security              : Enabled
Port Status                : Secure-up
Violation Mode             : Shutdown
Aging Time                 : 0 mins
Aging Type                 : Absolute
SecureStatic Address Aging : Disabled
Maximum MAC Addresses      : 2
Total MAC Addresses        : 2
Configured MAC Addresses   : 0
Sticky MAC Addresses       : 2
Last Source Address:Vlan   : 0800.2779.8d17:1
Security Violation Count   : 0
```

after
```
S09#show port-security address
               Secure Mac Address Table
-----------------------------------------------------------------------------
Vlan    Mac Address       Type                          Ports   Remaining Age
                                                                   (mins)
----    -----------       ----                          -----   -------------
   1    0800.2779.8d17    SecureSticky                  Fa0/4        -
   1    bc5f.f41b.60b6    SecureSticky                  Fa0/4        -
-----------------------------------------------------------------------------
Total Addresses in System (excluding one mac per port)     : 1
Max Addresses limit in System (excluding one mac per port) : 8192
S09#show port-security interface f0/4
Port Security              : Enabled
Port Status                : Secure-shutdown
Violation Mode             : Shutdown
Aging Time                 : 0 mins
Aging Type                 : Absolute
SecureStatic Address Aging : Disabled
Maximum MAC Addresses      : 2
Total MAC Addresses        : 2
Configured MAC Addresses   : 0
Sticky MAC Addresses       : 2
Last Source Address:Vlan   : bc5f.f41b.60b0:1
Security Violation Count   : 1
```

reakcja
```
*Mar  1 00:57:08.222: %LINEPROTO-5-UPDOWN: Line protocol on Interface Vlan1, changed state to down
*Mar  1 00:57:09.220: %LINEPROTO-5-UPDOWN: Line protocol on Interface FastEthernet0/4, changed state to down
*Mar  1 00:57:10.227: %LINK-3-UPDOWN: Interface FastEthernet0/4, changed state to down
*Mar  1 00:57:13.213: %LINK-3-UPDOWN: Interface FastEthernet0/4, changed state to up
*Mar  1 00:57:14.220: %LINEPROTO-5-UPDOWN: Line protocol on Interface FastEthernet0/4, changed state to up
*Mar  1 00:57:27.071: %PM-4-ERR_DISABLE: psecure-violation error detected on Fa0/4, putting Fa0/4 in err-disable state
*Mar  1 00:57:27.071: %PORT_SECURITY-2-PSECURE_VIOLATION: Security violation occurred, caused by MAC address bc5f.f41b.60b0 on port FastEthernet0/4.
*Mar  1 00:57:28.078: %LINEPROTO-5-UPDOWN: Line protocol on Interface FastEthernet0/4, changed state to down
*Mar  1 00:57:29.076: %LINK-3-UPDOWN: Interface FastEthernet0/4, changed state to down
```

#4.
```
R9#show run
Building configuration...

Current configuration : 2837 bytes
!
! Last configuration change at 07:45:17 UTC Fri Nov 30 2018 by secureBR
version 15.3
no service pad
service tcp-keepalives-in
service tcp-keepalives-out
service timestamps debug datetime msec localtime show-timezone
service timestamps log datetime msec localtime show-timezone
service password-encryption
service sequence-numbers
!
hostname R9
!
boot-start-marker
boot-end-marker
!
!
security authentication failure rate 10 log
security passwords min-length 6
logging console critical
enable secret 5 $1$ARiP$ZmlbCMD5fEDO.Bm.QiPBU.
enable password 7 00101E1610561B
!
aaa new-model
!
!
aaa authentication login local_auth local
!
!
!
!
!
aaa session-id common
memory-size iomem 15
!
no ip source-route
no ip gratuitous-arps
!
!
!
!
!
!
no ip bootp server
ip domain name pwr.local
ip cef
login block-for 1 attempts 50 within 10
no ipv6 cef
multilink bundle-name authenticated
!
!
!
key chain ripkey
 key 1
  key-string 7 02041750340A0E2319
!
!
license udi pid CISCO2901/K9 sn FCZ1836931D
!
!
archive
 log config
  logging enable
username Bejnarowicz password 7 141C1308160F2B
username Rodziewicz password 7 15190A0F1E212A
username secureBR secret 5 $1$r806$wP84tf4rSmJts6cZrbzVs1
!
redundancy
!
!
!
!
!
!
interface Embedded-Service-Engine0/0
 no ip address
 no ip redirects
 no ip unreachables
 no ip proxy-arp
 shutdown
 no mop enabled
!
interface GigabitEthernet0/0
 ip address 192.168.9.1 255.255.255.0
 no ip redirects
 no ip unreachables
 no ip proxy-arp
 duplex auto
 speed auto
 no mop enabled
!
interface GigabitEthernet0/1
 ip address 10.10.15.9 255.255.255.0
 no ip redirects
 no ip unreachables
 no ip proxy-arp
 ip rip authentication mode md5
 ip rip authentication key-chain ripkey
 duplex auto
 speed auto
 no mop enabled
!
interface Serial0/0/0
 no ip address
 no ip redirects
 no ip unreachables
 no ip proxy-arp
 shutdown
 clock rate 2000000
!
interface Serial0/0/1
 no ip address
 no ip redirects
 no ip unreachables
 no ip proxy-arp
 shutdown
 clock rate 2000000
!
router rip
 version 2
 passive-interface GigabitEthernet0/0
 network 10.0.0.0
 network 192.168.9.0
!
ip forward-protocol nd
!
no ip http server
no ip http secure-server
!
!
!
logging trap debugging
logging facility local2
no cdp run
!
!
access-list 100 permit udp any any eq bootpc
!
!
!
control-plane
!
!
banner motd ^C Bejnarowicz Rodziewicz gr9 ^C
!
line con 0
 exec-timeout 5 0
 login authentication local_auth
 transport output telnet
line aux 0
 exec-timeout 15 0
 login authentication local_auth
 transport output telnet
line 2
 exec-timeout 15 0
 login authentication local_auth
 no activation-character
 no exec
 transport preferred none
 transport output pad telnet rlogin lapb-ta mop udptn v120 ssh
 stopbits 1
line vty 0 4
 password 7 141C1308160F2B
 login authentication local_auth
 transport input ssh
!
scheduler allocate 20000 1000
!
end
```
