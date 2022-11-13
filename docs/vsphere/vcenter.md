---
layout: default
title: vCenter Installation
parent: vSphere
nav_order: 3
---

# vCenter Installation
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## Prerequirement
Make sure both A and ptr records are in DNS server.

```powershell
C:\Users\Admin>nslookup
默认服务器:  bjdc01.contoso.wiki
Address:  192.168.10.10

> set type=a
> vcenter.contoso.wiki
服务器:  bjdc01.contoso.wiki
Address:  192.168.10.10

名称:    vcenter.contoso.wiki
Address:  192.168.10.100

> bjesx01.contoso.wiki
服务器:  bjdc01.contoso.wiki
Address:  192.168.10.10

名称:    bjesx01.contoso.wiki
Address:  192.168.10.101

> set type=ptr
> 192.168.10.100
服务器:  bjdc01.contoso.wiki
Address:  192.168.10.10

100.10.168.192.in-addr.arpa     name = vcenter.contoso.wiki
> 192.168.10.101
服务器:  bjdc01.contoso.wiki
Address:  192.168.10.10

101.10.168.192.in-addr.arpa     name = bjesx01.contoso.wiki
```

## Install
```shell
# Mount VMware-VCSA-all-8.0.0-20519528.iso
# On Windows system, launch G:\vcsa-ui-installer\win32\installer.exe
1. "vCenter Server Installer" window, select "Install"
2. "Introduction" window, click "Next"
3. "End user license agreement" window, check "I accept the terms of the license agreement.", click "Next"
4. "vCenter Server deployment target" window, input the required information, click "Next"
# ESXi host or vCenter Server name: bjesx01.contoso.wiki
# HTTPS port: 443
# User name: root
# Password: ********
5. "Certificate Warning" window, click "Yes"
6. "Set up vCenter Server VM" window, input "VM name", "Set root password", and "Confirm root password", click "Next"
7. "Select deployment size" window, select "Deployment size" and "Storage size", click "Next"
8. "Select datastore" window, select the datastore, click "Next"
# NFS datastores are thin provisioned by default
9. "Configure network settings" window, input the required information, click "Next"
# Network: VM Network
# IP version: IPv4
# IP assignment: static
# FQDN: vcenter.contoso.wiki
# IP address: 192.168.10.100
# Subnet mask or prefix length: 255.255.255.0
# Default gateway: 192.168.10.1
# DNS server: 192.168.10.10
# HTTP: 80
# HTTPS: 443
10. "Ready to complete stage 1" window, click "Finish"
11. "Install - Stage 1: Deploy vCenter Server" window indicates："You have successfully deployed the vCenter Sever.", click "Continue"
12. "Install - Stage 2: Set Up vCenter Server" window, click "Next"
13. "vCenter Server Configuration" window, setup as below and click "Next"
# Time syncrinization mode: Synchronize time with the NTP servers
# NTP servers: 192.168.10.10
# SSH access: Activated
# For vCenter Server High Availability (HA), activate SSH access.
14. "SSO Configuration" window, setup as below and click "Next"
# Create a new ssh domain
# Single Sign-On domain name: vsphere.local (default)
# Single Sign-On username: administrator
# Single Sign-On password: **********
14. "Configure CEIP" window, click "Next"
15. "Ready to complete" window, review the settings and click "Finish"
16. "Warning" window, click "OK" to start
17. "Install - Stage 2: Complete" window indicates "You have successfully setup this vCenter Server."
# vCenter Server Getting Started Page : https://vcenter.contoso.wiki:443
```