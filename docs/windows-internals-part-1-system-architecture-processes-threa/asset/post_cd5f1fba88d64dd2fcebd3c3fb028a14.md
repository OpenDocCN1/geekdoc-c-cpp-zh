
and the SuperFetch component that we'll talk about later. The prefetcher signals %KerneObjects\PrefetchTraces% ready to inform the SuperFetch service that it can now query trace data.

> You can enable or disable prefetching of boot or application starts by editing the DWORD registry value EnablePrefetcher in the HKLM\SYSTEM\CurrentControl\Control\Session Manager\Memory Management\PrefetchParameters key. Set it to 0 to disable prefetching, 1 to enable prefetching of only applications, 2 for prefetching of boot, and 3 for both boot and applications.

The SuperFetch service (which hosts the local prefetcher, although it is a completely separate component from the actual SuperFetch functionality) performs a call to the internal NtQuerySystemInformation call requesting the trace data. The local prefetcher post-processes the data, combining it with previously collected data, and writes it to a %SystemRoot%\Prefetch folder (Figure 5-3). The file name is the name of the application to which the trace applies followed by a hash and a hexadecimal representation of the file's path. The file has a .pf extension. An example would be Notepad.EXE-9FB27COE.PF.

![](img/ff0e6a9d867a3a6e9527eb1d946810fc_430_0.png)

| Name | Date modified | Type | Size |
| --- | --- | --- | --- |
| CALCULATE.EXE-D758B153.pf | 17-Aug-2010 16:02:00 | PF File | 24 KB |
| C:\LAUNCHER.EXE-F70D2719.pf | 11-Sep-2010 11:59:59 | PF File | 5 KB |
| CMD.EXE-70E4F146.pf | 11-Sep-2010 11:59:59 | PF File | 19 KB |
| EXE-E7E8559f1e.pf | 11-Sep-2010 16:02:12 | PF File | 15 KB |
| CMD.EXE-8E7359B8.pf | 11-Sep-2010 11:59:59 | PF File | 7 KB |
| COMPATV.EXE-A9F2C4D0.pf | 30-Aug-2016 16:19:18 | PF File | 9 KB |
| COMPATMINE.EXE-B3E6F746.pf | 10-Sep-2017 10:17:45 | PF File | 17 KB |
| CONSENT.EXE-A1D8B066.pf | 11-Sep-2016 16:02:24 | PF File | 29 KB |
| CORPSET.EXE-E3D1B2C6.pf | 20-Aug-2016 20:23:37 | PF File | 4 KB |
| OSP.EXE-E3E2A1B4.pf | 20-Aug-2016 20:23:24 | PF File | 3 KB |
| CSRSET.EXE-F73AA5f9.pf | 20-Aug-2016 19:35:25 | PF File | 4 KB |
| TIH.EXE-A554A969.pf | 17-Aug-2016 10:59:19 | PF File | 7 KB |
| CRASHREPORTER.EXE-9FB27C0E.pf | 20-Aug-2016 20:14:54 | PF File | 7 KB |
| CREDENTIALHOST.EXE-A7504B8B5.pf | 06-Sep-2016 06:09:22 | PF File | 27 KB |
| NOTEPAD.EXE-51E1111.pf | 11-Sep-2010 11:59:03 | PF File | 10 KB |

**FIGURE 5-3** Prefetcher folder.

There is an exception to the file name rule for images that host other components, including the Microsoft Management Console (%SystemRoot%\System32\Mrc.exe), the service hosting process (%SystemRoot%\System32\svchost.exe), the RunDLL component (%SystemRoot%\System32\rundll3.exe) and DllHost (%SystemRoot%\System32\DllHost.exe). Because add-components are specified on the command line for instances, the prefetchers include the command line in the generated hash.

Thus, invocations of these applications with different components on the command line will result in different traces.

For a system boot, a different mechanism is used, called ReadyBoot. ReadyBoot tries to optimize I/O operations by creating large and efficient reads and storing the data in RAM. When system components require a disk, it is served through the stored RAM. This especially benefits mechanical disks, but can also be useful for SSDs. Information on the files to fetch is stored after boot in the ReadyBoot subdirectory of the Prefetch directory shown in Figure 5-33. Once boot is complete, the cached data in RAM is deleted. For very fast SSDs, ReadyBoot is off by default because its gains are marginal, if any.

When the system boots or an application starts, the prefetcher gives it an opportunity to prefetch. The prefetch looks in the prefetch directory to see if a trace exists for the prefetch scenario in query. If it does, the prefetch calls NTFS to prefetch any metadata file references, reads the contents of all the directories referenced, and finally opens each file referenced. Then calls the memory manager function MnPrefetch to read any data and code specified in that trace's not already in memory. The memory manager initiates all the reads asynchronously and then waits for them to complete before leaving an application's startup.

# EXPERIMENT: Watching prefetch file and writes

If you capture a trace of application startup with Process Monitor from Sysinternals on a client edition of Windows (Windows Server edition disabling prefetch), you can see the prefetcher check for read the application's prefetch file (if it exists). In addition, you can see the prefetcher write out roughly 10 seconds after the application starts. Here is a capture of Notepad startup with an Include filter set to prefetch so that Process Monitor shows only accesses to the %SystemRoot\Prefetch directory:

