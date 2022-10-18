---
layout: default
title: Network
nav_order: 3
has_children: true
permalink: /docs/network
---

# Network

Network is the basis of the whole IT infrastructure. We can not imagine the situation without network.

IP Addresses reserved for use on private networks
{: .note }
10.0.0.0 to 10.255.255.255
172.16.0.0 to 172.31.255.255
192.168.0.0 to 192.168.255.255

## 1.1 Choosing private IPv4 address

{: .warning }
1. We need to reserve enough IP address for all devices (Desktop, Laptop, Mobile, etc), Class A may be good choose. 
{: .warning }
2. Pay attention to potential IP confiction in your environment (Docker may use IP address of Class B, etc).

## 1.2 Example of a company with three Offices

```yaml
Beijing Office 10.10.0.0/255.255.0.0
Shanghai Office 10.20.0.0/255.255.0.0
Shenzhen Office 10.30.0.0/255.255.0.0
```

## 1.3 Example of Beijing office

```yaml
Windows Server 10.10.10.0/255.255.255.0 (Available IP address 10.10.10.1 - 10.10.10.254)
Linux Server 10.10.20.0/255.255.254.0 (Available IP address 10.10.20.1 - 10.10.21.254)
```
