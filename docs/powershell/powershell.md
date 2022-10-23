---
layout: default
title: PowerShell Script
nav_order: 9
has_children: true
permalink: /docs/powershell
---

# PowerShell

## Windows general commands

System
```powershell
msinfo32
msconfig
mstsc
sfc /scannow
runas /noprofile /user:alphabook\admin01 cmd
wuauclt /detectnow
wuauclt /reportnow
gpupdate /force
gpresult /h GPreport.html
xcopy C:\Source C:\Destination /e /h /y
```

Network
```powershell
ipconfig /all
ipconfig /flushdns
ipconfig /release
arp -a
ping
tracert
nslookup
netsh winsock reset
route print
route add 10.20.0.0 mask 255.255.0.0 192.168.12.1
route delete 10.20.0.0
netstat -an | find "LISTENING"
```

Disk
```powershell
diskpart
```

KMS
```powershell
slmgr.vbs /?
..\office15\cscript ospp.vbs
# Windows server 2019 eval to standard (KSM Key)
dism /online /set-edition:ServerStandard /productkey:N69G4-B89J2-4G8F4-WWYCC-J464C /accepteula
```

Domain Environment
```powershell
net user /domain user01
set l
nltest
netdom query fsmo
nslookup
dcdiag
repadmin
ntdsutil
net stop netlogon
net start netlogon
```

## Windows general tools

```powershell
Remote Desktop Connection Manager
Remote Server Administration Tools
Bginfo
TreeSize
DeviceTool
Device Viewer
Windows USB/DVD Download Tool
Windows Update Troubleshooter
Account Lockout Status(LockoutStatus.exe)
System repair disk
DaRT (Microsoft Diagnostics and Recovery Toolset)
WinDbg
Process Explorer
Process Monitor
PStools
```