| Seq | Event | Time of Day | Process Name | PID | Operation | Path | Result |
|---|---|---|---|---|---|---|---||
| 1 | 13 | 11:31:38.256 | notepad.exe | 1428 | Query | C:\Windows\Prefetch\NOTEPAD_EXE_9FB27CO.pf | SUCCESS |
| 2 | 13 | 11:31:38.307 | notepad.exe | 1429 | QueryFile | C:\Windows\Prefetch\NOTEPAD_EXE_9FB27CO.pf | SUCCESS |
| 3 | 13 | 11:31:38.337 | notepad.exe | 1429 | QueryFile | C:\Windows\Prefetch\NOTEPAD_EXE_9FB27CO.pf | SUCCESS |
| 4 | 13 | 11:31:38.337 | notepad.exe | 1429 | QueryFile | C:\Windows\Prefetch\NOTEPAD_EXE_9FB27CO.pf | SUCCESS |
| 4 | 13 | 11:31:38.256 | notepad.exe | 1428 | Query | C:\Windows\Prefetch\NOTEPAD_EXE_9FB27CO.pf | SUCCESS |
| 5 | 13 | 11:31:38.307 | notepad.exe | 1429 | QueryFile | C:\Windows\Prefetch\NOTEPAD_EXE_9FB27CO.pf | SUCCESS |
| 6 | 13 | 11:31:38.337 | notepad.exe | 1429 | QueryFile | C:\Windows\Prefetch\NOTEPAD_EXE_9FB27CO.pf | SUCCESS |
| 7 | 13 | 11:31:38.256 | notepad.exe | 1428 | Query | C:\Windows\Prefetch\NOTEPAD_EXE_9FB27CO.pf | SUCCESS |
| 8 | 13 | 11:31:38.307 | notepad.exe | 1429 | QueryFile | C:\Windows\Prefetch\NOTEPAD_EXE_9FB27CO.pf | SUCCESS |
| 9 | 13 | 11:31:38.337 | notepad.exe | 1429 | QueryFile | C:\Windows\Prefetch\NOTEPAD_EXE_9FB27CO.pf | SUCCESS |
| 10 | 13 | 11:31:38.256 | notepad.exe | 1428 | Query | C:\Windows\Prefetch\NOTEPAD_EXE_9FB27CO.pf | SUCCESS |
| 11 | 13 | 11:31:38.307 | notepad.exe | 1429 | QueryFile | C:\Windows\Prefetch\NOTEPAD_EXE_9FB27CO.pf | SUCCESS |
| 12 | 13 | 11:31:38.337 | notepad.exe | 1429 | QueryFile | C:\Windows\Prefetch\NOTEPAD_EXE_9FB27CO.pf | SUCCESS |
| 13 | 13 | 11:31:38.256 | notepad.exe | 1428 | Query | C:\Windows\Prefetch\NOTEPAD_EXE_9FB27CO.pf | SUCCESS |
| 14 | 13 | 11:31:38.307 | notepad.exe | 1429 | QueryFile | C:\Windows\Prefetch\NOTEPAD_EXE_9FB27CO.pf | SUCCESS |
| 15 | 13 | 11:31:38.337 | notepad.exe | 1429 | QueryFile | C:\Windows\Prefetch\NOTEPAD_EXE_9FB27CO.pf | SUCCESS |
| 16 | 13 | 11:31:38.256 | notepad.exe | 1428 | Query | C:\Windows\Prefetch\NOTEPAD_EXE_9FB27CO.pf | SUCCESS |
| 17 | 13 | 11:31:38.307 | notepad.exe | 1429 | QueryFile | C:\Windows\Prefetch\NOTEPAD_EXE_9FB27CO.pf | SUCCESS |
| 18 | 13 | 11:31:38.337 | notepad.exe | 1429 | QueryFile | C:\Windows\Prefetch\NOTEPAD_EXE_9FB27CO.pf | SUCCESS |
| 19 | 13 | 11:31:38.256 | notepad.exe | 1428 | Query | C:\Windows\Prefetch\NOTEPAD_EXE_9FB27CO.pf | SUCCESS |

*(Note: The OCR table contained many repeated/shifted rows; I have cleaned to reflect the logical flow of the Notepad startup capture as described.)*

![](img/ff0e6a9d867a3a6e9527eb1d946810fc_431_0.png)

Lines 0–3 the Notepad prefetch file being read in the context of the Notepad process during its startup. Lines 7–19 (which have time stamps 10 seconds later than the first four) show the SuperFetch service—running in the context of a Svchost process—writing out the updated prefetch file.

To minimize even further, every three days or during system idle periods, the SuperFetch service organizes a list of files and directories in the order that are referenced during a boot or application start and stores them in a file named %SystemRoot\Prefetch\Layout.ini (see Figure 5-34). This list includes frequently accessed files tracked by SuperFetch.

It launches the system defragmenter with a command-line option that tells the defragmenter to defagment based on the contents of the file instead of performing a full-deagment. The defragmenter finds a contiguous area on each volume large enough to hold all the listed files and directories that reside on that volume and moves them in their entirety into that area so they are stored one after the other. Thus, future prefetching operations will be more efficient because all the data is now stored physically on the disk in the order it will be.

# Placement policy

When a read receives a page, the memory manager must determine whether in physical memory to put the virtual page. The set of rules it uses to determine the best position is called a placement policy. Windows considers the size of CPU memory caches when choosing page frames to minimize unnecessary thrashing of the cache.
