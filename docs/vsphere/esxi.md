---
layout: default
title: ESXi
parent: vSphere
nav_order: 1
---

# ESXi
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## Install

```shell
1. "Welcome to the VMware ESXi 8.0.0 Installation" window, press "Enter" to continue
2. "End User License Agreement (EULA)" window, press "F11" to accept and continue
3. "Select a Disk to Install or Upgrade" window, keep default and press "Enter" to continue
4. "Please select a keyboard layout" window, keep default (US Default) and press "Enter" to continue
5. "Enter a root password" window, input root password twice and press "Enter" to continue
6. "Confirm Install" window, press "F11" to install
7. "Installation Compete" window, press "Enter" to reboot
```

## Configure IP address
```shell
1. Press "F2" to customize system
2. "Authentication Required" windows, input password, press "Enter"
3. Select "Configure Management Network", press "Enter"
4. Select "IPv4 Configuration", press "Enter"
5. Check option "Set static IPv4 address and network configuration:"
6. Fill "IPv4 Address", "Subnet Mask" and "Default Gateway" and press "Enter"
```

## Configure DNS
```shell
1. Press "F2" to customize system
2. "Authentication Required" windows, input password, press "Enter"
3. Select "Configure Management Network", press "Enter"
4. Select "DNS Configuration", press "Enter"
5. Check option "Use the following DNS server addresses and hostname:"
6. Fill "Primary DNS Server", "Alternate DNS Server" and "Hostname" and press "Enter"
```

## Network VLAN

A VLAN is a virtual network within a physical network.

```shell
1. Press "F2" to customize system
2. "Authentication Required" windows, input password, press "Enter"
3. Select "Configure Management Network", press "Enter"
4. Select "VLAN (optional)", press "Enter"
5. Fill "VLAN ID" and press "Enter"
```

Port configuration on swith side (Cisco Switch)
```js
interface Ethernet1/1
  description To BJ ESXi Host 01
  switchport
  switchport mode trunk
  switchport trunk allowed vlan 10,20,30
  no shutdown
```

Port configuration on swith side (H3C Switch)
```css
interface ten-gigabitethernet 1/0/1
description To BJ ESXi Host 01
port link-type trunk
port trunk permit vlan 10 20 30
```

## Network fault-tolerance and load-balancing

Use two or more network NICs for fault-tolerance and load-balancing.

```shell
1. Press "F2" to customize system
2. "Authentication Required" windows, input password, press "Enter"
3. Select "Configure Management Network", press "Enter"
4. Select "Network Adapters", press "Enter"
5. By default one adapter is checked, we could add the second or more adapters, and press "Enter"
```

First port configuration on swith side (Cisco Switch)
```js
interface Ethernet1/1
  description To BJ ESXi Host 01
  switchport
  switchport mode trunk
  switchport trunk allowed vlan 10,20,30
  no shutdown
```

Second port configuration on swith side (Cisco Switch)
```js
interface Ethernet1/1
  description To BJ ESXi Host 01
  switchport
  switchport mode trunk
  switchport trunk allowed vlan 10,20,30
  no shutdown
```

First port configuration on swith side (H3C Switch)
```css
interface ten-gigabitethernet 1/0/1
description To BJ ESXi Host 01
port link-type trunk
port trunk permit vlan 10 20 30
```

Second port configuration on swith side (H3C Switch)
```css
interface ten-gigabitethernet 1/0/1
description To BJ ESXi Host 01
port link-type trunk
port trunk permit vlan 10 20 30
```

Above configuration, we do not do EthernetChannel or link-aggregation, this is a basic working way.