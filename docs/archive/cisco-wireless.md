---
layout: default
title: Cisco Wireless
parent: Archive
nav_order: 3
---

# Cisco Wireless
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## Cisco 5520 Wireless LAN Controller
Height: 1U / Throughput: 20Gbps / AP Support: 1500 / Client Support: 20000

AIR-CT5520-50-K9 / Cisco 5520 wireless controller supporting 50 APs w/rack kit

Interfaces and indicators

2 x 10 Gigabit Ethernet interfaces or 2 x 1 Gigabit Ethernet interfaces

Small Form-Factor Pluggable Plus (SFP+) options (only Cisco SFP+s supported), including S-Class Optics

Small Form-Factor Pluggable (SFP) options (only Cisco SFPs supported), including S-Class Optics

1 x service port: 1 Gigabit Ethernet port (RJ-45)

1 x redundancy port: 1 Gigabit Ethernet port (RJ-45)

1 x Cisco Integrated Management Controller port: 10/100/1000 Ethernet (RJ-45)

1 x console port: Serial port (RJ-45)

LED indicators: Network Link, Diagnostics

## WLAN Express Setup
Service Port (SP) default IP 192.168.1.1

Configure IP address on PC with 192.168.1.100 and access http://192.168.1.1

Create a new admin account

Setup System Name / Country / Date & Time / Timezone / NTP Server / Management IP Address / Subnet Mask / Default Gateway / Management VLAN ID

Setup Employee Network / Network Name / Security / Pass Phrase / VLAN / DHCP Server Address

Setup Guest Network / Network Name / Security / Pass Phrase / VLAN / DHCP Server Address

Setup Advanced Setting Client Density / Traffic Type / Virtual IP Address / Local Mobility Group / Service Port interface / Service Port IP Address / Service Port Network

Apply

## Command Line Interface
 ```js
imm address <ip address> <net mask> <gateway ip>
imm summary
config network secureweb enable
config network webmode disable
config network ssh enable
config network telnet disable
save config
show network summary
```

## APs
As the APs are connected to the network, they should automatically find the controller via the CAPWAP discovery algorithms

The Dynamic Host Configuration Protocol (DHCP) server will assign each AP an IP address

CCisco Aironet 1850 Access Point

https://www.cisco.com/c/en/us/products/wireless/aironet-1850-series-access-points/index.html

## Reference
Cisco 5520 Wireless LAN Controller Deployment Guide

https://www.cisco.com/c/en/us/td/docs/wireless/controller/technotes/8-1/5520-WLC-DG/b_Cisco-5520-WLC-deployment-guide.html

Cisco 5520 and 8540 Wireless Controller Troubleshooting Guide

https://www.cisco.com/c/en/us/td/docs/wireless/controller/technotes/troubleshooting/trb-guide-wlc-5520-8540.pdf