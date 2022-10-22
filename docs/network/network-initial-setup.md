---
layout: default
title: Initial Setup
parent: Network
nav_order: 1
---

# Network device initial setup
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## Putty 
Switch <-> Console cable <-> Laptop（Putty）
[[File:Putty.png|thumb|alt=|none]]

## General 
```shell
system-view
sysname switch01
undo info-center enable
save
```

## SSH Login 
```shell
system-view
public-key local create rsa
ssh server enable
line vty 0 10
authentication-mode scheme
quit
local-user admin class manage
password simple Password123
service-type ssh
authorization-attribute user-role network-admin
quit
```

## AUX Login 
```shell
line aux 0
authentication-mode scheme
quit
local-user admin class manage
password simple Password123
service-type terminal
authorization-attribute user-role network-admin
undo authorization-attribute user-role network-operator
quit
```

## NTP 
```shell
clock timezone Beijing add 08:00:00
ntp-service enable
ntp-service unicast-server 10.10.10.10
ntp-service unicast-server 10.10.10.11
display ntp sessions
display ntp status
display clock
```

=== VLAN ===
```shell
vlan 100
description Office
interface vlan-interface 100
ip address 10.10.100.1 255.255.255.0
```

=== Interface ===
```shell
# Gigabitethernet 1000M
interface Gigabitethernet 1/0/1
description Location 001
port access vlan 100
show this
# shudown & undo shutdown when needed
shutdown
undo shutdown
# Setup speed & duplex when needed
speed 1000
duplex full
```

=== Trunk ===
```shell
# ten-gigabitethernet 10000M
interface ten-gigabitethernet 1/0/48
description To Core Switch
port link-type trunk
port trunk permit vlan all
```

=== Etherchanel ===
```shell
interface bridge-aggregation 1
quit
interface range ten-gigabitethernet 1/0/47 to 1/0/48
port link-aggregation group 1
quit
interface bridge-aggregation 1
port link-type trunk
port trunk permit vlan all
show link-aggregation summary
show link-aggregation verbose
```

=== LLDP ===
```shell
sytem-view
lldp enable
display lldp neighbor-information
display lldp neighbor-information interface Ten-GigabitEthernet 1/0/48
```

=== Display ===
```shell
display current-configuration
display current-configuration interface
display current-configuration interface Gigabitethernet 1/0/1
display interface brief
display this
display saved-configuration
display version
diaply vlan
```

=== Save and backup configuration ===
```shell
# Save configuration
save
# Free (Windows) TFTP Server from solarwinds
# Backup to TFTP
backup startup-configuration to 10.10.10.10
# Restore from TFTP backup
restore startup-configuration from 10.10.10.10 start-configuration-backup.cfg
# Restore to factory defaut（!!!Be careful）
<BJ-1F-SW01>reset saved-configuration
```

=== IRF Stack ===
```shell
# On switch01
irf domain 20
irf member 1 priority 32
int Ten-GigabitEthernet 1/0/26
shutdown
irf-port 1/2
port group interface Ten-GigabitEthernet 1/0/26
quit
int Ten-GigabitEthernet 1/0/26
undo shutdown

# On switch02
irf member 1 renumber 2
save
reboot
int Ten-GigabitEthernet 2/0/26
shutdown
irf-port 2/1
port group interface Ten-GigabitEthernet 2/0/26
quit
int Ten-GigabitEthernet 2/0/26
undo shutdown

# On swith01
irf-port-configuration active

# On switch01 or switch02
display irf link
display irf topology
display irf configuration
display irf-port load-sharing mode
```