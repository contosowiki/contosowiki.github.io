---
layout: default
title: Cisco Router
parent: Network
nav_order: 2
---

# Cisco Router
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## Basic setup
show ip route summary

## Administrative Distance
| Routing Protocol        | AD          |
|:-------------|:------------------|
| Directly connected interface           | 0 |
| Static route | 1   |
| OSPF           | 110      |
| RIP           | 120 |

## Static Route
```shell
ip route 172.16.0.0 255.255.0.0 e0/0 192.168.12.2
ip route 0.0.0.0 0.0.0.0 e0/0 192.168.12.2
ip route 0.0.0.0 0.0.0.0 e0/1 192.168.13.3 10
```

## OSPF (Open Shortest Path First)
```shell
router ospf 1 // router ospf process-id
interface fastEthernet 0/1
ip ospf 1 area 0
ip ospf cost 1
interface fastEthernet 0/2
ip ospf 1 area 0
ip ospf cost 2
interface vlan 10
ip ospf 1 area 1
router ospf 1
passive-interface vlan 10
show ip ospf interface brief
show ip ospf neighbor
show ip route ospf
reference-bandwidth (100 Mbps by default)
router ospf 1
auto-cost reference-bandwidth 1000 (The reference bandwidth in terms of Mbits per second)
interface fastEthernet 0/1
bandwidth 100000 (Bandwidth in kilobits)
Cost = reference-bandwidth / bandwidth
```

## NAT
```shell
interface Ethernet0
ip address 192.168.1.1 255.255.255.0
ip nat inside
interface Ethernet1
ip address 211.120.200.2 255.255.255.0
ip nat outside
ip nat inside static 192.168.1.100 211.120.200.100
show ip nat translations
```

## ACL
```shell
FTP (Active Mode)
access-list 102 permit tcp any host 192.168.1.100 eq ftp
access-list 102 permit tcp any host 192.168.1.100 eq ftp-data established
FTP (Passive Mode)
access-list 102 permit tcp any host 192.168.1.100 eq ftp
access-list 102 permit tcp any host 192.168.1.100 gt 1024
SMTP
access-list 102 permit tcp any host 192.168.1.100 eq smtp
https://www.cisco.com/c/zh_cn/support/docs/ip/access-lists/26448-ACLsamples.html
```