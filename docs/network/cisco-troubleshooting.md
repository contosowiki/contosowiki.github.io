---
layout: default
title: Cisco Troubleshooting
parent: Network
nav_order: 7
---

# Cisco Troubleshooting
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## Check the switch port based on IP address
 ```js
# On core switch
show arp | include 192.168.200.100
show mac address-table | include 3a00.031e.bb00
Locate the access switch from above input
# On access switch
show mac address-table | include 3a00.031e.bb00
```

## Check IP based on MAC address
 ```js
show arp | include 0000.0000.0001
```

## Private VLAN Sticky-ARP issue
 ```js
# global
no ip sticky-arp
# interface
ip sticky-arp ignore
```

## Arp entry does not age out and need clean arp cache manually
 ```js
Command clean arp-cache may not work
And need to use command clean ip arp
Cisco Bug cscsk46195
In Cisco IOS® software, the ARP cache timeout is set to four hours (240 minutes) by default
Show interface vlan 10 | include ARP
The extra time is the jitter added to each dynamic ARP entry when it is created. Random jitter is added to the ARP cache timeout in order to avoid synchronous expiration of the ARP entries, which might trigger an ARP storm. Jitter should be a random number between 0 seconds and 30 minutes, with a maximum jitter of 30 minutes
show arp 192.168.200.100 detail
```

## Debug DHCP
 ```js
debug dhcp server events
show ip dhcp pool VLAN10
show ip dhcp conflict
no ip dhcp conflict logging
ip dhcp conflict resolution
```

## 10/100/1000M port only work on 100M mode
 ```js
Cat 5E or higher
All 4 pairs
```

## Lost package when ping iDRAC IP address
 ```js
iDRAC may not work properly on 10/100/1000M Auto mode
Set 100M on switch port manually
```

## MAC Vendor Lookup
https://macvendors.com/

## Create reservation in DHCP scope on Cisco switch
 ```js
Get client-id
show ip dhcp binding
Add IP reservation
ip dhcp pool Lab
address 192.168.200.100 client-id 01FC.AA14.8B0B.0C
Why do some computers use "Client-Identifier" and others use "Hardware-address"?
If the client chooses to send a Client-Identifier the server has to use it; If the client does not the server uses Hardware-address.
Remove IP reservation
clear ip dhcp binding 192.168.200.100
```

## Ping
 ```js
# Example 1
C:\Users\administrator>ping 192.168.200.10
Pinging 192.168.200.10 with 32 bytes of data:
Reply from 192.168.200.10: bytes=32 time<1ms TTL=64
Reply from 192.168.200.10: bytes=32 time<1ms TTL=64
Reply from 192.168.200.10: bytes=32 time<1ms TTL=64
Reply from 192.168.200.10: bytes=32 time<1ms TTL=64
Ping statistics for 192.168.200.10:
Packets: Sent = 4, Received = 4, Lost = 0 (0% loss),
Approximate round trip times in milli-seconds:
Minimum = 0ms, Maximum = 0ms, Average = 0ms
# Example 2
C:\Users\administrator>ping 192.168.200.20
Pinging 192.168.200.20 with 32 bytes of data:
Reply from 192.168.200.20: bytes=32 time<1ms TTL=128
Reply from 192.168.200.20: bytes=32 time<1ms TTL=128
Reply from 192.168.200.20: bytes=32 time<1ms TTL=128
Reply from 192.168.200.20: bytes=32 time<1ms TTL=128
Ping statistics for 192.168.200.20:
Packets: Sent = 4, Received = 4, Lost = 0 (0% loss),
Approximate round trip times in milli-seconds:
Minimum = 0ms, Maximum = 4ms, Average = 1ms
```