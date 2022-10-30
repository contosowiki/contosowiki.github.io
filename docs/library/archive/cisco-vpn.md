---
layout: default
title: Cisco VPN
parent: Archive
grand_parent: Library
nav_order: 5
---

# Cisco VPN
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## Topology
LAN 1 (10.10.X.X / 16) & WAN 1 (12.12.12.1) <---> Internet (12.12.12.2 & 23.23.23.2) <---> WAN 2 (23.23.23.3) & LAN 2 (10.20.X.X / 16)

## IPSec VPN Site to Site
1. Enable IKE
 ```js
crypto isakmp enable
```
2. Create IKE Policy
 ```js
crypto isakmp policy 10
encryption 3des
hash md5
group 2
authentication pre-share
lifetime 86400
```
3. Setup Keystring
 ```js
crypto isakmp key keystring address 23.23.23.3
```
4. Configure IPSec transform-set
 ```js
crypto ipsec transform-set Site2SiteSet esp-3des
mode tunnel
```
5. Create crypto map
 ```js
crypto map Site2SiteMap 10 ipsec-isakmp
set peer 23.23.23.3
set pfs group2
set transform-set Site2SiteSet
set security-association lifetime second 86400
```
6. Apply crypto map to interface
 ```js
interface fastEthernet 0/1
crypto map Site2SiteMap
Show command to check
show crypto isakmp sa
show crypto isakmp policy
show crypto ipsec transform-set
show crypto map
show crypto ipsec sa
```

## Except the private network from the NAT process
 ```js
access-list 120 deny ip 10.10.0.0 0.0.255.255 10.20.0.0 0.0.255.255
access-list 120 permit ip 10.10.0.0 0.0.255.255 any
ip nat inside source list 120 interface FastEthernet 0/0 overload
```