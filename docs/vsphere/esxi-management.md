---
layout: default
title: ESXi Management
parent: vSphere
nav_order: 2
---

# ESXi Management
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

Access ESXi from https://x.x.x.x

## License
```shell
Host -> Manage -> Licensing -> Assign license -> Check License -> Assign License
```

## Time
```shell
# Time is key important for all systems

# Enable and start ntpd service
Host -> Manage -> Services -> ntpd -> Start
Host -> Manage -> Services -> ntpd -> Actions -> Policy -> Start and stop with host

# Setup NTP
Host -> Manage -> System -> Time & Date -> Edit NTP Setttings -> Use Network Time Protocol (enable NTP client) -> NTP Servers -> Save

```

## Storage
```shell
# Add NFS datastore
Storage -> New datastore -> Mount NFS datastore -> Name / NFS server / NFS share / NFS version -> Next -> Finish

# NFS mount details
Name: My nfs
NFS Server: x.x.x.x
NFS Share: /nfs
NFS Version: NFS 3
```

## Networking
```shell
# There is default virtual switch named by "VSwitch0"
# There is default port group (management) named by "Management Network" (Function: Management, vMotion, Provisioning, Fault tolerance logging, etc)
# There is default port group (Virtual Machine) named by "VM Network"

# Add new port group as needed
Networking -> Add port group -> Name / VLAN ID / Virtual switch -> ADD
```

## Virtual Machines
```shell
# Create new virtual machine from scratch
Virtual Machines -> Create / Register VM -> Create new virtual machine -> Name / Compatibility / Guest OS family / Guest OS version -> Next -> Select storage -> Next -> Hardware customize settings -> Next -> Finish

# We could also "Deploy a virtual machine from an OVF or OVA file" or "Register an existing virtual machine"
```