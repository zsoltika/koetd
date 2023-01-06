---
title: "TIL powershell pwd és könyvtár-megjegyzés"
tags:
- TIL
- powershell
- CLI
---

Meglepődtem, midőn a PowerSHellből kiadott `pwd` nem működött, de nyilván az első Google keresés kidobta hogy a megfejtés itt az automatikusan beállított `$PWD` változó. 

Ami miatt kerestem, az az, hogy munkakönyvtárakat könyvjelzőzhessel. Linuxon (shellben) erre sok megoldás van, és némelyik működik Powershellben is, pl. a [zoxide](https://github.com/ajeetdsouza/zoxide). De nyilván ez túl későn jutott eszembe, így megintcsak az első Googel keresés után:


```powershell
$ Install-Module -Name PSBookmark

Untrusted repository
You are installing the modules from an untrusted repository. If you trust this repository, change its InstallationPolicy value by running the
Set-PSRepository cmdlet. Are you sure you want to install the modules from 'PSGallery'?
[Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help (default is "N"): A

$ $PWD

Path
----
C:\Users\REDACTED\PATH\ALSO\REDACTED

$ save redacted_path $PWD
$ cd SOMEWHERE_ELSE
$ # do something
$ goto redacted_path
```

Megy mint a karikacsapás.