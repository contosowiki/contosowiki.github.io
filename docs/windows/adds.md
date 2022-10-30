---
layout: default
title: Active Directory
parent: Windows
nav_order: 1
---

# Active Directory
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## Active Directory Domain Services Design

* Single forest single domain is preferred, 2,150,000,000 objects per domain, FQDN less than 64 characters
* Selecting the Forest Root Domain (corp.contoso.wiki) https://technet.microsoft.com/en-us/library/cc726016(v=ws.10).aspx
* PDC acts as a key role (time root in forest, etc)
* Implement multiple/backup domain controllers (all GCs)
* Implement multiple sites as needed (site, subnet,site link(180 minutes default, 15 minutes minimum), bridge all site links(default))
* Enable [[Active Directory Recycle Bin]]
* Enable [[Protect object from accidental deletion]] (User, OU, etc)
* Fill more AD account properties (City, Country, Phone, Job Title, Department, Manager...) [[Create AD user with PowerShell]]
* Grant permission per group, not a single user
* [[Account Lockout]] Policy
* [[Delegate IT helpdesk group join computer into domain permission]]

## Install first domain controller

### Install Windows Server 2019

```powershell
# Check Operating System version
(Get-WmiObject -Class Win32_OperatingSystem).Caption
Microsoft Windows Server 2019 Standard
```

### Rename hostname

```powershell
# BJ stands for Beijing
# DC stands for Domain Controller
Rename-Computer BJDC01
Restart-Computer
Get-Content Env:COMPUTERNAME
```

### Configure IP information

```powershell
IP address: 10.10.10.10
Subnet mask: 255.255.255.0
Default gateway: 10.10.10.1
Preferred DNS server: 10.10.10.10
```

### Install Active Directory Domain Services

```powershell
From Start Menu, Click "Server Manager"
Click "Add roles and features"
Click "Next"
Keep default option "Role-based or feature-based installation", Click "Next"
Keep defaut option, Click "Next"
Select "Active Directory Domain Services", and Click "Add Features" from the pop up window
Click "Next"
Click "Next"
Click "Next"
Click "Install"
Click "Close" when finish
```

### Post-deployment Configuration

```powershell
Click "Flag" icon
Click "Promote this server to a domain controller"
Select "Add a new forest", input "contoso.wiki" as "Root domain name", click "Next"
Keep default option
# Forest functional level: Windows Server 2016
# Domain functional level: Windows Server 2016
# Domain Name System (DNS) Server checked
# Global Catalog (GC) checked
# Read only domain controller (RODC) unchecked and unavailabled for the first Domain Controller
Input the Directory Services Restore Mode (DSRM) password, click "Next"
Keep default DNS Options, click "Next"
Keep default NetBIOS domain name, click "Next"
Keep default options of AD DS database, log files, and SYSVOL, click "Next"
Click "Next"
Click "Install" after Prerequisites Check done
```

### Configure time

```powershell
# By default, the first domain controller is PDC too, PDC is the time root of the forest.
w32tm /config /computer:BJDC01.contoso.wiki /manualpeerlist:time.windows.com /syncfromflags:manual /update
```

### FSMO Role Holders

Schema master / Forest level"： To make change Schema in forest (such as implement Exchange, Lync, SCCM)

Domain naming master / Forest level: To add/remove domain in forest

PDC / Domain level: Time root in forest (PDC->DCs->Computers); Group policy central management; Handle password change specially (the change will sync to PDC immediately); Handle user account lock specially

RID pool master / Domain level: Assign RIDs to DCs (500/time)

Infrastucture master / Domain level: Objects reference in different domains

Get list of FSMO role holders
```powershell
netdom query fsmo
Schema master               BJDC01.contoso.wiki
Domain naming master        BJDC01.contoso.wiki
PDC                         BJDC01.contoso.wiki
RID pool manager            BJDC01.contoso.wiki
Infrastructure master       BJDC01.contoso.wiki
```

or

```powershell
# Forest Level
Get-ADForest | Select-Object DomainNamingMaster, SchemaMaster
DomainNamingMaster  SchemaMaster       
------------------  ------------       
BJDC01.contoso.wiki BJDC01.contoso.wiki
# Domain Level
Get-ADDomain | Select-Object InfrastructureMaster, RIDMaster, PDCEmulator
InfrastructureMaster RIDMaster           PDCEmulator        
-------------------- ---------           -----------        
BJDC01.contoso.wiki  BJDC01.contoso.wiki BJDC01.contoso.wiki
```

## Install second/backup domain controller

### Install Windows Server 2019

