---
layout: default
title: Cisco Switch
parent: Network
nav_order: 1
---

# Cisco Switching
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## Basic Setup and query
```shell
enable
configure terminal
hostname CoreSwitch01
enable secret cisco
write-memory
show flash:
show running-config
show interface status
show interfaces description
show running-config interface fastEthernet 0/1
show interface fastEthernet 0/1 switchport
show mac-address-table
show arp
show interface counters
show int f0/0 | include rate
```

## SSH
```shell
ip domain-name alphabook.cn
crypto key generate rsa
username cisco privilege 15 secret cisco
line vty 0 4
login local
transport input ssh
```

## Vlan
```shell
vlan 1 (management vlan by default)
Create vlan (Manually on all switches)
vlan 10
vlan 20
show vlan brief
interface vlan 10
ip address 192.168.100.1 255.255.255.0
no shutdown
```

## VLAN ACL
```shell
ip access-list extended local-17
permit ip host 192.168.99.17 192.168.99.0 0.0.0.255
exit
vlan access-map block-17 10
match ip address local-17
action drop
vlan access-map block-17 20
action forward
exit
vlan filter block-17 vlan-list 99
```

## VTP Vlan Trunk Protocol (risk)
```shell
configure trunk first
mode: server / client / transparent
vtp domain alphabook
vtp mode server
vtp password cisco
vtp pruning (on server)
show vtp status
```

## Spanning-tree
```shell
PVST+ (Cisco)
RPVST Rapid PVST (Cisco)
MST Multiple Spanning Tree
spanning-tree mode mst
spanning-tree mst configuration
name cisco
revision 1
instance 1 vlan 10,11,12
instance 2 vlan 20,21,22
spanning-tree mst 1 root primary
spanning-tree mst 2 root secondary
```

## Switchport Mode Access
```shell
interface fastEthernet 0/1
description 1F-P001
switchport mode access
switchport access vlan 10
interface fastEthernet 0/2
description 1F-P002
switchport mode access
switchport access vlan 20
```

## Switchport Mode Access (Advanced Security)
```shell
switchport port-security mac-address 0000.1111.2222
switchport port-security maximum 1
switchport port-security violation shutdown
switchport port-security violation protect
show port-security
show errdisable recovery
```

## Switchport Mode Trunk
```shell
interface range gigabitEthernet 0/1 - 2
switchport trunk encapsulation dot1q
switchport mode trunk
switchport nonegotiate
switchport trunk native vlan 10
switchport trunk allowed vlan 1,10,20,30,1002-1005
switchport trunk allowed vlan add 40
show switchport trunk
show interface gigabitEthernet 0/1 trunk
```

## EthernetChannel
```shell
interface range gigabitEthernet 0/1 - 2
switchport trunk encapsulation dot1q
switchport mode trunk
channel-group 1 mode on
port-channel load-balance src-dst-mac
show etherchannel summary
show etherchannel port-channel
show etherchannel load-balance
```

## Switchport mirror
```shell
monitor session 1 source interface fastEthernet 0/1
monitor session 1 destination interface fastEthernet 0/1
show monitor 1
no monitor session 1
```

## StackWise
```shell
Cisco StackWise technology provides an innovative new method for collectively utilizing the capabilities of a stack of switches. Individual switches intelligently join to create a single switching unit with a 32-Gbps switching stack interconnect. Configuration and routing information is shared by every switch in the stack, creating a single switching unit. Switches can be added to and deleted from a working stack without affecting performance.
show switch
show switch stack-ports
switch stack-member-number priority new-priority-value
https://www.cisco.com/c/en/us/products/collateral/switches/catalyst-3750-series-switches/prod_white_paper09186a00801b096a.html
```

## Virtual Port Channel and HSRP
```shell
It eliminates the need to run Spanning Tree Protocol (STP).
It provides a loop-free topology.
Because we are no longer running STP, every link is leveraged.
It improves high availability.
It allows downstream devices to be connected to two separate devices, thus providing more redundancy.
```

## VRRP Virtual Router Redundancy Protocol
```shell
interface vlan 10
vrrp 10 ip 192.168.10.1
vrrp priority 105 (100 by default)
show vrrp brief
```

## 802.1x Authentication
```shell
configure terminal
aaa new-model
aaa authentication dot1x default group radius
dot1x system-auth-control
radius-server host 192.168.1.100
radius-server key cisco
interface fastEthernet 0/1
switchport mode access
authentication port-control auto
dot1x pae authenticator
dot1x host-mode multi-host
show dot1x
```

## DHCP
```shell
UDP (Client 67, Server 68) DHCP Discover / DHCP Offer / DHCP Request / DHCP ACK
service dhcp
no ip dhcp conflict logging
ip dhcp pool poolVlan10
network 192.168.10.0 255.255.255.0
default-router 192.168.10.1
dns-server 192.168.10.20
lease 7
ip dhcp excluded-address 192.168.10.1 192.168.10.49
Multiple VLANs
ip helper-address 192.168.10.1
```

## POE
```shell
power inline auto max 6000
power inline never
show power inline
```

## Voice VLAN
```shell
switchport voice vlan 120
show interface fastEthernet 0/1
Storm Control
```

## Backup and Restore
```shell
copy running-config tftp:
copy tftp: running-config
```

## Reset Configuration
```shell
erase startup-config
dir
delete flash:vlan.dat
reload
```

## Reset Password
```shell
flash_init
load_helper
dir flash:
rename flash:config.text flash:config.old
boot
rename flash:config.old flash:config.text
copy flash:config.text system:running-config
enable secret cisco
write memory
```

## Error Disable
```shell
errdisable detect cause ?
errdisable recovery cause ?
errdisable recovery interval ?
show errdisable detect
show errdisable recovery
```

## Trick
```shell
service password-encryption
no ip domain-lookup
no switchport
no ip routing
no cdp run
default interface fastEthernet 0/1
PVID Port Vlan ID
AAA Authentication / Authorization / Accounting
TTL
Multicast address 224.0.0.0 - 239.255.255.255
```