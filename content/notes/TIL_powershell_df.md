---
title: "TIL powershell df"
tags:
- TIL
- powershell
- CLI
---

Az első gondolatom a `get-disk` volt, de nyilván nem mutatja meg a még felhasználható tárhelyet. Szerencsére a `get-volume` igen.

```powershell
$ get-volume

DriveLetter FriendlyName FileSystemType DriveType HealthStatus OperationalStatus  SizeRemaining      Size
----------- ------------ -------------- --------- ------------ -----------------  -------------      ----
            Recovery     NTFS           Fixed     Healthy      OK                       4.35 GB   4.77 GB
C           Windows      NTFS           Fixed     Warning      Full Repair Needed       28.8 GB 471.56 GB
```

És hát úgy tűnik, jöhet a `chkdisk` :-/