Thus, invocations of these applications with different components on the command line will result in different traces.

For a system boot, a different mechanism is used, called ReadyBoot. ReadyBoot tries to optimize I/O operations by creating large and efficient reads and storing the data in RAM. When system components require a disk, it is served through the stored RAM. This especially benefits mechanical disks, but can also be useful for SSDs. Information on the files to fetch is stored after boot in the ReadyBoot subdirectory of the Prefetch directory shown in Figure 5-33. Once boot is complete, the cached data in RAM is deleted. For very fast SSDs, ReadyBoot is off by default because its gains are marginal, if any.

When the system boots or an application starts, the prefetcher gives it an opportunity to prefetch. The prefetch looks in the prefetch directory to see if a trace exists for the prefetch scenario in query. If it does, the prefetch calls NTFS to prefetch any metadata file references, reads the contents of all the directories referenced, and finally opens each file referenced. Then calls the memory manager function MnPrefetch to read any data and code specified in that trace's not already in memory. The memory manager initiates all the reads asynchronously and then waits for them to complete before leaving an application's startup.

# EXPERIMENT: Watching prefetch file and writes

If you capture a trace of application startup with Process Monitor from Sysinternals on a client edition of Windows (Windows Server edition disabling prefetch), you can see the prefetcher check for read the application's prefetch file (if it exists). In addition, you can see the prefetcher write out roughly 10 seconds after the application starts. Here is a capture of Notepad startup with an Include filter set to prefetch so that Process Monitor shows only accesses to the %SystemRoot\Prefetch directory:

| Seq | Event | Time of Day | Process Name | PID | Operation | Path | Result |
|---|---|---|---|---|---|---|-|
| 1 | 13 | 11:31:38.256 | notepad.exe | 1428 | Query | C:\Windows\Prefetch\NOTEPAD_EXE_9FB27CO.pf | SUCCESS |
| 2 | 13 | 11:31:38.307 | notepad.exe | 1429 | QueryFile | C:\Windows\Prefetch\NOTEPAD_EXE_9FB27CO.pf | SUCCESS |
| 3 | 13 | 11:31:38.337 | notepad.exe | 1429 | QueryFile | C:\Windows\Prefetch\NOTEPAD_EXE_9FB27CO.pf | SUCCESS |
| 4 | 13 | 11:31:38.354 | notepad.exe | 1429 | QueryFile | C:\Windows\Prefetch\NOTEPAD_EXE_9FB27CO.pf | SUCCESS |
| 5 | 13 | 11:32:38.76601 | notepad.exe | 3524 | QueryFile | C:\Windows\Prefetch | SUCCESS |
| 6 | 13 | 11:32:38.76601 | notepad.exe | 3524 | QueryFile | C:\Windows\Prefetch | SUCCESS |
| 7 | 13 | 11:32:38.87048 | notepad.exe | 1436 | QueryFile | C:\Windows\Prefetch | SUCCESS |
| 8 | 13 | 11:32:38.87048 | notepad.exe | 1436 | CreateFileMapping | C:\Windows\Prefetch\NOTEPAD_EXE_9FB27CO.pf | SUCCESS |
| 9 | 13 | 11:32:38.87048 | notepad.exe | 1436 | CreateFileMapping | C:\Windows\Prefetch\NOTEPAD_EXE_9FB27CO.pf | SUCCESS |
| 10 | 13 | 11:32:38.87113 | notepad.exe | 1436 | CreateFile | C:\Windows\Prefetch\NOTEPAD_EXE_9FB27CO.pf | FILE LOCKED WITH |
| 11 | 13 | 11:32:38.87123 | notepad.exe | 1436 | QueryFile | C:\Windows\Prefetch\NOTEPAD_EXE_9FB27CO.pf | SUCCESS |
| 12 | 13 | 11:32:38.87163 | notepad.exe | 1436 | QueryFile | C:\Windows\Prefetch\NOTEPAD_EXE_9FB27CO.pf | SUCCESS |
| 13 | 13 | 11:32:38.87669 | notepad.exe | 1436 | QueryFile | C:\Windows\Prefetch\NOTEPAD_EXE_9FB27CO.pf | SUCCESS |
| 14 | 13 | 11:32:38.87662 | notepad.exe | 1436 | QueryFile | C:\Windows\Prefetch\NOTEPAD_EXE_9FB27CO.pf | SUCCESS |
| 15 | 13 | 11:32:38.87725 | notepad.exe | 1436 | WriteFile | C:\Windows\Prefetch\NOTEPAD_EXE_9FB27CO.pf | SUCCESS |
| 16 | 13 | 11:32:38.87728 | notepad.exe | 1436 | WriteFile | C:\Windows\Prefetch\NOTEPAD_EXE_9FB27CO.pf | SUCCESS |
| 17 | 13 | 11:32:38.87746 | notepad.exe | 1436 | CreateBasicInformation | C:\Windows\Prefetch\NOTEPAD_EXE_9FB27CO.pf | SUCCESS |
| 18 | 13 | 11:32:38.87746 | notepad.exe | 1436 | WriteFile | C:\Windows\Prefetch\NOTEPAD_EXE_9FB27CO.pf | SUCCESS |
| 19 | 13 | 11:32:38.87753 | notepad.exe | 1436 | WriteFile | C:\Windows\Prefetch\NOTEPAD_EXE_9FB27CO.pf | SUCCESS |
| 20 | 13 | 11:32:38.87753 | notepad.exe | 1436 | Query | C:\Windows\Prefetch | SUCCESS |
| 21 | 13 | 11:43:29.76215 | explorer.exe | 3624 | QueryDirectory | C:\Windows\Prefetch | SUCCESS |
| 22 | 13 | 11:43:29.7974 | explorer.exe | 3624 | QueryFile | C:\Windows\Prefetch | SUCCESS |
| 23 | 13 | 11:43:29.79759 | explorer.exe | 3524 | CreateFile | C:\Windows\Prefetch | SUCCESS |

![](bbox=[0.181, 0.563, 0.81, 0.735])