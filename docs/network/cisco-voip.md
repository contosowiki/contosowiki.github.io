---
layout: default
title: Cisco VoIP
parent: Network
nav_order: 6
---

# Cisco VoIP
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## VoiceGW
 ```js
hostname VoiceGW
interface fastEthernet 0/0
ip address 192.168.100.254 255.255.255.0
no shutdown
ip dhcp pool VoicePool
network 192.168.100.0 255.255.255.0
default-router 192.168.100.254
option 150 ip 192.168.100.254
telephony-service
max-dn 10
max-ephones 10
ip source-address 192.168.100.254 port 2000
ephone-dn 1
number 3001
ephone-dn 2
number 3002
ephone 1
type 7960
mac-address 000C.8586.CAAA
button 1:1
ephone 2
type 7960
mac-address 0005.5E3C.31AC
button 1:2
```

## VoiceSwitch01
 ```js
hostname VoiceSwitch01
interface range fastEthernet 0/1-24
switchport voice vlan 1
```