```powershell
# Check Operating System version
(Get-WmiObject -Class Win32_OperatingSystem).Caption
Microsoft Windows Server 2019 Standard
```

### Rename hostname

```powershell
# BJ stands for Beijing
# DC stands for Domain Controller
Rename-Computer BJDC02
Restart-Computer
Get-Content Env:COMPUTERNAME
```

### Configure IP information

```powershell
IP address: 10.10.10.11
Subnet mask: 255.255.255.0
Default gateway: 10.10.10.1
Preferred DNS server: 10.10.10.10
```

### Join Domain

```powershell
# Do a ping test
ping contoso.wiki

Pinging contoso.wiki [10.10.10.10] with 32 bytes of data:
Reply from 10.10.10.10: bytes=32 time<1ms TTL=128
Reply from 10.10.10.10: bytes=32 time<1ms TTL=128
Reply from 10.10.10.10: bytes=32 time<1ms TTL=128
Reply from 10.10.10.10: bytes=32 time<1ms TTL=128

Ping statistics for 10.10.10.10:
    Packets: Sent = 4, Received = 4, Lost = 0 (0% loss),
Approximate round trip times in milli-seconds:
    Minimum = 0ms, Maximum = 0ms, Average = 0ms

# Join Domain
Add-Computer –Domainname "contoso.wiki"  -Restart
```

### Install Active Directory Domain Services

```powershell
# Log in with domain administrator (contoso\administrator)
From Start Menu, Click "Server Manager"
Click "Add roles and features"
Click "Next"
Keep default option "Role-based or feature-based installation", Click "Next"
Keep defaut option, Click "Next"
Select "Active Directory Domain Services", Click "Next"
Click "Next"
Click "Next"
Click "Install"
Click "Close" when finish
```

### Post-deployment Configuration

```powershell
Click "Flag" icon
Click "Promote this server to a domain controller"
Keep default option "Add a domain controller to an existing domain", click "Next"
Keep default option
# Domain Name System (DNS) Server checked
# Global Catalog (GC) checked
# Read only domain controller (RODC) unchecked
# Site name: Default-First-Site-Name
Input the Directory Services Restore Mode (DSRM) password, click "Next"
Keep default DNS Options, click "Next"
Keep default Additional Options, click "Next"
Keep default options of AD DS database, log files, and SYSVOL, click "Next"
Click "Next"
Click "Install" after Prerequisites Check done
```

List domain controllers

```powershell
# Get all domain controllers
Get-ADGroupMember "Domain Controllers"

distinguishedName : CN=BJDC02,OU=Domain Controllers,DC=contoso,DC=wiki
name              : BJDC02
objectClass       : computer
objectGUID        : 65d42249-74d7-4b35-be83-8192c782ca3c
SamAccountName    : BJDC02$
SID               : S-1-5-21-1387974904-744306665-268114308-1103

distinguishedName : CN=BJDC01,OU=Domain Controllers,DC=contoso,DC=wiki
name              : BJDC01
objectClass       : computer
objectGUID        : 8d1cf2be-0c95-4815-8e74-5ed711c62146
SamAccountName    : BJDC01$
SID               : S-1-5-21-1387974904-744306665-268114308-1000

# Get all domain controllers and get basic information
Get-ADGroupMember "Domain Controllers" | Get-ADDomainController | Select-Object Name,Forest,Domain,Site,IsGlobalCatalog,IPv4Address | Format-Table

Name   Forest       Domain       Site                    IsGlobalCatalog IPv4Address
----   ------       ------       ----                    --------------- -----------
BJDC02 contoso.wiki contoso.wiki Default-First-Site-Name            True 10.10.10.11
BJDC01 contoso.wiki contoso.wiki Default-First-Site-Name            True 10.10.10.10
```

Get list of FSMO role holders

```powershell
netdom query fsmo
Schema master               BJDC01.contoso.wiki
Domain naming master        BJDC01.contoso.wiki
PDC                         BJDC01.contoso.wiki
RID pool manager            BJDC01.contoso.wiki
Infrastructure master       BJDC01.contoso.wiki
```

or

```powershell
# Forest Level
Get-ADForest | Select-Object DomainNamingMaster, SchemaMaster
DomainNamingMaster  SchemaMaster       
------------------  ------------       
BJDC01.contoso.wiki BJDC01.contoso.wiki
# Domain Level
Get-ADDomain | Select-Object InfrastructureMaster, RIDMaster, PDCEmulator
InfrastructureMaster RIDMaster           PDCEmulator        
-------------------- ---------           -----------        
BJDC01.contoso.wiki  BJDC01.contoso.wiki BJDC01.contoso.wiki
```