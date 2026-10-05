# System Summary

| Name | Description | Path | Type | Started | Mode | Status |
| --- | --- | --- | --- | --- | --- | --- |
| Inware | 1984 DHO Compliant Hot... | c:\windows\system32\drivers\inware.sys | Kernel | No | Manual | Stopped |
| Compware | | c:\windows\system32\drivers\compware.sys | Kernel | No | Manual | Stopped |
| PreEnv | | c:\windows\system32\drivers\prenv.sys | Kernel | No | Manual | Stopped |
| Environment variables | | c:\windows\system32\drivers\envvars.sys | Kernel | No | Manual | Stopped |
| acdev | | ACPI Devices | c:\windows\system32\drivers\acdev.sys | Kernel | No | Manual | Stopped |
| aspdev | | c:\windows\system32\drivers\aspdev.sys | Kernel | No | Manual | Stopped |
| Network Connections | | c:\windows\system32\drivers\netconn.sys | Kernel | No | Manual | Stopped |
| Runtime | | ACPI Web Alarm Driver | c:\windows\system32\drivers\rtalarm.sys | Kernel | No | Manual | Stopped |
| Loaded Modules | | c:\windows\system32\drivers\loadmod.sys | Kernel | No | Manual | Stopped |
| Program Groups | | Application Handler for... | c:\windows\system32\drivers\progrp.sys | Kernel | Yes | Running | OK |
| Starting Programs | | c:\windows\system32\drivers\startpr.sys | Kernel | Yes | Running | OK |
| Old Registration | AMD AMD6 Processor Controller | c:\windows\system32\drivers\oldreg.sys | Kernel | No | Manual | Stopped |
| Windows Error Reporting | | c:\windows\system32\drivers\werfault.sys | Kernel | No | Manual | Stopped |
| amndata | | c:\windows\system32\drivers\amndata.sys | Kernel | No | Manual | Stopped |
| amndata | | c:\windows\system32\drivers\amndata.sys | Kernel | No | Manual | Stopped |

Find
[ ] search selected only [ ] search category names only Find Next

The list of drivers from the registry keys under HKLM\System\CurrentControlSet\Services. This is shared between drivers and services. It can be started by the Service Control Manager (SCM). The way to distinguish a driver and a service for eachsubkey is by looking at the Type value. A small value (1, 2, 4, 8) indicates a driver, while 16 (0x10) and 32 (0x20) indicates a Windows service. For more information on the driverskey, consult Chapter 9 in Part 2.

You can also view the list of kernel-mode drivers with Process Explorer. Run Process Explorer, select the System process, and select DLLs from the Lower Pane View entry in the View:

![](bbox=[0.195, 0.445, 0.805, 0.665])

| PID | Image | CPU | Memory | Working Set | Thread | Company Name | Base | |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 4 | System | 0.0 | 28448 | 28448 | 4 | Microsoft Corporation | 0x000000000000000 | |
| 512 | smss.exe | 0.0 | 800 | 800 | 1 | Microsoft Corporation | 0x000000000000000 | |
| 640 | services.exe | 0.0 | 12400 | 12400 | 3 | Microsoft Corporation | 0x000000000000000 | |
| 1244 | explorer.exe | 0.0 | 15120 | 15120 | 12 | Microsoft Corporation | 0x000000000000000 | |
| 2500 | svchost.exe | 0.0 | 4500 | 4500 | 8 | Microsoft Corporation | 0x000000000000000 | |
| 3200 | lsass.exe | 0.0 | 9200 | 9200 | 2 | Microsoft Corporation | 0x000000000000000 | |
| 4100 | wininit.exe | 0.0 | 2100 | 2100 | 1 | Microsoft Corporation | 0x000000000000000 | |
| 5000 | csrss.exe | 0.0 | 3300 | 3300 | 4 | Hardware Vendor and DPCs | 0x000000000000000 | |

Process Explorer lists the loaded drivers, their version information (including company and description), and load address (assuming you have configured Process Explorer to display the corresponding columns).

Finally, if you're looking at a crash dump (or live system) with the kernel debugger, you can see a similar detail with the kernel debugger km:

```
kd> lm km
start end module name
80626000 80631100 kdcom             (deferred)
Image path: kdcom.dll
```

CHAPTER 6 I/O system 497