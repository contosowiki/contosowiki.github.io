---
layout: default
title: Cisco Firewall
parent: Archive
nav_order: 4
---

# Cisco Firewall
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## Firepower Initial Configuration
```js
Configure PC (no internet) as below:
IP address: 192.168.45.2
Netmask: 255.255.255.0
Gateway: 192.168.45.1
Connect to management port
Access appliance's default IP address: https://192.168.45.45
Username: admin
Password: Admin123
Setup Outside Interface / Management Interface / Time Zone / NTP Time Server
Firepower 2100 default port
Outside Interface: Ethernet1/1
Inside Interface: Ethernet1/2
```

## Zone
After initial configuration, there are inside_zone and outside_zone

Each interface must belong to a zone, because you configure policies based on security zones, not interfaces

Create interface, then create zone, and add the interface

## Configure AD Identity Realms
Objects -> Identity Realm

Identity—The realm provides user identity and group membership information, which you can then use in access control rules

Remote access VPN—The realm provides authentication services, which determine whether a connection is allowed